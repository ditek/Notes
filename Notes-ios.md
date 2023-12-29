# Shortcuts
On the Navigator Panel on the left side, the following keyboard shortcuts cycle through the different navigators.

    ⌘ + 0 = Show or Hide the Navigator Panel
    ⌘ + 1 = Project
    ⌘ + 2 = Source Control
    ⌘ + 3 = Symbol
    ⌘ + 4 = Find
    ⌘ + 5 = Issue
    ⌘ + 6 = Test
    ⌘ + 7 = Debug
    ⌘ + 8 = Breakpoint
    ⌘ + 9 = Report

The Utility Area on the right side of Xcode can also be toggled with the following keyboard shortcuts:

    ⌥ + ⌘ + 0 = Show or Hide the Utility Area
    ⌥ + ⌘ + 1 = File Inspector
    ⌥ + ⌘ + 2 = Quick Help Inspector
    ⌥ + ⌘ + 3 = Identity Inspector
    ⌥ + ⌘ + 4 = Attributes Inspector
    ⌥ + ⌘ + 5 = Size Inspector
    ⌥ + ⌘ + 6 = Connections Inspector

# Concepts

## MVC Design Pattern
- Model: Stores the app data.
- View: Graphics, text and interactive elements.
    + Storyboard
    + Assets
    + LaunchScreen
- Controller: Connects the view and the model.
    + Delegates
    + View Controllers

## Delegate Pattern
Delegation allows one object to send messages to another object when a specific event happens.
It often involves implementing a protocol with the methods that would be called upon certain events.
An example of delegates is `AVAudioRecorderDelegate` which defines a method that's called when recording finishes.

Delegates can be set either from Storyboard (for UI components) or by setting the `delegate` property on an object.

## Completion Handler
Using it allows passing a closure to function that would be called on function completion. This allows separating data processing from UI for example.

```go
// In `model/Student.swift`
class Student{
    func requestPicture(_ completionHandler: @escaping (UIImage?, Error?) -> Void) {
        // Obtain image from DB or API
        guard image = imageFromDB() else {
            completionHandler(nil, error)
            return
        }
        completionHandler(image, nil)
    }
}

// In `View/ViewController.swift`
student.requestPicture { image, error in
    imageView.image = image
}
```

_______________________________________________________________________________

# UI Design

## Storyboard
- AppDelegate: Listens to system events: app start, memory warnings, sent to background.
- ViewController: 

### Actions and Outlets
An Action is a function that gets triggered by a UI event, e.g. button press.
An Outlet is an instance of a UI component.

To create an Action/Outlet we have several options:
1. We open Storyboard in Assistant mode and Ctrl + drag the UI component to the code.
2. Create the Actions/Outlets in code first and then from the Navigator to create an:
    - Outlet: Ctrl + drag from the VC to the component.
    - Action: Ctrl + drag from the component to the VC
3. From the connections inspector: Select the VC from Navigator (left panel) and from the utilities panel (right panel) select the Connections Inspector. Here we have an overview of all connections and we can easily create/remove then.

In code, the actions/outlets are defined as follows:

```go
@IBOutlet weak var startButton: UIButton!
@IBAction func startRecording(_ sender: Any) {}
```

## App Lifecycle
- Not running
- Inactive (foreground): App is being launched and cannot receive events.
- Active (foreground): App is fully launched and can receive events. 
- Background: UI not shown but can execute code.
- Suspended: App in memory but cannot execute code.

### ViewController Lifecycle
- `viewDidLoad()`: Called when  UIViewController is first loaded into memory.
- `viewWillAppear()`: Called when the view controller is about to appear on screen.
- `viewDidAppear()`: Called after the view controller appears on screen.
- `viewWillDisappear()`: Called when the view controller is about to disappear.
- `viewDidDisappear()`: Called after the view controller disappears.

To use any of those functions we need to overload them in the UIViewController class. Make sure to call the superclass implementation of the function:

```go
class ViewController: UIViewController {    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated: Bool)
    }
}

```

_______________________________________________________________________________

## Multiple View
No other components are needed to transition between views using Modal presentation. However, for other presentation modes, we need a navigation controller.

To place the view controller in a navigation controller either:
- select it and then: Editor -> Embed In -> Navigation Controller.
- right click on the navigation controller and set `root view controller property`.

### Transition Using Segues

__Segue from a button press__

- To link pressing a button to the new view controller, Ctrl + drag from the button to the view controller.
- You can also right click on the button and drag from `Targeted Segues` to the target view controller.
- Release and choose a `Segue` type. `Show` would cause a transition to the second view controller.
- `sender` argument of the segue will be the `UIButton` object.

