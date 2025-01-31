<Variant platform="android" api="collect-launch-info" repeat="2"/>

The Android SDK automatically registers an `Application.ActivityLifecycleCallbacks`and listens for `onActivityResumed`. When an activity is resumed, SDK collects the data from the activity. Currently, it is being used in the following scenarios:

* Tracking deep link clickthrough
* Tracking push message clickthrough
* Tracking Local Notification clickthrough

<Variant platform="ios" api="collect-launch-info" repeat="14"/>

#### Swift

The `collectLaunchInfo` method should be used in the following use cases:

* Tracking a deep link clickthrough
  * From `application(_:didFinishLaunchingWithOptions:)`
  * Extract `userInfo` from `url: UIApplication.LaunchOptionsKey`
* Tracking a push message clickthrough
  * From `application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`

**Syntax**

```swift
(void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```swift
ACPCore.collectLaunchInfo(userInfo)
```

#### Objective-C

The `collectLaunchInfo` method should be used in the following use cases:

* Tracking a deep link clickthrough
  * From `application:didFinishLaunchingWithOptions`
  * Extract `userInfo` from `UIApplicationLaunchOptionsURLKey`
* Tracking a push message clickthrough
  * From `application:didReceiveRemoteNotification:fetchCompletionHandler:`

**Syntax**

```objectivec
(void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

**Example**

```objc
 [ACPCore collectLaunchInfo:launchOptions];
```

<Variant platform="android" api="collect-pii" repeat="5"/>

#### Java

**Syntax**

```java
public static void collectPII(final Map<String, String> piiData);
```

**Example**

```java
Map<String, String> data = new HashMap<String, String>();
data.put("firstname", "customer");
//The rule to trigger a PII needs to be setup for this call
//to result in a network send
MobileCore.collectPII(data);
```

<Variant platform="ios" api="collect-pii" repeat="10"/>

#### Swift

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```

**Example**

```objectivec
MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
```

#### Objective-C

**Syntax**

```swift
(void) collectPii: (nonnull NSDictionary<NSString*, NSString*>*) data;
```

**Example**

```objectivec
[ACPCore collectPii:data:@{@"key1" : "@value1",
                           @"key2" : "@value2"
                           }];
```

<Variant platform="react-native" api="collect-pii" repeat="10"/>

#### Javascript

**Syntax**

```jsx
ACPCore.collectPii(data: [String : String])
```

**Example**

```jsx
ACPCore.collectPii({"myPii": "data"});
```

#### Swift

**Syntax**

```swift
ACPCore.collectPii(data: [String : String])
```

**Example**

```objectivec
MobileCore.collectPii(["key1" : "value1","key2" : "value2"]);
```

<Variant platform="android" api="get-application" repeat="6"/>

#### Java

`MobileCore.getApplication` will return `null` if the `Application` object was destroyed or if `MobileCore.setApplication` was not previously called.

**Syntax**

```java
public static Application getApplication()
```

**Example**

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```

<Variant platform="xamarin" api="get-application" repeat="4"/>

#### C#

`ACPCore.Application` may be `null` if the `Application` object was destroyed or was not set in the Core.

**Example**

```csharp
var app = ACPCore.Application;
if (app != null) {
    ...
}
```

<Variant platform="android" api="get-log-level" repeat="5"/>

#### Java

**Syntax**

```java
public static LoggingMode getLogLevel()
```

**Example**

```java
LoggingMode mode = MobileCore.getLogLevel();
```

<Variant platform="ios" api="get-log-level" repeat="10"/>

#### Swift

**Syntax**

```swift
(ACPMobileLogLevel) logLevel;
```

**Example**

```swift
let logLevel:ACPMobileLogLevel = ACPCore.logLevel();
```

#### Objective-C

**Syntax**

```objectivec
(ACPMobileLogLevel) logLevel;
```

**Example**

```objectivec
var logLevel:ACPMobileLogLevel = [ACPCore logLevel];
```

<Variant platform="react-native" api="get-log-level" repeat="3"/>

#### Javascript

**Example**

```jsx
ACPCore.getLogLevel().then(level => console.log("AdobeExperienceSDK: Log Level = " + level));
```

<Variant platform="unity" api="get-log-level" repeat="3"/>

#### C#

**Example**

```csharp
ACPCore.ACPMobileLogLevel logLevel = ACPCore.GetLogLevel();
```

<Variant platform="xamarin" api="get-log-level" repeat="3"/>

#### C#

**Example**

```csharp
var logLevel = ACPCore.LogLevel;
```

<Variant platform="android" api="get-sdk-identities" repeat="6"/>

#### Java

**Syntax**

```java
void getSdkIdentities(AdobeCallback<String> callback);
```

* _callback_ is invoked with the SDK identities as a JSON string. If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

**Example**

```java
MobileCore.getSdkIdentities(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // handle the json string
    }
});
```

<Variant platform="ios" api="get-sdk-identities" repeat="9"/>

#### Objective-C

**Syntax**

```objectivec
(void) getSdkIdentities: (nullable void (^) (NSString* __nullable content)) callback;
(void) getSdkIdentitiesWithCompletionHandler: (nullable void (^) (NSString* __nullable content, NSError* _Nullable error)) completionHandler;
```

* _callback_ is invoked with the SDK identities as a JSON string.
* _completionHandler_ is invoked with the SDK identities as a JSON string, or _error_ if an unexpected error occurs or the request times out. The default timeout is 1000ms.

**Example**

```objectivec
[ACPCore getSdkIdentities:^(NSString * _Nullable content){
    NSLog(content);

[ACPCore getSdkIdentitiesWithCompletionHandler:^(NSString * _Nullable content, NSError * _Nullable error) {
        if (error) {
            // handle error here
        } else {
            // handle the retrieved identities
            NSLog(content);
        }
    }];
```

#### Swift

**Example**

```swift
MobileCore.getSdkIdentities { (content, error) in
    // handle completion
}
```

<Variant platform="android" api="log" repeat="10"/>

#### Java

The `MobileCore` logging APIs use the `android.util.Log` APIs to log messages to Android. Based on the `LoggingMode` that is passed to `MobileCore.log()`, the following Android method is called:

* `LoggingMode.VERBOSE` uses `android.util.Log.v`
* `LoggingMode.DEBUG` uses `android.util.Log.d`
* `LoggingMode.WARNING` uses `android.util.Log.w`
* `LoggingMode.ERROR` uses `android.util.Log.e`

All log messages from the Adobe Experience SDK to Android use the same log tag of `AdobeExperienceSDK`. For example, if logging an error message is using `MobileCore.log()`, the call to `android.util.Log.e` looks like `Log.e("AdobeExperienceSDK", tag + " - " + message)`.

**Syntax**

```java
public static void log(final LoggingMode mode, final String tag, final String message)
```

**Example**

```java
MobileCore.log(LoggingMode.DEBUG, "MyClassName", "Provided data was null");
```

**Output**

```text
D/AdobeExperienceSDK: MyClassName - Provided data was null
```

<Variant platform="ios" api="log" repeat="15"/>

#### Objective-C

The log messages from the Adobe Experience SDK are printed to the Apple System Log facility and use a common format that contains the tag `AdobeExperienceSDK`. For example, if logging an error message using `ACPCore.log()`, the printed output looks like `[AdobeExperienceSDK ERROR <tag>]: message[AEP SDK ERROR - <testLabel>] Test message`.

**Syntax**

```objectivec
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```objectivec
[ACPCore log: ACPMobileLogLevelDebug, tag:@"MyClassName", message:@"Provided data was nil"];
```

**Output**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

#### Swift

**Syntax**

```swift
+ (void) log: (ACPMobileLogLevel) logLevel tag: (nonnull NSString*) tag message: (nonnull NSString*) message;
```

**Example**

```swift
ACPCore.log(ACPMobileLogLevel.debug, tag: "MyClassName", message: "Provided data was nil");
```

**Output**

```text
[AdobeExperienceSDK DEBUG <MyClassName>]: Provided data was nil
```

<Variant platform="react-native" api="log" repeat="6"/>

#### JavaScript

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `ACPMobileLogLevel`.

**Example**

```jsx
ACPCore.log(ACPMobileLogLevel.ERROR, "React Native Tag", "React Native Message");
```

Note: `ACPMobileLogLevel` contains the following getters:

```jsx
const ERROR = "ACP_LOG_LEVEL_ERROR";
const WARNING = "ACP_LOG_LEVEL_WARNING";
const DEBUG = "ACP_LOG_LEVEL_DEBUG";
const VERBOSE = "ACP_LOG_LEVEL_VERBOSE";
```

<Variant platform="xamarin" api="log" repeat="8"/>

#### C#

The log messages from the Adobe Experience SDK are printed to the Log facility and use a common format that contains the tag `AdobeExperienceSDK`.

**iOS syntax**

```csharp
ACPCore.Log(ACPMobileLogLevel.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK ERROR <xamarin tag>]: xamarin message
```

**Android syntax**

```csharp
ACPCore.Log(LoggingMode.Error, "xamarin tag", "xamarin message");
```

```text
[AdobeExperienceSDK] xamarin tag - xamarin message
```

<Variant platform="android" api="register-extension" repeat="4"/>

After you register the extensions, call the `start` API in Mobile Core to initialize the SDK as shown below. This step is required to boot up the SDK for event processing. The following code snippet is provided as a sample reference.

#### Java

**Example**

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
...
import android.app.Application;
...
public class MainApp extends Application {
  ...
  @Override
  public void on Create(){
    super.onCreate();
    MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
    ...
    try {
      UserProfile.registerExtension();
            Identity.registerExtension();
            Lifecycle.registerExtension();
            Signal.registerExtension();
            MobileCore.start(new AdobeCallback () {
            @Override
            public void call(Object o) {
            MobileCore.configureWithAppID("<your_environment_id_from_Launch>");
    }
});
    } catch (InvalidInitException e) {
      ...
    }
  }
}
```

<Variant platform="ios" api="register-extension" repeat="7"/>

The following snippet shows an example of how to add the initialization code. Note that this may need to be adjusted, depending on how your application is structured.

#### Objective-C

**Example**

```objectivec
#import "AppDelegate.h"
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore setLogLevel:ACPMobileLogLevelDebug];
  [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
    ...
  [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];
    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
      // only start lifecycle if the application is not in the background
      if (appState != UIApplicationStateBackground) {
        [ACPCore lifecycleStart:nil];
      }
    }];
    ...
  return YES;
}

@end
```

#### Swift

**Example**

```swift
import ACPCore
import ACPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
  func application(_application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool{
    ACPCore.setLogLevel(.debug)
        ACPCore.configure(withAppId: "<your_environment_id_from_Launch>")
    ...
    ACPUserProfile.registerExtension()
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPSignal.registerExtension()
        ACPCore.start {
        ACPCore.lifecycleStart(nil)
        }
    ...
    return true
  }
}
```

<Variant platform="react-native" api="register-extension" repeat="5"/>

For React Native apps, initialize the SDK using native code in your `AppDelegate` (iOS) and `MainApplication` (Android).

#### iOS

```objectivec
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
    [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];

    const UIApplicationState appState = application.applicationState;
    [ACPCore start:^{
      // only start lifecycle if the application is not in the background
      if (appState != UIApplicationStateBackground) {
        [ACPCore lifecycleStart:nil];
      }
    }];
    ...
  return YES;
}

@end
```

#### Android

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
...
import android.app.Application;
...
public class MainApplication extends Application implements ReactApplication {
  ...
  @Override
  public void on Create(){
    super.onCreate();
    ...
    MobileCore.setApplication(this);
    MobileCore.setLogLevel(LoggingMode.DEBUG);
    MobileCore.setWrapperType(WrapperType.REACT_NATIVE);

    try {
      UserProfile.registerExtension();
      Identity.registerExtension();
      Lifecycle.registerExtension();
      Signal.registerExtension();
      MobileCore.start(new AdobeCallback () {
          @Override
          public void call(Object o) {
            MobileCore.configureWithAppID("<your_environment_id_from_Launch>");
         }
      });
    } catch (InvalidInitException e) {
      ...
    }
  }
}
```

<Variant platform="flutter" api="register-extension" repeat="3"/>

#### Dart

For Flutter apps, initialize the SDK using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively.

The initialization code is located in the [Flutter ACPCore Github README](https://github.com/adobe/flutter_acpcore).

<Variant platform="cordova" api="register-extension" repeat="5"/>

For Cordova apps, initialize the SDK using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively.

#### iOS

```dart
// Import the SDK
#import "ACPCore.h"
#import "ACPLifecycle.h"
#import "ACPIdentity.h"
#import "ACPSignal.h"
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {  
  // make sure to set the wrapper type at the beginning of initialization
  [ACPCore setWrapperType:ACPMobileWrapperTypeCordova];

  //...
  [ACPCore configureWithAppId:@"yourAppId"];
  [ACPIdentity registerExtension];
  [ACPLifecycle registerExtension];
  [ACPSignal registerExtension];
  // Register any additional extensions

  [ACPCore start:nil];
}
```

#### Android

```java
// Import the SDK
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.WrapperType;

@Override
public void onCreate() {
  //...
  MobileCore.setApplication(this);
  MobileCore.configureWithAppID("yourAppId");

  // make sure to set the wrapper type at the beginning of initialization
  MobileCore.setWrapperType(WrapperType.CORDOVA);

  try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();

    // Register any additional extensions
  } catch (Exception e) {
    // handle exception
  }

  MobileCore.start(null);
}
```

<Variant platform="unity" api="register-extension" repeat="3"/>

#### C#

For Unity apps, initialize the SDK using the following code in the start function of the `MainScript`.

```csharp
using com.adobe.marketing.mobile;
using using AOT;

