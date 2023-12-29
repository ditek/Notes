
# PlatformIO

## Setup File

```sh
# platformio.ini
# NodeMCU
upload_port = /dev/cu.SLAB_USBtoUART
upload_speed = 460800
monitor_port = /dev/cu.SLAB_USBtoUART
monitor_speed = 115200
```

___
# ESP8266

## IO

```cpp
#define LED 2  //On board LED
pinMode(LED, OUTPUT);
digitalWrite(LED, true);
```

## Deep Sleep
<https://arduinodiy.wordpress.com/2020/01/18/very-deepsleep-and-energy-saving-on-esp8266>

We need to connect RST to GPIO16 (D0 on NodeMCU). That's becaues GPIO16 has a WAKE feature.
Once the deep sleep timer ends, GPIO 16 sends a LOW signal to RST cuasing the chip to wake up.
The RST pin has an internal pull-up resistor.

To store data between deep sleep cycles, we need to use RTC memory (see <## RTC Memory>).

```cpp
// Put the device in deep sleep for a set time
ESP.deepSleep(30e6); 
// Put the device in deep sleep forever (waiting for an interrupt)
ESP.deepSleep(0);
// Disable radio when we wake up
ESP.deepSleep(SLEEPTIME, WAKE_RF_DISABLED);
```

## Radio
```cpp
  // Scan for an access point advertising the desired network
  WiFiMulti.addAP(WIFI_SSID, WIFI_PASSWORD);

  // Provide AP and channel to avoid scanning (and save power)
  WiFi.begin( WLAN_SSID, WLAN_PASSWD, rtcData.channel, rtcData.ap_mac, true );

  // Obtain Wifi channel and AP info
  rtcData.channel = WiFi.channel();
  memcpy( rtcData.ap_mac, WiFi.BSSID(), 6 );

  // Switch Radio off
  WiFi.mode( WIFI_OFF );
  WiFi.forceSleepBegin();
  // Return control to the ESP ROM. yield() should work as well.
  delay( 1 );

  // Switch Radio back on
  WiFi.forceSleepWake();
  delay( 1 );

  // Disable the WiFi persistence.
  // If enabled, we save WiFi settings in the flash memory and use it to auto-reconnect.
  WiFi.persistent( false );
```

__Imporve connection speed__

We do that by saving AP info before we go to sleep and reuse that when we wake up rather than scanning again.

```cpp
  struct {
    uint32_t crc32;
    uint8_t channel;
    uint8_t ap_mac[6];
    uint8_t padding;
  } rtcData;

  void setup() {
    // Disable the WiFi persistence. The ESP8266 will not load and save WiFi settings in the flash memory.
    WiFi.persistent( false );

    // Try to read WiFi settings from RTC memory
    bool rtcValid = false;
    if ( ESP.rtcUserMemoryRead( 0, (uint32_t*)&rtcData, sizeof( rtcData ) ) ) {
      // Calculate the CRC of what we just read from RTC memory, but skip the first 4 bytes as that's the checksum itself.
      uint32_t crc = calculateCRC32( ((uint8_t*)&rtcData) + 4, sizeof( rtcData ) - 4 );
      if ( crc == rtcData.crc32 ) {
        rtcValid = true;
      }
    }
    // Make a quick connection if RTC data is good
    if ( rtcValid ) {
      WiFi.begin( WLAN_SSID, WLAN_PASSWD, rtcData.channel, rtcData.ap_mac, true );
    }
    else {
      WiFi.begin( WLAN_SSID, WLAN_PASSWD );
    }
    //------wait for connection
    int retries = 0;
    int wifiStatus = WiFi.status();
    while ( wifiStatus != WL_CONNECTED ) {
      retries++;
      if ( retries == 100 ) {
        // Quick connect is not working, reset WiFi and try regular connection
        WiFi.disconnect();
        delay( 10 );
        WiFi.forceSleepBegin();
        delay( 10 );
        WiFi.forceSleepWake();
        delay( 10 );
        WiFi.begin( WLAN_SSID, WLAN_PASSWD );
      }
      if ( retries == 600 ) {
        // Giving up after 30 seconds and going back to sleep
        WiFi.disconnect( true );
        delay( 1 );
        WiFi.mode( WIFI_OFF );
        ESP.deepSleep( SLEEPTIME, WAKE_RF_DISABLED );
        return; // Not expecting this to be called, the previous call will never return.
      }
      delay( 50 );
      wifiStatus = WiFi.status();
    }
  }
```

## RTC Memory
Struct data with the maximum size of 512 bytes can be stored in the RTC user memory.
The stored data can be retained between deep sleep cycles.
The size of written data should be a multiple of 4:

```cpp
  // The ESP8266 RTC memory is arranged into blocks of 4 bytes.
  // The access methods read and write 4 bytes at a time,
  // so the RTC data structure should be padded to a 4-byte multiple.
  struct {
    uint32_t crc32;       // 4 bytes
    uint8_t data[7];      // 7 bytes, 11 in total
    uint8_t padding;      // 1 byte,  12 in total
  } rtcData;
```

We calculate CRC of the read data to make sure it's valid.

```cpp
  // Read
  bool rtcValid = false;
  if ( ESP.rtcUserMemoryRead( 0, (uint32_t*)&rtcData, sizeof( rtcData ) ) ) {
    // Calculate the CRC of what we just read from RTC memory, but skip the first 4 bytes as that's the checksum itself.
    uint32_t crc = calculateCRC32( ((uint8_t*)&rtcData) + 4, sizeof( rtcData ) - 4 );
    if ( crc == rtcData.crc32 ) {
      rtcValid = true;
    }
  }

  // Write
  if (ESP.rtcUserMemoryWrite(0, (uint32_t*) &rtcData, sizeof(rtcData))) {
    Serial.println("Write success");
  }

  // Print memory data
  void printMemory() {
    char buf[3];
    uint8_t *ptr = (uint8_t *)&rtcData;
    for (size_t i = 0; i < sizeof(rtcData); i++) {
      sprintf(buf, "%02X", ptr[i]);
      Serial.print(buf);
      if ((i + 1) % 32 == 0) {
        Serial.println();
      } else {
        Serial.print(" ");
      }
    }
    Serial.println();
  }
```

## Ticker
Used to trigger a callback at set intervals.

```cpp
  #include <Ticker.h>
  Ticker blinker;
  void changeState() {
    digitalWrite(LED, !(digitalRead(LED)));
  }
  void changeToParam(char state) {
    digitalWrite(LED, state);
  }
  void setup() {
      //Initialize Ticker every 0.5s
      blinker.attach(0.5, changeState);
      blinker.attach_ms(500, changeState);
      // Call callback in the following loop() rather than in the system context
      blinker.attach_scheduled(0.5, changeState);
      // With 1 argument. This argument's size has to be less or equal to
      // 4 bytes (so char, short, int, float, void*, char*)
      blinker.attach(0.5, std::bind(changeToParam, char(1)));
      blinker.attach(0.5, changeToParam, char(1));
      // Lambda
      blinker.attach(0.5, []() {
        digitalWrite(LED, !digitalRead(LED));
      });
      // Detach
      blinker.detach();
  }
```

## Hardware Timer
Hardware Timer0 is used by WiFi Functions. We can use only Timer1.
Use of timer instead of Ticker gives advantage of precision timing and You can get timer interrupt in micro seconds.

```cpp
  // Volatile tells the compiler not to optimize the variable usage
  volatile int interrupts;

  void ICACHE_RAM_ATTR onTimerISR(){
    interrupts++;
    // Re-Arm the timer as using TIM_SINGLE
    timer1_write(2500000);//12us
  }
  void setup()
  {
      timer1_attachInterrupt(onTime); // Add ISR Function
      timer1_enable(TIM_DIV16, TIM_EDGE, TIM_SINGLE);
      /**
      Dividers:
        TIM_DIV1 = 0,   //80MHz (80 ticks/us - 104857.588 us max)
        TIM_DIV16 = 1,  //5MHz (5 ticks/us - 1677721.4 us max)
        TIM_DIV256 = 3  //312.5Khz (1 tick = 3.2us - 26843542.4 us max)
      Reloads:
        TIM_SINGLE  0 //on interrupt routine you need to write a new value to start the timer again
        TIM_LOOP  1 //on interrupt the counter will start with the same value again
      */
      
      // Arm the Timer for our 0.5s Interval
      timer1_write(25e5); // 2500000 / 5 ticks per us from TIM_DIV16 == 500,000 us interval 
  }
```

___

# Libraries

## Adafruit SSD1306
For connecting 0.96" OLed screen

__Definitions__

```cpp
#define SCREEN_WIDTH 128 // OLED display width, in pixels
#define SCREEN_HEIGHT 64 // OLED display height, in pixels
#define SCREEN_ADDRESS 0x3C
```

__Dependencies__

- `Adafruit BusIO`
- `Adafruit GFX`

## Adafruit BMP280
Pressure and altitude sensor.

__Dependencies__

- `Adafruit Unified Sensor`

___

## Regex

Supported expressions:
<https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions>

```cpp
#include <regex.h>
const char* regExpression = ">([a-zA-Z]+)</[span]{1,4}><span>([0-9]{2}:[0-9]{2})</span>";
regex_t regex;

typedef struct {
    vector<String> matches;
    long next;
} regexSubMatch;


void setupRegex(const char* expression) {
    if (regcomp(&regex, expression, REG_EXTENDED)) {
        Serial.println("Could not compile regex");
        exit(1);
    }
}


regexSubMatch runRegexOnce(String payload) {
    regexSubMatch subMatch;
    char payloadChar[payload.length() + 1];
    regmatch_t matches[MAX_REGEX_MATCHES];
    payload.toCharArray(payloadChar, payload.length());
    int reti = regexec(&regex, payloadChar, MAX_REGEX_MATCHES, matches, 0);
    if (!reti)
    {
        subMatch.next = matches[0].rm_eo;
        // Ignore the first element as it contains the whole string
        for (size_t i = 1; i < MAX_REGEX_MATCHES; i++)
        {
            auto match = matches[i];
            if (match.rm_so == -1) {
                break;
            }
            Serial.println(payload.substring(match.rm_so, match.rm_eo));
            subMatch.matches.push_back(payload.substring(match.rm_so, match.rm_eo));
        }
    }
    else if (reti == REG_NOMATCH) {}
    else {
        char msgbuf[100];
        regerror(reti, &regex, msgbuf, sizeof(msgbuf));
        Serial.printf("ERROR: Regex match failed: %s\n", msgbuf);
        exit(1);
    }
    return subMatch;
}


vector<String> runRegex(String payload) {
    auto m = runRegexOnce(payload);
    vector<String> matches;
    int pos = 0;
    while (m.matches.size() > 0) {
        // Append to the main vector
        matches.insert(matches.end(), m.matches.begin(), m.matches.end());
        pos += m.next;
        // Pick the string from the last match onward
        auto sub = payload.substring(pos);
        m = runRegexOnce(sub);
    }
    return matches;
}
```

## CRC32
```cpp
uint32_t calculateCRC32(const uint8_t *data, size_t length) {
  uint32_t crc = 0xffffffff;
  while (length--) {
    uint8_t c = *data++;
    for (uint32_t i = 0x80; i > 0; i >>= 1) {
      bool bit = crc & 0x80000000;
      if (c & i) {
        bit = !bit;
      }
      crc <<= 1;
      if (bit) {
        crc ^= 0x04c11db7;
      }
    }
  }
  return crc;
}
```
___

# Devices

## Displays

### OLED

__0.91 OLED__
- Dimentions: 128x32
- Library: Adafruit_SSD1306
- I2C Address: 0x3C

## Chips

### I2C Multiplexer

__TCA9548A__
- 1-to-8 I2C multiplexer
- I2C Address: Default: 0x70. Using pins: 0b0111 0A2A1A0.
- Pins:
  + ~RST - Pulled high by default.
  + A2 A1 A0 - address pins. Pulled low. Connect to Vin to set the address to 0x71 - 0x77.
  + SDx, SCx - I2C pins. Not pulled up.

___

# Tools

## EspExceptionDecoder
Used to decode the BackTrace printed with ESP crashes.

https://github.com/me-no-dev/EspExceptionDecoder

___

# Snippets

## I2C Scanner

```cpp
uint8_t nDevices = 0;
for (uint8_t addr = 1; addr < 127; addr++) {
    Wire.beginTransmission(addr);
    if (!Wire.endTransmission()) {
      Serial.print("Found I2C 0x");  Serial.println(addr, HEX);
      nDevices++;
    }
}
Serial.printf("Found %d devices", nDevices);
```