__Segue from code__

- First create a segue between the two view controllers by pressing Ctrl + dragging the mouse from the first to the second.
- Give the segue a unique identifier, e.g. "mySegueID"
- Call `performSegue` function:

```go
@IBAction func gotoSecondView(_ sender: Any) {
    // We can send an optional value
    let variableToSend = 10
    performSegue(withIdentifier: "mySegueID", sender: optionalVariableToSend)
}
```

#### Prepare for Segue
This method is called automatically before a segue is performed. It can be used to prepare for the segue.

```go
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
    if segue.identifier == "mySegueID" {
        let destinationVC = segue.destination as! MyDestinationViewController
        // In case we sent a value
        let myVar = sender as! Int
        // Now we can assign it to a local variable in the destination VC
        destinationVC.destinationVar = myVar
    }
}
```

### Presenting VCs

#### Custom VCs
Here we assume the target VC is created using Storyboard.

```go
// Make sure that the VC has an identifier in storyboard
let controller = storyboard?.instantiateViewController(withIdentifier: "MyDestinationViewController") as! MyDestinationViewController
// Option 1: Use Modal transition
present(controller, animated: true, completion: nil)
// Option 2: Use Show transition
self.navigationController?.pushViewController(controller, animated: true)
// If Option 2 is used, we need to add a button in the destination VC to move back
navigationController?.popToRootViewController(animated: true)
```

#### Built-in VCs
iOS has a few built-in VCs
- `UIActivityViewController`: Shows the activities the user can perform (copy, share, etc.)
- `UIImagePickerController`: Pick an image.
- `UIAlertController`: Shows an alert.

```go
let image = UIImage()
let activityVC = UIActivityViewController(activityItems: [image], applicationActivities: nil)

let alertVC = UIAlertController(title: "Error", message: "It's broken", preferredStyle: .actionSheet)
// We can add an action to dismiss the alert
let okAction = UIAlertAction(title: "OK", style: .default) {
    action in self.dismiss(animated: true, completion: nil)
}
alertVC.addAction(okAction)

let imagePickerVC = UIImagePickerController()
```

We can use the `present` function to show the VCs.

```go
// Params:
// - animated: whether to animate the view transition.
// - completion: a function to call upon completion
present(_ viewControllerToPresent: UIViewController, animated: Bool, completion: (() -> Void)? = nil)
// Example:
present(UIImagePickerController(), animated: true, completion: nil)
```

##### UIImagePickerController
Allows the user to pick an image or take a photo via the camera.

__Properties__

```go
let pickerController = UIImagePickerController()
// A class the implements the delegate
pickerController.delegate = self
// Whether the resizing & cropping interface should be presented after selecting a picture
// If true, use the .editedImage instead of the .originalImage key inside the picker delegate
pickerController.allowsEditing = true
// Media types are valid with the source is not the camera i.e. storage
pickerController.mediaTypes = ["public.image", "public.movie"]
// Available sources: `camera`, `photoLibrary` (default), `savedPhotosAlbum` (only camera roll)
pickerController.sourceType = .photoLibrary
// Check if a source is available
UIImagePickerController.isSourceTypeAvailable(type)
```

__Delegate__

    UIImagePickerControllerDelegate, UINavigationControllerDelegate

__Delegate Callbacks__

```go
    // Called when the user picks an item
    imagePickerController(_:didFinishPickingMediaWithInfo:)
    // Called when the user clicks cancel
    imagePickerControllerDidCancel(_:) 
```

__info.plist__

- `NSCameraUsageDescription`
- `NSPhotoLibraryUsageDescription`

__Usage__

```go
func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any]) {
    if let image = info[.originalImage] as? UIImage {
        imageView.image = image
        picker.dismiss(animated: true, completion: nil)
    }
}
```

##### UIActivityViewController
Shows the activities the user can perform (copy, share, etc.).

__Properties__

```go
let vc = UIActivityViewController(activityItems: [memeImage], applicationActivities: nil)
// Handler to execute after the activity view controller is dismissed.
vc.completionWithItemsHandler = {}
// Signature
func(activityType: UIActivity.ActivityType?, completed: Bool, returnedItems: [Any]?, error: Error?) -> Void
// Example
vc.completionWithItemsHandler = { (type, completed, items, error) in
    if completed {
        ...
    }
}
```

__info.plist__

- `NSPhotoLibraryAddUsageDescription`

### Storing Shared Data

#### AppDelegate
The simplest option. It uses the app delegate, to which all VCs have access.