public class MainScript : MonoBehaviour
{
    [MonoPInvokeCallback(typeof(AdobeStartCallback))]
    public static void HandleStartAdobeCallback()
    {   
        ACPCore.ConfigureWithAppID("1423ae38-8385-8963-8693-28375403491d");
    }

    // Start is called before the first frame update
    void Start()
    {   
        if (Application.platform == RuntimePlatform.Android) {
            ACPCore.SetApplication();
        }

        ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.VERBOSE);
        ACPCore.SetWrapperType();
        ACPIdentity.registerExtension();
        ACPLifecycle.registerExtension();
        ACPSignal.registerExtension();
        ACPCore.Start(HandleStartAdobeCallback);
    }
}
```

<Variant platform="xamarin" api="register-extension" repeat="6"/>

#### C#

For Xamarin Forms applications, the SDK initialization differs, depending on the platform being targeted.

#### iOS

```csharp
using Com.Adobe.Marketing.Mobile;

[Register("AppDelegate")]
public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
{
  //
  // This method is invoked when the application has loaded and is ready to run. In this
  // method you should instantiate the window, load the UI into it and then make the window
  // visible.
  //
  // You have 17 seconds to return from this method, or iOS will terminate your application.
  //
  public override bool FinishedLaunching(UIApplication app, NSDictionary options)
  {
    global::Xamarin.Forms.Forms.Init();
    LoadApplication(new App());

    // set the wrapper type
    ACPCore.SetWrapperType(ACPMobileWrapperType.Xamarin);

    // set launch config
    ACPCore.ConfigureWithAppID("your-app-id");

    // register SDK extensions
    ACPIdentity.RegisterExtension();
    ACPLifecycle.RegisterExtension();
    ACPSignal.RegisterExtension();

    // start core
    ACPCore.Start(null);
  }
```

#### Android

```csharp
using Com.Adobe.Marketing.Mobile;

[Activity(Label = "TestApp", Icon = "@mipmap/icon", Theme = "@style/MainTheme", MainLauncher = true, ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
  protected override void OnCreate(Bundle savedInstanceState)
  {
    base.OnCreate(savedInstanceState);

    global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
    LoadApplication(new App());

    // set the wrapper type
    ACPCore.SetWrapperType(WrapperType.Xamarin);

    // register SDK extensions
    ACPCore.Application = this.Application;
    ACPIdentity.RegisterExtension();
    ACPLifecycle.RegisterExtension();
    ACPSignal.RegisterExtension();

    // start core
    ACPCore.Start(null);
}
```

<Variant platform="ios" api="register-url-handler" repeat="5"/>

#### Objective-C

**Syntax**

```objectivec
+ (void) registerURLHandler: (nonnull BOOL (^) (NSString* __nullable url)) callback;
```

**Example**

```objectivec
[ACPCore registerURLHandler:^BOOL(NSString * _Nullable url) {
    ...
}];
```

<Variant platform="android" api="reset-identities" repeat="6"/>

#### Java

This method is only available in Mobile Core v.1.8.0 and above.

**Syntax**

```java
void resetIdentities();
```

**Example**

```java
MobileCore.resetIdentities();
```

<Variant platform="ios" api="set-app-group" repeat="10"/>

#### Swift

**Syntax**

```swift
public static func setAppGroup(_ group: String?)
```

**Example**

```swift
ACPCore.setAppGroup("app-group-id")
```

#### Objective-C

**Syntax**

```objc
public static func setAppGroup(_ group: String?)
```

**Example**

```objc
[ACPCore setAppGroup:@"app-group-id"];
```


<Variant platform="xamarin" api="set-app-group" repeat="5"/>

#### C#

**Syntax**

```csharp
public static void SetAppGroup (string appGroup);
```

**Example**

```csharp
ACPCore.SetAppGroup("app_group");
```

<Variant platform="android" api="set-application" repeat="5"/>

#### Java

**Syntax**

```java
public static void setApplication(final Application app)
```

**Example**

```java
public class CoreApp extends Application {

   @Override
   public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.start(null);
   }
}
```

<Variant platform="xamarin" api="set-application" repeat="3"/>

#### C#

**Example**

```csharp
public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
{
  protected override void OnCreate(Bundle savedInstanceState)
  {
    base.OnCreate(savedInstanceState);
    ACPCore.Application = this.Application;
    ACPCore.Start(null);
  }
}
```

<Variant platform="android" api="set-log-level" repeat="5"/>

#### Java

**Syntax**

```java
public static void setLogLevel(LoggingMode mode)
```

**Example**

```java
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;

MobileCore.setLogLevel(LoggingMode.VERBOSE);
```

<Variant platform="ios" api="set-log-level" repeat="10"/>

#### Swift

**Syntax**

```swift
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```swift
import ACPCore

ACPCore.setLogLevel(ACPMobileLogLevel.verbose);
```

#### Objective-C

**Syntax**

```objc
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```objc
#import "ACPCore.h"

[ACPCore setLogLevel: ACPMobileLogLevelVerbose];
```

<Variant platform="react-native" api="set-log-level" repeat="5"/>

#### Javascript

**Syntax**

```jsx
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```jsx
import {ACPMobileLogLevel} from '@adobe/react-native-acpcore';
ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
```

<Variant platform="flutter" api="set-log-level" repeat="5"/>

#### Dart

**Syntax**

```dart
(void) setLogLevel: (ACPMobileLogLevel) logLevel;
```

**Example**

```dart
import 'package:flutter_acpcore/src/acpmobile_logging_level.dart';
FlutterACPCore.setLogLevel(ACPLoggingLevel.VERBOSE);
```

<Variant platform="cordova" api="set-log-level" repeat="7"/>

#### Cordova

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ACPCore.ACPMobileLogLevelError
* ACPCore.ACPMobileLogLevelWarning
* ACPCore.ACPMobileLogLevelDebug
* ACPCore.ACPMobileLogLevelVerbose

**Syntax**

```jsx
ACPCore.setLogLevel = function(logLevel, success, fail);
```

**Example**

```jsx
ACPCore.setLogLevel(ACPCore.ACPMobileLogLevelVerbose, successCallback, errorCallback);
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```

<Variant platform="unity" api="set-log-level" repeat="7"/>

#### C#

From least to most verbose, the order of Mobile SDK logging modes is as follows:

* ACPCore.ACPMobileLogLevel.ERROR
* ACPCore.ACPMobileLogLevel.WARNING
* ACPCore.ACPMobileLogLevel.DEBUG
* ACPCore.ACPMobileLogLevel.VERBOSE

**Syntax**

```csharp
public static void SetLogLevel(ACPMobileLogLevel logLevel)
```

**Example**

```csharp
ACPCore.SetLogLevel(ACPCore.ACPMobileLogLevel.ERROR);
```

<Variant platform="xamarin" api="set-log-level" repeat="13"/>

#### C#

From least to most verbose, the order of Mobile SDK logging modes is as follows for iOS:

* ACPMobileLogLevel.Error;
* ACPMobileLogLevel.Warning;
* ACPMobileLogLevel.Debug;
* ACPMobileLogLevel.Verbose;

From least to most verbose, the order of Mobile SDK logging modes is as follows for Android:

* LoggingMode.Error;
* LoggingMode.Warning;
* LoggingMode.Debug;
* LoggingMode.Verbose;

**iOS syntax**

```csharp
public static ACPMobileLogLevel LogLevel { get, set }
```

**Android syntax**

```csharp
public unsafe static LoggingMode LogLevel { get, set }
```

**iOS example**

```csharp
ACPCore.LogLevel = ACPMobileLogLevel.Verbose;
```

**Android example**

```csharp
ACPCore.LogLevel = LoggingMode.Verbose;
```

<Variant platform="android" api="set-push-identifier" repeat="6"/>

#### Java

**Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

* _pushIdentifier_  is a string that contains the device token for push notifications.

**Example**

```java
//Retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```

<Variant platform="ios" api="set-push-identifier" repeat="12"/>

#### Swift

**Syntax**

```swift
@objc(setPushIdentifier:)
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

```swift
// Set the deviceToken that the APNs has assigned to the device
MobileCore.setPushIdentifier(deviceToken)
```

#### Objective-C

**Syntax**

```objc
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_  is a string that contains the device token for push notifications.

**Example**

```objectivec
// Set the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

<Variant platform="android" api="set-icon-resource-id" repeat="11"/>

#### Java

#### setSmallIconResourceID

**Syntax**

```java
public static void setSmallIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setSmallIconResourceID(R.mipmap.ic_launcher_round);
```

#### setLargeIconResourceID

**Syntax**

```java
public static void setLargeIconResourceID(int resourceID)
```

**Example**

```java
 MobileCore.setLargeIconResourceID(R.mipmap.ic_launcher_round);
```

<Variant platform="xamarin" api="set-icon-resource-id" repeat="11"/>

#### C#

#### setSmallIconResourceID

**Syntax**

```csharp
public unsafe static void SetSmallIconResourceID (int resourceID);
```

**Example**

```csharp
ACPCore.SetSmallIconResourceID(Resource.Mipmap.icon_round);
```

#### setLargeIconResourceID

**Syntax**

```csharp
public unsafe static void SetLargeIconResourceID (int resourceID);
```

**Example**

```csharp
 ACPCore.SetLargeIconResourceID(Resource.Mipmap.icon_round);
```

<Variant platform="android" api="track-action" repeat="6"/>

#### Java

**Syntax**

```java
public static void trackAction(final String action, final Map<String, String> contextData)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();
additionalContextData.put("customKey", "value");
MobileCore.trackAction("loginClicked", additionalContextData);
```

<Variant platform="ios" api="track-action" repeat="12"/>

#### Swift

**Syntax**

```swift
@objc(trackAction:data:)
static func track(action: String?, data: [String: Any]?)
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```swift
ACPCore.track(action: "action name", data: ["key": "value"])
```

#### Objective-C

**Syntax**

```objc
+ (void) trackAction: (nullable NSString*) action data: (nullable NSDictionary*) contextData;
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```objc
 [ACPCore trackAction:@"action name" data:@{@"key":@"value"}];
```

<Variant platform="react-native" api="track-action" repeat="6"/>

#### Javascript

**Syntax**

```jsx
trackAction(action?: String, contextData?: { string: string });
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```jsx
ACPCore.trackAction("action name", {"key": "value"});
```

<Variant platform="flutter" api="track-action" repeat="6"/>

#### Dart

**Syntax**

```dart
Future<void> trackAction (String action, {Map<String, String> contextData});
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```dart
FlutterACPCore.trackAction("action name",  data: {"key": "value"});
```

<Variant platform="cordova" api="track-action" repeat="6"/>

#### Cordova

**Syntax**

```jsx
ACPCore.trackAction = function(action, contextData, success, fail);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on this hit.
* _success_ callback is invoked when trackAction executes successfully.
* _fail_ callback is invoked when trackAction fails.

**Example**

```jsx
ACPCore.trackAction("cordovaAction", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```

<Variant platform="unity" api="track-action" repeat="6"/>

#### C#

**Syntax**

```csharp
public static void TrackAction(string name, Dictionary<string, string> contextDataDict)
```

* _name_ contains the name of the action to track.
* _contextDataDict_ contains the context data to attach on the hit.

**Example**

```csharp
var contextData = new Dictionary<string, string>();
contextData.Add("key", "value");
ACPCore.TrackAction("action", contextData);
```

<Variant platform="xamarin" api="track-action" repeat="11"/>

#### C#

**iOS syntax**

```csharp
public static void TrackAction (string action, NSMutableDictionary<NSString, NSString> data);
```

* _action_ contains the name of the action to track.
* _data_ contains the context data to attach on the hit.

**Android syntax**

```csharp
public unsafe static void TrackAction (string action, IDictionary<string, string> contextData);
```

* _action_ contains the name of the action to track.
* _contextData_ contains the context data to attach on the hit.

**iOS example**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackAction("action", data);
```

**Android example**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackAction("action", data);
```

<Variant platform="android" api="track-state" repeat="7"/>

#### Java

In Android, `trackState` is typically called every time a new `Activity` is loaded.

**Syntax**

```java
public static void trackState(final String state, final Map<String, String> contextData)
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```java
Map<String, String> additionalContextData = new HashMap<String, String>();        
additionalContextData.put("customKey", "value");
MobileCore.trackState("homePage", additionalContextData);
```

<Variant platform="ios" api="track-state" repeat="12"/>

#### Swift

**Syntax**

```swift
+ (void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```swift
ACPCore.trackState("state name", data: ["key": "value"])
```

#### Objective-C

**Syntax**

```objectivec
(void) trackState: (nullable NSString*) state data: (nullable NSDictionary*) contextData;
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```objectivec
 [ACPCore trackState:@"state name" data:@{@"key":@"value"}];
```

<Variant platform="react-native" api="track-state" repeat="6"/>

#### Javascript

**Syntax**

```jsx
trackState(state?: String, contextData?: { string: string });
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```jsx
ACPCore.trackState("state name", {"key": "value"});
```

<Variant platform="flutter" api="track-state" repeat="6"/>

#### Dart

**Syntax**

```dart
Future<void> trackState (String state, {Map<String, String> contextData});
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Example**

```dart
FlutterACPCore.trackState("state name",  data: {"key1: "value"})
```

<Variant platform="cordova" api="track-state" repeat="6"/>

#### Cordova

**Syntax**

```jsx
ACPCore.trackState = function(state, contextData, success, fail);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.
* _success_ callback is invoked when trackState executes successfully.
* _fail_ callback is invoked when trackState fails.

**Example**

```jsx
ACPCore.trackState("cordovaState", {"cordovaKey":"cordovaValue"}, successCallback, errorCallback);
```

<Variant platform="unity" api="track-state" repeat="6"/>

#### C#

**Syntax**

```csharp
public static void TrackState(string name, Dictionary<string, string> contextDataDict)
```

* _state_ contains the name of the state to track.
* _contextDataDict_ contains the context data to attach on the hit.

**Example**

```csharp
var dict = new Dictionary<string, string>();
dict.Add("key", "value");
ACPCore.TrackState("state", dict);
```

<Variant platform="xamarin" api="track-state" repeat="11"/>

#### C#

**iOS syntax**

```csharp
public static void TrackState (string state, NSMutableDictionary<NSString, NSString> data);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**Android syntax**

```csharp
public unsafe static void TrackState (string state, IDictionary<string, string> contextData);
```

* _state_ contains the name of the state to track.
* _contextData_ contains the context data to attach on the hit.

**iOS example**

```csharp
var data = new NSMutableDictionary<NSString, NSString>
{
  ["key"] = new NSString("value")
};
ACPCore.TrackState("state", data);
```

**Android example**

```csharp
var data = new Dictionary<string, string>();
data.Add("key", "value");
ACPCore.TrackState("state", data);
```

<Variant platform="android" api="public-classes" repeat="13"/>

#### Java

#### AdobeCallback

The `AdobeCallback` class provides the interface to receive results when the asynchronous APIs perform the requested action.

```java
public interface AdobeCallback<T> {    
    void call(final T value);
}
```

#### AdobeCallbackWithError

The `AdobeCallbackWithError` class provides the interface to receive results or an error when the asynchronous APIs perform the requested action.

When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is stopped and the fail method is called with the corresponding `AdobeError`.

```java
public interface AdobeCallbackWithError<T> extends AdobeCallback<T> {
    void fail(final AdobeError error);
}
```

#### AdobeError

The `AdobeError` class shows the errors that can be passed to an `AdobeCallbackWithError`:

* `UNEXPECTED_ERROR` - An unexpected error occurred.
* `CALLBACK_TIMEOUT` - The timeout was met.
* `CALLBACK_NULL` - The provided callback function is null.
* `EXTENSION_NOT_INITIALIZED` - The extension is not initialized.

**Example**

```java
MobileCore.getPrivacyStatus(new AdobeCallbackWithError<MobilePrivacyStatus>() {
  @Override
  public void fail(final AdobeError error) {
    if (error == AdobeError.UNEXPECTED_ERROR) {
      // handle unexpected error
    } else if (error == AdobeError.CALLBACK_TIMEOUT) {
      // handle timeout error
    } else if (error == AdobeError.CALLBACK_NULL) {
      // handle null callback error
    } else if (error == AdobeError.EXTENSION_NOT_INITIALIZED) {
      // handle extension not initialized error
    }
  }

  @Override
  public void call(final MobilePrivacyStatus value) {
    // use MobilePrivacyStatus value
  }
});
```

<Variant platform="ios" api="public-classes" repeat="8"/>

#### ACPError

The `ACPError` class shows the errors that can be passed to a completion handler callback from any API which uses one:

* `ACPErrorUnexpected` - An unexpected error occurred.
* `ACPErrorCallbackTimeout` - The timeout was met.
* `ACPErrorCallbackNil` - The provided callback function is nil.
* `ACPErrorExtensionNotInitialized` - The extension is not initialized.

**Example**

**Objective-C**

```objc
[ACPCore getSdkIdentities:^(NSString * _Nullable content, NSError * _Nullable error) {
  if (error) {
    if (error.code == ACPErrorCallbackTimeout) {
      // handle timeout error
    } else if (error.code == ACPErrorCallbackNil) {
      // handle nil callback error
    } else if (error.code == ACPErrorExtensionNotInitialized) {
      // handle extension not initialized error
    } else if (error.code == ACPErrorUnexpected) {
      // handle unexpected error

    ....

  } else {
    // use privacy status
  }
}];
```

**Swift**

```swift
ACPCore.getPrivacyStatus { (privacyStatus, error) in
  if let error = error {
    let callbackError: NSError = (error as NSError)
    if (callbackError.code == ACPError.callbackTimeout.rawValue) {
      // handle timeout error
    } else if (callbackError.code == ACPError.callbackNil.rawValue) {
      // handle nil callback error
    } else if (callbackError.code == ACPError.extensionNotInitialized.rawValue) {
      // handle extension not initialized error
    } else if (callbackError.code == ACPError.unexpected.rawValue) {
      // handle unexpected error
    }
  } else {
    // use privacyStatus
  }
}
```

<Variant platform="xamarin" api="public-classes" repeat="18"/>

#### Android

**IAdobeCallback**

This class provides the interface to receive results when the async APIs perform the requested action.

```csharp
public interface IAdobeCallback : IJavaObject, IDisposable, IJavaPeerable
{
    void Call (Java.Lang.Object p0);
}
```

**IAdobeCallbackWithError**

This class provides the interface to receive results or an error when the async APIs perform the requested action. When using this class, if the request cannot be completed within the default timeout or an unexpected error occurs, the request is aborted and the _fail_ method is called with the corresponding _AdobeError_.

```csharp
public interface IAdobeCallbackWithError : IAdobeCallback, IJavaObject, IDisposable, IJavaPeerable
{
    void Fail (AdobeError p0);
}
```

**AdobeError**

Errors which may be passed to an AdobeCallbackWithError:

* `UnexpectedError` - An unexpected error occurred.
* `CallbackTimeout` - The timeout was met.
* `CallbackNull` - The provided callback function is null.
* `ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatus(new AdobeCallbackWithError());
class AdobeCallbackWithError : Java.Lang.Object, IAdobeCallbackWithError
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("String callback content: " + stringContent);
    }
    else
    {
      Console.WriteLine("null content in string callback");
    }
  }
  public void Fail(AdobeError error)
  {
    if (error == AdobeError.UnexpectedError)
    {
      // handle unexpected error
    }
    else if (error == AdobeError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error == AdobeError.CallbackNull)
    {
      // handle null callback error
    }
    else if (error == AdobeError.ExtensionNotInitialized)
    {
        // handle extension not initialized error
    }
```

#### iOS

**ACPError**

Errors which may be passed to a completion handler callback from any API which uses one:

* `ACPError.Unexpected` - An unexpected error occurred.
* `ACPError.CallbackTimeout` - The timeout was met.
* `ACPError.CallbackNil` - The provided callback function is nil.
* `ACPError.ExtensionNotInitialized` - The extension is not initialized.

**Example**

```csharp
ACPCore.GetPrivacyStatusWithCompletionHandler((privacyStatus, error) => {
  if (error != null)
  {
    if ( error.Code == (int)ACPError.CallbackTimeout)
    {
      // handle timeout error
    }
    else if (error.Code == (int)ACPError.CallbackNil) 
    {
      // handle nil callback error
    }
    else if (error.Code == (int)ACPError.ExtensionNotInitialized)
    {
      // handle extension not initialized error
    }
    else if (error.Code == (int)ACPError.Unexpected)
    {
      // handle unexpected error
    }
  }
  else
  {
    Console.WriteLine("privacy status: " + privacyStatus);
  }
});
```