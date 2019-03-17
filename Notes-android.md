# Android
<!-- MarkdownTOC -->

- [Definitions](#definitions)
- [Data Types](#data-types)
    - [String](#string)
    - [Time and Date](#time-and-date)
    - [ArrayList](#arraylist)
    - [Bundle](#bundle)
    - [Anonymous Classes](#anonymous-classes)
        - [Using an Anonymous Inner Class to Define a Listener](#using-an-anonymous-inner-class-to-define-a-listener)
        - [Using an Anonymous Inner Class to Start a Thread](#using-an-anonymous-inner-class-to-start-a-thread)
    - [Cursor](#cursor)
    - [ContentValues](#contentvalues)
- [App Components](#app-components)
    - [Activities](#activities)
        - [Launch Mode](#launch-mode)
        - [Providing Up Navigation](#providing-up-navigation)
    - [Fragments:](#fragments)
    - [Services](#services)
        - [Types of services](#types-of-services)
        - [Service class:](#service-class)
        - [Intent Service:](#intent-service)
        - [Foreground Service](#foreground-service)
    - [Content Providers](#content-providers)
        - [ContentResolver](#contentresolver)
        - [Creating Content Providers](#creating-content-providers)
    - [Broadcast Receiver](#broadcast-receiver)
        - [Receiver Class](#receiver-class)
        - [Registering the receiver](#registering-the-receiver)
        - [Receiving Sticky Intents](#receiving-sticky-intents)
- [Sync Adapter](#sync-adapter)
- [Job Dispatcher](#job-dispatcher)
    - [Firebase Job Dispatcher](#firebase-job-dispatcher)
    - [Android Framework JobScheduler](#android-framework-jobscheduler)
    - [Evernote's Android-job](#evernotes-android-job)
- [Lifecycle](#lifecycle)
- [Various Topics](#various-topics)
    - [Context](#context)
    - [Android Version](#android-version)
- [Views](#views)
    - [AdapterView](#adapterview)
        - [ListView](#listview)
    - [RecyclerView](#recyclerview)
        - [How it works:](#how-it-works)
        - [How it works - functional steps:](#how-it-works---functional-steps)
        - [Usage:](#usage)
- [Listeners](#listeners)
    - [Listening to internal events](#listening-to-internal-events)
- [Resources](#resources)
    - [The R Class](#the-r-class)
    - [Accessing resources](#accessing-resources)
    - [Values](#values)
        - [Dimensions](#dimensions)
    - [Strings](#strings)
        - [Get String Resource](#get-string-resource)
        - [Quantity Strings \(Plurals\)](#quantity-strings-plurals)
    - [Localization](#localization)
        - [RTL Support](#rtl-support)
    - [Accessibility](#accessibility)
    - [Drawables](#drawables)
        - [Drawable to Bitmap](#drawable-to-bitmap)
- [Java Views and XML Layouts](#java-views-and-xml-layouts)
    - [Referencing an XML view in Java](#referencing-an-xml-view-in-java)
- [UI](#ui)
    - [General](#general)
        - [Screen Size](#screen-size)
    - [XML Namespaces](#xml-namespaces)
    - [Common view properties](#common-view-properties)
    - [Reusable Layouts](#reusable-layouts)
    - [Custom Layout](#custom-layout)
    - [Alternative Layouts](#alternative-layouts)
    - [White space](#white-space)
        - [Adding a line/box](#adding-a-linebox)
    - [Styles](#styles)
        - [Style Inheritance](#style-inheritance)
        - [Useful styles](#useful-styles)
    - [Themes](#themes)
    - [Color Palette](#color-palette)
    - [Touch Selectors](#touch-selectors)
        - [Color State List](#color-state-list)
        - [State List Drawable](#state-list-drawable)
    - [Level List Drawables](#level-list-drawables)
    - [Splash Screen](#splash-screen)
- [UI Components](#ui-components)
    - [View groups](#view-groups)
    - [ConstraintLayout](#constraintlayout)
    - [Toolbar](#toolbar)
        - [Setup](#setup)
        - [Usage](#usage-1)
    - [AppBarLayout](#appbarlayout)
    - [CoordinatorLayout](#coordinatorlayout)
        - [Responding to Scroll Events](#responding-to-scroll-events)
        - [Creating Collapsing Effects](#creating-collapsing-effects)
        - [Creating Parallax Animations](#creating-parallax-animations)
        - [More Scrolling Effects](#more-scrolling-effects)
    - [SwitchIconView](#switchiconview)
        - [Setup](#setup-1)
        - [Usage](#usage-2)
        - [Public methods:](#public-methods)
    - [Floating Action Button](#floating-action-button)
- [UI Components in Java](#ui-components-in-java)
    - [Instantiating a view](#instantiating-a-view)
        - [New Views](#new-views)
        - [Existing Views](#existing-views)
    - [Common view methods](#common-view-methods)
    - [Data Binding](#data-binding)
        - [Configure data binding in Java](#configure-data-binding-in-java)
        - [Using data binding expressions](#using-data-binding-expressions)
- [Logging \(writing to LogCat\)](#logging-writing-to-logcat)
- [View generated events \(click, etc.\)](#view-generated-events-click-etc)
- [Intents](#intents)
    - [Explicit Intent](#explicit-intent)
    - [Implicit Intent](#implicit-intent)
    - [PendingIntent](#pendingintent)
    - [Attaching Intent to Menu Item](#attaching-intent-to-menu-item)
        - [Intent Filter](#intent-filter)
    - [Passing Objects Through Intents](#passing-objects-through-intents)
        - [Serialization](#serialization)
        - [Parcelable](#parcelable)
    - [Extras](#extras)
- [URI](#uri)
    - [URI format:](#uri-format)
    - [URI Builder:](#uri-builder)
        - [URI to URL](#uri-to-url)
    - [ContentUris](#contenturis)
- [Toast](#toast)
- [Snackbar](#snackbar)
- [Adapters](#adapters)
    - [ArrayAdapter](#arrayadapter)
    - [CursorAdapter](#cursoradapter)
- [Menus](#menus)
    - [Options Menu](#options-menu)
        - [Attaching Intent to Menu Item](#attaching-intent-to-menu-item-1)
        - [ShareActionProvider](#shareactionprovider)
- [HTTP Connections](#http-connections)
    - [Manually](#manually)
    - [OkHttp](#okhttp)
- [Scanner](#scanner)
- [Permissions](#permissions)
- [JSON](#json)
    - [Elements](#elements)
    - [Example](#example)
    - [Parsing](#parsing)
    - [JSONObject Functions](#jsonobject-functions)
- [Threading](#threading)
    - [AsyncTask](#asynctask)
    - [Loaders](#loaders)
        - [Classes and interfaces](#classes-and-interfaces)
        - [_LoaderManager_ Methods](#_loadermanager_-methods)
    - [AsyncTaskLoader](#asynctaskloader)
        - [Methods](#methods)
        - [Example](#example-1)
    - [CursorLoader](#cursorloader)
- [Preferences](#preferences)
    - [Should I use preferences?](#should-i-use-preferences)
    - [Common Preferences Objects](#common-preferences-objects)
    - [Preferences XML](#preferences-xml)
    - [Invoking Intents](#invoking-intents)
    - [Preferences in Java](#preferences-in-java)
        - [Functions](#functions)
        - [Getting Preference Values](#getting-preference-values)
        - [Editing Preference Values](#editing-preference-values)
        - [Set up Preference Change Listener](#set-up-preference-change-listener)
        - [Bind Preference Summary to the Preference Value:](#bind-preference-summary-to-the-preference-value)
    - [ListPreference](#listpreference)
- [Notifications](#notifications)
    - [Building a Notification](#building-a-notification)
        - [Notification Styles](#notification-styles)
    - [Issuing a Notification](#issuing-a-notification)
    - [Clear Notifications](#clear-notifications)
    - [Notification Actions](#notification-actions)
- [Firebase](#firebase)
    - [Setup](#setup-2)
    - [Real-time DB](#real-time-db)
        - [Code](#code)
- [SQLite](#sqlite)
    - [SQLite Commands](#sqlite-commands)
    - [Querries](#querries)
    - [SQL Data Types](#sql-data-types)
    - [Foreign Keys](#foreign-keys)
    - [Inner Join](#inner-join)
    - [SQL in Java](#sql-in-java)
        - [Contracts](#contracts)
        - [SQLiteOpenHelper](#sqliteopenhelper)
        - [SQL Database Operations](#sql-database-operations)
        - [Reading/Writing Databases](#readingwriting-databases)
        - [Integrating with a RecyclerView](#integrating-with-a-recyclerview)
- [Testing](#testing)
    - [Instrumented Tests](#instrumented-tests)
        - [Dependencies](#dependencies)
        - [Usage](#usage-3)
        - [Testing Intents](#testing-intents)
        - [Matchers](#matchers)
        - [Actions](#actions)
        - [Test Example](#test-example)
- [Libraries and Tools](#libraries-and-tools)
    - [ButterKnife](#butterknife)
        - [Dependencies](#dependencies-1)
        - [Usage](#usage-4)
        - [RESOURCE BINDING](#resource-binding)
        - [NON-ACTIVITY BINDING](#non-activity-binding)
        - [LISTENER BINDING](#listener-binding)
    - [Stetho \(Debug Network and DB\)](#stetho-debug-network-and-db)
        - [Dependencies](#dependencies-2)
    - [Gson](#gson)
        - [Dependencies](#dependencies-3)
        - [Deserializing JSON objects](#deserializing-json-objects)
        - [Deserializing JSON arrays](#deserializing-json-arrays)
    - [MP Android Chart](#mp-android-chart)
        - [Dependencies](#dependencies-4)
        - [Usage](#usage-5)
    - [Guava \(CSV Parsing and String Utilites\)](#guava-csv-parsing-and-string-utilites)
        - [Dependencies](#dependencies-5)
        - [String Splitting and CSV Parsing](#string-splitting-and-csv-parsing)
        - [String operations](#string-operations)
    - [Annotations Library](#annotations-library)
        - [Dependencies](#dependencies-6)
        - [Usage](#usage-6)
    - [Schematics \(Help with Content Providers\)](#schematics-help-with-content-providers)
    - [Volly \(Networking\)](#volly-networking)
    - [Android-SwitchIcon \(Switch icon with animation\)](#android-switchicon-switch-icon-with-animation)
- [Widgets](#widgets)
    - [Widget Components](#widget-components)
    - [Add to the Manifest](#add-to-the-manifest)
    - [Widget Preview Image](#widget-preview-image)
    - [Collection Widgets](#collection-widgets)
        - [RemoteViewsFactory](#remoteviewsfactory)
        - [RemoteViewsService](#remoteviewsservice)
        - [Collection Widget Layout](#collection-widget-layout)
        - [Updating the widget](#updating-the-widget)
- [Android Virtual Device \(Emulator\)](#android-virtual-device-emulator)
- [APIs](#apis)
    - [Weather API](#weather-api)
    - [The Movie DB](#the-movie-db)
- [ADB](#adb)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [Android Studio Templates](#android-studio-templates)
- [Design time attributes \(tools namespace\)](#design-time-attributes-tools-namespace)
- [Online materials](#online-materials)

<!-- /MarkdownTOC -->

________________________________________________________________________________________________
# Definitions
Gradle
  - Gradle is the build system that packages up and compiles Android Apps.

________________________________________________________________________________________________
# Data Types

## String
Check if empty
:  `TextUtils.isEmpty(string)`

Check equality
:  `string1.equals(string2)`

Formatting strings
:  `String hoursAndMinutes = getString("%1$02d:%2$02d", hours, minutes);`

________________________________________________________________________________________________
## Time and Date
```java
Timestamp departureTime;    // Stores date-time in milliseconds
long millisUntilDeparture = departureTime.getTime() - System.currentTimeMillis();
// Convert millies to minutes
long minutesUntilDeparture = TimeUnit.MILLISECONDS.toMinutes(millisUntilDeparture);
// Convert minutes to hours
long hoursUntilDeparture = TimeUnit.MINUTES.toHours(minutesUntilDeparture);
// Convert hours to minutes
long minutesUntilDeparture = TimeUnit.HOURS.toMinutes(hoursUntilDeparture);
// Formatting time
SimpleDateFormat timeFormat = new SimpleDateFormat("hh:mm a", Locale.getDefault());
SimpleDateFormat dateTimeFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.getDefault());
String dateString = DateFormat.format("dd/MM/yyyy", departureTime).toString();
// Show date/time relative to now (in 3 minutes, 2 hours ago, Apr 22, tomorrow)
String relativeDateString = DateUtils.getRelativeTimeSpanString(task.dueDateMillis);
String departureTimeStr = timeFormat.format(departureTime);
```

________________________________________________________________________________________________
## ArrayList
ArrayList is a dynamic list that extends List interface.

Constructor:
> `ArrayList([Collection C][int Capacity])`

Declaration:

```java
    List<int> list = new ArrayList<int>();
    List<int> list = new ArrayList<>();   // See note below
    List<int> list = new ArrayList<>(Arrays.asList(myArray));
    ArrayList<int> list = new ArrayList<int>();
```

- The declaration with `List<T>` is preferred because:
    - Most APIs expect List type
    - The container can be easily converted to a LinkedList later.
- Since Java 1.7 specifying the type on the declaration's right side is not necessary.
- When ArrayList gets full it creates another array and uses `System.arrayCopy()` to copy all elements from one array to another array. In such cases expanding the size is recommended.

Traversal:
- `Foreach` loop is recommended if no items need to be removed otherwise use iterators.
- You can use either `Iterator` or `ListIterator` for traversing.
- `ListIterator` will allow you to traverse in both directions 
- Both `Iterator` and `ListIterator` will allow you to remove elements while traversing.
    ```java
    Iterator itr = stringList.iterator();
    ListIterator itr = stringList.listIterator();
    while(itr.hasNext()) {System.out.println(itr.next());}
    ```
- Backwards traversal: `for(int i = list.size() - 1; i >= 0; i--)`

 Functions
```java
isEmpty()   // preferred over .isSize()==0
size()
get(index)
remove(index)
```

________________________________________________________________________________________________
## Bundle
- It is a key-value storage mechanism with a string key.
- Usually used to pass data between activities: `intent.putExtra(key, value)` or save the state of an activity: `onSaveInstanceState(Bundle outState)`.

## Anonymous Classes
- Anonymous inner classes allow the developer to create, define, and use a custom object all in one _line_. 
- To create an anonymous inner class, you only provide the right-hand side of the definition. Begin with the new keyword, followed by the class or interface you wish to extend or implement, followed by the class definition.

### Using an Anonymous Inner Class to Define a Listener

Android developers often use anonymous inner classes to define specialized listeners, which register callbacks for specific behavior when an event occurs. For example, to listen for clicks on a View control, the developer must call the `setOnClickListener()` method, which takes a single parameter: a `View.OnClickListener` object.
Developers routinely use the anonymous inner class technique to create, define and use their custom `View.OnClickListener`, as follows:

```java
Button button = (Button) findViewById(R.id.MyButton);
button.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                // User clicked my button, do something here!
            }
});
```

### Using an Anonymous Inner Class to Start a Thread

Let’s look at another example. It’s quite common to define a new `Thread` class, provide the implementation of its `run()` method, and start that thread, all in one go:

```java
new Thread() { 
  public void run()
  {
    doWorkHere();
  }
}.start();
```

________________________________________________________________________________________________
## Cursor
`Cursor` is a control structure that enables traversal over the rows and columns of the table returned by a database query and will be pointing at one of the rows at all times. A database query will return a reference to a `Cursor` object that points to the query result. See [SQL in Java](#sql-in-java) for usage details.

Functions
: 
- `moveToFirst/Last()`- Point at the first/last row. Return false if it does not exist.
- `moveToNext/Previous()`- Move to the next/previous row. Return false if it does not exist.
- `moveToPosition(int rowIndex)`- Point at rowIndex. Return false if it does not exist.
- `getString(int columnIndex)`- Get the string at the specified row.
- `getInt(int columnIndex)`- Get the integer at the specified row.
- `getColumnIndex(String columnName)`- Get the index of a column given its name.
- `getCount()`- Get the number of rows in cursor.
- `close()`- Closes the cursor to prevent memory leaks.

 Iterating over a Cursor:
```java
int nameCol = cursor.getColumnIndex(DbContract.COLUMN_NAME);
void nextName(){
    while(cursor.moveToNext())
        String name = cursor.getString(nameCol);
}
void allNames(){
    if (cursor != null)
        if (!cursor.moveToNext())
            cursor.moveToFirst();
}
void onDestroy(){
    cursor.close();
}
// When updating a cursor, e.g. in an adapter, remember to close the old one
void setData(Cursor cursor) {
    if (mCursor != null) {
        mCursor.close();
    }
    mCursor = cursor;
    notifyDataSetChanged();
}
```

________________________________________________________________________________________________
## ContentValues
A `ContentValues` object contains a set of key-value pairs and are used to write data to a database. See [SQL in Java](#sql-in-java) for usage example.

Functions
: 
- `put(String key, Object value)`- Put any primitive object.
- `get(String key)`- Get the object stored at the provided key.
- `getAsType(String key)`- Cast the return value before return, e.g. `getAsString`, `getAsInteger`
- `valueSet()`- Returns a set of all of the keys and values `Set<Entry<String, Object>>`
- `remove(String key)`- Remove the entry with the specified key.
- `size()`- Return size

________________________________________________________________________________________________
# App Components
App components are the essential building blocks of an Android app. Each component is a different point through which the system (but not necessarily the user) can enter your app.

## Activities
- An activity is a component of Android apps that the user interacts with and maps to one screen of the app.
- Each activity is independent of the others and a different app can start any one of these activities (if allowed). E.g. a camera app can start the activity in the email app that composes new mail to share a picture.
- You can define which activity to use as the main activity in the Android manifest file by declaring it with an <intent-filter> that includes the MAIN action and LAUNCHER category.

```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

- If you have a child activity then you need to declare that in the manifest as:  

```xml
<activity
  android:name=".ChildActivity"
  android:parentActivityName=".MainActivity">
  <meta-data
      android:name="android.support.PARENT_ACTIVITY"
      android:value=".MainActivity" />
</activity>
```
_Note: The meta-data part is added for compatibility with Android 4.0 and lower and it can be removed if only Android 4.1 and up is supported._

Other properties
: 
- `android:label`: Set activity label.
- `android:launchMode`: See details below.

### Launch Mode
A task is a stack which contains a collection of activity instances. Normally, when a user starts an app a new task will be created, and the first activity instance is called the task root. 

Launch modes allows you to define how a new instance or the existing instance of an activity is associated with the current task. The available modes are:

_Standard (default)_
: An activity can be instantiated multiple times. The instances can be located anywhere in the activity stack and can belong to any task. An example of adding an instance to a different task is sharing via the Email app, where an instance of the compose activity is added to your task. 

_SingleTop_
: The only difference from the standard mode is, if an instance of the activity already exists at the top of the target task, that instance will receive the new intent in an `onNewIntent()` call (as opposed to `onCreate()` for a new instance).  
If you navigate up to an activity on the current stack, the behavior is determined by the parent activity's launch mode. If the parent activity has launch mode singleTop, the parent is brought to the top of the stack, and its state is preserved. The navigation intent is received by the parent activity's `onNewIntent()` method. If the parent activity has launch mode standard, the current activity and its parent are both popped off the stack, and a new instance of the parent activity is created to receive the navigation intent.

_SingleTask_
: An Activity with singleTask launchMode is allowed to have only one instance in the system (a.k.a. Singleton). The system creates the activity at the root of a new task and routes the intent to it. However, if an instance of the activity already exists, the system routes the intent to the existing instance through a call to its `onNewIntent()` method, rather than creating a new one.  
The activity allows other activities to be part of its task. It's always at the root of its task, but other activities (necessarily "standard" and "singleTop" activities) can be launched into that task. 

_SingleInstance_
: Same as "singleTask", except that the system doesn't launch any other activities into the task holding the instance. If it starts another activity, that activity is assigned to a different task. The activity is always the single and only member of its task.

**Example**

```xml
<activity
    android:name=".MainActivity"
    android:launchMode="singleTop">
    ...
</activity>
```

### Providing Up Navigation
**_1. Add Up Action_**  
To allow Up navigation with the app icon in the action bar, call `setDisplayHomeAsUpEnabled()`:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    //...
    getActionBar().setDisplayHomeAsUpEnabled(true);
}
```

This adds a left-facing caret alongside the app icon and enables it as an action button such that when the user presses it, your activity receives a call to `onOptionsItemSelected()`. The ID for the action is `android.R.id.home`.

_NOTE:_ Use `getSupportActionBar()` to support APIs lower that API 11.

**_2. Navigate Up to Parent Activity_**
Now we can call `NavUtils.navigateUpFromSameTask()`, which finishes the current activity and starts (or resumes) the appropriate parent activity. The the parent activity is brought forward depends on its launch mode:
- If the parent activity has launch mode `singleTop` the parent activity is brought to the top of the stack, and receives the intent through its `onNewIntent()` method.
- If the parent activity has launch mode `standard` the parent activity is popped off the stack, and a new instance of that activity is created on top of the stack to receive the intent.

```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    int id = item.getItemId();
    // When the home button is pressed, take the user back to the parent
    if (id == android.R.id.home) {
        NavUtils.navigateUpFromSameTask(this);
        return true;
    }
    return super.onOptionsItemSelected(item);
}
```

If no parent activity is specified, we can set the "UP" button to work as a back button:

```java
public boolean onOptionsItemSelected(MenuItem item) {
    int id = item.getItemId();
    if (id == android.R.id.home) {
        onBackPressed();
    }
    return super.onOptionsItemSelected(item);
}
```

## Fragments:
- A Fragment represents a portion of UI in an Activity.
- An activity can have a single fragment (as in phones) or can combine multiple fragments to build a multi-pane UI.
- A fragment can be reused in multiple activities.
- Fragments can be added or removed from an Activity.
- The PlaceholderFragment is automatically generated as an inner class of the activity, but fragments don’t need to be inner classes.
- Getting the root view of a fragment:  
  `View rootView = inflater.inflate(R.layout.fragment_main, container, false);`
- Use rootView instead of getActivity() to find items the parent activity:  
  `TextView txtForecast = (TextView) rootView.findViewById(R.id.txt_forecast);`
- When the host activity is created, both it, and the fragments it contains, call their `onCreate()` methods. Then, right after this creation, fragments call their `` method to inflate their view dynamically!

__Getting Fragment Instance in Parent Activity__

```java
SettingsFragment fragment = (SettingsFragment)getSupportFragmentManager()
        .findFragmentById(R.id.settings);
if (fragment != null)
    fragment.updateOptions();
```

__Send Data from Activity to Fragment__

```java
/** In the activity **/
@Override
public void onCreate(Bundle savedInstanceState) {
    ...
    Fragment settingsFragment = new SettingsFragment();
    Bundle bundle = new Bundle();
    bundle.putSerializable("settingsID", options);
    settingsFragment.setArguments(bundle);
    getSupportFragmentManager()
            .beginTransaction()
            .replace(R.id.settings, settingsFragment)
            .commit();
}

/** In the fragment **/
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    Serializable options = getArguments().getSerializable("settingsID");
    return super.onCreateView(inflater, container, savedInstanceState);
}
```

## Services
- A Service is a component that performs operations in the background without a user interface.
- For example: playing music in the background or fetching network data.

### Types of services
1. Start service
    By calling startService() from a context. The service doesn't communicate back.
2. Schedule service
    Using a JobService, which is a service that starts at some point in the future or when a condition is met. You define when the service should run using a scheduler e.g. JobScheduler.
3. Bind service
    A bound service offers a service-client like interface. A component, e.g. an activity, can bind to the service using bindService() method, and will function as the client. Bound services can communicate back to the components that started them.

### Service class:
The service will start by default on the main thread. Therefore, it needs to create a background thread, e.g. AsyncTask.
Service lifecycle
    Call to `startService()`
    =>  `onCreate()` 
    =>  `onStartCommand()`
    =>  Service Running (start `AsyncTask`)
    =>  call to `stopSelf()` (called by the service or its client)
    =>  `onDestroy()`

### Intent Service:
Unlike the service class it runs in a background thread by default.

1. Create a class that extends `IntentService`
2. Register the service in AndroidManifest.xml
3. Specify service behavior by overriding `onHandleIntent()`
4. Start the service in a similar manner to starting an activity by intent.

```java
// 1. Extend `IntentService`
public class MyIntentService extends IntentService{
    // 3. Specify service behavior
    protected void onHandleIntent(@Nullable Intent intent) {
        // background work
    }
}
// 4. Starting the service
Intent intent = new Intent(this, MyIntentService.class);
startService(intent);
```
```xml
<!-- 2. Register the service in AndroidManifest.xml -->
<service android:name=".MyIntentService" android:exported="false"/>
```

### Foreground Service
A foreground service is a service that the user is actively aware of and is not a candidate for the system to kill when low on memory. A foreground service must provide a notification for the status bar, which is placed under the Ongoing heading. This means that the notification cannot be dismissed unless the service is either stopped or removed from the foreground. For example, a music player that's actively playing music.

To request that your service run in the foreground, call `startForeground()`, which takes an integer that uniquely identifies the notification and the `Notification` for the status bar.

To remove the service from the foreground, call `stopForeground()`, which takes a boolean, which indicates whether to remove the status bar notification as well. This method does _not_ stop the service. 

```java
Intent notificationIntent = new Intent(this, ExampleActivity.class);
PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, notificationIntent, 0);
Notification notification = new Notification.Builder(this)
    ...
    .setContentIntent(pendingIntent)
    .build();
startForeground(ONGOING_NOTIFICATION_ID, notification);
stopForeground(true);
```

________________________________________________________________________________________________

## Content Providers

### ContentResolver
To use a ContentProvider we need a ContentResolver, which acts as the interface to the ContentProvider. Steps for using a ContentProvider
1. Get permission to use the ContentProvider.
2. Get the ContentResolver
3. Pick one of four basic actions on the data: query, insert, update, delete
4. Identify the data you are reading or manipulating to create a URI
5. In the case of reading from the ContentProvider, display the information in the UI

A ContentResolver is needed to interact with ContentProviders. It can be obtained as:

```java
ContentResolver resolver = getContentResolver();
```

ContentResolver actions:
: 
1. `Cursor query()` - Read from the data.
2. `insert()`- Add rows to the data.
3. `update()`- Update the data.
4. `delete()`- Delete rows from the data.

 The function signatures are similar to the database operations:
```java
/* Query */
Cursor resolver.query(String table,           // The table to query
                     String[] projection,    // The columns to return. Null to return all.
                     String selection,       // The columns for the WHERE clause (filter rows)
                     String[] selectionArgs, // The values for the WHERE clause (filter arguments)
                     String orderBy)         // The sort order
mData = resolver.query(TVContract.Shows.CONTENT_URI, null, null, null, null);
// Query should be done in a background thread, a Loader for example.
public Cursor loadInBackground() {
    // Query and load all task data in the background; sort by priority
    try {
        return getContentResolver().query(TaskContract.TaskEntry.CONTENT_URI,
                null,
                null,
                null,
                TaskContract.TaskEntry.COLUMN_PRIORITY);

    } catch (Exception e) {
        Log.e(TAG, "Failed to asynchronously load data.");
        e.printStackTrace();
        return null;
    }
}

/* Insert */
ContentValues contentValues = new ContentValues();
contentValues.put(TaskContract.TaskEntry.COLUMN_DESCRIPTION, description);
Uri uri = getContentResolver().insert(, contentValues);

/* Update */
Uri uri = ContentUris.withAppendedId(TaskContract.TaskEntry.CONTENT_URI, id);
resolver.update(uri, contentValues, null, null);

/* Delete */
resolver.delete(TVTimeContract.CONTENT_URI, null, null);
```


### Creating Content Providers
1.. Create a class that extends `ContentProvider` abstract class and implement `onCreate()`  
ContentProvider methods:
: 
- Uri insert(Uri contentUri, ContentValues values)- Insert a row with `values` into the table specified in the `contentUri`, e.g. `content://authority/table`. Returns a content URI for the new row in the format: `content://authority/table/<row_id>`.

```java
// 1. Extend ContentProvider class
public class TaskContentProvider extends ContentProvider {
    private TaskDbHelper mTaskDbHelper;
    public boolean onCreate() {
        mTaskDbHelper = new TaskDbHelper(getContext());
        return true;
    }
}
```

2.. Register the ContentProvider in the Manifest. You need to provide the authority which is typically the package name of the app. The name is the package name and class.  Exported field determines whether the ContentProvider can be accessed by other apps.

```xml
<!-- 2. Register the ContentProvider in the Manifest -->
<provider
    android:name="com.example.android.myapp.data.TaskContentProvider"
    android:authorities="com.example.android.myapp"
    android:exported="false" />
```

3.. Define URIs that identify the provider and define the the tasks and datatypes that it can work with. The _path_ part of the URI indicates the data of interest (e.g. table name). `content://com.example.myapp/tasks` refers to the `task` table. If a subset is needed, say a column, we can define a URI with the column name after the path (i.e. `../tasks/title`). For a URI that refers to a certain id we can use `../tasks/1` or use a wild-card `../tasks/#` to match any integer. In a similar manner, an asterisk (`*`) can be used to match any string.

4.. Add the URIs to the Contract class.

```java
// 3. Define URIs
public class TaskContract {
    // The authority, which is how your code knows which Content Provider to access
    public static final String AUTHORITY = "com.example.android.myapp";
    // The base content URI = "content://" + <authority>
    public static final Uri BASE_CONTENT_URI = Uri.parse("content://" + AUTHORITY);
    // Define the possible paths for accessing data in this contract
    // This is the path for the "tasks" directory
    public static final String PATH_TASKS = "tasks";
    /* TaskEntry is an inner class that defines the contents of the task table */
    public static final class TaskEntry implements BaseColumns {
        // TaskEntry content URI = base content URI + path
        public static final Uri CONTENT_URI =
                BASE_CONTENT_URI.buildUpon().appendPath(PATH_TASKS).build();
    }
}
```

5.. Build a `URIMatcher` to match URI patterns to integers:
: Rather that having if statements to check the received URI we use a `URIMatcher`. First we define a set of static integers for each case we expect. E.g. `100` for `../tasks` and `101` for `../tasks/#`. 

```java
    // (1) Define final integer constants for the directory of tasks and a single item.
    // It's a convention to use 100, 200, 300, etc for directories,
    // and related ints (101, 102, ..) for items in that directory.
    public static final int TASKS = 100;
    public static final int TASK_WITH_ID = 101;
    // (3) Declare a static variable for the Uri matcher that you construct
    private static final UriMatcher sUriMatcher = buildUriMatcher();
    // (2) Define a static buildUriMatcher method that associates URI's with their int match
    /** Initialize a new matcher object without any matches,
     then use .addURI(String authority, String path, int match) to add matches
     */
    public static UriMatcher buildUriMatcher() {
        // Initialize a UriMatcher with no matches by passing in NO_MATCH to the constructor
        UriMatcher uriMatcher = new UriMatcher(UriMatcher.NO_MATCH);
        /*
          All paths added to the UriMatcher have a corresponding int.
          For each kind of uri you may want to access, add the corresponding match with addURI.
          The two calls below add matches for the task directory and a single item by ID.
         */
        uriMatcher.addURI(TaskContract.AUTHORITY, TaskContract.PATH_TASKS, TASKS);
        uriMatcher.addURI(TaskContract.AUTHORITY, TaskContract.PATH_TASKS + "/#", TASK_WITH_ID);

        return uriMatcher;
    }
```

6.. Implement the required CRUD (Create, Read, Update, Delete) methods (query, insert, update, delete)
:
- `Uri insert (Uri uri, ContentValues values)`
- `String getType(Uri uri)` - Return MIME type, e.g. content.

```java
public Uri insert(@NonNull Uri uri, ContentValues values) {
    // (1) Get access to the task database (to write new data to)
    final SQLiteDatabase db = mTaskDbHelper.getWritableDatabase();

    // (2) Write URI matching code to identify the match for the tasks directory
    int match = sUriMatcher.match(uri);
    Uri returnUri;

    switch (match) {
        case TASKS:
            // (3) Insert new values into the database
            long id = db.insert(TABLE_NAME, null, values);
            if ( id > 0 ) {
                returnUri = ContentUris.withAppendedId(TaskContract.TaskEntry.CONTENT_URI, id);
            } else {
                throw new android.database.SQLException("Failed to insert row into " + uri);
            }
            break;
        default:
            throw new UnsupportedOperationException("Unknown uri: " + uri);
    }

    // (4) Notify the resolver if the uri has been changed, and return the newly inserted URI
    getContext().getContentResolver().notifyChange(uri, null);
    // Return constructed uri (it points to the newly inserted row of data)
    return returnUri;
}

public Cursor query(@NonNull Uri uri, String[] projection, String selection,
                    String[] selectionArgs, String sortOrder) {
    // (1) Get access to underlying database (read-only for query)
    final SQLiteDatabase db = mTaskDbHelper.getReadableDatabase();
    // (2) Write URI match code and set a variable to return a Cursor
    int match = sUriMatcher.match(uri);
    Cursor retCursor;
    // (3) Query for the tasks directory and write a default case
    switch (match) {
        // Query for the tasks directory
        case TASKS:
            retCursor =  db.query(TABLE_NAME,
                    projection,
                    selection,
                    selectionArgs,
                    null,
                    null,
                    sortOrder);
            break;
        
        case TASK_WITH_ID:
          // Get the id from the URI
          String id = uri.getPathSegments().get(1);
          // Selection is the _ID column = ?, and the Selection args = the row ID from the URI
          String mSelection = "_id=?";
          String[] mSelectionArgs = new String[]{id};
          // Construct a query as you would normally, passing in the selection/args
          retCursor =  db.query(TABLE_NAME,
                  projection,
                  mSelection,
                  mSelectionArgs,
                  null,
                  null,
                  sortOrder);
          break;
        
        default:
            throw new UnsupportedOperationException("Unknown uri: " + uri);
    }
    // (4) Set a notification URI on the Cursor and return that Cursor
    retCursor.setNotificationUri(getContext().getContentResolver(), uri);
    return retCursor;
}

public int delete(@NonNull Uri uri, String selection, String[] selectionArgs) {
        final SQLiteDatabase db = mTaskDbHelper.getWritableDatabase();
        int match = sUriMatcher.match(uri);
        int tasksDeleted; // starts as 0

        // (2) Write the code to delete a single row of data
        // We expect the selection parameters to be passed as null
        switch (match) {
            // Handle the single item case, recognized by the ID included in the URI path
            case TASK_WITH_ID:
                // Get the task ID from the URI path
                String id = uri.getPathSegments().get(1);
                // Use selections/selectionArgs to filter for this ID
                tasksDeleted = db.delete(TABLE_NAME, "_id=?", new String[]{id});
                break;
            default:
                throw new UnsupportedOperationException("Unknown uri: " + uri);
        }

        // (3) Notify the resolver of a change and return the number of items deleted
        if (tasksDeleted != 0) {
            getContext().getContentResolver().notifyChange(uri, null);
        }
        // Return the number of tasks deleted
        return tasksDeleted;
    }

public int update(@NonNull Uri uri, ContentValues values, String selection,
                  String[] selectionArgs) {
    final SQLiteDatabase db = mTaskDbHelper.getWritableDatabase();
    //Keep track of if an update occurs
    int tasksUpdated;
    int match = sUriMatcher.match(uri);

    switch (match) {
        case TASK_WITH_ID:
            //update a single task by getting the id
            String id = uri.getPathSegments().get(1);
            tasksUpdated = db.update(
                TABLE_NAME, values, "_id=?", new String[]{id});
            break;
        default:
            throw new UnsupportedOperationException("Unknown uri: " + uri);
    }

    if (tasksUpdated != 0) {
        //set notifications if a task was updated
        getContext().getContentResolver().notifyChange(uri, null);
    }

    return tasksUpdated;
}
/* getType() handles requests for the MIME type of data. We are working with two types of data:
    1) a directory and 2) a single row of data.
    This method gives a way to standardize the data formats that your provider accesses,
     and this can be useful for data organization.
 */
@Override
public String getType(@NonNull Uri uri) {
    int match = sUriMatcher.match(uri);

    switch (match) {
        case TASKS:
            // directory
            return "vnd.android.cursor.dir" + "/" + TaskContract.AUTHORITY + "/" + TaskContract.PATH_TASKS;
        case TASK_WITH_ID:
            // single item type
            return "vnd.android.cursor.item" + "/" + TaskContract.AUTHORITY + "/" + TaskContract.PATH_TASKS;
        default:
            throw new UnsupportedOperationException("Unknown uri: " + uri);
    }
}
```

________________________________________________________________________________________________
## Broadcast Receiver
- Enables apps to receive intents that are broadcast by the system or by other apps even when the app isn't running.
- Receivers use intent filter to indicate the broadcasts they are interested in.
- Receivers are meant to listen to broadcasts, react and complete within 5 seconds, which usually means starting a service and sending notifications.

### Receiver Class
```java
public class MyReceiver extends BroadcastReceiver {
  @Override
  public void onReceive(Context context, Intent intent) {
    Toast.makeText(context, "Intent Detected.", Toast.LENGTH_LONG).show();
}}
```

### Registering the receiver
Receivers need to be registered in order to listen to broadcasts. This can be done statically by adding an entry in the manifest or dynamically during the activity lifecycle.
* _Statically_: The intent is delivered to the app even if it's not running. Some broadcast intents won't let you define a static broadcast receiver (intents that have `FLAG_RECEIVER_REGISTERED_ONLY`). In this case, it needs to be defined at runtime (dynamically).

```xml
<receiver android:name=".MyReceiver">
  <intent-filter>
    <action android:name="android.intent.action.BOOT_COMPLETED" />
  </intent-filter>
</receiver>
```

* _Dynamically_: Broadcasts can be received only after calling `registerReceiver()` while the app is running.

```java
public class MainActivity{
    ChargingBroadcastReceiver mChargingReceiver;
    IntentFilter mChargingIntentFilter;
    protected void onCreate(Bundle savedInstanceState) {
        mChargingReceiver = new ChargingBroadcastReceiver();
        mChargingIntentFilter = new IntentFilter();
        mChargingIntentFilter.addAction(Intent.ACTION_POWER_CONNECTED);
        mChargingIntentFilter.addAction(Intent.ACTION_POWER_DISCONNECTED);
    }
    protected void onResume() {
        registerReceiver(mChargingReceiver, mChargingIntentFilter);
    }
    protected void onPause() {
        unregisterReceiver(mChargingReceiver);
    }
}
```

### Receiving Sticky Intents
In the previous charging example, the app will be informed about charging events occuring while it's alive. However, when it runs it wouldn't be able to know the charging state.

On API level 23+ we can use the `BatteryManager` to know the charging state. Prior to Android 23+ you needed to use a sticky intent to get battery state. A sticky intent is a broadcast intent that, unlike normal broadcast intent, sticks around, allowing your app to access it at any point.

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M){
    BatteryManager batteryManager = (BatteryManager) getSystemService(BATTERY_SERVICE);
    isCharging = batteryManager.isCharging();
} else {
    IntentFilter ifilter = new IntentFilter(Intent.ACTION_BATTERY_CHANGED);
    Intent batteryStatus = context.registerReceiver(null, ifilter);
    int status = batteryStatus.getIntExtra(BatteryManager.EXTRA_STATUS, -1);
    isCharging = status == BatteryManager.BATTERY_STATUS_CHARGING || status == BatteryManager.BATTERY_STATUS_FULL;
}
```

________________________________________________________________________________________________

# Sync Adapter
Sync adapter is a method to sync your local mobile data with a back-end server that provides automatic execution, user authentication and network detection.

> Note: SyncAdapter do not notify us or return status when they complete. We can use a SharedPrefernce to store status and use OnSharedPreferenceChangeListener to get notified.

________________________________________________________________________________________________
# Job Dispatcher

## Firebase Job Dispatcher
It needs Google play services to run.

 Gradle dependency:
```groovy
implementation 'com.firebase:firebase-jobdispatcher:0.6.0'
```

1. Create a service that extends from `JobService`. By default, jobs are executed on the main thread, so making an anonymous class extending `AsyncTask` is a good idea.

```java
import com.firebase.jobdispatcher.JobService;

public class MyFirebaseJobService extends JobService{
    AsyncTask mBackgroundTask;

    @Override
    public boolean onStartJob(final JobParameters job) {
        mBackgroundTask = new AsyncTask() {
            protected Object doInBackground(Object[] params) {
                Context context = MyFirebaseJobService.this;
                ReminderTasks.executeTask(context, ReminderTasks.ACTION_CHARGING_REMINDER);
                return null;
            }
            protected void onPostExecute(Object o) {
                // The job is successful so pass false in order not to reschedule it
                boolean rescheduleJob = false;
                jobFinished(job, rescheduleJob);
            }
        };
        mBackgroundTask.execute();
        // Return whether there is still work remaining.
        // The job is still running on the background thread, so return true.
        return true;
    }

    /* Called when the job requirements are no longer met, e.g. download over wifi. */
    @Override
    public boolean onStopJob(JobParameters job) {
        // Cancel the AsyncTask if it isn't done
        if(mBackgroundTask != null) mBackgroundTask.cancel(true);
        // Return true to retry the job when the conditions are met again
        return true;
    }

}
```

2. Add the service to the Manifest.

```xml
        <service android:name=".MyFirebaseJobService"
            android:exported="false">
            <intent-filter>
                <action android:name="com.firebase.jobdispatcher.ACTION_EXECUTE"/>
            </intent-filter>
        </service>
```

2. Use `FirebaseJobDispatcher` to create a new job.

```java
Driver driver = new GooglePlayDriver(context);
FirebaseJobDispatcher dispatcher = new FirebaseJobDispatcher(driver);

Job myJob = dispatcher.newJobBuilder()
    // the JobService that will be called
    .setService(MyJobService.class)
    // uniquely identifies the job
    .setTag("complex-job")
    // one-off job
    .setRecurring(false)
    // don't persist past a device reboot
    .setLifetime(Lifetime.UNTIL_NEXT_BOOT)
    // start between 0 and 15 minutes (900 seconds)     
    .setTrigger(Trigger.executionWindow(0, 900))
    // overwrite an existing job with the same tag
    .setReplaceCurrent(true)
    // retry with exponential backoff 
    .setRetryStrategy(RetryStrategy.DEFAULT_EXPONENTIAL)
    // constraints that need to be satisfied for the job to run
    .setConstraints(
        // only run on an unmetered network
        Constraint.ON_UNMETERED_NETWORK,
        // only run when the device is charging
        Constraint.DEVICE_CHARGING
    )
    .build();
```

## Android Framework JobScheduler
Native Android scheduler, but only provides compatibility back to API 21 (Lollipop).
<http://evernote.github.io/android-job/>

## Evernote's Android-job
Doesn't require Google Services and provides compatibility back to API 14.


________________________________________________________________________________________________
# Lifecycle
![Activity lifecycle](https://developer.android.com/guide/components/images/activity_lifecycle.png)  
- To navigate transitions between stages of the activity lifecycle, the Activity class provides a core set of six callbacks:
  > `onCreate()`, `onStart()`, `onResume()`, `onPause()`, `onStop()`, and `onDestroy()`.

- `onRestart()` state happens when the activity is momentarily not displayed and then is displayed again, without being re-created. E.g. when we hit home and re-launch the app.
- When the activity is destroyed its views lose their state (contents). To save it we need to overload `onSaveInsanceState(Bundle)`, which is called __after__ `onPause()`.
- Example:

```java
    private static final String STATE_KEY = "state_data";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        //...
        if(savedInstanceState!=null && savedInstanceState.containsKey(STATE_KEY))
            mTextView.setText(savedInstanceState.getString(STATE_KEY));
    }
    @Override
    public void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        outState.putString(STATE_KEY, mTextView.getText().toString());
    }
```
________________________________________________________________________________________________
# Various Topics

## Context
- A context object contains the context of current state of the application. It lets newly created objects understand what has been going on.
- The context can be an Application or an Activity/Service.
- Getting the context:
    - From within an activity:
        `getApplicationContext()`, `getContext()`, `getBaseContext()`, `this`
    - From within a fragment:
        `getActivity()`
        * It can return null if it is called before onAttach of the respective fragment
    - From an AsyncTask that is defined inside an activity:
        ActivityName.this
        `getBaseContext()`
    - From an AsyncTask that is defined inside a fragment:
        `ForecastFragment.this.getActivity()`

## Android Version
Some features require knowing which version of Android the user is running. That can be checked like this:

```java
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {}
```

________________________________________________________________________________________________
# Views

Common methods:
: 
- `setTag(Object tag)`: Sets the tag associated with this view. Can be used to store view related data.
- `setTag(int key, Object tag)`: Sets a tag associated with this view and a key.

## AdapterView
### ListView
- **Note** ListView is deprecated and replaced with RecyclerView
- ListView is a subclass of AdapterView optimized for displaying lists by displaying many copies of a single layout
- An Adapter is used to populate a ListView.
- Functions:
  - `setAdapter(Adapter)`   Bind the ListView to an Adapter
  - `setOnItemClickListner`
- Listen to click events:
    ```java
    listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
        @Override
        public void onItemClick(AdapterView<?> adapterView, View view, int position, long id) {
      // Suppose mAdapter is Adapter<String> that populates listView
          String selectedText = mAdapter.getItem(position);
        }
      });
    ```

- getView:
- convertView: gives ListView the opportunity to recycle views.

## RecyclerView

### How it works:
  - The RecyclerView connects to an Adapter that is used to provide it with views when needed.
  - The Adapter is also used to bind data (from some data source) to the views.
  - The Adapter sends each view to the RecyclerView in a ViewHolder.
  - The ViewHolder contains a reference to the view object.
  - Each ViewHolder is in charge of displaying a single item, which has its own view/views.
  - The ViewHolder also caches views associated with each item.
  - The RecyclerView uses the layout manager to arrange the items.
  - The RecyclerView creates only as many view holders as are needed to display the on-screen portion of the dynamic content, plus a few extra.
  - As the user scrolls through the list, the RecyclerView takes the off-screen views and rebinds them to the data which is scrolling onto the screen.
  - Overview:
    `Data Source =====> Adapter ====(ViewHolders)====> RecyclerView <----> LayoutManager`
  - More details:
    <https://developer.android.com/guide/topics/ui/layout/recyclerview.html>

### How it works - functional steps:
  - We start with an empty RecyclerView and an array as the data source.
  - The RecyclerView calls getItemCount to know the number of items it will be displaying.
  - The RecyclerView asks the Adapter to create ViewHolder objects and inflate item views by calling onCreateViewHolder, which returns a new ViewHolder object associated with the new view.
  - After each ViewHolder is created, the RecyclerView will call onBindViewHolder to populate each item with data.
  - When the user scrolls, the RecyclerView will reuse the ViewHolders asking the Adapter to bind new data to them.

### Usage:
 Add a dependency to build.gradle:
```groovy
implementation 'com.android.support:recyclerview-v7:25.1.0'
//recyclerview-v7 is library name, 25.1.0 is the library version
```
 Add in XML layout:
`<android.support.v7.widget.RecyclerView ... />`  
Create a new layout XML to define how the list items look like. E.g. a LinearLayout can be a line in a vertical RecyclerView.

Set up the ViewHolder:
: 
1. Create a ViewHolder class (it will be placed within the Adapter class)
2. Create a member variable to hold a reference to the TextView that will hold the data.
3. Use the View object passed to the constructor to get a reference to the display TextView and store in the variable created in #1.

```java
    // 1 Create a ViewHolder class
    class MyViewHolder extends RecyclerView.ViewHolder{
        // 2
        TextView dataTextView;
        // 3
        public MyViewHolder(View itemView){
            super(itemView);
            dataTextView = (TextView) itemView.findViewById(R.id.tv_item_number);
        }
    }
```

Set up the Adapter:
: 
1. Create an Adapter that inherits RecyclerView.Adapter with a generic of type MyViewHolder.
2. Override onCreateViewHolder (called when the RecyclerView instantiates a new ViewHolder)
  2.a- Inflate the list item xml layout into a view
  2.b- Return a new ViewHolder passing the view just created.
3. Override onBindViewHolder (called when the RecyclerView wants to populate the view with data)
  3.a- Pass the position to the ViewHolder bind function.
4. Override getItemCount (returns the number of data in the data source)
5. If the data set that the adapter uses changes notifyDataSetChanged() should be called.

```java
    // 1 Create an Adapter class
    public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder>{
        private String[] mDataArray;
        MyAdapter(String[] data){
            mDataArray = data;
        }
        // 2 Override onCreateViewHolder
        @Override
        public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
            // 2.a Inflate the list item xml layout into a view
            Context context = parent.getContext();
            int layoutIdForListItem = R.layout.number_list_item;
            LayoutInflater inflater = LayoutInflater.from(context);
            boolean shouldAttachToParentImmediately = false;
            View thisItemsView = inflater.inflate(layoutIdForListItem, parent, shouldAttachToParentImmediately);
            // or a bit simpler:
            LayoutInflater inflater = LayoutInflater.from(parent.getContext());
            View thisItemsView = inflater.inflate(R.layout.list_item_layout, parent, false);
            // 2.b Return a new ViewHolder passing the view just created
            return new MyViewHolder(thisItemsView);
        }
        // 3
        @Override
        public void onBindViewHolder(MyViewHolder holder, int position) {
            String selectedData = mDataArray[position];
            holder.dataTextView.setText(selectedData);
        }
        // 4
        @Override
        public int getItemCount() {
            return mDataArray.length;
        }
        // 5 Implement a function to update the data and notify the RecyclerView
        public void setData(String[] data) {
            mDataArray = data;
            notifyDataSetChanged();
        }
        // If using a cursor as data source remember to close the old one before updating
        public void setData(Cursor cursor) {
            if (mCursor != null) {
                mCursor.close();
            }
            mCursor = cursor;
            notifyDataSetChanged();
        }
        class MyViewHolder extends RecyclerView.ViewHolder {...}  // Created above
    }
```

Attach the adapter to the RecyclerView in the activity onCreate method:
: 
1. Create member variables for the RecyclerView and the Adapter
2. Use findViewById to get a reference to the RecyclerView
3. Create a layoutManager and set the RecyclerView to use it. It can be:
    - `LinearLayout`: Provides similar functionality to `ListView`
    - `GridLayout`: Lays out items in a grid (see tip below).
    - `StaggeredGridLayout`: Lays out children in a staggered grid formation.
4. Tell the RecyclerView that all the items will have fixed size allow it to optimize itself
5. Create a new Adapter and pass it to the RecyclerView.

```java
    public class MainActivity extends AppCompatActivity {
      static final int NUM_LIST_ITEMS = 100;
      // 1 Create member variables for the RecyclerView and the Adapter
      MyAdapter mAdapter;
      RecyclerView mRecyclerView;

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          ...
          // 2 Use findViewById to get a reference to the RecyclerView
          mRecyclerView = (RecyclerView) findViewById(R.id.rv_numbers);
          // 3 Create a layoutManager and set the RecyclerView to use it
          LinearLayoutManager layoutManager = new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false);
          mRecyclerView.setLayoutManager(layoutManager);
          // 4 Tell the RecyclerView that all the items will have fixed size
          mRecyclerView.setHasFixedSize(true);
          // 5 Create a new Adapter and pass it to the RecyclerView
          mAdapter = new MyAdapter(NUM_LIST_ITEMS);
          mRecyclerView.setAdapter(mAdapter);
      }
    }
```

Variable number of columns for a GridLayoutManager:

```java
int mNoOfColumns = Utilities.calculateNoOfColumns(this, VIEW_WIDTH);
GridLayoutManager layoutManager = new GridLayoutManager(this, mNoOfColumns);

/** Calculates the number of columns that fit on the screen */
public static int calculateNoOfColumns(Context context, int imageViewWidth) {
    DisplayMetrics displayMetrics = context.getResources().getDisplayMetrics();
    float dpWidth = displayMetrics.widthPixels / displayMetrics.density;
    return (int) (dpWidth / imageViewWidth);
}
```

Add a click listener (optional):

The long way:
: 
1. Add an interface, that will function as a Listener, to the Adapter class that defines one void method, a click handler.
2. Create a member variable, mListener, of the Listener type you just created in the Adapter class.
3. Add a Listener parameter to the Adapter constructor and store it in mListener.
4. Implement View.OnClickListener in the ViewHolder class.
5. Override onClick in the ViewHolder class. You can get the clicked item position using getAdapterPosition()
6. Call setOnClickListener on the View passed into the ViewHolder class constructor
7. Make MainActivity Implement MyAdapter.ListItemClickListener
8. Override ListItemClickListener's onListItemClick method
9. Fix the Adapter definition in the MainActivity according to the new constructor.

```java
    public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder>{
        // 2 Create a member variable, mListener
        final private ListItemClickListener mOnClickListener;
        // 1 Add an interface that will function as a Listener
        public interface ListItemClickListener {
            void onListItemClick(int clickedItemIndex);
        }
        // 3 Add a Listener parameter to the Adapter constructor
        public MyAdapter(int numberOfItems, ListItemClickListener listener) {
            mNumberItems = numberOfItems;
            mOnClickListener = listener;
            viewHolderCount = 0;
        }
        // 4. Implement View.OnClickListener in the ViewHolder class
        class MyViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
            ...
            // 6. Call setOnClickListener on the View passed into the ViewHolder constructor
            public MyViewHolder(View view) {
                ...
                // Since the ViewHolder implements View.OnClickListener use 'this' as the OnClickListener
                view.setOnClickListener(this);
            }
            // 5. Override onClick
            @Override
            public void onClick(View v) {
                // Pass click position to the listener
                int clickedPosition = getAdapterPosition();
                mOnClickListener.onListItemClick(clickedPosition);
            }
          }
        }

    /* MainActivity.java */
    // 7. Make MainActivity Implement MyAdapter.ListItemClickListener
    public class MainActivity extends AppCompatActivity implements MyAdapter.ListItemClickListener {
        ...
        @Override
        protected void onCreate(Bundle savedInstanceState) {
          ...
          // 9. Adjust to match the modified constructor
          mAdapter = new MyAdapter(NUM_LIST_ITEMS, this);
        }
        // 8. Override ListItemClickListener's onListItemClick method
        @Override
        public void onListItemClick(int clickedItemIndex) {
          Toast.makeText(this, String.valueOf(clickedItemIndex), Toast.LENGTH_SHORT).show();
        }
    }
```

 The short way:
```java
/* In MyAdapter.java */
final private ListItemClickListener mOnClickListener;
List<String> mData;
MyAdapter() {
    mOnClickListener = new ItemClickListener() {
        @Override
        public void onListItemClick(int clickedItemIndex) {
            Log.i(TAG, "onListItemClick: " + mData.get(clickedItemIndex).key);
        }
    };
}
```

Using a Cursor:
: 
1. Add a member variable to store the cursor
2. Adjust the adapter constructor to take a cursor argument and assign it to the member cursor.
3. Adjust `getItemCount()` to return the cursor count.
4. Adjust `onBindViewHolder()` to move the cursor to the passed in position. Update the `ViewHolder` views.
5. Create a function to allow for updating the cursor.
6. Update the `MainActivity`

```java
    /* MyAdapter.java */
    // 1. Add a member variable to store the cursor
    private Cursor mCursor;
    // 2. Adjust the adapter constructor to take a cursor argument
    public GuestListAdapter(Context context, Cursor cursor) {
        this.mContext = context;
        this.mCursor = cursor;
    }
    // 3. Adjust getItemCount() to return the cursor count.
    public int getItemCount() {
        return mCursor.getCount();
    }
    // 4. Adjust onBindViewHolder to move the cursor to the passed in position.
    public void onBindViewHolder(GuestViewHolder holder, int position) {
    if(!mCursor.moveToPosition(position))
        return;
    // Call getString on the cursor to get the name
    String name = mCursor.getString(mCursor.getColumnIndex(TableEntry.COLUMN_NAME));
    // Set the holder's nameTextView text to the name
    holder.nameTextView.setText(name);
    }
    // 5. Create a function to allow for updating the cursor.
    void swapCursor(Cursor cursor){
        if (mCursor != null) 
            mCursor.close();
        mCursor = cursor;
        if(mCursor!=null)
            this.notifyDataSetChanged();
    }

    /* MainActivity.java */
    protected void onCreate(Bundle savedInstanceState) {
      //...
      Cursor cursor = getDbContents();
      mAdapter = new MyAdapter(this, cursor);
    }
    public void updateDbEntries(cursor) {
      mAdapter.swapCursor(cursor);
    }

```

Add swipe action:
: 
1. Create an `ItemTouchHelper` and override `onSwiped()` method
2. Attach the touch helper to the RecyclerView

```java
ItemTouchHelper touchHelper = new ItemTouchHelper(new ItemTouchHelper.SimpleCallback(0,
        ItemTouchHelper.LEFT | ItemTouchHelper.RIGHT) {
    @Override
    public boolean onMove(RecyclerView recyclerView, RecyclerView.ViewHolder viewHolder, RecyclerView.ViewHolder target) {
        return false;
    }
    @Override
    public void onSwiped(RecyclerView.ViewHolder viewHolder, int direction) {
        long id = (long) viewHolder.itemView.getTag();
        removeGuest(id);
        mAdapter.swapCursor((getAllGuests()));
        // If you are using a loader don't forget to restart it so it gets the new data
        getLoaderManager().restartLoader(LOADER_ID, null, MainActivity.this);
    }
});
touchHelper.attachToRecyclerView(myRecyclerView);
```

________________________________________________________________________________________________
# Listeners
- An event listener is an interface in the View class that contains a single callback method, which will be called by the Android framework when the View to which the listener has been registered is triggered by user interaction.
- Interfaces include, for example:
  - View.OnClickListener, contains the onClick() callback.
  - View.OnLongClickListener, contains the onLongClick() callback.

__Handling events:__

  - To define one of these methods and handle your events, implement the interface in your Activity (Method 2) or define it as an anonymous class (Method 1).
  - Then, pass an instance of your implementation to the respective View.set...Listener() method. (E.g., call setOnClickListener() and pass it your implementation of the OnClickListener.)

Method 1 - Anonymous implementation of the Listener

```java
// Create an anonymous implementation of OnClickListener
private OnClickListener mCorkyListener = new OnClickListener() {
    public void onClick(View v) {
      // do something when the button is clicked
    }
};

protected void onCreate(Bundle savedValues) {
    ...
    // Capture our button from layout
    Button button = (Button)findViewById(R.id.corky);
    // Register the onClick listener with the implementation above
    button.setOnClickListener(mCorkyListener);
    ...
}
```

Method 2 - Implement the Listener as a part of your Activity

```java
public class ExampleActivity extends Activity implements OnClickListener {
    protected void onCreate(Bundle savedValues) {
        ...
        Button button = (Button)findViewById(R.id.corky);
        button.setOnClickListener(this);
    }

    // Implement the OnClickListener callback
    public void onClick(View v) {
      // do something when the button is clicked
    }
    ...
}
```

Resources: https://developer.android.com/guide/topics/ui/ui-events.html

## Listening to internal events
To listen to an event created from another class, we need to create our own listener interface:

```java
/* Create UiUpdateRequestListener.java */
public interface UiUpdateRequestListener {
    void onUiUpdateRequest(String param);
}

/* In the event generator class SubTab.java */
private UiUpdateRequestListener mUiUpdateRequestListener;

public void setUiUpdateRequestListener(UiUpdateRequestListener listener) {
    mUiUpdateRequestListener = listener;
}

private void requestUiUpdate() {
    if (mUiUpdateRequestListener != null)
        mUiUpdateRequestListener.onUiUpdateRequest();
}

/* In MainActivity.java */
mSubTab.setUiUpdateRequestListener(param -> upateUi(param));
// or without using lambda
mSubTab.setUiUpdateRequestListener(new UiUpdateRequestListener() {
    @Override
    public void onUiUpdateRequest(String param) {
        upateUi(param);
    }
});
```

________________________________________________________________________________________________
# Resources

## The R Class
- When your application is compiled the R class is generated.
- It creates constants that allow you to dynamically identify the various contents of the res folder.
- setContentView(layout) inflates a layout - reads the XML file and generates Java objects for each of the tags in it

## Accessing resources
- Java
  R.resource_type.resource_name
  R.string.s1
  R.drawable.icon
- XML
  @resource_type/resource_name
  @string/s1
- Common resource types
  drawable, string, layout, id, color

## Values

### Dimensions
```xml
<!-- res/values/dimens.xml -->
<resources>
    <dimen name="textview_height">25dp</dimen>
    <dimen name="font_size">16sp</dimen>
</resources>
```

```java
// Java
Resources res = getResources();
float fontSize = res.getDimension(R.dimen.font_size);

// Kotlin
val fontSize: Float = resources.getDimension(R.dimen.font_size);
```
________________________________________________________________________________________________
## Strings

### Get String Resource
In code:  
    `String x = getString(R.string.string_name);`
In XML:  
    `android:text="@string/string_name"`

String with placeholders:

```xml
<string name="welcome_messages">Hello, %1$s! You have %2$d new messages.</string>
```
```java
String text = res.getString(R.string.welcome_messages, username, mailCount);
```

### Quantity Strings (Plurals)
Different languages have different rules for grammatical agreement with quantity. In English, we write "1 book", but for any other quantity we'd write "n books". The full set supported by Android is `zero`, `one`, `two`, `few`, `many`, and `other`.

It's often possible to avoid quantity strings by using quantity-neutral formulations such as "Books: 1". This makes your life and your translators' lives easier, if it's an acceptable style for your application.

 Syntax:
```xml
<plurals
    name="plural_name">
    <item
        quantity=["zero" | "one" | "two" | "few" | "many" | "other"]
        >text_string</item>
</plurals>
```

 Example XML file saved at res/values/strings.xml:
```xml
<plurals name="numberOfSongsAvailable">
    <!--
         As a developer, you should always supply "one" and "other"
         strings. Your translators will know which strings are actually
         needed for their language. Always include %d in "one" because
         translators will need to use %d for some languages).
      -->
    <item quantity="one">%d song found.</item>
    <item quantity="other">%d songs found.</item>
</plurals>
```

 Example XML file saved at res/values-pl/strings.xml:
```xml
<plurals name="numberOfSongsAvailable">
    <item quantity="one">Znaleziono %d piosenkę.</item>
    <item quantity="few">Znaleziono %d piosenki.</item>
    <item quantity="other">Znaleziono %d piosenek.</item>
</plurals>
```

 Java code:
```java
int count = getNumberOfsongsAvailable();
Resources res = getResources();
String songsFound = res.getQuantityString(R.plurals.numberOfSongsAvailable, count, count);
```

________________________________________________________________________________________________
## Localization

- Resources for each supported locale are stored in relevant folder in `res/` directory.
- Each folder name has a suffix that refers to the language e.g. `values-fr` and `values-ar` while `values` contain the defaults. The OS will select the appropriate resource folder.
- `values/string.xml` contains string and string-array definitions as:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
  <!-- Title for the application. [CHAR LIMIT=12] -->
  <string name="app_name">Sólo Java</string>
  <!-- Name for the order summary. It will be shown in the format of "Name: Amy". -->
  <string name="order_summary_name">Nombre: <xliff:g id="name" example="Amy">%s</xliff:g></string>
  <string-array name="pref_example_list_values">
          <item>1</item>
          <item>0</item>
      </string-array>
</resources>
```

`xliff` denotes a part of the string that should not be translated. It is useful when there is a parameter in the string e.g. to have this string;
  "Received at 2 o'clock"

```java
context.getString(R.string.received_at) + time + context.getString(R.string.oclock)
```
OR

```xml
<string name="received_at_oclock">
  Received at
  <xliff:g id="time" example="5">%1$s</xliff:g>
  o'clock
</string>
```

You can indicate that a string does not need translation as:  
    `<string name="app_name" translatable="false">Just Java</string>`

- Display a number in the local currency:
  `NumberFormat.getCurrencyInstance().format(number)`

> NOTE: To export the string automatically to `strings.xml` select it with the mouse and press `ALT+ENTER`, then select Extract string resource and give it a name.
> NOTE: Translations Editor in Android Studio displays all the strings and their available translations.

### RTL Support
- Add `android:supportsRtl="true"` to `<application>` in `AndroidManifest.xml`.
- Use start/end instead of left/right in your layout properties.

________________________________________________________________________________________________

## Accessibility

Accessibility requirements:
1. *Describe UI controls*: Provide content description for textless components such as ImageButtons, CheckBoxe and ImageView using `android:contentDescription` or `setContentDescription()`. For decorative graphics set the description to `Null`.
2. *Enable focus-based navigation*: Make sure that any element that accepts input is reachable when a keyboard is used for example. To do this set the components to be focusable and the focus order to be logical.
3. *No audio-only feedback*: Audio feedback must always have a secondary feedback mechanism such as hepatic/visual feedback or system notification.

________________________________________________________________________________________________
## Drawables

### Drawable to Bitmap
```java
Resources resources = context.getResources();
Bitmap bitmap = BitmapFactory.decodeResource(resources, R.drawable.my_icon);
```

________________________________________________________________________________________________
# Java Views and XML Layouts
- To turn an xml layout into java view objects, we need to inflate the layout. After the layout is inflated, we need to associate it with an Activity or Fragment. This process of inflating and associating is a little different depending on whether it’s a layout for an Activity or Fragment.

** For an Activity **
- We inflate the layout and associate it with the Activity by calling the setContentView method in onCreate in our Activity:  
`setContentView(R.layout.activity_main);`

** For a Fragment **
- In our Fragment classes we inflate the layout in the `onCreateView` method, which includes a `LayoutInflater` as a parameter:  
`View rootView = inflater.inflate(R.layout.fragment_main, container, false);`
- The root view, or view element which contains all the other views, is returned by the inflate method of the `LayoutInflater`. We then should return this rootView for the `onCreateView`.

## Referencing an XML view in Java
- In XML add an id property:  
  `android:id="@+id/my_i`
    - @: Do not treat the string as a string literal, but look for the contents in the resources
    - +: Create the id if it does not exist
    - id: Declares that this is an id not a reference to a style, string or image
- In Java:  
  `newTextView = (TextView) findViewById(R.id.my_id);`

________________________________________________________________________________________________
# UI

## General
- Density-independent pixel (dp) is a size unit that takes the same physical space regardless of the pixel density.
- All components align to an 8dp square baseline grid.
- Iconography in toolbars align to a 4dp square baseline grid.
- All touch targets should have dimensions of at least 48dp.
- Scale-independent pixel (sp) is a size unit for fonts that takes the same physical space regardless of the pixel density.

### Screen Size
```java
// Depricatred way
screenWidth = myActivity.getWindowManager().getDefaultDisplay().getWidth();
screenHeight = myActivity.getWindowManager().getDefaultDisplay().getHeight();
// Recommended way
Point screenSize = new Point();
myActivity.getWindowManager().getDefaultDisplay().getSize(screenSize);
screenWidth = screenSize.x;
screenHeight = screenSize.y;
```

## XML Namespaces
- In the UI XMLs the `anrdoid` namespace is usually needed and is defined
  `xmlns:android="http://schemas.android.com/apk/res/android"`
- `xmlns:tools="http://schemas.android.com/tools"` mimics the android namespace but allows the properties to be applied only on the design preview (will disappear in runtime)
- `xmlns:app="http://schemas.android.com/apk/res-auto"`

## Common view properties

General view properties:
: 
- `android:id`- Values: @+id/textview1
- `android:layout_width/height`- Values: `match_parent`, `wrap_content`, `int dp`.

`TextView` properties:
: 
- `android:textSize`- Values: `int sp`.
- `android:textAppearance`- Values: `?android:textAppearanceMedium`.
- `android:textAllCaps`- Values: `ture`, `false`.
- `android:textColor`- Values: `@android:color/black`.
- `android:fontFamily`- Values: `sans-serif`, `sans-serif-light`, `sans-serif-thin`, ...
- `android:drawableStart`- Values: A drawable to place at the start of the view.
- `android:drawablePadding`- Values: int (padding between the drawable and the text).

`LinearLayout` properties:
: 
- `android:orientation`- Values: `vertical`, `horizontal`.

`LinearLayout` children properties:
: 
- `android:layout_weight`- Value: `int`. Used in LinearLayout items to assign a weight them. More weight means more space in the layout. `layout_width/height` (depending wether the layout is horizontal/vertical) needs to be `0dp`.

`RelativeLayout` children properties:
: 
- `android:layout_below`- Values:` @id/textview0`
- `android:layout_toRightOf`- Values: `@id/textview1`

```xml
android:layout_alignParentBottom="true"
android:layout_centerHorizontal="true"
<!-- Using android:textAppearance is preferred over explicit sp values -->
```

## Reusable Layouts
To reuse a set of views in several places we can place them in a view group and put it in a dedicated layout file and then include it when needed. If a view group isn't actually needed we can put the views in a `<merge>` tag.

```xml
<!-- titlebar.xml -->
<FrameLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    tools:showIn="@layout/activity_main" >
    <ImageView android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:src="@drawable/gafricalogo" />
</FrameLayout>

<!-- buttons.xml -->
<merge xmlns:android="http://schemas.android.com/apk/res/android">
    <Button
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/add"/>
    <Button
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/delete"/>
</merge>
```

> *Note*: The `tools:showIn` attribute in the XML above is a special attribute that is removed during compilation and used only at design-time in Android Studio — it specifies a layout that includes this file, so you can preview (and edit) this file as it appears while embedded in a parent layout.

Now you can use the `<include>` tag to reuse the component. You can as well override its `android:layout_*` parameters, but then you must override both `android:layout_height` and `android:layout_width` first.

```xml
<!-- activity_main.xml -->
<LinearLayout
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"

    <include layout="@layout/titlebar"/>
    <include layout="@layout/buttons"/>
    ...
</LinearLayout>

<!-- activity_details.xml -->
<LinearLayout
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"

    <include android:id="@+id/news_title"
         android:layout_width="match_parent"
         android:layout_height="match_parent"
         layout="@layout/title"/>
    ...
</LinearLayout>
```

## Custom Layout
We can create a custom layout based on an XML layout. For example, if our custom layout is based on `LinearLayout` we do the following:
1. Create an XML layout with a `LinearLayout` as a root
2. Create a Java class that inherits `LinearLayout`.
3. Inflate the XML layout and attach it to the current Java object.
4. Call the inflation function in all three constructors.

__Note:__  
The convinience function `inflate()` used below is equivilent to:

```java
LayoutInflater inflater = (LayoutInflater) activity.getSystemService( Context.LAYOUT_INFLATER_SERVICE );
inflater.inflate( R.layout.player_toolbar, this, true );
```

```xml
<!-- card.xml -->
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content">
    <ImageView
        android:id="@+id/thumbnail"
        android:layout_width="72dip"
        android:layout_height="72dip"/>
    <TextView
        android:id="@+id/description"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

```java
public class Card extends LinearLayout {
    private TextView description;
    private ImageView thumbnail;

    public Card(Context context) {
        super(context);
        init();
    }

    public Card(Context context, AttributeSet attrs) {
        super(context, attrs);
        init();
    }

    public Card(Context context, AttributeSet attrs, int defStyle) {
        super(context, attrs, defStyle);
        init();
    }

    private void init() {
        inflate(getContext(), R.layout.card, this);
        /** NOTE
        inflate() is a convinience function which can be used instead of:
        > LayoutInflater inflater = (LayoutInflater) activity.getSystemService( Context.LAYOUT_INFLATER_SERVICE );
        > inflater.inflate( R.layout.card, this, true );

        */
        this.description = (TextView)findViewById(R.id.description);
        this.thumbnail = (ImageView)findViewById(R.id.thumbnail);
    }
}
```

## Alternative Layouts
*_Minimum screen width _*  
By add a suffix in the format `-sw<size in dp>`, e.g. `-sw720dp`, to the layout name you specify the minimum screen width that this layout support.

- 600 dp is the smallest width of a typical 7" tablet screen.
- 600 dp is the smallest width of a typical 10" tablet screen.

*_Landscape Layout_*  
We can change how an activity looks like in landscape mode. First create a new folder called `layout-land` and place the modified layout in it.

## White space
- Adding white spaces in UI can be done using padding or margins.
- Padding adds a space between the view's content and its edges (space within the view).
- Margins add a space between the view and its parent layout (space around the view).
- White spaces are recommended to be multiples of 8dp.
- Attributes: `layout_margin`, `layout_marginLeft`, `padding`, `paddingTop`, etc.

### Adding a line/box
 Use the 'View' view:
```xml
<View android:layout_width="match_parent"
android:layout_height="1dp"
android:background="@android:color/darker_gray"/>
```

## Styles
A style is a collection of properties that specify the format for a view.

Styles are defined in `res/styles.xml`. Each style has a set of items. The item name is the property it sets.

```xml
<!-- Style for a header TextView -->
<style name="HeaderText">
    <item name="android:layout_width">match_parent</item>
    <item name="android:textSize">20sp</item>
    <item name="android:textColor">#4527A0</item>
</style>
```

### Style Inheritance
 To create a style/theme that builds on an existing style/theme set the parent field:
```xml
<style name="BoldHeaderText" parent="HeaderText">
    <item name="android:textStyle">bold</item>
</style>
<style name="AppTheme" parent="Theme.AppCompat.Light">
<style name="Code" parent="@android:style/TextAppearnce.Medium">
```

To use the style in the activity.xml add with the view properties:  
  `style="@style/CodeFont"`

Theme - Add a style with the name AppTheme:

```xml
<!-- Base the theme on an existing one -->
<style name="AppTheme" parent="Theme.AppCompat.Light">
      <!-- Primary theme color of the app (sets background color of app bar) -->
      <item name="colorPrimary">#FF9800</item>
      <!-- Background color of buttons in the app -->
      <item name="colorButtonNormal">#FF9800</item>
  <!-- Color UI controls -->
      <item name="colorAccent">#536DFE</item>
  </style>
```

### Useful styles
- `android:textAppearance="@style/TextAppearance.AppCompat.Caption"`- Useful for labels.
- 

## Themes
A theme is a style that is applied to an entire Activity or application. Android comes with several themes like: 
- `Theme.AppCompat.Light.DarkActionBar`- A light theme.
- `Theme.AppCompat`- A dark theme.
- `Theme.Material.Wallpaper.NoTitleBar`

To change an activity's theme
The app theme is set in the `AndroidManifest.xml`.

## Color Palette
It's common to use one primary color, two shades of it (light and dark) and an accent which is usually bright and has high contrast with the primary color.

The colors `colorPrimary`, `colorPrimaryDark`, `colorAccent` are the default app colors in Android. So the menu bar, FAB, radio buttons, etc. will be colored based on them.

```xml
<!-- colors.xml -->
<resources>
    <!-- Base application colors -->
    <color name="colorPrimary">#673AB7</color>
    <color name="colorPrimaryDark">#512DA8</color>
    <color name="colorPrimaryLight">#D1C4E9</color>
    <color name="colorAccent">#FF9100</color>
</resources>
```
Resources:
- [Google vibrant color palettes](https://material.google.com/style/color.html#color-color-palette).
- [Primary and accent color palette generator](https://www.materialpalette.com/).


## Touch Selectors
Touch selectors are used to change the color/background of a view based on its touch state. A touch selector can be a `ColorStateList`, for providing colors, or a `StateListDrawable`, for providing drawables. `StateList`s are created from XML resource files in the `color`/`drawable` subdirectory. An XML file contains a single `selector` element with a number of `item` elements inside. The first item that matches the current state (starting from top) will be used.

### Color State List
*_Syntax_*

```xml
<selector xmlns:android="http://schemas.android.com/apk/res/android" >
    <item
        android:color="hex_color"
        android:state_pressed=["true" | "false"]
        android:state_focused=["true" | "false"]
        android:state_selected=["true" | "false"]
        android:state_checkable=["true" | "false"]
        android:state_checked=["true" | "false"]
        android:state_enabled=["true" | "false"]
        android:state_window_focused=["true" | "false"] />
</selector>
```

*_Example_*

```xml
<!-- res/color/button_text.xml -->
 <selector xmlns:android="http://schemas.android.com/apk/res/android">
   <item android:state_focused="true" android:color="@color/sample_focused" />
   <item android:state_pressed="true" android:state_enabled="false"
           android:color="@color/sample_disabled_pressed" />
   <item android:state_enabled="false" android:color="@color/sample_disabled_not_pressed" />
   <item android:color="@color/sample_default" />
 </selector>
 
 <!-- activity_main.xml -->
<Button
    ...
    android:textColor="@color/button_text" />
```

### State List Drawable
*_Syntax_*

```xml
<selector xmlns:android="http://schemas.android.com/apk/res/android"
    android:constantSize=["true" | "false"]
    android:dither=["true" | "false"]
    android:variablePadding=["true" | "false"] >
    <item
        android:drawable="@[package:]drawable/drawable_resource"
        android:state_pressed=["true" | "false"]
        android:state_focused=["true" | "false"]
        android:state_hovered=["true" | "false"]
        android:state_selected=["true" | "false"]
        android:state_checkable=["true" | "false"]
        android:state_checked=["true" | "false"]
        android:state_enabled=["true" | "false"]
        android:state_activated=["true" | "false"]
        android:state_window_focused=["true" | "false"] />
</selector>
```

*_Example_*

```xml
<!-- res/drawable/button.xml -->
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true"
          android:drawable="@drawable/button_pressed" /> <!-- pressed -->
    <item android:state_focused="true"
          android:drawable="@drawable/button_focused" /> <!-- focused -->
    <item android:state_hovered="true"
          android:drawable="@drawable/button_focused" /> <!-- hovered -->
    <item android:drawable="@drawable/button_normal" /> <!-- default -->
</selector>
 
 <!-- activity_main.xml -->
<Button
    ...
    android:background="@drawable/button" />
```

## Level List Drawables
Level lists provide different drawables based on a numerical value. Setting the level value of the drawable with `setLevel()` loads the drawable resource in the level list that has a `android:maxLevel` value greater than or equal to the value passed to the method.

*_Syntax_*

```xml
<level-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item
        android:drawable="@drawable/drawable_resource"
        android:maxLevel="integer"
        android:minLevel="integer" />
</level-list>
```

*_Example_*

```xml
<!-- res/drawable/status.xml -->
<level-list xmlns:android="http://schemas.android.com/apk/res/android" >
    <item android:drawable="@drawable/status_off"
          android:maxLevel="0" />
    <item android:drawable="@drawable/status_on"
          android:maxLevel="1" />
</level-list>
 
 <!-- activity_main.xml -->
<Button
    ...
    android:background="@drawable/status" />
```

## Splash Screen
First create an XML drawable: `res/drawable/background_splash.xml`.

*Note: Make sure the bitmap source isn't a vector drawable
*
```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:drawable="?attr/colorPrimary" />
    <item>
        <bitmap
            android:gravity="center"
            android:src="@drawable/music_note" />
    </item>
</layer-list>
```

Create a new `SplashTheme` in `styles.xml`:

```xml
<style name="SplashTheme" parent="Theme.AppCompat.NoActionBar">
    <item name="android:windowBackground">@drawable/background_splash</item>
</style>

```

Create a new `SplashActivity` class:

```java
public class SplashActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        Intent intent = new Intent(this, MainActivity.class);
        startActivity(intent);
        finish();
    }
}
```

Set `SplashTheme` as the activity's theme in `AndroidManifest.xml`:

```xml
<activity
    android:name=".SplashActivity"
    android:theme="@style/SplashTheme">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

________________________________________________________________________________________________
# UI Components

## View groups
- Frame layout
  - Useful (and more efficient) for simple layouts with a single view.
  - Views are all aligned against the frame boundaries.
- Linear layout
  - Useful for stacking views vertically or horizontally
  - The only way to break up the display proportionately
  ** To make the layout scrollable put it in a ScrollView.
- Relative layout
  - Allows positioning layout relative to each other or the parent view.
- Constraint layout

## ConstraintLayout
Setup

```groovy
dependencies {
  implementation 'com.android.support.constraint:constraint-layout:1.0.1'
}
```


## Toolbar
The Toolbar is a generalization of the ActionBar. The key difference that distinguishes the Toolbar from the ActionBar include is that Toolbar is a View included in a layout like any other View and therefor it is easier to position, animate and control.

See <http://guides.codepath.com/android/Using-the-App-Toolbar> for more details.

### Setup
If you're targeting an API level < 21, ensure the AppCompat-v7 support library is added to your application `build.gradle`. Otherwise, you can just use `Toolbar` in your xml file.

```groovy
dependencies {
  implementation 'com.android.support:appcompat-v7:25.2.0'
}
```

Second, disable the theme-provided ActionBar by having your theme extend from `Theme.AppCompat.NoActionBar` (or the light variant) within the `res/styles.xml` file:

```xml
<resources>
  <!-- Base application theme. -->
  <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
  </style>
</resources>
```

### Usage
Add a `ToolBar` to your layout as any other view. You'll want to add `android:fitsSystemWindows="true"` to the parent layout of the `Toolbar` to ensure that the height of the activity is calculated correctly.

```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
      android:id="@+id/toolbar"
      android:minHeight="?attr/actionBarSize"  
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:titleTextColor="@android:color/white"
      android:background="?attr/colorPrimary"/>

    <!-- Layout for content is here. This can be a RelativeLayout  -->

</LinearLayout>
```

 Next, in your Activity or Fragment, set the Toolbar to act as the ActionBar by calling the `setSupportActionBar(Toolbar)` method:
```java
void onCreate(Bundle savedInstanceState) {
    Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
    setSupportActionBar(toolbar);
}
```

To animate the ToolBar it must be surrounded by an `AppBarLayout`.

## AppBarLayout
AppBarLayout is a vertical LinearLayout which implements many of the features of material designs app bar concept, namely scrolling gestures.

Children should provide their desired scrolling behavior through `setScrollFlags(int)` and the associated layout xml attribute: `app:layout_scrollFlags`.

This view depends heavily on being used as a direct child within a CoordinatorLayout. If you use AppBarLayout within a different ViewGroup, most of it's functionality will not work.

AppBarLayout also requires a separate scrolling sibling in order to know when to scroll such as `RecyclerView` or `NestedScrollView`. The binding is done through the `AppBarLayout.ScrollingViewBehavior` behavior class, meaning that you should set your scrolling view's behavior to be an instance of `AppBarLayout.ScrollingViewBehavior`.

Scroll events in the associated scrolling sibling trigger changes inside views declared within AppBarLayout by using the `app:layout_scrollFlags` attribute. The `scroll` flag used within the attribute `app:layout_scrollFlags` must be enabled along with either `enterAlways`, `enterAlwaysCollapsed`, `exitUntilCollapsed`, or `snap`.

```xml
<android.support.design.widget.CoordinatorLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

    <android.support.v4.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:layout_behavior="@string/appbar_scrolling_view_behavior">
        <!-- Your scrolling content -->
    </android.support.v4.widget.NestedScrollView>

    <android.support.design.widget.AppBarLayout
            android:layout_height="wrap_content"
            android:layout_width="match_parent">

        <android.support.v7.widget.Toolbar
                app:layout_scrollFlags="scroll|enterAlways"/>

        <android.support.design.widget.TabLayout
                app:layout_scrollFlags="scroll|enterAlways"/>

    </android.support.design.widget.AppBarLayout>
</android.support.design.widget.CoordinatorLayout>
```

## CoordinatorLayout
`CoordinatorLayout` is a super-powered `FrameLayout`. `CoordinatorLayout` extends the ability to accomplish many of the Material Design scrolling effects without needing to write your own custom animation code.

First, make sure you are not using the deprecated ActionBar (see Toolbar section). Also make sure that the CoordinatorLayout is the main layout container.

```xml
<android.support.design.widget.CoordinatorLayout 
    android:id="@+id/main_content"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true">

      <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />

</android.support.design.widget.CoordinatorLayout>
```

### Responding to Scroll Events
To make the Toolbar responsive to scroll events we need to surround it with an AppBarLayout. As mentioned in [AppBarLayout](#appbarlayout) section, it needs to associated with a scrollable sibling with `app:layout_behavior` set properly. For a RecyclerView the code would be:

```xml
<android.support.design.widget.AppBarLayout
        android:id="@+id/appbar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
        android:fitsSystemWindows="true">
  <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light" />
 </android.support.design.widget.AppBarLayout>

 <android.support.v7.widget.RecyclerView
        android:id="@+id/rvToDoList"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior">
```

### Creating Collapsing Effects
If we want to create the collapsing toolbar effect, we must wrap the Toolbar inside `CollapsingToolbarLayout`.

> NOTE: I noticed that the title does not show up when using this code. Use the code in the previous section for simple scrolling or the next one for parallax.

```xml
<android.support.design.widget.AppBarLayout
        ...>
    <android.support.design.widget.CollapsingToolbarLayout
            android:id="@+id/collapsing_toolbar"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:fitsSystemWindows="true"
            app:contentScrim="?attr/colorPrimary"
            app:expandedTitleMarginEnd="64dp"
            app:expandedTitleMarginStart="48dp"
            app:layout_scrollFlags="scroll|exitUntilCollapsed">

            <android.support.v7.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:layout_scrollFlags="scroll|enterAlways"></android.support.v7.widget.Toolbar>

    </android.support.design.widget.CollapsingToolbarLayout>
</android.support.design.widget.AppBarLayout>
```

### Creating Parallax Animations
The `CollapsingToolbarLayout` also enables us to use an `ImageView` that fades out as it collapses. To create this effect, we add an `ImageView` and declare an `app:layout_collapseMode="parallax"` attribute to the tag.

```xml
<android.support.design.widget.CollapsingToolbarLayout
    ...>

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        app:layout_scrollFlags="scroll|enterAlways"></android.support.v7.widget.Toolbar>
    <ImageView
        android:src="@drawable/my_pic"
        app:layout_scrollFlags="scroll|enterAlways|enterAlwaysCollapsed"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:scaleType="centerCrop"
        app:layout_collapseMode="parallax"
        android:minHeight="100dp"/>

</android.support.design.widget.CollapsingToolbarLayout>
```

### More Scrolling Effects
Check out this web page: <http://guides.codepath.com/android/handling-scrolls-with-coordinatorlayout>

## SwitchIconView
Google launcher-style implementation of switch (enable/disable) icon

### Setup
```groovy
repositories {
    maven { url "https://jitpack.io" }
}
dependencies {
    implementation 'com.github.zagum:Android-SwitchIcon:1.3.4'
}
```

### Usage
```xml
<com.github.zagum.switchicon.SwitchIconView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:padding="8dp"
    app:si_animation_duration="500"
    app:si_disabled_alpha=".3"
    app:si_disabled_color="#b7b7b7"
    app:si_tint_color="#ff3c00"
    app:si_enabled="false"
    app:si_no_dash="true"
    app:srcCompat="@drawable/ic_cloud"/>
```

### Public methods:
```java
public void setIconEnabled(boolean enabled);
public void setIconEnabled(boolean enabled, boolean animate);
public boolean isIconEnabled();
public void switchState();
public void switchState(boolean animate);
```

## Floating Action Button
Usage:
(Use `layout_anchor` to position FAB between two views)

```xml
    <android.support.design.widget.FloatingActionButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_margin="16dp"
        android:clickable="true"
        android:src="@drawable/star"
        android:tint="@android:color/white"
        app:layout_anchor="@id/collapsing_toolbar"
        app:layout_anchorGravity="bottom|right|end" />
```

 Change FAB icon:
```java
floatingActionButton.setImageDrawable(ContextCompat.getDrawable(getContext(), R.drawable.ic_full_sad));
```

________________________________________________________________________________________________
# UI Components in Java

## Instantiating a view

### New Views
 Using a constructor (context can be an activity)
```java
  TextView myView = new TextView(context);
```

 Using a factory method (documentation recommends this way for some data types)
```java
MediaPlayer player = MediaPlayer.create(context, R.raw.song);
Toast toastMsg = Toast.makeText(context, msgText, duration);
```

### Existing Views
We can look for the view by its id in the views hierarchy within a certain container. Not specifying a container means the search will be on the entire context (`this`).

```java
LinearLayout container = (LinearLayout) findViewById(R.id.container_id);
TextView myView = (TextView) container.findViewById(R.id.view_id);
```

## Common view methods
  - `textView.setText(txt);`
  - `textView.setTextColor(Color.RED);`
  - `imgView.setImageResource(R.drawable.img1);`

## Data Binding
Using the data binding library simplifies binding data to UI components and minimizes glue code. It requires these steps:

1. Enable data binding in build.gradle
2. Add `layout` as the root tag of the UI. Android will generate a new class based on the name of the layout. For example, if the layout file is called `activity_main.xml` the new class will be called `ActivityMainBinding`.
3. Create an instance of the binding class in the activity.
4. Point the data binding instance (`mBinding`) to the correct content view using `DatabindingUtil.setContentView`.
5. Create a Java object that stores the data.
6. Bind each attribute in the views to the corresponding data.

```groovy
// 1. Enable data binding in build.gradle
android {
    dataBinding.enabled = true
}
```

```xml
<!-- activity_main.xml -->
<!-- 2. Add <layout> as the root tag -->
<layout xmlns:android="http://schemas.android.com/apk/res/android">
   <LinearLayout
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:id="@+id/textViewFirstName"/>
       <TextView
           android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:id="@+id/textViewLastName"/>
   </LinearLayout>
</layout>
```

```java
/* MainActivity.java */
public class MainActivity extends AppCompatActivity {
    // 3. Create an instance of the binding class
    ActivityMainBinding mBinding;
    protected void onCreate(Bundle savedInstanceState) {
        // 4. Set the content view
        mBinding = DataBindingUtil.setContentView(this, R.layout.activity_main);
    }
}
// 5. Create a Java object that stores the data.
/* User.java */
public class User {
   public final String firstName;
   public final String lastName;
   public User(String firstName, String lastName) {
       this.firstName = firstName;
       this.lastName = lastName;
   }
}
```

There are two ways to bind the data, either in Java for each view or using binding expressions.

### Configure data binding in Java
```java
void displayUserInfo(User user){
    mBinding.textViewFirstName.setText(user.firstName);
    mBinding.textViewLastName.setText(user.lastName);
}
```

### Using data binding expressions
Data-binding layout files start with a root tag of `layout` followed by a `data` element. Expressions within the layout are written in the attribute properties using the `@{}` syntax.

```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android">
   <data>
       <variable name="user" type="com.example.User"/>
   </data>
   <LinearLayout
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:id="@+id/textViewFirstName"
           android:text="@{user.firstName}"/>
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:id="@+id/textViewFirstName"
           android:text="@{user.lastName}"/>
   </LinearLayout>
</layout>
```
Then you need to bind the data in Java:

```java
protected void onCreate(Bundle savedInstanceState) {
   User user = new User("Test", "User");
   mBinding.setUser(user);
}
```

Binding expressions can be more complex. Basically, most valid Java statements can be used. For example:

```xml
<TextView
    android:text="@{MyStringUtils.capitalize(user.lastName)}"
    android:text="@{user.getLastName}"
    android:visibility="@{user.show ? View.VISIBLE : View.GONE}"
   />
```

________________________________________________________________________________________________
# Logging (writing to LogCat)
- Log class can be used to print a message with a certain severity level to the log.
- Available levels (ordered from low to high): v(erbose), d(ebug), i(nfo), w(arn), e(rror), a(ssert)
- Only error, warn and info are preserved in release versions, while d and v for development

_Usage:_
  - Error: a behavior that should not happen or a crash
  - Warn: problems that do not cause a crash but still concerning, e.g. low disk space in media apps.
  - Info: informational messages, e.g. being connected to the Internet.

_Examples:_

```java
// tag_string is used to identify message source e.g. activity
Log.i(tag_string, msg_string);
```

To make sure that we always print the correct class name we can define a string with the class name in the top of class body:

```java
private final String LOG_TAG = MyClass.class.getSimpleName();
Log.i(LOG_TAG, msg_string);
```

Printing function name:

```java
Log.i(TAG, Thread.currentThread().getStackTrace()[2].getMethodName());
```

________________________________________________________________________________________________
# View generated events (click, etc.)
- Add onClick (or other event) attribute to the XML of a view:
  `android:onClick="method_name"`
- Add a method with the following signature
  `public void method_name(View view)`
- To deal with 'view' cast it to the correct type first
  `boolean checked = ((CheckBox)view).isChecked();`

________________________________________________________________________________________________
# Intents
- An intent is a messageing object used to request an action from another app component, e.g. sending email, calling etc.
- Intents usecases are:
  * Starting an activity
    - You can start a new instance of an Activity by passing an Intent to startActivity().
    - If you want to receive a result from the activity when it finishes, call startActivityForResult(). Your activity receives the result as a separate Intent object in its onActivityResult() callback.
  * Starting an service
    - You can start a service to perform a one-time operation (such as download a file) by passing an Intent to startService().
    - For services with a client-server interface, you can bind to the service by passing an Intent to bindService().
  * Delivering a broadcast
    - A broadcast is a message that any app can receive. E.g. the system delivers a broadcast for device charging event.
    - You can deliver a broadcast to other apps by passing an Intent to sendBroadcast(), sendOrderedBroadcast(), or sendStickyBroadcast().

- Intent components
  * ComponentName
    - Required to build an explicit intent.
    - Can be set within the constructor or using `setComponent()` and includes the full target class name including package name e.g. com.example.MyActivity
  * Action
    - A string that specifies the action type to perform.
      - ACTION_VIEW: use it to show some information to the user e.g. a photo in a gallery app or an address in a map app.
      - ACTION_SEND: use it when you have data the user can share through another app.
    - The action can be specified in the constructor or using `setAction()`
  * DataURI
    - Includes the URI that references the data and/or the data MIME type (which can be inferred by the action and therefore not always needed)
    - When the system cannot infer the type from the URI and the action, it should be explicitly set.
    - `setData()` sets data URI, `setType()` sets the MIME type, and `setDataAndType()` sets both.
    - `setData()` and `setType()` nullify each other and should not be called together.
  * Category
    - A string containing additional information about the kind of component that should handle the intent. Usually not needed.
    - CATEGORY_BROWSABLE specifies an activity able to be started by a web browser.
  * Optional extras.
    - Key-value pairs that carry additional information required to accomplish the requested action. Some actions require certain extras.
    - Many predefined extras exist. You can define your own as well.
  * Flags
    - Metadata of the intent that instruct the system how to launch an activity e.g. whether to place in the list of recent activities

## Explicit Intent
Explicit intent specifies the exact app component (class name) it needs to run. Usually used for components of own app.  
An intent is explicit when the ComponentName field of the intent is set. Other intent properties are optional.

Example 1 - Start a service

```java
// Intent starts a service called DownloadService
Intent downloadIntent = new Intent(this, DownloadService.class);
downloadIntent.setData(Uri.parse(fileUrl));
startService(downloadIntent);
```

Example 2 - Start an activity without passing data

```java
// Start an activity without passing data
startActivity(new Intent(context, SettingsActivity.class));
```

Example 3 - Start an activity with passing data

```java
// Start an activity with passing data
Class destinationActivity = ChildActivity.class;
Intent intent = new Intent(context, destinationActivity);
intent.putExtra(Intent.EXTRA_TEXT, myData);
startActivity(intent);
// OR
startActivity(new Intent(context, ChildActivity.class)
    .putExtra(Intent.EXTRA_TEXT, myData));
```

Receiving data from an intent:

```java
// In onCreate() of the activity or onCreateView() of the fragment triggered by the intent
Intent intent = getActivity().getIntent();
if (intent != null && intent.hasExtra(Intent.EXTRA_TEXT))
  passedStr = intent.getStringExtra(Intent.EXTRA_TEXT);
```

## Implicit Intent
- Implicit intent specifies the functionality it needs regardless of who is going to serve it.
- The system find the appropriate component based on the intent filters declared in the manifest file of other apps.
- Common usecases:
    * Call
      - ACTION_DIAL
      - DataURI:  tel:212555312
    * Location
      - ACTION_VIEW
      - DataURI:  geo:47.9,-122.3
    * Email
      - ACTION_SEND
      - EXTRA_EMAIL:  "to" field
      - EXTRA_SUBJECT: "subject" field
- Media types (MIME):
    - The media type helps Android determine which app can open the content.
    - A media type consists of : type_name/subtype_name[;parameters]
    - E.g. the media type of most web data is: text/html;charset=UTF-8
    - Other examples: text/plain, text/rtf, image/png, video/mp4
    - ShareCompat class contains helper functions to create share intents and build emails (see the examples)

- Usage:
    ```java
    // 1.a Create an intent and set its action type and data
    Intent intent = new Intent(ACTION_TYPE, DATA_URI);
    // 1.b Create an intent setting its action type and set the data later
    Intent intent = new Intent(ACTION_TYPE);
    intent.setData(DATA);
    // 2. Make sure there is an app that can handle the intent
    if (intent.resolveActivity(getPackageManager()) != null)
      startActivity(intent);
    ```
- Example 1 - Open map using coordinates:
    ```java
    Intent intent = new Intent(Intent.ACTION_VIEW);
    intent.setData(Uri.parse("geo:47.9,-122.3"));
    ```
- Example 2 - Open map using location:
    ```java
    Uri geoLocation = Uri.parse("geo:0,0?").buildUpon()
              .appendQueryParameter("q", location)
              .build();
    intent.setData(geoLocation);
    ```
- Example 3 - Open web page
    ```java
    // URL must start with http or https
    Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://msn.com");
    ```
- Example 4.a - Share text and manually building the intent:
    ```java
    Intent sendIntent = new Intent(Intent.ACTION_SEND);
    sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
    sendIntent.setType("text/plain");
    ```
- Example 4.a - Share text and use ShareCompat to build the intent:
    ```java
    String mimeType = "text/plain";
    String title = "Share with friends";
    Intent intent = ShareCompat.IntentBuilder.from(this)
            .setChooserTitle(title)
            .setType(mimeType)
            .setText(shareText)
            .getIntent();
    // Or even faster...
    ShareCompat.IntentBuilder.from(this)
            .setChooserTitle(title)
            .setType(mimeType)
            .setText(shareText)
            .startChooser();
    ```

## PendingIntent
Allows other applications to launch an activity from our app. For example, in order to allow our app to be launched from a notification we need to grant the system NotificationManager permission to do so. A `PendingIntent` includes a description of an intent and target action to perform with it.

To create a `PendingIntent` instance we can use on of the static method in the `PendingIntent` class:
- `getActivity()`
- `getService()`
- `getBroadcast()`

Flags:
- `Flag_UPDATE_CURRENT`- if the intent is created again, keep the intent but update the data

```java
PendingIntent.getActivity(
    Context context,    // The context in which the activity should be started
    int requestCode,    // Unique code of the PendingIntent
    Intent intent,      // The desired intent
    int flags           // Help creating multiple PendingIntents for a single intent.
);                      //  Use Flag_UPDATE/CANCEL_CURRENT for a single instance.
// Example:
private static final int My_INTENT_ID = 3417;
PendingIntent pendingIntent = PendingIntent.getActivity(
    context, My_INTENT_ID, intent, PendingIntent.Flag_UPDATE_CURRENT);
```

> Note: If you are using the PendingIntent to launch an activity don't forget to set it in the manifest as `SingleTop` so it doesn't recreate it if it exists.


## Attaching Intent to Menu Item
If a menu item sole functionality is to start an activity using an intent (calling startActivity(intent)), this item can be bound to an intent when the menu is created.

*_Usage_*:  
In `onCreateOptionsMenu()` do this:

```java
public boolean onCreateOptionsMenu(Menu menu) {
    ...
    MenuItem menuItem1 = menu.findItem(R.id.action_open_map);
    MenuItem menuItem2 = menu.findItem(R.id.action_open_child_activity);
    menuItem1.setIntent(createOpenMapIntent());
    menuItem2.setIntent(createOpenChildIntent());
    ...
}
```

### Intent Filter
  - If an app wants to be listed as an option for handling certain intents it adds an intent-filter within its manifest entry.
  - The intent-filter tells that the app can perform action X on all data which has the Y scheme. For example:
    ```xml
    <intent-filter>
      <action:name="android.intent.action.VIEW"/>
      <data android:scheme="geo" />
    </intent-filter>
    ```

## Passing Objects Through Intents
  - Parcelable and Serialization are used for marshaling and unmarshaling Java objects.
  - Serialization creates a lot of garbage objects and therefore it is slower.

### Serialization
```java
public class Person implements Serializable {
    private String name;
    private int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
// MainActivity.java
public final static String SER_KEY = "MovieData";
public void sendData(){
    Person mPerson = new Person("John", 25);
    Intent intent = new Intent(this,ChildActivity.class);
    Bundle bundle = new Bundle();
    bundle.putSerializable(SER_KEY,mPerson);
    intent.putExtras(bundle);
    startActivity(intent);
}
// ChildActivity.java
protected void onCreate(Bundle savedInstanceState) {
  Person mPerson = (Person) getIntent().getSerializableExtra(MainActivity.SER_KEY);
}
```

### Parcelable
**NOTE:** Check Parceler library below

To allow for your class instances to be sent as a Parcel you must implement the `Parcelable` interface along with a static field called `CREATOR`. The `Parcelable` interface has two methods: `describeContents()` and `writeToParcel()`.

```java
public class Person implements Parcelable {
    private String name;
    private int age;
    // We can have other parcelable objects in our class
    private ParcelableObject info;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    // This constructor is private since it only needed in the CREATOR field
    private Person(Parcel in){
        this.name = in.readString();
        this.age = in.readInt();
        this.info = in.readParcelable(ParcelableObject.class.getClassLoader());
    }

    public static final Parcelable.Creator<Person> CREATOR = new Creator<Person>() {
        @Override
        public Person createFromParcel(Parcel source) {
            return new Person(source);
        }
        @Override
        public Person[] newArray(int size) {
            return new Person[size];
        }
    };
    // These two methods need to be overridden
    @Override
    public int describeContents() {
        // Usually returns 0
        return 0;
    }
    // This is where our data is saved to the Parcel
    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(name);
        dest.writeInt(age);
        dest.writeParcelable(info, flags);
    }
}
// MainActivity.java
public void sendData(){
    Person mPerson = new Person("John", 25);
    Intent intent = new Intent(this,ChildActivity.class);
    intent.putExtra("MyData", mPerson);
    startActivity(intent);
}
// ChildActivity.java
protected void onCreate(Bundle savedInstanceState) {
  Person mPerson = getIntent().getParcelableExtra("MyData");
}
```

#### Parceler library
Parceler is a code generation library that generates the Parcelable boilerplate source code at compile time

__Dependencies__

```groovy
implementation 'org.parceler:parceler-api:1.1.6'
annotationProcessor 'org.parceler:parceler:1.1.6'
```

__Usage__

```java
@Parcel
public class Person implements Serializable {
    private String name;
    private int age;
    @ParcelConstructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
// MainActivity.java
public void sendData(){
    Person mPerson = new Person("John", 25);
    Intent intent = new Intent(this,ChildActivity.class);
    intent.putExtra("MyData", Parcels.wrap(mPerson));
    startActivity(intent);
}
// ChildActivity.java
protected void onCreate(Bundle savedInstanceState) {
    Person mPerson = Parcels.unwrap(getIntent().getParcelableExtra("MyData"));
}
```

## Extras
- Common intents guide for implicit intents:
    <https://developer.android.com/guide/components/intents-common.html>

________________________________________________________________________________________________
# URI

## URI format:
```
  [scheme://][authority][:port][/path][/path][?query][&query.....][#fragment]
  https://www.myawesomesite.com/turtles/types?type=1&sort=relevance#section-name
  content://com.example.udacity.exampleapp/data         // ContentProvider URI
```
## URI Builder:
`URI.Builder` contain convenience methods for constructing URI objects from strings. 
Let's say we want to create this URI:  
`https://www.myawesomesite.com/turtles/types?type=1&sort=relevance#section-name`

Code to create it:

```java
Uri.Builder builder = new Uri.Builder();
builder.scheme("https")
  .authority("www.myawesomesite.com")
  .appendPath("turtles")
  .appendPath("types")
  .appendQueryParameter("type", "1")
  .appendQueryParameter("sort", "relevance")
  .fragment("section-name");
String myUrl = builder.build().toString();
```

The path can be put in a const string:

```java
final String BASE_URL = "http://api.openweathermap.org/../daily?";
Uri builtUri = Uri.parse(BASE_URL).buildUpon()
        .appendQueryParameter(FORMAT_PARAM, format)
        .appendQueryParameter(DAYS_PARAM, Integer.toString(numDays))
        .build();
```

### URI to URL
The URI can be converted to a URL by passing it as a string to the Java URL class constructor as following:

> NOTE: `MalformedURLException` must be handled when calling the URL constructor

Target URL:
      `https://api.github.com/search/repositories?q=android&sort=stars`

```java
final static String GITHUB_BASE_URL = "https://api.github.com/search/repositories";
final static String PARAM_QUERY = "q";
final static String PARAM_SORT = "sort";
final static String sortBy = "stars";
public static URL buildUrl(String githubSearchQuery) {
    Uri builtUri = Uri.parse(GITHUB_BASE_URL).buildUpon()
            .appendQueryParameter(PARAM_QUERY, githubSearchQuery)
            .appendQueryParameter(PARAM_SORT, sortBy)
            .build();
    URL url = null;
    try {
        url = new URL(builtUri.toString());
    } catch (MalformedURLException e) {
        e.printStackTrace();
    }
    return url;
}
```

## ContentUris
This class contains convenience methods for appending id values to a URI. The methods include:
- `Uri withAppendedId(Uri uri, long id)`- Append an id to a URI.
- `long parseId(Uri uri)`- Get the id of the URI.

```java
final Uri CONTENT_URI = Uri.parse("content://user_dictionary/words");
Uri rowUri = ContentUris.withAppendedId(CONTENT_URI, 4);
// Returns content://user_dictionary/words/4
```

________________________________________________________________________________________________
# Toast
 Show a Toast:
```java
int duration = Toast.LENGTH_SHORT;
Toast toast = Toast.makeText(context, text, duration);
toast.show();
// OR
Toast.makeText(context, text, duration).show();
```

 Cancel a Toast. This allows a new Toast to replace an older one immediately. mToast should be defined as a class member variable.
```java
if(mToast != null) mToast.cancel();
mToast = Toast.makeText(this, s, Toast.LENGTH_SHORT);
mToast.show();
```

________________________________________________________________________________________________
# Snackbar
- Snackbars are shown on the bottom of the screen and contain text with an optional single action. They usually fade out after some time.
- Add Gradle dependency:
    `implementation 'com.android.support:design:25.1.1'`
- Usage:

    ```java
    // Show forever
    Snackbar.make(parentView, "No Connection", Snackbar.LENGTH_INDEFINITE).show();
    // Show, add action and set color
    Snackbar sb = Snackbar.make(parentView, "No Connection", Snackbar.LENGTH_LONG)
      .setAction("Retry", new MyUndoListener())
      .setActionTextColor(R.color.green);
    //...
    public class MyUndoListener implements View.OnClickListener{
        @Override public void onClick(View v) {...}
    }
    // Add action METHOD2
    Snackbar sb = Snackbar.make(parentView, "Message is deleted", Snackbar.LENGTH_LONG)
                    .setAction("UNDO", new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar snackbar1 = Snackbar.make(parentView, "Message is restored!", Snackbar.LENGTH_SHORT);
                snackbar1.show();
            }
        });
    // Dismiss
    mySnackbar.dismiss();
    ```

- `parentView` is a `CoordinatorLayout`, `FrameLayout`, or the top-most container layout, whichever comes first.
- Adding a listener:

- Changing action button text color

    ```java
    View sbView = snackbar.getView();
    TextView textView = (TextView) sbView.findViewById(android.support.design.R.id.snackbar_text);
    textView.setTextColor(Color.YELLOW);
    ```

________________________________________________________________________________________________
# Adapters
- Adapters act as a bridge between UI (AdapterView in particular) and the underlying data.
- The Adapter provides access to the data items and is responsible for making a View for each item in the data set.
- You can populate an AdapterView (e.g. RecyclerView) by binding its instance to an Adapter, which retrieves data from an external source and creates a View that represents each data entry.
- There are several subclasses of Adapter that are useful for retrieving different kinds of data and building views for an AdapterView. The most common are ArrayAdapter and SimpleCursorAdapter.

## ArrayAdapter
- Useful when the data source is an array.
- By default it creates a view for each array item by calling toString() on it and placing the contents in a TextView.
- After creating the adapter call setAdapter() on the ListView.
- An ArrayAdapter automatically calls notifyDataSetChanged() when modified to notify the ListView that it is updated.
- Constructor:
    ```java
    ArrayAdapter<T>(context,  // App context
    layout,   // The layout that contains a TextView for each string in the array
    view,   // The relevant TextView
    array )
    ```
- Modifying an adapter:
    ```java
    mAdapter.clear();
    mAdapter.addAll(strList);
    ```
- Example:
    ```java
    ArrayAdapter<String> adapter = ArrayAdapter<>(getActivity(), R.layout.my_list, R.id.my_list_textview, dataList);
    ListView listView = (ListView) findViewById(R.id.listview);
    listView.setAdapter(adapter);
    ```

## CursorAdapter
The `CursorAdapter` will inflate views using an xml layout file and create ViewHolders that will fill the main `ListView`.

________________________________________________________________________________________________
# Menus
Menu options are defined in xml (res/menu/) and can be declared for fragments or activities.

XML format:
: 
- `<menu>` Defines a J:Menu, which is a container for menu items. It is the root node in the file and can hold one or more <item> and <group> elements.
- `<item>` Creates a J:MenuItem. may contain a nested `<menu>` element in order to create a submenu.
- `<group>` An optional, invisible container for `<item>` elements. It allows categorizing menu items so they share properties such as active state and visibility.

XML Example:

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
  <item android:id="@+id/new_game"
      android:icon="@drawable/ic_new_game"
      android:title="@string/new_game"
      android:showAsAction="ifRoom"/>
</menu>
```

XML Attributes:
: 
  `android:showAsAction`  Specifies if the item should appear on the action bar.  
  `android:orderInCategory` - Explicitly specify item order.

## Options Menu
- The options menu includes actions that are relevant to the current activity context (activity or fragment).
- If both activity and fragment(s) declare options menu items they are combined where the activity's items appear first.
- Action buttons are menu items that appear in the menu bar.
- Overflow menu host menu items except the action buttons and usually has the most frequently used items first.
- An item can be set to move from the overflow menu to the action bar when there is room.
- Creating Menu Resource:
  - Right click res folder -> New -> Android Resource Directory
  - Resource type = menu. Choose a name.
  - Right click menu folder -> New -> Menu Resource File

Functions:
: 
- setHasOptionsMenu(true); has to be added to onCreate() or in the constructor in the case of a fragment.
- To specify an options menu, override onCreateOptionsMenu() and inflate the menu resource into the J:Menu provided in the callback (in the parameters list).
- You can use add() and findItem() to add or retrieve menu items.
- Handling click events:  
  * Override onOptionsItemSelected() which passes the J:MenuItem selected.
  * android:onClick attribute in xml can be used to specify a click handler which must accept a MenuItem parameter.
- To identify an item call getItemId() on MenueItem and compare it to the desired R.id

XML:
: The XML may contain a context field that refers to the owner activity. This is only to show the menu in the layout preview; it doesn't have an actual effect.

```xml
<menu tools:context=".MainActivity">
<menu tools:context="com.example.android.sunshine.app.DetailActivity">
```

Examples:

```java
@Override
public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setHasOptionsMenu(true);
}
@Override
// In an activity
public boolean onCreateOptionsMenu(Menu menu) {
  MenuInflater inflater = getMenuInflater();
  inflater.inflate(R.menu.game_menu, menu);
  return true;
}
// In a fragment
public void onCreateOptionsMenu(Menu menu, MenuInflater inflater){
  inflater.inflate(R.menu.forecastfragment, menu);
}
@Override
public boolean onOptionsItemSelected(MenuItem item) {
  switch (item.getItemId()) {
    case R.id.new_game:
      newGame();
      return true;
    default:
      return super.onOptionsItemSelected(item);
  }
}
```

### Attaching Intent to Menu Item
See [Intents] for details.

### ShareActionProvider
It provides a share action in the options menu and only requires a share intent.

Usage:

```java
private ShareActionProvider mShareActionProvider;
/* In Fragment#onCreateOptionsMenu */
public void onCreateOptionsMenu(Menu menu, MenuInflater inflater) {
inflater.inflate(R.menu.detailfragment, menu);
// Locate MenuItem with ShareActionProvider
MenuItem item = menu.findItem(R.id.action_share);
// Fetch and store ShareActionProvider
mShareActionProvider = (ShareActionProvider) MenuItemCompat.getActionProvider(item);
setShareIntent(createShareForecastIntent());
}
// Create a share intent
private Intent createShareForecastIntent() {
  Intent shareIntent = new Intent(Intent.ACTION_SEND);
  shareIntent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET);
  shareIntent.setType("text/plain");
  shareIntent.putExtra(Intent.EXTRA_TEXT, mForecastStr + FORECAST_SHARE_HASHTAG);
  return shareIntent;
}
// Call to update the share intent
private void setShareIntent(Intent shareIntent) {
  if (mShareActionProvider != null) {
    mShareActionProvider.setShareIntent(shareIntent);
  } else {
    Log.d(LOG_TAG, "Share Action Provider is null?");
  }
}
```

Note: While the sample snippet demonstrates how to use this provider in the context of a menu item, its use is not limited to menu items.

Tips:
+ 1.1 If your application contains multiple activities and some of them provide the same options menu, consider creating an activity that implements nothing except the onCreateOptionsMenu() and onOptionsItemSelected() methods. Then extend this class for each activity that should share the same options menu.
+ 1.2  If you want to add menu items to one of the descendant activities, override onCreateOptionsMenu() in that activity. Call super.onCreateOptionsMenu(menu) so the original menu items are created, then add new menu items with menu.add().


________________________________________________________________________________________________
# HTTP Connections
_Required permissions:_

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

_Check Connectivity_

```java
static public boolean isNetworkAvailable(Context c) {
    ConnectivityManager cm =
            (ConnectivityManager)c.getSystemService(Context.CONNECTIVITY_SERVICE);

    NetworkInfo activeNetwork = cm.getActiveNetworkInfo();
    return activeNetwork != null &&
            activeNetwork.isConnectedOrConnecting();
}
```

## Manually
Android has two available HTTP clients: HttpUrlConnection class (recommended) and Apache HttpClient class. Both support https, streaming uploads and downloads, configurable timeouts, IPv6 and connection pooling.

_Example:_

```java
// This function takes a URL querry which is used to receive a response as a JASON formatted string:
String getResponseFromHttpUrl(URL url) throws IOException {
    HttpURLConnection urlConnection = null;
    BufferedReader reader = null;

    // Will contain the raw JSON response as a string.
    String forecastJsonStr = null;

    try {
        // Create the request, and open the connection
        urlConnection = (HttpURLConnection) url.openConnection();
        urlConnection.setRequestMethod("GET");
        urlConnection.connect();

        // Read the input stream into a String
        InputStream inputStream = urlConnection.getInputStream();
        if (inputStream == null) {
            return null;
        }
        StringBuffer buffer = new StringBuffer();
        reader = new BufferedReader(new InputStreamReader(inputStream));

        String line;
        while ((line = reader.readLine()) != null) {
            buffer.append(line + "\n");
        }

        if (buffer.length() == 0) {
            // Stream was empty.  No point in parsing.
            return null;
        }
        forecastJsonStr = buffer.toString();
        return forecastJsonStr;
    } catch (IOException e) {
        Log.e("PlaceholderFragment", "Error ", e);
        return null;
    } finally{
        if (urlConnection != null) {
            urlConnection.disconnect();
        }
        if (reader != null) {
            try {
                reader.close();
            } catch (final IOException e) {
                Log.e("PlaceholderFragment", "Error closing stream", e);
            }
        }
    }
}
```

Using a scanner (see |Scanner| for details):

```java
public static String getResponseFromHttpUrl(URL url) throws IOException {
    HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();
    try {
        InputStream in = urlConnection.getInputStream();
        Scanner scanner = new Scanner(in);
        // Set the delimiter to \A (beginning of the stream) so it returns the whole stream
        scanner.useDelimiter("\\A");
        if (scanner.hasNext()) {
            return scanner.next();
        } else {
            return null;
        }
    } finally {
        urlConnection.disconnect();
    }
}
```

## OkHttp
Library for sending and receive HTTP-based network requests.

Setup:      
: `implementation 'com.squareup.okhttp3:okhttp:3.6.0'`

_Synchronous Get:_

```java
// Not to be used in UI thread
private final OkHttpClient client = new OkHttpClient();
public static String getResponseFromHttpUrl(URL url) throws IOException {
        Request request = new Request.Builder()
                .url(url.toString())
                .build();
        Response response = client.newCall(request).execute();
        if (!response.isSuccessful()) throw new IOException("Unexpected code " + response);
        return response.body().string();
}
```

________________________________________________________________________________________________
# Scanner
- A simple text scanner which can parse primitive types and strings using regular expressions.
- A Scanner breaks its input into tokens using a delimiter pattern, which by default matches whitespace.
- The resulting tokens may then be converted into values of different types using the various next methods.
- The scanner can also use delimiters other than whitespace. This example reads several items in from a string:
    ```java
      String input = "red fish blue fish";
      Scanner s = new Scanner(input).useDelimiter("\\s*fish\\s*");
      System.out.println(s.next());  // prints "red"
      System.out.println(s.next());  // prints "blue"
      s.close();
    ```
- The scanner has several advantages when reading from a HttpURLConnection InputStream:
  - It buffers the data and handles buffers of different sizes
  - Handles character encoding - translates from UTF-8 (JSON default) to UTF-16 (Android default)
  - See [HTTP](#http-connections) for usage example.

________________________________________________________________________________________________
# Permissions
To make use of protected features of the device, you must include one or more `<uses-permission>` tags in your app manifest:

```xml
<uses-permission android:name="android.permission.RECEIVE_SMS" />
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

If the device is running Marshmallow or later we need to ask the user to grant the permissions:

```java
// build.gradle dependency
implementation 'com.android.support:support-v4:26.1.0'

/** In MyActivity **/
// Create a constant to hold the request code
private static final int PERMISSION_REQUEST_CODE_EXT_STORAGE = 724;

// Check if the permission is granted
private void tryToDoStuff() {
    // If the device is running Marshmallow or later we need to ask for permission
    if (ContextCompat.checkSelfPermission(this,
            Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED) {
        if (ActivityCompat.shouldShowRequestPermissionRationale(this,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
            // Explain to the user why you need the permission before asking again
        } else {
            // No explanation needed; request the permission
            ActivityCompat.requestPermissions(this,
                    new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                    PERMISSION_REQUEST_CODE_EXT_STORAGE);
            // For Kotlin:
            // arrayOf(Manifest.permission.WRITE_EXTERNAL_STORAGE),
        }
        return;
    }
    doStuff()
}

// Handle the permissions request response
@Override
public void onRequestPermissionsResult(int requestCode,
                                       String permissions[], int[] grantResults) {
    switch (requestCode) {
        case PERMISSION_REQUEST_CODE_EXT_STORAGE: {
            // If request is canceled, the result arrays are empty.
            if (grantResults.length > 0
                    && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                // permission was granted
                chooseSong();
            } else {
                // permission denied. Disable the functionality.
                Toast.makeText(this, "Storage access denied. Can't load files.",
                        Toast.LENGTH_SHORT).show();
            }
        }
        // other 'case' lines to check for other
        // permissions this app might request.
    }
}
```

To make testing permissions easier, we can grant/revoke permissions through ADB:

```sh
adb shell pm grant <package_name> <permission_name>
adb shell pm revoke com.midisheetmusic android.permission.CAMERA
adb shell pm revoke <package_name> <permission_name>
```

________________________________________________________________________________________________
# JSON
JavaScript Object Notation is a data exchange format and is an alternative for XML.

## Elements
- Objects: A collection of name/value pairs. Represented by a curly bracket ({)
- Array:  Array of JSON objects. Represented by a square bracket ([)
- Key:  A string that is related to a key.
- Value:  Can be string, integer, etc.

## Example
```json
{
  "name": "John",
  "isAlive": true,
  "age": 25,
  "address": {
    "streetAddress": "21 2nd Street",
    "postalCode": "10021-3100"
  },
  "phoneNumbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "office",
      "number": "646 555-4567"
    }
  ],
  "children": [],
  "spouse": null
}
```
## Parsing
1. Create a JSONObject object and specify the JSON data string:
  String data;
    ```java
    JSONObject reader = new JSONObject(data);
    ```
2. Create a JSONObject/JSONArray object for the object/array you want to extract:
    ```java
    JSONObject sys  = reader.getJSONObject("sys");
    JSONArray daysList = forecastJson.getJSONArray("list");
    ```
3. Get the required object from a JSONArray by index or iterate on it:
    ```java
    JSONObject dayInfo = daysList.getJSONObject(0);
    for(int i=0; i < daysList.length(); i++)
      JSONObject dayInfo = daysList.getJSONObject(i);
    ```
4. Use getString(key) (or one of the functions below) to get the value of a specified key:
    > `String country = sys.getString("country");`


## JSONObject Functions
- `getBoolean()`, `getInt()`, `getDouble()`, `getLong()` can be used when value type is other that string.
- `length()`: Return the number of name/value mappings in the object
- `names()`:  Return an array containing the string names in the object.
- `getJSONArray(str)`:  Returns the value mapped by name if it exists and is a JSONArray, or null otherwise.
- `JSONObject.get*()` throw JSONException on failure.
- If "get" in any of the previous functions is replaced with "opt" we get an older functions that returns null on failure.


________________________________________________________________________________________________
# Threading
- By default, android uses a single thread for UI and internal operations.
- If an operation (e.g. network access) blocks the UI thread for more than 5 seconds the OS shows "App not responding" dialog.
- If the app attempts to perform network operations in the main thread the app will crash and throw NetworkOnMainThreadEsception.
- To perform intensive work, worker threads should be used.

## AsyncTask
- AsyncTask allows performing asynchronous work on your user interface.
- It performs the blocking operations in a worker thread and then publishes the results on the UI thread
- AsyncTasks should ideally be used for short operations (a few seconds at the most.)
- If the thread needs to run for a long time use the APIs provided by the java.util.concurrent package such as Executor, ThreadPoolExecutor and FutureTask.
- An AsyncTask is defined by 3 generic types, called Params, Progress and Result, and 4 steps, called onPreExecute, doInBackground, onProgressUpdate and onPostExecute.

Usage
: 
- Subclass AsyncTask and implement the doInBackground() callback method.
- To update UI implement onPostExecute(), which delivers the result from doInBackground() and runs in the UI thread.
- You can implement other optional functions (mentioned below).
- You can then run the task by calling execute() from the UI thread.

Functions (chronological order)
: 
- onPreExecute(),         invoked on the UI thread before the task is executed. E.g. it can show a progress bar in the UI.
- doInBackground(Params...)   executes automatically on a worker thread
- publishProgress(Progress...)  can be called at anytime in doInBackground() to execute onProgressUpdate() on the UI thread
- onProgressUpdate(Progress...) invoked on the UI thread after a call to publishProgress(Progress...)
- onPostExecute(Result),    invoked on the UI thread after the background computation finishes.

Canceling
: 
- A task can be canceled at any time by invoking cancel(boolean) on the AsyncTask object.
- onCancelled(Object) will be invoked instead of onPostExecute() after doInBackground() returns.
- You should check the return value of isCancelled() periodically from doInBackground()

Generic types:
: 
`AsyncTask<Params, Progress, Result>`
: 
1. Params, the type of the parameters sent to the task upon execution.
2. Progress, the type of the progress units published during the background computation.
3. Result, the type of the result of the background computation.
NOTE: The types can be AsyncTask<Void, Void, Void>.

CAUTION:
: 
- Since AsyncTask is created within an activity, changing screen orientation may destroy the working thread.
- Therefor, AsyncTask should only be used for tasks lasting a second or two and which lifecycle is tied to the host activity. In other cases services should be used.

_Example:_

```java
@Override
public void onClick(View v) {
  // Direct calling
  new DownloadImageTask().execute("example.com/image.png");
  // Can also use an instance
  AsyncTask imageTask = new DownloadImageTask();
  imageTask.execute("example.com/image.png");
  // Or like this
  AsyncTask imageTask = new DownloadImageTask().execute("example.com/image.png");
  imageTask.cancel();
  }

private class DownloadImageTask extends AsyncTask<String, Void, Bitmap> {
  protected Bitmap doInBackground(String... urls) {
    return loadImageFromNetwork(urls[0]);
  }
  protected void onPostExecute(Bitmap result) {
    mImageView.setImageBitmap(result);
  }
}
```

## Loaders
Loaders are responsible for performing queries on a separate thread, monitoring the data source for changes, and delivering new results to a LoaderManager when changes are detected.

Usage:
: 
1. Have the your activity or fragment implement `LoaderManager.LoaderCallbacks<T>`
2. Create an instance of the `LoaderManager`
3. Implement your own subclass of `Loader` or `AsyncTaskLoader` to load data from some other source.
4. Create a constant int (Loader ID) to uniquely identify your Loader.
5. Initialize the loader within the activity's `onCreate()` or the fragments `onActivityCreated()` by calling `initLoader()` on the `LoaderManager`.


### Classes and interfaces
There are multiple classes and interfaces that may be involved when using loaders in an app. 

**_LoaderManager_**  
An abstract class associated with an `Activity` or `Fragment` for managing one or more `Loader` instances. There is only one `LoaderManager` per activity or fragment, but a `LoaderManager` can manage multiple loaders.  
To get `LoaderManager`, call `getLoaderManager()` from the activity or fragment.  
To start loading data from a loader, call either `initLoader()` or `restartLoader()`. The system automatically determines whether a loader with the same integer ID already exists and will either create a new loader or reuse an existing loader.

**_LoaderManager.LoaderCallbacks_**  
This interface contains callback methods that are called when loader events occur. It is typically implemented by your activity or fragment and is registered when you call `initLoader()` or `restartLoader()`.  
The interface defines three callback methods: 

* `onCreateLoader(int, Bundle)`
  : Called when the system needs a new loader to be created (after calling `initLoader()` for example). Your code should create a `Loader` object and return it to the system.
* `onLoadFinished(Loader, D)`
  : Called when a loader has finished loading data. Typically, your code should update the UI with the loaded data.
* `onLoaderReset(Loader)`
  : Called when a previously created loader is being reset (when you call `destroyLoader(int)` or when the activity or fragment is destroyed), and thus making its data unavailable. Your code should remove any references it has to the loader's data.

**_Loader_**  
Loaders perform the loading of data. This class is abstract and serves as the base class for all loaders. You can directly subclass `Loader` or use one of the following built-in subclasses to simplify implementation:  

* `AsyncTaskLoader` - an abstract loader that provides an `AsyncTask` to perform load operations on a separate thread.
* `CursorLoader` - a concrete subclass of `AsyncTaskLoader` for asynchronously loading data from a `ContentProvider`. It queries a `ContentResolver` and returns a Cursor.

### _LoaderManager_ Methods
**_initLoader()_**  
: Prepares the loader. Either re-connect with an existing one, or start a new one.  
If the Loader does not exist, `onCreateLoader()` method is triggered.

Example:  
:   `getLoaderManager().initLoader(0, null, this);`

Arguments:
: 
- A unique ID that identifies the loader.
- Optional arguments to supply to the loader at construction (null in this example).
- A `LoaderManager.LoaderCallbacks` implementation, which the `LoaderManager` calls to report loader events. In this example, the local class implements the `LoaderManager.LoaderCallbacks` interface, so it passes a reference to itself, this.

**_restartLoader()_**  
: Discards the loader's old data. Useful when the user's query changes for example. It takes the same arguments as `initLoader()`

Example:  
:   `getLoaderManager().restartLoader(0, null, this);`


<!-- ### _LoaderManager_ Callbacks
A class implementing `LoaderManager.LoaderCallbacks` need to overload these methods:
**_onCreateLoader()_**  
Instantiate and return a new Loader for the given ID. It is called, for example, through `initLoader()` if the loader does not exist.

**_onLoadFinished()_** — Called when a previously created loader has finished its load.
**_onLoaderReset()_** — Called when a previously created loader is being reset, thus making its  -->

## AsyncTaskLoader
Abstract Loader that provides an `AsyncTask` to perform load operations on a separate thread. It is not bound to an activity instance so it will not be destroyed with the activity similar to `AsyncTask`.  

### Methods

* `onStartLoading()`
  : Similar to `onPreExecute()` in `AsyncTask`. Runs in the UI thread.
* `loadInBackground()`
  : Similar to `doInBackground()` in `AsyncTask`. Runs in a background thread. When it finishes it calls `deliverResult(D)` on the UI thread.
* `deliverResult(D)`
  : Called when `doInBackground()` finishes, which passes the result data to it. It is not necessary to overload this method unless there is a need to process the data before the Loader finishes. For example, the data can be cached eliminating the need for calling `forceLoad()` more often than needed in `onStartLoading()` (see the code example).

### Example

```java
public class MainActivity extends AppCompatActivity 
        implements LoaderManager.LoaderCallbacks<String> {

    private static final String SEARCH_QUERY_URL_EXTRA = "query";
    private static final int LOADER_ID = 22;

    void onCreate(){
        //...
        getSupportLoaderManager().initLoader(LOADER_ID, null, this);
    }


    @Override
    public Loader<String> onCreateLoader(int id, final Bundle args) {
        // Return a new AsyncTaskLoader<String> as an anonymous inner class with 
        // this as the constructor's parameter
        return new AsyncTaskLoader<String>(this) {

            // A variable to cache the data
            private String mData;

            @Override
            protected void onStartLoading() {
                // If no arguments were passed, simply return.
                if (args == null) {
                    return;
                }
                // If we already have cached results, just deliver them. Otherwise, force a load.
                if (mData != null){
                    deliverResult(mData);
                } else {
                    forceLoad();
                }
            }

            @Override
            public String loadInBackground() {
                // Extract the search query from the args using our constant
                String searchQueryUrlString = args.getString(SEARCH_QUERY_URL_EXTRA);
                String searchResults;
                // Process the request...
                return searchResults;
            }

            // If we don't cache the data using mData, we don't have to override this method
            @Override
            public void deliverResult(String data) {
                mData = data;
                super.deliverResult(data);
            }

            // Attempt to cancel the current load task if possible (optional)
            @Override protected void onStopLoading() {
                cancelLoad();
            }
        };
    }

    @Override
    public void onLoadFinished(Loader<String> loader, String returnedData) {
        if (null == returnedData) {
            showErrorMessage();
        } else {
            mSearchResultsTextView.setText(returnedData);
          }
    }

    @Override
    public void onLoaderReset(Loader<String> loader) {
        /* Required method to implement the LoaderCallbacks<D> interface */
    }

    private void newSearch(String searchUrl) {
        Bundle bundle = new Bundle();
        bundle.putString(SEARCH_QUERY_URL_EXTRA, searchUrl);

        // Create a Loader if it does not exist or restart it if it exists
        LoaderManager loaderManager = getSupportLoaderManager();
        Loader<String> loader = loaderManager.getLoader(LOADER_ID);
        if (loader == null){
            loaderManager.initLoader(LOADER_ID, bundle, this);
        } else {
            loaderManager.restartLoader(LOADER_ID, bundle, this);
        }
    }
}

```

## CursorLoader
An extension of AsyncTaskLoader that queries the ContentResolver and returns a Cursor.

```java
public class MainActivity extends AppCompatActivity 
        implements LoaderManager.LoaderCallbacks<String> {
    private static final int LOADER_ID = 0;
    void onCreate(){
        getSupportLoaderManager().initLoader(LOADER_ID, null, this);
    }

    private void updateAdapterData() {
        // Create a Loader if it does not exist or restart it if it exists
        LoaderManager loaderManager = getSupportLoaderManager();
        Loader<String> loader = loaderManager.getLoader(LOADER_ID);
        if (loader == null){
            loaderManager.initLoader(LOADER_ID, bundle, this);
        } else {
            loaderManager.restartLoader(LOADER_ID, bundle, this);
        }
    }

    @Override
    public Loader<Cursor> onCreateLoader(int id, Bundle args) {
        return new CursorLoader(this,
                DatabaseContract.CONTENT_URI,
                DatabaseContract.TaskColumns.ALL_COLUMNS.toArray(new String[0]),
                null, null, null);
    }

    @Override
    public void onLoadFinished(Loader<Cursor> loader, Cursor data) {
        mAdapter.setCursor(data);
    }

    @Override
    public void onLoaderReset(Loader<Cursor> loader) {
        mAdapter.setCursor(null);
    }
}
```


________________________________________________________________________________________________
# Preferences
- Settings in android use the Preference API
- Settings are built of 'Preference' objects instead of views, e.g. `CheckBoxPreference` and `ListPreference`.
- Each Preference has a corresponding key-value pair that the system uses to save the setting in a default `SharedPreferences` file for your app settings.
- When the user changes a setting, the system updates the corresponding value in the `SharedPreferences` file.
- Because your app's settings UI is built using Preference objects instead of View objects, you need to use a specialized Activity or Fragment subclass to display the list settings.
- You should use a traditional Activity that hosts a `PreferenceFragment` that displays your app settings or use `PreferenceActivity` (deprecated) to create a two-pane layout for large screens when you have multiple groups of settings.

## Should I use preferences?
![](http://developer.android.com/design/media/settings_flowchart.png)

## Common Preferences Objects
- `CheckBoxPreference`
- `ListPreference`
- `EditTextPreference`

## Preferences XML
- Create a directory res/xml (New >> Android resource directory >> Res. type: xml)
- Create a new xml resource file with Root-element: `PreferenceScreen`
- Add Preference elements as required.
- You can use `PreferenceCategory` and `PreferenceScreen` to organize the settings.

```xml
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
    <CheckBoxPreference
        android:key="@string/pref_sync_key"
        android:title="@string/pref_sync_label"
        android:summaryOff="@string/pref_sync_false"
        android:summaryOn="Sync on"
        android:defaultValue="@bool/pref_sync_default" />
    <EditTextPreference
        android:title="Location"
        android:key="location"
        android:defaultValue="Oslo"
        android:singleLine="true" />
</PreferenceScreen>
```

Common Attributes:
: 
- `android:key` : Specifies a unique key the system uses when saving this setting's value in the SharedPreferences.
- `android:title` : A user-visible name for the setting.
- `android:dialogTitle` : For `ListPreferences`. Equals to `android:title` if not provided.
- `android:defaultValue` : The initial value of the field
- `android:summary` : Extra writing under the title. Can contain the current value or more details.
- `android:summaryOn/Off` : Summary of the field when set/cleared

_NOTE:_ When saving the Preference key string in `strings.xml` set `translatable` to `false`.

```xml
<string name="pref_sync_key" translatable="false">pref_sync</string>
```

_BEST PRACTICE:_ Save all literals (integers, bools, etc.) in resource files:

```xml
<!-- In res/values/bools.xml -->
<resources>
    <bool name="pref_sync_default">true</bool>
</resources>
```
```java
boolean sync_default = getResources().getBoolean(R.bool.pref_sync_default);
```

## Invoking Intents
A preference item can be used to invoke an implicit or explicit intent as:
 
```xml
<Preference android:title="@string/prefs_web_page" >
    <intent android:action="android.intent.action.VIEW"
            android:data="http://www.example.com" />
</Preference>
```

- `android:action` : The action to assign, as per the `setAction()` method.
- `android:data` : The data to assign, as per the `setData()` method.
- `android:mimeType` : The MIME type to assign, as per the `setType()` method.
- `android:targetClass` : The class part of the component name, as per the `setComponent()` method.
- `android:targetPackage` : The package part of the component name, as per the `setComponent()` method.

## Preferences in Java
1.. Create an activity that extends `PreferenceActivity` (deprecated) or a fragment that extends `PreferenceFragment` (android>3.0). Load the preferences from an XML resource in `OnCreate()`

```java
    public static class SettingsFragment extends PreferenceFragment{
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            addPreferencesFromResource(R.xml.preferences);
        }
    }
```

2.. If using a fragment, set it as the main content of the activity:

```java
    public class SettingsActivity extends Activity {
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            // Display the fragment as the main content.
            getFragmentManager().beginTransaction()
                    .replace(android.R.id.content, new SettingsFragment())
                    .commit();
        }
    }
```

   or add it as an XML tag to the activity layout:

```xml
    <fragment xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/activity_settings"
        android:name="android.example.com.myApp.SettingsFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

### Functions
PreferenceFragment functions:
: 
- `findPreference(String key)` : Return a `Preference` instance given its key
- `getPreferenceScreen()` : Return the local `PreferenceScreen` instance
- `setPreferenceSummary(Preference p, String s)` : Set the preference summary of a `Preference`
- `preferenceScreen.getSharedPreferences()` : Return the local `SharedPreferencs` instance
- `preferenceScreen.getPreferenceCount()` : Return the number of existing preferences
- `preferenceScreen.getPreference(i)` : Return the `Preference` object with the index i in the `PreferenceScreen`.
- `sharedPreferences.getString(String key, String default)` : Get the value of a `Preference` given its key.
- `preference.getKey()` : Return the key of a Preference

### Getting Preference Values
_NOTE: If you are using more than one SharedPreferences file, use `getSharedPreferences` method._

```java
SharedPreferences sharedPref = PreferenceManager.getDefaultSharedPreferences(getActivity());
// Get methods format: sharedPref.getType(String prefKey, Type defaultValue)
String locationPref = sharedPref.getString(getString(R.string.pref_location_key), defaultString);
```

### Editing Preference Values
```java
SharedPreferences sharedPref = PreferenceManager.getDefaultSharedPreferences(getActivity());
SharedPreferences.Editor editor = sharedPref.edit();
// Put methods format: editor.putType(String prefKey, Type value)
editor.putBoolean("pref_key", true);
editor.apply();
```

### Set up Preference Change Listener

There are two type of Change Listeners:  
- `PreferenceChangeListener` is triggered before a value is saved to the SharedPreferences file. Because of this, it can prevent an invalid update to a preference.  
- `SharedPreferenceChangeListener` is triggered after a value is saved to the SharedPreferences file.  

#### PreferenceChangeListener
`onPreferenceChange ` method is triggered before a value is saved to the SharedPreferences file and will return either true or false, depending on whether the preference should actually be saved. 

1. Implement `OnPreferenceChangeListener` in the Fragment
2. Attach the listener to the desired preference in `onCreatePreferences`
3. Override `onPreferenceChanged()` and return true if the new value should be stored.

```java
// 1. Implement `OnPreferenceChangeListener` in the Fragment
public class SettingsFragment extends PreferenceFragment implements Preference.OnPreferenceChangeListener
{
    // 2. Attach the listener to the desired preference in `onCreatePreferences`
    public void onCreatePreferences(Bundle bundle, String s) {
        Preference preference = findPreference(getString(R.string.pref_size_key));
        preference.setOnPreferenceChangeListener(this);
    }
    // 3. Override `onPreferenceChanged()` and return true if the new value should be stored.
    public boolean onPreferenceChange(Preference preference, Object newValue) {
       Toast error = Toast.makeText(getContext(), "Please select a number between 0.1 and 3", Toast.LENGTH_SHORT);
       if (preference.getKey().equals(getString(R.string.pref_size_key))) {
           String stringSize = ((String) (newValue)).trim();
           if (stringSize.equals("")) stringSize = "1";
           try {
               float size = Float.parseFloat(stringSize);
               if (size > 3 || size <= 0) {
                   error.show();
                   return false;
               }
           } catch (NumberFormatException e) {
               error.show();
               return false;
           }
       }
       return true;
    }
}
```

#### SharedPreferenceChangeListener
1. Implement `SharedPreferences.OnSharedPreferenceChangeListener` in the Activity/Fragment
2. Override `onSharedPreferenceChanged()`
3. Register the listener in `onCreate()`
4. Unregister the listener in `onDestroy()`

In an Activity:

```java
// 1. Implement OnSharedPreferenceChangeListener
public class MainActivity extends AppCompatActivity implements SharedPreferences.OnSharedPreferenceChangeListener {
    // 2. Override onSharedPreferenceChanged()
    @Override
    public void onSharedPreferenceChanged(SharedPreferences sharedPreferences, String key) {
        // Do something with the new preference
        if (key.equals(getString(R.string.pref_sync_key))) {
            boolean prefBool = sharedPreferences.getBoolean(key, getResources().getBoolean(R.bool.pref_sync_default));
        }
    }
    // 3. Register the listener in `onCreate()`
    protected void onCreate(Bundle savedInstanceState) {
        PreferenceManager.getDefaultSharedPreferences(this)
                .registerOnSharedPreferenceChangeListener(this);
    }
    // 4. Unregister the listener in `onDestroy()`
    protected void onDestroy() {
        PreferenceManager.getDefaultSharedPreferences(this)
                .unregisterOnSharedPreferenceChangeListener(this);
    }
}
```

In a Fragment:

```java
// 1. Implement `SharedPreferences.OnSharedPreferenceChangeListener`
public class SettingsFragment extends PreferenceFragment implements SharedPreferences.OnSharedPreferenceChangeListener {
    // 2. Override `onSharedPreferenceChanged()`
    @Override
    public void onSharedPreferenceChanged(SharedPreferences sharedPreferences, String key) {
        // Do something
    }
    // 3. Register the listener in `onCreate()`
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        getPreferenceScreen().getSharedPreferences().registerOnSharedPreferenceChangeListener(this);
    }
    // 4. Unregister the listener in `onDestroy()`
    public void onDestroy() {
        super.onDestroy();
        getPreferenceScreen().getSharedPreferences().unregisterOnSharedPreferenceChangeListener(this);
    }
}
```


### Bind Preference Summary to the Preference Value:

1. Implement `OnSharedPreferenceChangeListener` in the PreferenceFragment as explained earlier
2. Write a function (e.g. `setPreferenceSummary`) to set preference summary according to its type.
3. Call `setPreferenceSummary` in `onCreatePreferences()`
4. Call `setPreferenceSummary` in `onSharedPreferenceChanged()`

_Example:_ Bind summary to value for all none-CheckBoxPreference preferences as its value is boolean

```java
    // 1. Implement `OnSharedPreferenceChangeListener` in the PreferenceFragment
    // 2. Write a function to set preference summary according to its type.
    private void setPreferenceSummary(Preference preference, String value) {
        if (preference instanceof ListPreference) {
            // For list preferences, figure out the label of the selected value and set the summary to that label
            ListPreference listPreference = (ListPreference) preference;
            int prefIndex = listPreference.findIndexOfValue(value);
            if (prefIndex >= 0)
                listPreference.setSummary(listPreference.getEntries()[prefIndex]);
        } else if (preference instanceof EditTextPreference) {
            // For EditTextPreferences, set the summary to the value
            preference.setSummary(value);
        }
    }
    // 3. Call `setPreferenceSummary` in `onCreatePreferences()`
    public void onCreatePreferences(Bundle bundle, String s) {
        SharedPreferences sharedPreferences = getPreferenceScreen().getSharedPreferences();
        PreferenceScreen preferenceScreen = getPreferenceScreen();
        // Go through all of the preferences, and set up their preference summary.
        for (int i = 0; i < preferenceScreen.getPreferenceCount(); i++) {
            Preference p = preferenceScreen.getPreference(i);
            if(!(p instanceof CheckBoxPreference)){
                String value = sharedPreferences.getString(p.getKey(), "");
                setPreferenceSummary(p, value);
            }
        }
    }
    // 4. Call `setPreferenceSummary` in `onSharedPreferenceChanged()`
    @Override
    public void onSharedPreferenceChanged(SharedPreferences sharedPreferences, String key) {
        Preference p = findPreference(key);
        if(null != p && !(p instanceof CheckBoxPreference)){
            String value = sharedPreferences.getString(p.getKey(), "");
            setPreferenceSummary(p, value);
        }
    }
```

## ListPreference
In addition to the general preference properties we should supply:  
1. `android:entries`: Array with all the option labels.   
2. `android:entryValues`: Array with all the values that will be saved to the preferences file. Must be in sync with `android:entries`.

Functions
: 
- `findIndexOfValue(value)` : Get an entry index given its value
- `getEntries()` : Get an array of the entries (labels)
- `setSummary(summary)` : Set list summary

Usage example:

```xml
<ListPreference
    android:key="@string/pref_units_key"
    android:title="@string/pref_units_label"
    android:dialogTitle="@string/pref_units_label"
    android:defaultValue="@string/pref_units_metric"
    android:entries="@array/pref_units_options"
    android:entryValues="@array/pref_units_values" />
```
```xml
<!-- In res/values/arrays.xml -->
<!-- NOTE: Labels ordering must match values ordering -->
<resources>
    <array name="pref_units_options">
        <item>@string/pref_units_meter_label</item>
        <item>@string/pref_units_inch_label</item>
    </array>
    <array name="pref_units_values">
        <item>@string/pref_units_meter_value</item>
        <item>@string/pref_units_inch_value</item>
    </array>
</resources>
```
Getting selected value:

```java
private void loadUnitFromPref(SharedPreferences sharedPreferences){
    String unit = sharedPreferences.getString(getString(R.string.pref_units_key),
        getString(R.string.pref_units_meter_value));
}
```

________________________________________________________________________________________________
# Notifications
To create a notification we use a notification builder to describe it and a notification manager to display it.

## Building a Notification
To build notifications we create a `NotificationCompat.Builder` object. Several properties can be set for the `Builder`. However, only the first three are mandatory:
- `setContentTitle()`- A title
- `setContentText()`- Detail text. If the text is long it will be trimmed. Set a suitable style to allow for displaying the full text.
- `setSmallIcon()`- A small icon
- `setLargIcon()`- A large icon. Takes a `Bitmap`.
- `setColor()`- Notification color.
- `setStyle()`- Assign one of the available styles (see [example styles](#notification-styles).)
- `setDefaults()`- Notification options: `DEFAULT_SOUND`, `DEFAULT_VIBRATE`, `DEFAULT_LIGHTS`.
- `setContentIntent()`- Supply a `PendingIntent` to send when the notification is clicked. See [PendingIntent](#pendingintent).
- `setAutoCancel()`- Whether the notification is automatically canceled when the clicked. The `PendingIntent` set with `setDeleteIntent` will be broadcast when the notification is canceled.

A priority can be assigned to the notification if SDK >= JELLY_BEAN.

For example:

```java
NotificationCompat.Builder builder = new NotificationCompat.Builder(this)
        .setContentTitle("My notification")
        .setContentText("Hello World!");
        .setSmallIcon(R.drawable.notification_icon)

NotificationCompat.Builder builder = new NotificationCompat.Builder(context)
        .setContentTitle(context.getString(R.string.notification_title))
        .setContentText(context.getString(R.string.notification_body))
        .setSmallIcon(R.drawable.notification_icon)
        .setLargeIcon(getMyLargeIcon(context))
        .setColor(ContextCompat.getColor(context, R.color.colorPrimary))
        .setStyle(new NotificationCompat.BigTextStyle()
            .bigText(context.getString(R.string.notification_body)))
        .setDefaults(Notification.DEFAULT_VIBRATE)
        .setContentIntent(intent)
        .setAutoCancel(true);

if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
    builder.setPriority(Notification.PRIORITY_HIGH);
}
```

### Notification Styles
Notifications in the notification drawer appear in two main visual styles, normal view and big view. The big view of a notification only appears when the notification is expanded.
- BigTextStyle- Will show the text passed to it when the notification is expanded.
- BigPictureStyle- Generates large-format notifications that include a large image attachment.

```java
.setStyle(new NotificationCompat.BigTextStyle()
        .bigText(context.getString(R.string.notification_body)))
.setStyle(new Notification.BigPictureStyle()
        .bigPicture(aBigBitmap))
```

## Issuing a Notification
1. Get an instance of `NotificationManager`.
2. Use the `notify()` method to issue the notification passing a notification ID (any unique integer). You can use this ID to update the notification later on.
3. Call `build()` on the `NotificationBuilder`, which returns a Notification object containing your specifications.

```java
private static final int NOTIFICATION_ID = 1138;
NotificationManager notificationManager = (NotificationManager)
        context.getSystemService(Context.NOTIFICATION_SERVICE);
notificationManager.notify(NOTIFICATION_ID, notificationBuilder.build());
```

## Clear Notifications
```java
notificationManager.cancel(int id); // Cancel a specific notification
notificationManager.cancelAll(); // Cancel all notifications
```

## Notification Actions
```java
Intent dismissIntent = new Intent(context, MyIntentService.class);
intent.setAction(CommonConstants.ACTION_DISMISS_NOTIFICATION);
PendingIntent pendingIntent = PendingIntent.getService(
        context, MY_PENDING_INTENT_ID, dismissIntent, PendingIntent.FLAG_UPDATE_CURRENT);
NotificationCompat.Action action = new NotificationCompat.Action(
        R.drawable.ic_cancel_black, "Dismiss", pendingIntent);
NotificationCompat.Builder builder = new NotificationCompat.Builder(context)
        .addAction();

/* MyIntentService.java */
public class MyIntentService extends IntentService {
    protected void onHandleIntent(Intent intent) {
        String action = intent.getAction();
        if (ACTION_DISMISS_NOTIFICATION.equals(action)) {
            doSomething();
        }
        NotificationManager notificationManager = (NotificationManager)
                context.getSystemService(Context.NOTIFICATION_SERVICE);
        notificationManager.cancelAll();
    }
}
```

________________________________________________________________________________________________
# Firebase

## Setup
From the "Firebase Console" create a new project then select “Add Firebase to your Android App”. Generate the debug certificate and copy the SHA1 line (`keytool` can be found in the Java installation directory):

```shell
keytool -exportcert -list -v -alias androiddebugkey -keystore %USERPROFILE%\.android\debug.keystore
```

- Copy the generated `google-services.json` to the project's `app` directory.
- Add rules to your root-level build.gradle file, to include the google-services plugin:

```
dependencies {
    classpath 'com.google.gms:google-services:3.1.0'
}
```

- In your module Gradle file (usually the `app/build.gradle`), add the apply plugin line at the bottom of the file to enable the Gradle plug-in:

```
apply plugin: 'com.google.gms.google-services'
```

- Add the dependencies for the Firebase SDKs you want to use: <https://firebase.google.com/docs/android/setup#available_libraries>

## Real-time DB
Firebase stores data as JSON objects, i.e. the entire database is stored as a single JSON object. Data in the JSON tree exist as nodes, which are key-value pairs. Keys are always strings and must be unique within their context. Values can be primitive types, such as ints and strings, and nested objects. The nested objects can have unique push IDs generated by firebase to eliminate conflicts. Node values can also be arrays `[key1:value1, key2:value2]` (not recommended) and dictionaries `key1:value1, key2:value2}`.

An object is referred to by a path which starts with a `/` (db root), and has the form form: `/parentKey/childKey/grandChildKey`.

### Code
We need an instance of the Firebase database and a reference to the part of database we are interested in:

```java
private FirebaseDatabase mFirebaseDatabase;
private DatabaseReference mMessagesDatabaseReference;
void onCreate(Bundle savedInstanceState){
    mFirebaseDatabase = FirebaseDatabase.getInstance();
    // Get a reference to the root node
    DatabaseReference rootNode = mFirebaseDatabase.getRefernce();
    // Get a reference to a child node
    mMessagesDatabaseReference = mFirebaseDatabase.getRefernce().child("child_key");
}
```


________________________________________________________________________________________________
# SQLite

## SQLite Commands
```
sqlite3 sunshine.db
  .databases      Print available databases
  .tables         Print available tables
  .schema         Print schema
  .header on      Print colomn names
  .quit           Exit
```

## Querries
 Create tables:
```sql
  CREATE TABLE table_name(
     id INTEGER  PRIMARY KEY AUTOINCREMENT,
     column2 datatype  DEFAULT xxx,
     column3 datatype  NOT NULL,
     data INTEGER NOT NULL,
     timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
     UNIQUE ("date") ON CONFLICT REPLACE);
  CREATE TABLE weather( _id INTEGER PRIMARY KEY, date TEXT NOT NULL, min REAL NOT NULL);
  CREATE TABLE IF NOT EXISTS weather ( ... );
```
> AUTOINCREMENT can only be used with INTEGER datatype.  
> UNIQUE ensures that there is one entry per date. ON CONFLICT REPLACE will replace the old value on conflict.

 Querry rows:
```sql
  SELECT * FROM weather;
  SELECT * FROM weather WHERE date == 20140626;
  SELECT _id,date,min,max FROM weather WHERE date > 20140625 AND date < 20140628;
  SELECT * FROM weather WHERE min >= 18 ORDER BY max ASC;
  SELECT * FROM weather ORDER BY max DESC LIMIT 1;
```
 Insert rows:
```sql
  INSERT INTO table_name VALUES(<values_for_all_columns>);
  INSERT INTO weather    VALUES(1,'20140625',16,20,0,1029);
  INSERT INTO table_name (column_1, column_2) VALUES (value_1,value_2);
  INSERT INTO weather    (_id, date)          VALUES (1,'20140625');
```
 Update rows
```sql
  UPDATE weather SET min = 0, max = 100 where date >= 20140626 AND date <= 20140627;
```
 Delete rows
```sql
  DELETE FROM weather WHERE humidity != 0;
```
 Add columns
```sql
  ALTER TABLE weather ADD COLUMN description TEXT NOT NULL DEFAULT 'Sunny';
```
 Delete table
```sql
  DROP TABLE weather;
  DROP TABLE IF EXISTS weather;
```

## SQL Data Types
- Integer: `INTEGER, INT, UNSIGNED INT, TINYINT, SMALLINT, MEDIUMINT, BIGINT`
- Real:    `REAL, DOUBLE, FLOAT`
- Numeric: `NUMERIC, DECIMAL(10,5), BOOLEAN, DATE, DATETIME`
- Text:    `TEXT, CHAR(20)`

## Foreign Keys
- A `FOREIGN KEY` is a pointer to a `PRIMARY KEY` in another table.
- The `FOREIGN KEY` constraint is used to prevent actions that would destroy links between tables, like inserting invalid data into the foreign key column,

Example: Create a `FOREIGN KEY` field called `location_id` that points to the `_id` field in the `location_table`

```sql
CREATE TABLE weather(
    _id INTEGER PRIMARY KEY AUTOINCREMENT,
    FOREIGN KEY (location_id) REFERENCE location_table (_id));
```

## Inner Join
- Creates a new table by combining columns of two tables based upon the join-predicate.
- `INNER` keyword is optional as this is the default type of join.

_Example_  
Assume we have two tables:

|ID|DepartmentName|
|--|--------------|
|31|Sales         |
|33|Engineering   |

|Name   |DepartmentID|
|-------|------------|
|Smith  |31          |
|Jones  |33          |
|Robinson|34         |

This inner join query will return a table which is the combination of `employee` and `department` tables where the `employee.DepartmentID = department.ID` 

```sql
SELECT * FROM employee INNER JOIN department
  ON employee.DepartmentID = department.ID;
```

This query will return:

|Name |DepartmentID|ID|DepartmentName|
|-----|------------|--|--------------|
|Smith|31          |31|Sales         |
|Jones|33          |33|Engineering   |

A query with implicit join will return the same result:

```sql
SELECT * FROM employee, department
WHERE employee.DepartmentID = department.ID;
```

We can choose to get some of the columns only:

```sql
SELECT employee.Name, employee.DepartmentID, department.DepartmentName 
FROM employee 
INNER JOIN department ON
employee.DepartmentID = department.DepartmentID
```

|Name |DepartmentID|DepartmentName|
|-----|------------|--------------|
|Smith|31          |Sales         |
|Jones|33          |Engineering   |

## SQL in Java

### Contracts
The SQL database tables are defined using contracts (contract classes), where the tables and columns are specified. A good practice is to put the definitions that are global to the whole database in the root of the contract class and create an inner-class for each table.

**Note:** `BaseColumns` is an interface that defines `_id` column that auto-increments and can function as a primary key. Its implementation is expected if you hand off data to a `ContentProvider`. It's not always necessary to implement, but it is a good practice.

```java
public class WeatherContract {
    // To prevent someone from accidentally instantiating the contract class,
    // make the constructor private.
    private WeatherContract() {}
    /* Inner class that defines the contents of the weather table */
    public static final class WeatherEntry implements BaseColumns {
        public static final String TABLE_NAME = "weather";
        // Column with the foreign key into the location table.
        public static final String COLUMN_LOC_KEY = "location_id";
        public static final String COLUMN_TEMP = "temperature";
        // A list of columns is useful when needing to query a ContentProvider for all the columns
        public static final List<String> QUOTE_COLUMNS = new ArrayList<>(Arrays.asList(
                _ID,
                COLUMN_LOC_KEY,
                COLUMN_TEMP
        ));
        // OR using the Guava ImmutableList:
        public static final ImmutableList<String> QUOTE_COLUMNS = ImmutableList.of(
                _ID,
                COLUMN_LOC_KEY,
                COLUMN_TEMP
        );
    }
}
```

### SQLiteOpenHelper
`SQLiteOpenHelper` is a class used to create the database and upgrade it when the `DATABASE_VERSION` changes. In addition, it provides a reference to the database to other classes.     
1. Extend the SQLiteOpenHelper class
2. Create `static final` members for `DATABASE_NAME`, `DATABASE_VERSION` and SQL queries.
3. Create a Constructor that takes a context and calls the parent constructor
4. Override the onCreate method and execute the query to create the table.
5. Override the onUpgrade method and execute the query to recreate/alter the table.

```java
import com.example.android.myApp.data.WaitlistContract.WaitlistEntry;
// 1. extend the SQLiteOpenHelper class
public class WaitlistDbHelper extends SQLiteOpenHelper {
    // 2. Create `static final String` members
    public static final String DATABASE_NAME = "waitlist.db";
    private static final int DATABASE_VERSION = 1;
    // 3. Create a Constructor that takes a context and calls the parent constructor
    WaitlistDbHelper(Context context) {
        super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }
    // 4. Override the onCreate method and execute the query to create the table.
    @Override
    public void onCreate(SQLiteDatabase db) {
        final String SQL_CREATE_ENTRIES  =
                "CREATE TABLE " + WaitlistEntry.TABLE_NAME + " (" +
                        WaitlistEntry._ID + " INTEGER PRIMARY KEY, " +
                        WaitlistEntry.COLUMN_GUEST_NAME + " TEXT NOT NULL, " +
                        WaitlistEntry.COLUMN_PARTY_SIZE + " INTEGER NOT NULL, " +
                        WaitlistEntry.COLUMN_TIMESTAMP + " TIMESTAMP DEFAULT CURRENT_TIMESTAMP" +
                        ");";
        db.execSQL(SQL_CREATE_ENTRIES );
    }
    // 5. Override the onUpgrade method and execute the query to recreate/upgrade the table.
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        final String SQL_DELETE_ENTRIES =
                "DROP TABLE IF EXISTS " + WaitlistEntry.TABLE_NAME;
        db.execSQL(SQL_DELETE_ENTRIES);
        onCreate(db);
    }
}
```

### SQL Database Operations
 Syntax:
```java
// Return a Cursor containing the query result
Cursor db.query (String table,           // The table to query
                 String[] columns,       // The columns to return. Null to return all.
                 String selection,       // The columns for the WHERE clause
                 String[] selectionArgs, // The values for the WHERE clause
                 String groupBy,         // A filter for how to group rows. Null for no grouping.
                 String having,          // Which row groups to include in the cursor
                 String orderBy)         // The sort order
// Insert a row. Returns new row ID or -1 on error
long db.insert( String table, 
                String nullColumnHack,      // Used when values is empty. Normally set to null
                ContentValues values) 
// Return number of deleted rows
int db.delete ( String table, 
                String whereClause,   // The condition for removing the rows. If null, remove all.
                String[] whereArgs)   // If the WHERE clause includes ?'s, they will be replaced with whereArgs

```

 Example:
```java
// Specify which columns from the database we are interested in
String[] columns = {
    BookEntry._ID,
    BookEntry.COLUMN_TITLE
    };
String selection = BookEntry.COLUMN_TITLE + " = ?";
String[] selectionArgs = new String[]{ "Desired Title"};
String sortOrder = BookEntry.COLUMN_DATE + " DESC";

// SELECT * FROM table;
Cursor cursor_basic = db.query(BookEntry.TABLE_NAME, null, null, null, null, null, null);

// SELECT _id, title FROM table WHERE title=="Desired Title" ORDER BY date DESC;
Cursor cursor = db.query(
    BookEntry.TABLE_NAME,                     // The table to query
    columns,                                  // The columns to return
    selection,                                // The columns for the WHERE clause
    selectionArgs,                            // The values for the WHERE clause
    null,                                     // don't group the rows
    null,                                     // don't filter by row groups
    sortOrder                                 // The sort order
    );
// DELETE FROM table WHERE _ID = 1;
String id = "1";
db.delete(BookEntry.TABLE_NAME, BookEntry._ID + "=" + id, null);
db.delete(BookEntry.TABLE_NAME, BookEntry._ID + "= ?", new String[]{id});
// INSERT
db.insert(BookEntry.TABLE_NAME, null, contentValues);
```

### Reading/Writing Databases
1. Get a reference to the database from the DBHelper class in read/write mode (writable allows for reading and writing).
2. Create ContentValues of what you want to insert.
3. Insert ContentValues into the database and get a raw ID back.
4. Query the database and receive a Cursor back.

```java
private SQLiteDatabase mDb;
protected void onCreate(Bundle savedInstanceState) {
    WaitlistDbHelper dbHelper = new WaitlistDbHelper(this);
    // Get a writable database reference
    mDb = dbHelper.getWritableDatabase();
}
// Run a query on the DB and return a list of the desired contents
List<String> readFromDb(){
    List<String> contents = new ArrayList<>();
    // Run a query to read some data from the database (see previous section for usage)
    Cursor cursor = mDb.query(...);
    if(cursor.moveToFirst()){
        contents.add(cursor.getString(cursor.getColumnIndex(WaitlistEntry.COLUMN_GUEST_NAME)));
        while(cursor.moveToNext())
            contents.add(cursor.getString(cursor.getColumnIndex(WaitlistEntry.COLUMN_GUEST_NAME)));
    }
    return contents;
}
// Write a row to the DB
void writeToDb(String name, int size){
    ContentValues contentValues = new ContentValues();
    contentValues.put(WaitlistEntry.COLUMN_GUEST_NAME, name);
    contentValues.put(WaitlistEntry.COLUMN_PARTY_SIZE, size);
    mDb.insert(WaitlistEntry.TABLE_NAME, null, contentValues);
}
```

### Integrating with a RecyclerView


________________________________________________________________________________________________
# Testing
[Espresso cheat sheet](https://google.github.io/android-testing-support-library/docs/espresso/cheatsheet)

Remember to follow the 3 General steps of Espresso View Testing:

1. Find the view
2. Perform action on the view
3. Check if the view does what you expected

## Instrumented Tests
Instrumented tests test UI components and need to be run on a device or emulator. Espresso is useful for testing: Views, AdapterViews, Intents, Idling Resources (asynchronous code that runs off the main thread e.g. DB access).

### Dependencies
```groovy
defaultConfig {
        ...
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
dependencies {
    androidTestCompile 'com.android.support:support-annotations:25.3.1'
    androidTestCompile 'com.android.support.test.espresso:espresso-core:2.2.2'
    androidTestCompile 'com.android.support.test:runner:0.5'
}
```

### Usage
Create a new Java class in `app/src/androidTest/java/app_name` and annotate with `@RunWith(AndroidJUnit4.class)`. This tells Android Studio to run the test with AndroidJUnit4, which helps control launching the app as well as running UI tests on it.

`@Rule`: Used to set the test rules
- `ActivityTestRule` is a rule that provides functional testing for a specific single activity.
    The `ActivityTestRule` is a rule provided by Android used for functional testing of a single activity. The activity that will be tested will be launched before each test that's annotated with `@Test` and before methods annotated with `@before`. The activity will be terminated after the test and methods annotated with `@After` are complete. This rule allows you to directly access the activity during the test.
- `IntentsTestRule` initializes Intents before each Espresso test (`@Test`) is run and releases the Intent after each test is run. The associated activity is terminated after each test.

```java
    //Single views
    onView(ViewMatcher)
        .perform(ViewAction)
        .check(ViewAssertion);
    // AdapterViews
    onData(ObjectMatcher)
        .DataOptions
        .perform(ViewAction)
        .check(ViewAssertion);
```

`DataOptions` includes:
- `inAdapterView(Matcher)`
- `atPosition(Integer)`
- `onChildView(Matcher)`


### Testing Intents
In the course of testing intents we use two concepts:
- *_Intent Stub_* - A code that acts as a fake response to an intent call during a test. Used for testing intent *responses*. Created using `intending` function.

```java
    // Stub all Intents to ContactsActivity to return VALID_PHONE_NUMBER. Note that the Activity
    // is never launched and result is stubbed.
     @Test
     public void pickContactButton_click_SelectsPhoneNumber() {
        private static final String VALID_PHONE_NUMBER = "123-345-6789";
        intending(hasComponent(hasShortClassName(".ContactsActivity")))
                .respondWith(new ActivityResult(Activity.RESULT_OK,
                        ContactsActivity.createResultData(VALID_PHONE_NUMBER)));
    }
```

- *_Intent Verification_* - Used to verify that the intended information is what was actually sent. Created using `intended` function.

```java
    @Test
    public void typeNumber_ValidInput_InitiatesCall() {
        // The click action sends an intent
        onView(withId(R.id.button_call_number)).perform(click());

        // Verify that an intent to the dialer was sent with the correct action, data and package
        intended(allOf(
                hasAction(Intent.ACTION_CALL),
                hasData(INTENT_DATA_PHONE_NUMBER),
                toPackage(PACKAGE_ANDROID_DIALER)));
    }
```

_Blocking external Intents_

```java
    @Before
    public void stubAllExternalIntents() {
        // By default Espresso Intents does not stub any Intents. Stubbing needs to be setup
        // before every test run. In this case all external Intents will be blocked.
        intending(not(isInternal())).respondWith(new ActivityResult(Activity.RESULT_OK, null));
    }

```

_Insure permissions are granted_  
Insure required permissions are granted for Android M+ devices.

```java
    @Before
    public void grantPhonePermission() {
        // In M+, trying to call a number will trigger a runtime dialog. Make sure
        // the permission is granted before running this test.
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            getInstrumentation().getUiAutomation().executeShellCommand(
                    "pm grant " + getTargetContext().getPackageName()
                            + " android.permission.CALL_PHONE");
        }
    }

```


### Matchers
`Matcher<View>` (ViewMatcher):  
<https://developer.android.com/reference/android/support/test/espresso/matcher/ViewMatchers.html>

`Matcher<Object>`:  
<http://hamcrest.org/JavaHamcrest/javadoc/1.3/org/hamcrest/Matchers.html>

_String Matcher_

``` java
onData(is(instanceOf(String.class)), is("Americano")));
//partial text match:
onData(is(instanceOf(String.class)), containsString("ricano")));
//starts with text:
onData(is(instanceOf(String.class)), startsWith("Amer")));
```

_Map Matcher_

```java
// For SimpleAdapter that returns key-value pairs stored as a Map
onData(is(instanceOf(Map.class)), hasEntry(equalTo("jobTitle"), is("Barista")));
```

_CursorAdapter Matcher_

```java
onData(is(instanceOf(Cursor.class)), CursorMatchers.withRowString("job_title", is("Barista")));
```


### Actions
```java
    // Clicking
    .perform(click())
    // Typing
    .perform(typeText(VALID_PHONE_NUMBER), closeSoftKeyboard());
```

### Test Example

```java
import static android.support.test.espresso.Espresso.onView;
import static android.support.test.espresso.action.ViewActions.click;
import static android.support.test.espresso.assertion.ViewAssertions.matches;
import static android.support.test.espresso.matcher.ViewMatchers.withId;
import static android.support.test.espresso.matcher.ViewMatchers.withText;

@RunWith(AndroidJUnit4.class)
public class MyActivityBasicTest {
    @Rule
    public ActivityTestRule<MyActivity> mActivityTestRule
            = new ActivityTestRule<MyActivity>(MyActivity.class);
    @Test
    public void clickIncrementButton_ChangesQuantityAndCost(){
        /* Regular Views */
        //1. Find the view
        //2. Perform action on the view
        onView(withId(R.id.increment_button)).perform(click());
        //3. Check if the view does what you expected
        onView(withId(R.id.quantity_text_view)).check(matches(withText("1")));
        onView(withId(R.id.cost_text_view)).check(matches(withText("$5.00")));

        // Check if an activity is launched
        onView(withId(R.id.activity_detail)).check(matches(isDisplayed()));

        /* AdapterViews */
        // onData(ObjectMatcher)
        //     .DataOptions
        //     .perform(ViewAction)
        //     .check(ViewAssertion);
        onData(anything())
            .inAdapterView(withId(R.id.tea_grid_view)).atPosition(1)
            .perform(click());
        // Checks that the activity opens with the correct tea name displayed
        onView(withId(R.id.tea_name_text_view)).check(matches(withText("Green Tea")));
    }
}
```

________________________________________________________________________________________________
# Libraries and Tools

## ButterKnife
Provides field and method binding for Android views which uses annotation processing to generate boilerplate code for you.

### Dependencies
```groovy
    implementation 'com.jakewharton:butterknife:8.6.0'
    annotationProcessor 'com.jakewharton:butterknife-compiler:8.6.0'
```

### Usage

 Eliminate `findViewById` calls by using `@BindView` on fields.
``` java
class ExampleActivity extends Activity {
  @BindView(R.id.user) EditText username;
  @BindView(R.id.pass) EditText password;

  @BindString(R.string.login_error) String loginErrorMessage;

  @OnClick(R.id.submit) void submit() {
    // TODO call server...
  }

  @Override public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.simple_activity);
    ButterKnife.bind(this);
    // TODO Use fields...
  }
}
```

### RESOURCE BINDING
 Bind pre-defined resources with `@BindBool`, `@BindColor`, `@BindDimen`, `@BindDrawable`, `@BindInt`, `@BindString`
```java
class ExampleActivity extends Activity {
  @BindString(R.string.title) String title;
  @BindDrawable(R.drawable.graphic) Drawable graphic;
  @BindColor(R.color.red) int red; // int or ColorStateList field
  @BindDimen(R.dimen.spacer) Float spacer; // int (for pixel size) or float (for exact value) field
  // ...
}
```

### NON-ACTIVITY BINDING
 You can also perform binding on arbitrary objects by supplying your own view root.
```java
public class FancyFragment extends Fragment {
  @BindView(R.id.button1) Button button1;
  @BindView(R.id.button2) Button button2;

  @Override public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(R.layout.fancy_fragment, container, false);
    ButterKnife.bind(this, view);
    // ...
    return view;
  }
}
```

### LISTENER BINDING
 Listeners can also automatically be configured onto methods. All arguments to the listener method are optional.
```java
@OnClick(R.id.submit)
public void submit() {
  // TODO submit data to server...
}
```

 Define a specific type and it will automatically be cast.
```java
@OnClick(R.id.submit)
public void sayHi(Button button) {
  button.setText("Hello!");
}
```

 Specify multiple IDs in a single binding for common event handling.
```java
@OnClick({ R.id.door1, R.id.door2, R.id.door3 })
public void pickDoor(DoorView door) {
  if (door.hasPrizeBehind()) {
    Toast.makeText(this, "You win!", LENGTH_SHORT).show();
  } else {
    Toast.makeText(this, "Try again", LENGTH_SHORT).show();
  }
}
```

________________________________________________________________________________________________
## Stetho (Debug Network and DB)
Facebook's Stetho project enables you to use Chrome debugging tools to troubleshoot network traffic, database files, and view layouts. With this library, you need to have an active emulator or device running, and you use Chrome to connect to the device by typing `chrome://inspect`.

### Dependencies
```groovy
  implementation 'com.facebook.stetho:stetho:1.5.0'
```

 Create a new class that extends `Application` and override `onCreate` method:
```java
public class MyApplication extends Application {
    public void onCreate() {
        super.onCreate();
        Stetho.initializeWithDefaults(this);
    }
}
```

 Add the Application class to the Manifest
```xml
<application 
    android:name=".MyApplication"
    ... >
</application>
```

________________________________________________________________________________________________
## Gson
Gson is a Java library that can be used to convert Java Objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object.

### Dependencies
```groovy
  implementation 'com.google.code.gson:gson:2.8.0'
```

### Deserializing JSON objects
 Let's say we have the following JSON:
```json
 {
    "id": "58d96993925141442f028bef",
    "author": "in_the_crease",
    "content": "Don't let the title and promotional ..."
}
```

 We want to parse the JSON into this class. We can either name the fields according to the expected JSON or annotate the field with `@SerializedName` and use any name. Note that we don't have to take all the fields.
```java
public class Review {
    @SerializedName("id")
    int reviewId;
    String author;
}
```

 The code to convert:
```java
Gson gson = new Gson();
Review review = gson.fromJson(jsonString, Review.class);
```

### Deserializing JSON arrays
```json
[
    {   "id": "1234123",
        "author": "in_the_crease",
        "content": "Don't let the title and promotional ..."
    },
    {   "id": "235234",
        "author": "author2",
        "content": "More random content ..."
    }
]
```

 An extra step is needed when parsing to a container, e.g. `ArrayList`:
```java
Gson gson = new Gson();
Type listType = new TypeToken<List<MovieData>>() {}.getType();
List<MovieData> parsedMovieData = gson.fromJson(resultsArray.toString(), listType);
```

________________________________________________________________________________________________
## MP Android Chart
This library supports `LineChart`, `BarChart`, `ScatterChart`, `CandleStickChart`, `PieChart`, `BubbleChart` or `RadarChart`. We will discuss `LineChart` below.

### Dependencies
```groovy
implementation 'com.github.PhilJay:MPAndroidChart:v3.0.2'
```

### Usage
```xml
    <com.github.mikephil.charting.charts.LineChart
        android:id="@+id/chart"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

Adding data:

For `LineChart` the `Entry` class represents a single entry in the chart. Other classes are available (e.g. `BarEntry`).

```java
LineChart chart = new LineChart(Context);
YourData[] dataObjects = ...;

List<Entry> entries = new ArrayList<Entry>();
for (YourData data : dataObjects) {
    // turn your data into Entry objects
    entries.add(new Entry(data.getValueX(), data.getValueY())); 
}
```

Next, the entries list needs to be added to a `LineDataSet` which allows data styling. The `label` will show up as the data legend if enabled.

```java
LineDataSet dataSet = new LineDataSet(entries, "Label"); // add entries to dataset
dataSet.setColor(...);
dataSet.setValueTextColor(...); // styling, ...
```

Finally, the `LineDataSet` object/objects are added to the a `LineData` object, which holds all the data to be represented by the chart. Then we set the data object to the chart and refresh it:

```java
LineData lineData = new LineData(dataSet);
chart.setData(lineData);
chart.invalidate(); // refresh
```

_____________
## Guava (CSV Parsing and String Utilites)
A library with several useful utilities

### Dependencies
```groovy
implementation 'com.android.support:support-annotations:25.3.1'
```

### String Splitting and CSV Parsing
```java
List<String> lines = Lists.newArrayList(Splitter.on('\n')
                .trimResults()
                .omitEmptyStrings()
                .split(mHistory));
```

### String operations
Including string joining, splitting matching, Charset convesion and CaseFormat (i.e. `LOWER_CAMEL`, `LOWER_HYPHEN`, etc.)
<https://github.com/google/guava/wiki/StringsExplained>

________________________________________________________________________________________________
## Annotations Library
Using enums in Android is expensive, so it is recommended to use `static final integer` constants. However, to get the type safety we get with enums we can use the Android Support Annotations library. It allows us to denotes that the annotated integer element, represents a logical type and that its value should be one of the explicitly named constants.

- `@interface` is used to declare the new enumerated annotation type.
- `@IntDef` and `@StringDef` specify the constants that will be part of the type.
- `@Retention(RetentionPolicy.SOURCE)`  tells the compiler not to store the enumerated annotation data in the `.class` file so it doesn't affect our runtime.

### Dependencies
```groovy
implementation 'com.android.support:support-annotations:25.3.1'
```

### Usage
```java
// Define the list of accepted constants and declare the NavigationMode annotation
@Retention(RetentionPolicy.SOURCE)
@IntDef({NAVIGATION_MODE_STANDARD, NAVIGATION_MODE_LIST, NAVIGATION_MODE_TABS})
public @interface NavigationMode {}

// Declare the constants
public static final int NAVIGATION_MODE_STANDARD = 0;
public static final int NAVIGATION_MODE_LIST = 1;
public static final int NAVIGATION_MODE_TABS = 2;

// A method that returns a NavigationMode
@NavigationMode
public abstract int getNavigationMode();

// A method that takes a NavigationMode as a parameter
public abstract void setNavigationMode(@NavigationMode int mode);
```

________________________________________________________________________________________________
## Schematics (Help with Content Providers)
A library to reduce the boiler plate code required for content providers.

________________________________________________________________________________________________
## Volly (Networking)
Volley is an HTTP library that makes networking for Android apps easier and faster.

```groovy
implementation 'com.android.volley:volley:1.1.1'
```

_Permissions_

```
android:permission="android.permission.INTERNET"
```

________________________________________________________________________________________________
## Android-SwitchIcon (Switch icon with animation)
Google launcher-style implementation of switch (enable/disable) icon with easy animation.
See <https://github.com/zagum/Android-SwitchIcon>.

________________________________________________________________________________________________
# Widgets

## Widget Components
_1.. `AppWidgetProviderInfo` XML file_  
It includes the widget meta-data such as its size, preview image etc.
- The widget dimensions can be chosen based how many home screen cells the widget would cover as `Size = 70dp * n - 30dp`
- `android:updatePeriodMillis` defines how often the `AppWidgetProvider` should be called to update the widget.

```xml
<!-- xml/my_widget_info.xml -->
<appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
    android:initialLayout="@layout/widget_today_small"
    android:minHeight="@dimen/widget_today_default_height"
    android:minWidth="@dimen/widget_today_default_width"
    android:previewImage="..."
    android:updatePeriodMillis="0" />
```

_2.. Widget Layout_  
The actual layout of the widget.

```xml
<!-- layout/widget_today.xml -->
<LinearLayout
    ...
    android:id="@+id/widget">
    <ImageView
        android:id="@+id/widget_image"
        tools:src="@drawable/my_image" />
    <TextView
        android:id="@+id/widget_text"
        android:textAppearance="?android:textAppearanceLarge" />
</LinearLayout>
```

_3.. `AppWidgetProvider` class_  
It includes the logic for creating the widget views, filling them with data and setting up click listeners.

```java
public class TodayWidgetProvider extends AppWidgetProvider {
    public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
        // Perform this loop procedure for each widget instance
        for (int appWidgetId : appWidgetIds) {
            int layoutId = R.layout.widget_today_small;
            RemoteViews views = new RemoteViews(context.getPackageName(), layoutId);

            // Add the data to the RemoteViews
            views.setImageViewResource(R.id.widget_image, R.drawable.my_image);
            // Content Descriptions for RemoteViews were only added in ICS MR1
            setRemoteContentDescription(views, description);
            views.setTextViewText(R.id.widget_text, "Widget Text");

            // Create an Intent to launch MainActivity
            Intent launchIntent = new Intent(context, MainActivity.class);
            PendingIntent pendingIntent = PendingIntent.getActivity(context, 0, launchIntent, 0);
            views.setOnClickPendingIntent(R.id.widget, pendingIntent);

            // Tell the AppWidgetManager to perform an update on the current app widget
            appWidgetManager.updateAppWidget(appWidgetId, views);
        }
    }
}
```

_4.. Configuration Activity (optional)_  
Allows the user to setup the widget at creation time.

## Add to the Manifest
```xml
<receiver android:name="ExampleAppWidgetProvider" >
    <intent-filter>
        <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
    </intent-filter>
    <meta-data android:name="android.appwidget.provider"
               android:resource="@xml/example_appwidget_info" />
</receiver>
```

## Widget Preview Image
1. Use the WidgetPreview app in android emulator to generate the preview image.
2. Put the image in `drawable-nodpi` folder.
3. Use `android:previewImage` property in the `appwidget-provider` to set the image.

## Collection Widgets
(Guide: <https://www.sitepoint.com/killer-way-to-show-a-list-of-items-in-android-collection-widget/>)

Widgets use the `RemoteViewsService` to display collections that are backed by remote data, such as from a content provider.

The additional components required for a collection widget are:
- `RemoteViewsFactory` serves the purpose of an adapter in the widget's context (handles the task of filling the widget with appropriate data).
- `RemoteViewsService` which main purpose is to return a `RemoteViewsFactory` object.

### RemoteViewsFactory
- `onCreate` is called when the appwidget is created for the first time.
- `onDataSetChanged` is called whenever the appwidget is updated.
- `getCount` returns the number of records in the cursor. (In our case, the number of task items that need to be displayed in the app widget)
- `getViewAt` handles all the processing work. It returns a RemoteViews object which in our case is the single list item.
- `getViewTypeCount` returns the number of types of views we have in ListView. In our case, we have same view types in each ListView item so we return 1 there.

```java
public class WidgetRemoteViewsFactory implements RemoteViewsService.RemoteViewsFactory {
    private Context mContext;
    private Cursor mCursor;

    public WidgetRemoteViewsFactory(Context applicationContext, Intent intent) {
        mContext = applicationContext;
    }

    public void onCreate() {}

    public void onDataSetChanged() {
        if (mCursor != null)
            mCursor.close();

        final long identityToken = Binder.clearCallingIdentity();
        Uri uri = Contract.URI;
        mCursor = mContext.getContentResolver().query(uri, null, null, null, Contract._ID + " DESC");

        Binder.restoreCallingIdentity(identityToken);
    }

    public void onDestroy() {
        if (mCursor != null)
            mCursor.close();
    }

    public int getCount() {
        return mCursor == null ? 0 : mCursor.getCount();
    }

    public RemoteViews getViewAt(int position) {
        if (position == AdapterView.INVALID_POSITION || mCursor == null || !mCursor.moveToPosition(position)) {
            return null;
        }

        RemoteViews rv = new RemoteViews(mContext.getPackageName(), R.layout.collection_widget_list_item);
        rv.setTextViewText(R.id.widgetItemTaskNameLabel, mCursor.getString(1));
        return rv;
    }

    public RemoteViews getLoadingView() { return null; }

    public int getViewTypeCount() { return 1; }

    public long getItemId(int position) {
        return mCursor.moveToPosition(position) ? mCursor.getLong(0) : position;
    }

    public boolean hasStableIds() { return true; }

}
```

### RemoteViewsService
Create a new service class and add it to the Manifest:

```java
public class WidgetRemoteViewsService extends RemoteViewsService {
    public RemoteViewsFactory onGetViewFactory(Intent intent) {
        return new WidgetRemoteViewsFactory(this.getApplicationContext(), intent);
    }
}
```
```xml
<!-- BIND_REMOTEVIEWS permission lets the system bind your service to create the widget 
views for each row and prevents other apps from accessing your widget's data -->
<service android:name=".AppWidget.WidgetRemoteViewsService"
    android:permission="android.permission.BIND_REMOTEVIEWS"/>
```

Then we start the service in the widget provider:

```java
// WidgetProvider.java
public void onUpdate(Context context, AppWidgetManager appWidgetManager, int[] appWidgetIds) {
    for (int appWidgetId : appWidgetIds) {
        RemoteViews views = new RemoteViews(context.getPackageName(), R.layout.widget);
        // Start the RemoteViewsService
        Intent intent = new Intent(context, MyWidgetRemoteViewsService.class);
        views.setRemoteAdapter(R.id.widgetListView, intent);
        appWidgetManager.updateAppWidget(appWidgetId, views);
    }
}
```

### Collection Widget Layout
We need to add a `ListView` to the widget layout and create a `widget_list_item.xml` to define the list items.

### Updating the widget
Whenever you change the list contents you have to send a Broadcast to the `WidgetProvider`.
To do this, we define a new method in `CollectionAppWidgetProvider` class and call it whenever the data set changes. We also override the `onReceive` method to receive the broadcast.

```java
public static void sendRefreshBroadcast(Context context) {
    Intent intent = new Intent(AppWidgetManager.ACTION_APPWIDGET_UPDATE);
    intent.setComponent(new ComponentName(context, CollectionAppWidgetProvider.class));
    context.sendBroadcast(intent);
}

public void onReceive(final Context context, Intent intent) {
    final String action = intent.getAction();
    if (action.equals(AppWidgetManager.ACTION_APPWIDGET_UPDATE)) {
        // refresh all your widgets
        AppWidgetManager mgr = AppWidgetManager.getInstance(context);
        ComponentName cn = new ComponentName(context, CollectionAppWidgetProvider.class);
        mgr.notifyAppWidgetViewDataChanged(mgr.getAppWidgetIds(cn), R.id.widgetListView);
    }
    super.onReceive(context, intent);
}
```

________________________________________________________________________________________________
# Android Virtual Device (Emulator)
- `10.0.2.2` :  The host's `localhost` (`127.0.0.1`)
- `10.0.2.15`:  The emulated device network/ethernet interface

________________________________________________________________________________________________
# APIs

## Weather API
```
q=(city),(country_code)
zip=(zip_code),(country_code)
mode=xml/html (Default:JSON)
units=metric/imperial (Defautl:Kelvin)

api.openweathermap.org/data/2.5/weather?param1=xxx&param2=xxx
api.openweathermap.org/data/2.5/weather?q=Oslo,no&units=metric&APPID=[APPID]
api.openweathermap.org/data/2.5/forecast?q=Oslo,no&units=metric&APPID=[APPID]
api.openweathermap.org/data/2.5/forecast/daily?q=Oslo,no&units=metric&cnt=7&APPID=[APPID]
api.openweathermap.org/data/2.5/forecast/daily?q=94043,us&mode=json&units=metric&cnt=7&APPID=[APPID]
```

## The Movie DB
Example API Requests:

- Specific movie:
    <https://api.themoviedb.org/3/movie/550?api_key=[API_KEY]>
- Trailer:
    - <http://api.themoviedb.org/3/movie/[ID]/videos?api_key=[API_KEY]>
    - Video URL: <https://www.youtube.com/watch?v=[key]>  (key example: Rt2LHkSwdPQ)
    - Thumbnails:
        - <https://img.youtube.com/vi/[key]/mqdefault.jpg>
        - <https://img.youtube.com/vi/[key]/0.jpg> (a bit larger than default)
- Reviews:
    <http://api.themoviedb.org/3/movie/[ID]/reviews?api_key=[API_KEY]>
    <http://api.themoviedb.org/3/movie/234125/reviews?api_key=[API_KEY]>
- Popular movies list:
    - <http://api.themoviedb.org/3/movie/popular?api_key=[API_KEY]>
- Top-rated movies list:
    <http://api.themoviedb.org/3/movie/top_rated?api_key=[API_KEY]>

Constructing the image poster path:
:
1. The base URL will look like: `http://image.tmdb.org/t/p/`
2. Then you will need a size, which will be one of the following: `w92`, `w154`, `w185`, `w342`, `w500`, `w780`, or `original`. For most phones we recommend using `w185`.
3. And finally the poster path returned by the query, in this case `/nBNZadXqJSdt05SHLqgT0HuC5Gm.jpg`

Combining these three parts gives us a final url of <http://image.tmdb.org/t/p/w185/nBNZadXqJSdt05SHLqgT0HuC5Gm.jpg>


________________________________________________________________________________________________
# ADB
Simulate the phone being unplugged from usb charging:

    adb shell dumpsys battery set usb 0

On Android 6.0 or higher:

    adb shell dumpsys battery unplug

To "plug" the phone back in:

    adb shell dumpsys battery reset


________________________________________________________________________________________________
# Keyboard shortcuts
- Format all text:          Alt+Ctrl+L
- Extract string resource:      Alt+Enter
- Action menue and quick help     Ctrl+Shift+A
- Open a class file         Ctrl+N => name[:line_nr]
- Open a non-class file       Ctrl+Shift+N => = = =
- Incremental highlighting      Alt+UP
- Show function signature tooltip   Ctrl+P
- Show template (snippet) list    Ctrl+J
- Show available methods to override Ctrl+O
- Show method inline documentation  Ctrl+Q
- Rename              Shift+F6

- Instantiate an object of the expected type after "new"      Alt+Shift+Space:
- To view all exit points of a method, place the caret at one of them, e.g. the return statement, and press Alt+Shift+O

________________________________________________________________________________________________
# Android Studio Templates
- `logi/d/e/w`: `Log.i(TAG, String);`
- `logt`: `private static final String TAG = "ClassName";`
- `logm`: Log method name and its arguments
- `logr`: Log result of the method
- `.var`: Convert into a variable

________________________________________________________________________________________________
# Design time attributes (tools namespace)
- `showin`: Tell an included layout where it's going to be inserted. E.g. when reusing a layout
- `listitem`: Tell a RecyclerView or a ListView what the list item should be.

________________________________________________________________________________________________
# Online materials
- Material design guidelines:
  <http://www.google.com/design/spec/material-design/introduction.html>
- Nice appearance tips: Google+ tags: #AndroidDev #Protip
- Material design:
    * <http://android-developers.blogspot.no/2014/08/material-design-in-2014-google-io-app.html>

- Search engine optimization:
    * <https://www.fiksu.com/blog/seo-best-practices-android-apps>
    * <http://www.creativebloq.com/tips-naming-app-9112818> (Use time machine)
- Styling Android blog: <http://blog.stylingandroid.com/>
- Android support libraries blog: <https://chris.banes.me/>
- Android SDK Search chrome extention
- Design App Settings:
    + <https://www.google.com/design/spec/patterns/settings.html>
    + <http://developer.android.com/guide/topics/ui/settings.html>

________________________________________________________________________________________________
|Remember |
- Update |Menu| notes.
10/2/2017
- Card UI <http://www.technotalkative.com/lazy-productive-android-developer-4/>
- Shrink Your Code and Resources
    <https://developer.android.com/studio/build/shrink-code.html>
- Mock up tools <http://www.technotalkative.com/lazy-part-8-wireframemockup-tools/>
- Look into SyncAdapters <https://developer.android.com/training/sync-adapters/creating-sync-adapter.html>