```go
// Store a variable
let appDelegate = UIApplication.shared.delegate as! AppDelegate
appDelegate.myInt = 10
// Retrieve a variable
var myStoredInt: Int { return appDelegate.myInt }
// As a computed variable
var myStoredInt: Int {
    let appDelegate = UIApplication.shared.delegate as! AppDelegate
    return appDelegate.myInt
}
```

_______________________________________________________________________________

## Constraints
Fill parent:
- Ctrl + drag diagonally from the child view to the parent view.
- Shift + select:
    + Leading Space to Safe Area
    + Trailing Space to Safe Area
    + Top Space to Safe Area
    + Bottom Space to Safe Area
- Select each constraint in the document outline and set its constant to 0.

_______________________________________________________________________________

## Adding UI Components in Code
```go
class ViewController: UIViewController {
    override func viewDidLoad() {
        let label = UILabel(frame: CGRect(x: 100, y: 100, width: 50, height: 50))
        label.text = "Hello"
        // `view` points to the root view
        view.addSubview(label)

        // Add target action
        let button = UIButton()
        button.addTarget(self, action: #selector(ViewController.doStuff), for: .touchUpInside)
    }
    // Actions must have the @objc decorator
    @objc func doStuff(){...}
}
```

_______________________________________________________________________________

## UI Components

### ViewController
To create a new view controller either:
- create a class for the new view controller: File -> New -> File... -> Cocoa Touch Class -> Subclass of `UIViewController`.
- create a new swift file in which create a class that inherits `UIViewController`.

From Storyboard -> Identity Inspector, change the class field to the name of the name we chose for the new class.

__Properties__

```go
// Screen dimensions
view.frame.size.width
view.frame.size.height
```

### StackView
Allows stacking components vertically or horizontally.

__Properties__
- `Alignment` (of children): Fill, Leading, Trailing, Center.
- `Distribution` (of children).
- `Spacing`: Space between children.

### UIAlertController
```go
func showAlert(_ title: String, message: String) {
    let alert = UIAlertController(title: title, message: message, preferredStyle: .alert)
    alert.addAction(UIAlertAction(title: Alerts.DismissAlert, style: .default, handler: nil))
    self.present(alert, animated: true, completion: nil)
}
```

### UIButton
_Make sure images don't get squished on small screens_

```go
slowButton.imageView?.contentMode = .scaleAspectFill
```

### UIImageView
```go
let img = UIImageView()
// Image from assets
img.image = UIImage(named: "d\(secondValue)")

```

### UITextField

__Delegate__

`UITextFieldDelegate`

__Delegate Methods__

Editing lifecycle methods:

    // Whether to allow the text to be edited
    textFieldShouldBeginEditing(_:)
    // Called as soon as the user taps inside a textfield
    textFieldDidBeginEditing(_:)
    textFieldShouldEndEditing(_:)
    // Called when the text field loses focus
    textFieldDidEndEditing(_:)

The clear button (the ‘x’ on the right side of some text fields):

    textFieldShouldClear(_:)

When a user taps the return button:

    // Whether to process the pressing of the Return button
    textFieldShouldReturn(_:)

Asks the delegate whether to change the specified text. Called whenever user actions cause its text to change.
We return `true` if the specified text range should be replaced and `false` to keep the old text.
- `replacementString` is the new string. It's empty when the user deletes characters.
- `range` is the range of characters to be replaced.

    textField(_ textField:shouldChangeCharactersIn range:replacementString:) -> Bool

We usually have those two lines when we need to modify the text field:

```go
var newText = textField.text! as NSString
newText = newText.replacingCharacters(in: range, with: string)
```

__Methods__

```go
// Dismisses the keyboard
textField.resignFirstResponder()
// Check whether it's being edited
textField.isEditing
// Change text style

    strokeColor - This will give us our black outline.
    foregroundColor - This will provide the white fill.
    font - Here we select the font name.
    strokeWidth - Here we can control the outline width.

let textAttributes: [NSAttributedString.Key: Any] = [
    // This will give a black outline
    .strokeColor: UIColor.black ,
    // This will give a white fill
    .foregroundColor: UIColor.white,
    .font: UIFont(name: "HelveticaNeue-CondensedBlack", size: 40)!,
    // Outline width. Should be a negative float
    .strokeWidth:  -4.0
]
textField.defaultTextAttributes = textAttributes
```

### UITableView
The individual rows in a table view are managed by table view cells (`UITableViewCell`), which are responsible for drawing their contents.

__Delegate__

`UITableViewDelegate`: Handles responses to user events.
`UITableViewDataSource`: Handles access to data and cells.

__Delegate Methods__

```go
// How many rows to display in a given section
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
// Provides a cell to display for a given row. See usage below.
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
// Optional. Called when a row is selected
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) 
// Optional. Returns `1` by default.
// How many sections (cell groups) to display
func numberOfSections(in tableView: UITableView) -> Int
// Optional. If you change the appearance of your custom cell’s views, implement this to restore them to default
func prepareForReuse()
```

Instead of creating new cells to display data, we use `dequeueReusableCell(withIdentifier:for:)` to reuse a cell from the table view when possible. If no cells are available, the method instantiates a new one.
The cell identifier tells the method which type of cell it should create or reuse. We set the identifier in the cell properties.

Example:

```go
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    guard let cell = tableView.dequeueReusableCell(withIdentifier: "MyCell") else {
        fatalError("Failed to dequeue a cell with the specified identifier.")
    }
    let item = myList[indexPath.row]
    cell.textLabel?.text = item
    return cell
}

// We usually want to trigger a transition when a row is selected
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    let vc = self.storyboard!.instantiateViewController(withIdentifier: "MyViewController") as! MyViewController
    vc.field = myList[indexPath.row]
    navigationController!.pushViewController(vc, animated: true)
}
```

__Adding Navigation Bar to UITableViewController__

To add a navigation bar to a `UITableViewController` we need to place it in a navigation controller and then add this in the view controller:

```go
override func viewDidLoad() {
    navigationItem.rightBarButtonItem = UIBarButtonItem(barButtonSystemItem: .add, target: self, action: #selector(clickHandler))
}
```

__Cell Methods__

```go
// Invalidates the layer’s layout and marks it as needing an update.
setNeedsLayout()
```

### UICollectionView
Very similar to `UITableView`, but uses a grid to view the items.

__Delegate Methods__

```go
func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int
func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath:IndexPath)
func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell

// Example
override func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
    guard let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "MyCell", for: indexPath) else {
        fatalError("Failed to dequeue a cell with the specified identifier.")
    }
    cell.textLabel?.text = item
    return cell
}
```

__View Methods__

```go
/* Reloading Content */
func reloadData()                   // Reloads all of the data for the collection view.
func reloadSections(IndexSet)       // Reloads the data in the specified sections.
func reloadItems(at: [IndexPath])   // Reloads just the items at the specified index paths.
```

To lay out the elements in the grid we need a `UICollectionViewFlowLayout`.

#### UICollectionViewFlowLayout
A layout object that organizes items into a grid with optional header and footer views for each section.

Properties include:

- `minimumLineSpacing` governs the space between rows or columns
- `minimumInteritemSpacing` governs the space between items within a row or column
- `itemSize` governs cell size


```go
class VillainCollectionViewController: UICollectionViewController {
    
    @IBOutlet weak var flowLayout: UICollectionViewFlowLayout!
    override func viewDidLoad() {
        let space: CGFloat = 3.0
        let dimension = (view.frame.size.width - (2 * space)) / 3.0
        flowLayout.minimumInteritemSpacing = space
        flowLayout.minimumLineSpacing = space
        flowLayout.itemSize = CGSize(width: dimension, height: dimension)
    }
}
```

### Navigation Item
Every view controller has a navigation item by default. It can be customized in StoryBoard or in code.

```go
class MyViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        navigationItem.rightBarButtonItem = UIBarButtonItem(title: "Action", style: .plain, target: self, action: #selector(doStuff))
    }
    func doStuff() {}
}
```

### UINavigationController
Handles a stack of view controllers.

Every view controller has a reference to the navigation controller it's part of. It can be used to perform navigation.

```go
class MyViewController: UIViewController {
    func navigate() {
        if let navigationController = navigationController {
            // Navigate one step back (pop off the current VC)
            navigationController.popViewController(animated: true)
            // Navigate all the way to the root VC 
            navigationController.popToRootViewController(animated: true)
        }
    }
}
```

### UITabBarController
Includes a button bar that allows transitioning to different view controllers by adding them to its `view controller` list.

## UIPickerView
Uses a `PickerViewDataSource` and `PickerViewDelegate` to handle elements. They are very similar to the ones used in TableView.

_______________________________________________________________________________

# Platform Foundation

## NSNotification
Handles broadcasting events to registered observers.
`NotificationCenter` registers observers and delivers notifications. Objects use `NotificationCenter` instance to post and observe a notification.

### Posting a Notification

```go
// Syntax
// aName The name of the notification.
// anObject The object posting the notification.
// aUserInfo Optional information about the the notification.
func post(name aName: NSNotification.Name, object anObject: Any?, userInfo aUserInfo: [AnyHashable : Any]? = nil)

// Example
static let URLContainerDidAddURL = NSNotification.Name("URLContainerDidAddURL")
NotificationCenter.default.post(name: .URLContainerDidAddURL, object: self, userInfo: ["username": "Jon"])
```

### Observing Notification using Selector
When subscribing to system notifications, `object` argument would usually be `nil`.

```go
// Syntax
// observer: An object to register as an observer.
// anObject: If specified, only receive notifications from this sender. If nil, receive from all senders.
func addObserver(_ observer: Any, selector aSelector: Selector, name aName: NSNotification.Name?, object anObject: Any?)

// Example
func subscribe(for obj: MyObjectType) {
    NotificationCenter.default.addObserver(self,
        selector: #selector(urlContainerDidAddURL(_:)),
        name: .URLContainerDidAddURL,
        object: obj)
}
// A good practice is using name of the notification as the method name
@objc func urlContainerDidAddURL(_ notification: Notification) {
    let username = notification.userInfo?["username"]
}
```

### Observing Notification using Closure
`NotificationCenter` takes a closure that would handle the event and returns the observer object.

```go
func addObserver(
    forName name: NSNotification.Name?, object obj: Any?, queue: OperationQueue?, using block: @escaping (Notification) -> Void
) -> NSObjectProtocol

// Usage
private var observer: AnyObject?    func subscribe(for container: URLContainer) {
    guard observer == nil else { return }
    observer = NotificationCenter.default.addObserver(forName: .URLContainerDidAddURL, object: container, queue: nil) {notification in
        print(notification.userInfo?[URLContainer.urlKey])
    }
}
func unsubscribe() {
    if let observer = observer {
        NotificationCenter.default.removeObserver(observer)
        self.observer = nil
    }
}
deinit {
    unsubscribe()
}
```

### Unregistering an Observer

```go
// Syntax
func removeObserver(_ observer: Any, name aName: NSNotification.Name?, object anObject: Any?)

// Example
func unsubscribe(from obj: MyObjectType) {
    NotificationCenter.default.removeObserver(self, name: .URLContainerDidAddURL, object: obj)
}
```

_______________________________________________________________________________

# UIKit

## UIApplication
Provide several features including opening other apps.

### Redirecting to another app

```go
UIApplication.shared.open(url, options: [:], completionHandler: nil)
```

### Handling Redirect URLs
First, we add a URL Type to our project to tell iOS that we support that URL.
In Project -> Info -> URL Types, we set the following:
- Identifier: The unique app ID, e.g. com.ditek.MyApp
- URL Scheme: E.g. "signin".

https://auth.udacity.com/sign-up?next=https://classroom.udacity.com/authenticated

```go
// AppDelegate.swift 
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    
    let components = URLComponents(url: url, resolvingAgainstBaseURL: true)
    
    if components?.scheme == "signin" && components?.path == "authenticate" {
        let loginVC = window?.rootViewController as! LoginViewController
        _ = TMDBClient.createSessionId(completion: loginVC.handleSessionResponse(success:error:))
    }
    
    return true
}
```

_______________________________________________________________________________

# Built in Frameworks

## AVFoundation

```go
import AVFoundation
```

### AVAudioRecorder

```go
var audioRecorder: AVAudioRecorder!

@IBAction func recordAudio(_ sender: AnyObject) {
    let dirPath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0] as String
    let recordingName = "recordedVoice.wav"
    let pathArray = [dirPath, recordingName]
    let filePath = URL(string: pathArray.joined(separator: "/"))

    // AVAudioSession is an abstraction of the audio hardware.
    // The shared instance is an instance that's created by default when the app starts running.
    // Since there is only one audio hardware, there is one AVAudioSession, which is the shared session.
    let session = AVAudioSession.sharedInstance()
    // Set up the session for playing and recording audio
    try! session.setCategory(
        AVAudioSession.Category.playAndRecord, mode: AVAudioSession.Mode.default,
        options: AVAudioSession.CategoryOptions.defaultToSpeaker)

    try! audioRecorder = AVAudioRecorder(url: filePath!, settings: [:])
    audioRecorder.isMeteringEnabled = true
    audioRecorder.prepareToRecord()
    audioRecorder.record()
}
@IBAction func stopRecording(_ sender: Any) {
    audioRecorder.stop()
    let session = AVAudioSession.sharedInstance()
    try! session.setActive(false)
}
```

__Delegates__

`AVAudioRecorderDelegate`

Defines the following methods:

    audioRecorderDidFinishRecording(_ recorder: AVAudioRecorder, successfully flag: Bool)
    audioRecorderEncodeErrorDidOccur(_ recorder: AVAudioRecorder, error: Error?)

We need to set the current view controller as the delegate and implement the delegate protocol.

```go
class ViewController: UIViewController, AVAudioRecorderDelegate{
    var audioRecorder: AVAudioRecorder!
    func runsBeforeRecording(){
        audioRecorder.delegate = self
    }
    func audioRecorderDidFinishRecording(_ recorder: AVAudioRecorder, successfully flag: Bool) {
        if flag {
            print("Recording successful!")
        }
    }
}
```

### AVAudioEngine
Used to generate and process audio signals

```go
class PlaybackViewController: AVAudioPlayerDelegate {

    var audioFile: AVAudioFile!
    var audioEngine: AVAudioEngine!
    var audioPlayerNode: AVAudioPlayerNode!
    var stopTimer: Timer!

    func setupAudio() {
        // initialize audio file
        do {
            audioFile = try AVAudioFile(forReading: recordedAudioURL as URL)
        } catch {
            showAlert(Alerts.AudioFileError, message: String(describing: error))
        }        
    }

    // Connect List of Audio Nodes    
    func connectAudioNodes(_ nodes: AVAudioNode...) {
        for x in 0..<nodes.count-1 {
            audioEngine.connect(nodes[x], to: nodes[x+1], format: audioFile.processingFormat)
        }
    }

    @objc func stopAudio() {
        if let audioPlayerNode = audioPlayerNode {
            audioPlayerNode.stop()
        }
        if let stopTimer = stopTimer {
            stopTimer.invalidate()
        }                        
        if let audioEngine = audioEngine {
            audioEngine.stop()
            audioEngine.reset()
        }
    }
    
    func playSound(rate: Float, pitch: Float, echo: Bool = false, reverb: Bool = false) {
        // initialize audio engine components
        audioEngine = AVAudioEngine()
        
        // node for playing audio
        audioPlayerNode = AVAudioPlayerNode()
        audioEngine.attach(audioPlayerNode)
        
        // node for adjusting rate/pitch
        let changeRatePitchNode = AVAudioUnitTimePitch()
        changeRatePitchNode.pitch = pitch
        changeRatePitchNode.rate = rate
        audioEngine.attach(changeRatePitchNode)
        
        // node for echo
        let echoNode = AVAudioUnitDistortion()
        echoNode.loadFactoryPreset(.multiEcho1)
        audioEngine.attach(echoNode)
        
        // node for reverb
        let reverbNode = AVAudioUnitReverb()
        reverbNode.loadFactoryPreset(.cathedral)
        reverbNode.wetDryMix = 50
        audioEngine.attach(reverbNode)
        
        // connect nodes
        connectAudioNodes(audioPlayerNode, changeRatePitchNode, echoNode, reverbNode, audioEngine.outputNode)
        
        // schedule to play and start the engine!
        audioPlayerNode.stop()
        audioPlayerNode.scheduleFile(audioFile, at: nil) {
            var delayInSeconds: Double = 0
            
            if let lastRenderTime = self.audioPlayerNode.lastRenderTime, let playerTime = self.audioPlayerNode.playerTime(forNodeTime: lastRenderTime) {
                delayInSeconds = Double(self.audioFile.length - playerTime.sampleTime) / Double(self.audioFile.processingFormat.sampleRate) / Double(rate)
            }
            
            // schedule a stop timer for when audio finishes playing
            self.stopTimer = Timer(timeInterval: delayInSeconds, target: self, selector: #selector(PlaybackViewController.stopAudio), userInfo: nil, repeats: false)
            RunLoop.main.add(self.stopTimer!, forMode: RunLoop.Mode.default)
        }
        
        do {
            try audioEngine.start()
        } catch {
            showAlert(Alerts.AudioEngineError, message: String(describing: error))
            return
        }
        
        // play the recording!
        audioPlayerNode.play()
    }
}
```

## MapKit
The following code assumes creating a MKMapView and assigning its Delegate property to the VC.

```go
import MapKit

class MapViewController: UIViewController, MKMapViewDelegate {

    @IBOutlet weak var mapView: MKMapView!

    func addAnnotations() {
        let name = "Jessica"
        let locationStr = "Tarpon Springs, FL"
        let location = [
            "latitude" : 28.1461248,
            "longitude" : -82.75676799999999,
        ] as [String : Double]
        let lat = CLLocationDegrees(location["latitude"])
        let long = CLLocationDegrees(location["longitude"])
        let coordinate = CLLocationCoordinate2D(latitude: lat, longitude: long)

        // Here we create the annotation and set its coordinate, title, and subtitle properties
        let annotation = MKPointAnnotation()
        annotation.coordinate = coordinate
        annotation.title = name
        annotation.subtitle = locationStr

        // Place on the map
        self.mapView.addAnnotations([annotation])
    }
    
    // MARK: - MKMapViewDelegate
    
    // Create annotation view
    func mapView(_ mapView: MKMapView, viewFor annotation: MKAnnotation) -> MKAnnotationView? {
        let reuseId = "pin"
        var pinView = mapView.dequeueReusableAnnotationView(withIdentifier: reuseId) as? MKPinAnnotationView
        if pinView == nil {
            pinView = MKPinAnnotationView(annotation: annotation, reuseIdentifier: reuseId)
            pinView!.canShowCallout = true
            pinView!.pinTintColor = .red
            pinView!.rightCalloutAccessoryView = UIButton(type: .detailDisclosure)
        }
        else {
            pinView!.annotation = annotation
        }
        return pinView
    }
    
    // Respond to annotation taps
    func mapView(_ mapView: MKMapView, annotationView view: MKAnnotationView, calloutAccessoryControlTapped control: UIControl) {
        if control == view.rightCalloutAccessoryView {
            if let subtitle = view.annotation?.subtitle! {
                print(subtitle)
            }
        }
    }
}
```

_______________________________________________________________________________

# info.plist

```go
// Use camera
NSCameraUsageDescription
// Use photo library
NSPhotoLibraryUsageDescription
// Save to photo library
NSPhotoLibraryAddUsageDescription
```

_______________________________________________________________________________

# Networking

## URL

```go
/* Using `URL` */
// This class is somewhat lacking and we can only modify the path easily
let host = "google.com"
let finalURL = "google.com/en"
// URL from string
var url = URL(string: website)!
url?.appendPathComponent("en")

// Using `URLComponents` (part of `Foundation`)
let host = "google.com"
let finalURL = "https://google.com/search?query=hello"
var components = URLComponents()
components.scheme = "https"
components.host = "google.com"
components.path = "/search"
components.queryItems = [URLQueryItem(name: "query", value: "hello")]
```

A good way to manage URLs is using an enum.

```go
enum Endpoints {
    static let base = "https://api.themoviedb.org/3"
    static let apiKeyParam = "?api_key=\(TMDBClient.apiKey)"
    
    case getWatchlist
    case getFavourites
    
    var stringValue: String {
        switch self {
        case .getWatchlist: return Endpoints.base + "/account/\(Auth.accountId)/watchlist/movies" + Endpoints.apiKeyParam + "&session_id=\(Auth.sessionId)"
        }
    }
    
    var url: URL {
        return URL(string: stringValue)!
    }
}  
```

## URLSession
`URLSession` provides an API for downloading and uploading data to endpoints indicated by URLs.

Types of URL Session Tasks:
- `URLSessionDataTask`
- `URLSessionUploadTask`
- `URLSessionDownloadTask`
- `URLSessionStreamTask`

```go
/* Data task */
// `URLSession.shared` is a singleton created by default by the OS
let task = URLSession.shared.dataTask(with: imageURL) {data, response, error in
    guard let data = data else { return }
    receivedData = data
    // If we want to update UI components, we need to do it on the main thread
    DispatchQueue.main.async {
        self.imageView.image = UIImage(data: data)
    }
}
// The task is created in suspended state. We need to resume it manually
task.resume()

/* Download task */
// Similar to DataTask, but the data is saved to a temporary file
// whose location is passed to the completion closure
let task = URLSession.shared.dataTask(with: imageURL) {location, response, error in
    guard let location = location else { return }
    let imageData = try! Data(contentsOf: location)
    DispatchQueue.main.async {
        self.imageView.image = UIImage(data: imageData)
    }
}
task.resume()
```

__Allowing HTTP Connections__

To allow insecure connections, the following key needs to be added to `info.plist`

`App Transport Security Settings` -> `Exception Domains` -> <URL to allow> -> A key as boolean:
- `NSThirdPartyExceptionAllowsInsecureHTTPLoads`: For a domain you don't control.
- `NSExceptionAllowsInsecureHTTPLoads`: For a domain you control.
- `NSIncludesSubdomains`: To include subdomains as well.

## URLRequest
Use for building complex request that will be used with `URLSession`.

```go
var request = URLRequest(url: url)
request.httpMethod = "POST"
request.addValue("application/json", forHTTPHeaderField: "Content-Type")
request.httpBody = data

let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
    //...
}
task.resume()
```

## Notes Regarding URLs

```go
// Encoding special characters in the URL
"search term".addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)
```

_______________________________________________________________________________

# OS

## Reading files

```go
let imageData = try! Data(contentsOf: location)
let image = UIImage(data: data)
```

_______________________________________________________________________________

# JSON
The standart method for dealing with JSON is `Codable`. Older code and ObjectiveC used to use `JSONSerialization`.

## JSONSerialization
```go
// Parse a Data object as a json dictionary
let json = try JSONSerialization.jsonObject(with: data, options: []) as! [String: Any]
```

## Codable
The `Codable` protocol includes `Decodable` and `Encodable` protocols.

### Decodable

```go
let jsonStr = """{"status": 200, "message": "success"}"""
struct Response: Codable {
    let status: Int
    let message: String
}
let jsonData = jsonStr.data(using: .utf8)!
let response = try! JSONDecoder().decode(Response.self, from: jsonData)
```

In case the Codable struct field names aren't identical to the JSON keys, we can define a `CodingKey` enum.

```go
let jsonStr = """{"status": 200, "message": "success"}"""
struct Response: Codable {
    let status: Int
    let msg: String
    enum CodingKeys: String, CodingKey {
        // We need to define all keys event if they happen to match JSON ones.
        // We don't need to specify the string value though.
        case status
        case msg = "message"
    }
}
```

__Variable Data Structure - Method 1: enum__

In case the JSON could have different shapes, say different structure on success and failure, we use an enum:

```go
// On success
{ "username": "Jon", "userID": 10}
// On failure
{ "error":"Account not found"}

struct SuccessObject: Decodable {
    let username: String
    let userID: Int
}
enum ValueType: Decodable {
    case error(String)
    case success(SuccessObject)

    init(from decoder: Decoder) throws {
        // 1
        do {
            let singleValueContainer = try decoder.singleValueContainer()
            let msg = try singleValueContainer.decode(String.self)
            self = .error(msg)
            return
        } catch {}
        // 2
        do {
            let keyedContainer = try decoder.container(keyedBy: SuccessObject.CodingKeys.self)
            let obj = try singleValueContainer.decode(SuccessObject.self)
            self = .object(obj)
            return
        } catch {}
        // 3
        throw DecodingError.corruptedData
    }
}
```

__Variable Data Structure - Method 2: optionals__

We can use optionals and the non-present values would be nil. For the same data as the example above:

```go
struct ValueType: Decodable {
    let error: String?
    let username: String?
    let userID: Int?
}
```

### Encodable

```go
struct Request: Codable {
    let id: Int
    let message: String
}
let request = Request(id: 1, message: "hello")
let json = try! JSONEncoder().encode(request)
```

_______________________________________________________________________________

# Code Snippets

### Shift View When Keyboard Shows Up

```go
override func viewWillAppear(_ animated: Bool) {
    subscribeToKeyboardNotifications()
}
override func viewWillDisappear(_ animated: Bool) {
    unsubscribeFromKeyboardNotifications()
}
func subscribeToKeyboardNotifications() {
    NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillShow(_:)), name: UIResponder.keyboardWillShowNotification, object: nil)
    NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillHide(_:)), name: UIResponder.keyboardWillHideNotification, object: nil)
}
func unsubscribeFromKeyboardNotifications() {
    NotificationCenter.default.removeObserver(self, name: UIResponder.keyboardWillShowNotification, object: nil)
    NotificationCenter.default.removeObserver(self, name: UIResponder.keyboardWillHideNotification, object: nil)
}
@objc func keyboardWillShow(_ notification:Notification) {
    view.frame.origin.y -= getKeyboardHeight(notification)
}
@objc func keyboardWillHide(_ notification:Notification) {
    view.frame.origin.y = 0
}
func getKeyboardHeight(_ notification:Notification) -> CGFloat {
    let userInfo = notification.userInfo
    let keyboardSize = userInfo![UIResponder.keyboardFrameEndUserInfoKey] as! NSValue // of CGRect
    return keyboardSize.cgRectValue.height
}
```

### Render view to an image

```go
func generateMemedImage() -> UIImage {
    UIGraphicsBeginImageContext(self.view.frame.size)
    view.drawHierarchy(in: self.view.frame, afterScreenUpdates: true)
    let image: UIImage = UIGraphicsGetImageFromCurrentImageContext()!
    UIGraphicsEndImageContext()
    return image
}
```

### Screen Dimensions

```go
// In a view controller
view.frame.size.width
view.frame.size.height
```


