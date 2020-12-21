This is a quick guide to getting started with Appium on your MacOS for the very first time:

After spending a lot of time looking at several YouTube video, blogs, and official documentation, I quickly realized that most of the information either outdated (as of September, 2019) or not comprehensive enough. So, I decided to write simple and brief quick-setup guide that could help someone in my situation to get started with Appium.

For now I’ll only cover setting this up for iOS but I’ll revise this story soon, to include Android as well.

&nbsp;

Table of contents
--
- [Machine Setup](#machine-setup)
- [WebDriverAgent](#webdriveragent)
- [Create a project](#create-a-project)
- [Troubleshooting](#troubleshooting)
- [Reseources](#resources)

&nbsp;

## Machine Setup

Here are list of thing we need to install

- [JDK 8+](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
- [IntelliJ IDEA](https://www.jetbrains.com/idea/download/#section=mac)
- [Maven](http://maven.apache.org/download.cgi?Preferred=ftp://mirror.reverse.net/pub/apache/)
- [XCode](https://developer.apple.com/support/xcode/)
- [Command Line Tools](https://developer.apple.com/xcode/resources/)
- [NodeJS](https://nodejs.org/en/download/)
- [Carthage](https://github.com/Carthage/Carthage) 
- [authorize-ios]() 
- [ios-deploy]() 
- [ideviceinstaller](https://github.com/libimobiledevice/ideviceinstaller) 
- [ios_webkit_debug_proxy](https://github.com/google/ios-webkit-debug-proxy) 
- [xcpretty](https://github.com/xcpretty/xcpretty)
- [Appium](http://appium.io/docs/en/about-appium/getting-started/) 
- [Appium Doctor](https://github.com/appium/appium-doctor) 
- [Appium Desktop](https://github.com/appium/appium-desktop) 
- [Chromedriver](https://sites.google.com/a/chromium.org/chromedriver/) 

&nbsp;
[top](#table-of-contents)
&nbsp;

### Install XCode

Download the latest version of Xcode [from the Apple developer website](https://developer.apple.com/downloads/index.action) or get it [using the Mac App Store](https://itunes.apple.com/us/app/xcode/id497799835).

Once you have Xcode installed, open a terminal, run **`xcode-select --install`**, and click the Install button to install the required command line developer tools. Don't worry if you see a message telling you the software cannot be installed because it is not currently available from the Software Update Server. This usually means you already have the latest version installed. You can also get the command line tools from [the Apple developer website](https://developer.apple.com/downloads/index.action).

&nbsp;

### Install Appium and external dependencies
Now we'll use [Homebrew](https://brew.sh/) package manager to install all other software. If you already have [Homebrew](https://brew.sh/) installed, you can install by running the following command
   
```bash
> brew tap caskroom/cask
> brew cask install java
> brew cask intellij-idea-ce 
> brew install maven 
> brew install node 
> brew install carthage 
> brew install ideviceinstaller
> brew install libimobiledevice
> brew install ios-webkit-debug-proxy 
```
```
> npm install -g npm-autoinit
> npm install -g appium  
> npm install wd       
> npm install -g appium-doctor 
```
```
> gem install xcpretty
```

Now you can run the **`appium doctor`** to get a sense of what else do we need before we really get started. To run it, enter the following into terminal:
````
sayem@ ~: appium-doctor --ios
````
appium-doctor’s output should look something like this:

```bash
info AppiumDoctor Appium Doctor v.1.12.0
info AppiumDoctor ### Diagnostic for necessary dependencies starting ###
info AppiumDoctor  ✔ The Node.js binary was found at: /usr/local/bin/node
info AppiumDoctor  ✔ Node version is 12.10.0
info AppiumDoctor  ✔ Xcode is installed at: /Applications/Xcode.app/Contents/Developer
info AppiumDoctor  ✔ Xcode Command Line Tools are installed in: /Applications/Xcode.app/Contents/Developer
info AppiumDoctor  ✔ DevToolsSecurity is enabled.
info AppiumDoctor  ✔ The Authorization DB is set up properly.
info AppiumDoctor  ✔ Carthage was found at: /usr/local/bin/carthage. Installed version is: 0.33.0
info AppiumDoctor  ✔ HOME is set to: /Users/sayem
info AppiumDoctor ### Diagnostic for necessary dependencies completed, no fix needed. ###
info AppiumDoctor
info AppiumDoctor ### Diagnostic for optional dependencies starting ###
WARN AppiumDoctor  ✖ opencv4nodejs cannot be found.
WARN AppiumDoctor  ✖ ffmpeg cannot be found
WARN AppiumDoctor  ✖ mjpeg-consumer cannot be found.
WARN AppiumDoctor  ✖ idb and idb_companion are not installed
WARN AppiumDoctor  ✖ applesimutils cannot be found
info AppiumDoctor ### Diagnostic for optional dependencies completed, 5 fixes possible. ###
info AppiumDoctor
info AppiumDoctor ### Optional Manual Fixes ###
info AppiumDoctor The configuration can install optionally. Please do the following manually:
WARN AppiumDoctor  ➜ Why opencv4nodejs is needed and how to install it: https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/image-comparison.md
WARN AppiumDoctor  ➜ ffmpeg is needed to record screen features. Please read https://www.ffmpeg.org/ to install it
WARN AppiumDoctor  ➜ mjpeg-consumer module is required to use MJPEG-over-HTTP features. Please install it with 'npm i -g mjpeg-consumer'.
WARN AppiumDoctor  ➜ Why idb is needed and how to install it: https://github.com/appium/appium-idb
WARN AppiumDoctor  ➜ Why applesimutils is needed and how to install it: http://appium.io/docs/en/drivers/ios-xcuitest/
info AppiumDoctor
info AppiumDoctor ###
info AppiumDoctor
info AppiumDoctor Bye! Run appium-doctor again when all manual fixes have been applied!
info AppiumDoctor
```
If you don't already have [Homebrew](https://brew.sh/) installed, I would strongly recommend that you install it! It's incredibly useful for installing software dependencies like OpenSSL, MySQL, Postgres, Redis, SQLite, and more.

You can install it by running the following command:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### Appium Desktop

[Appium Desktop](http://appium.io/) is an Open source desktop app for starting an Appium server and inspecting your app. You can download the latest version of Appium Desktop [from the Appim Desktop github repository](https://github.com/appium/appium-desktop/releases) 

&nbsp;


## WebDriverAgent

WebDriverAgent is a WebDriver server implementation for iOS that can be used to remote control iOS devices. You need to install and setup WebDriverAgent to allow Appium to automate iOS devices.

- Open **Xcode > Preferences > Accounts**: Add developer's Apple ID

![Image description](https://github.com/sayems/appium/blob/master/img/account.png)

- Open **Terminal** and enter following command to find **WebDriverAgent** PATH:
```
sayem@ ~: npm ls -g appium-webdriveragent
```
```
/usr/local/lib
├─┬ appium@1.15.0
│ ├── appium-webdriveragent@1.3.5
│ └─┬ appium-xcuitest-driver@2.133.1
│   └── appium-webdriveragent@1.3.5  deduped
└─┬ appium-xcuitest-driver@3.0.0
  └── appium-webdriveragent@2.0.0
```
or user ```find``` command to find **WebDriverAgent** PATH:
```
find / -type d -name "*WebDriverAgent*"
```
```
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent/WebDriverAgentRunner
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent/WebDriverAgent.xcodeproj
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent/WebDriverAgentTests
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent/WebDriverAgentLib
```
It should be in ```/usr/local/lib/```
```
/usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent
```

- Open **Terminal** and enter following command to initialize **WebDriverAgent** project:
```
cd /usr/local/lib/node_modules/appium/node_modules/appium-webdriveragent
mkdir -p Resources/WebDriverAgent.bundle
sh ./Scripts/bootstrap.sh -d
```

#### Open WebDriverAgent in finder

In terminal type the following to open the WebDriverAgent folder
```
open .
```


**Common issues**
> Error code 13: re-run command with sudo: **sudo ./Scripts/bootstrap.sh -d**

> Error _Error StackTrace: Cannot find module 'eslint-config-appium': _missing paramter -d when running **./Scripts/bootstrap.sh**

&nbsp;


- Login to Apple developer account and [register device](https://www.wikihow.com/Add-a-New-Device-to-Your-Apple-Developer-Portal) to developer account.
- Open project **WebDriverAgent.xcodeproj** within folder **WebDriverAgent** in Xcode.

![Image description](https://github.com/sayems/appium/blob/master/img/webdriveragent.png)

- Select target **WebDriverAgentLib**, in the Signing section, check **Automatically manage signing** and select the team.

![Image description](https://github.com/sayems/appium/blob/master/img/xcode1.png)

- Then on the menu bar, select **Product > Build**

![Image description](https://github.com/sayems/appium/blob/master/img/xcode2.png)

- Repeat the last two steps for **WebDriverAgentRunner**
- Xcode may fail to create a provisioning profile for the `WebDriverAgentRunner` target:

![Image description](https://github.com/sayems/appium/blob/master/img/xcode-facebook-fail.png)


This necessitates manually changing the bundle id for the target by going into the "Build Settings" tab, and changing the "Product Bundle Identifier" from `com.facebook.WebDriverAgentRunner` to something that Xcode will accept:

![Image description](https://github.com/sayems/appium/blob/master/img/xcode-bundle-id.png)

- Build **WebDriverAgent** by executing this command on Terminal in WebdriverAgent folder to verify all above steps worked
```
xcodebuild -project WebDriverAgent.xcodeproj -scheme WebDriverAgentRunner -destination 'id=<udid>' test
```

##### UUID
To get the `UUID` of the real device connect, you can run the following command:
```
ios-deploy -c 
```
or
```
instruments -s devices
```

```
Known Devices:
iPhone 11 (13.0) [7F880C08-A1E2-4ED0-89FD-824301B8A20C] (Simulator)
iPhone 11 Pro (13.0) [B723EA9B-0594-4014-97A9-63F46FA4C3E] (Simulator)
iPhone 11 Pro (13.0) + Apple Watch Series 5 - 40mm (6.0) [B65275D-9AA8-4D58-8A84-B93CF01B68A2] (Simulator)
iPhone 11 Pro Max (13.0) [07484F3C-BD03-466D-ACF5-B1907D299C7D] (Simulator)
iPhone 11 Pro Max (13.0) + Apple Watch Series 5 - 44mm (6.0) [7C75E622-9C38-431F-AB76-E72BF35A15FB] (Simulator)
iPhone 4s (9.3) [86C308B0-720E-4AB3-878-8DC20CF5260A] (Simulator)
iPhone 5 (9.3) [823C91B9-03FB-4B18-B65-2E1C3B8ECA9A] (Simulator)
iPhone 5s (9.3) [E3C5673E-8E38-4459-B44-8832A5755F97] (Simulator)
iPhone 6 (9.3) [52F05C6C-FDBB-4FC2-847E-528BC7C45FB] (Simulator)
iPhone 6 Plus (9.3) [DE5FE6E0-BD77-475E-9C1-606FB61E53D2] (Simulator)
iPhone 6s (9.3) [891C17DB-30E2-4D39-B799-5DF48C1F82A] (Simulator)
iPhone 6s Plus (9.3) [9D9D1E2D-FC88-4E7E-9D67-AC21A1AA9423] (Simulator)
iPhone 8 (13.0) [24AD042A-EFD2-4612-8019-AD8952FEF02] (Simulator)
iPhone 8 Plus (13.0) [B855D910-6552-4D0B-D9B-FBECB7E02823] (Simulator)
```

    
- In case this dialog is displayed, select **Always Allow**.

![Image description](https://github.com/sayems/appium/blob/master/img/access.png)


If this was successful, the output should end with something like:
```json
    Test Suite 'All tests' started at 2017-01-23 15:49:12.585
    Test Suite 'WebDriverAgentRunner.xctest' started at 2017-01-23 15:49:12.586
    Test Suite 'UITestingUITests' started at 2017-01-23 15:49:12.587
    Test Case '-[UITestingUITests testRunner]' started.
        t =     0.00s     Start Test at 2017-01-23 15:49:12.588
        t =     0.00s     Set Up
```

(OPTIONAL) To completely verify , you can try accessing the WebDriverAgent server status (note: you must be on the same network as the device, and know its IP address, from Settings => Wi-Fi => Current Network)

```json
export DEVICE_URL='http://<device IP>:8100'
export JSON_HEADER='-H "Content-Type: application/json;charset=UTF-8, accept:application/json"'
curl -X GET '$JSON_HEADER' $DEVICE_URL/status
```
```json
You ought to get back output something like this:
 {
      "value" : {
        "state" : "success",
        "os" : {
          "name" : "iOS",
          "version" : "10.2"
        },
        "ios" : {
          "simulatorVersion" : "10.2",
          "ip" : "192.168.0.7"
        },
        "build" : {
          "time" : "Jan 23 2017 14:59:57"
        }
      },
      "sessionId" : "8951A6DD-F3AD-410E-A5DB-D042F42F68A7",
      "status" : 0
```

&nbsp;
&nbsp;

## Create a project


#### Mobile Browser
```java
    @Override
    public Mobile newMobile() {
        capabilities = new DesiredCapabilities();
        capabilities.setCapability(MobileCapabilityType.BROWSER_NAME, MobileBrowserType.SAFARI);
        capabilities.setCapability(MobileCapabilityType.AUTOMATION_NAME, AutomationName.IOS_XCUI_TEST);
        capabilities.setCapability(PLATFORM_VERSION, "13.0");
        capabilities.setCapability(IOSMobileCapabilityType.LAUNCH_TIMEOUT, 500000);
        capabilities.setCapability(MobileCapabilityType.DEVICE_NAME, "iPhone Simulator");

        IOSDriver<IOSElement> driver = new IOSDriver<>(service, capabilities);
        return makeBrowser(driver, elementImpls);
    }
```

#### Simulator code example

```java
 DesiredCapabilities cap = new DesiredCapabilities();
  
  cap.setCapability("platformName", "iOS");
  cap.setCapability("platformVersion", "11.4");
  cap.setCapability("deviceName", "iPhone 8");
  cap.setCapability(CapabilityType.BROWSER_NAME, "safari");
  cap.setCapability("app", “location of .app or .ipa file“);
 
  URL url = new URL("http://127.0.0.1:4723/wd/hub");
  
  IOSDriver driver = new IOSDriver(url, cap);
```

#### Real Device code example

```java
DesiredCapabilities caps = new DesiredCapabilities();
caps.setCapability("platformName", "iOS");
caps.setCapability("platformVersion", "12.4");
caps.setCapability("deviceName", "iPhone Xs");
caps.setCapability("automationName", "XCUITest");

caps.setCapability("app", app);

driver = new IOSDriver<MobileElement>(new URL("http://localhost:4723/wd/hub"), caps);
```

### Running Test

```java
public class GithubTest {

    private static AppiumDriverLocalService service = new AppiumServiceBuilder()
                .withArgument(GeneralServerFlag.SESSION_OVERRIDE)
                .usingAnyFreePort()
                .build();

    @Test
    public void shouldAnswerWithTrue() {

        IOSMobileFactory mobileFactory = new IOSMobileFactory(service);
        Mobile mobile = mobileFactory.newMobile();
        mobile.open("http://www.github.com", new GithubHome())
                .waitUpTo(1, ChronoUnit.MINUTES);

        mobile.closeAll();

    }

    @BeforeTest
    public void setupAppium(){
        service.start();
        if (!service.isRunning()) {
            throw new AppiumServerHasNotBeenStartedLocallyException(
                    "An appium server node is not started!");
        }
    }


    @AfterTest
    public void stop(){
        service.stop();
    }
}
```

&nbsp;
[top](#table-of-contents)
&nbsp;

## troubleshooting

If you get an error message:
```javascript
sayem@ ~: npm install -g appium
internal/modules/cjs/loader.js:584
    throw err;
    ^

Error: Cannot find module '../lib/utils/unsupported.js'
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:582:15)
    at Function.Module._load (internal/modules/cjs/loader.js:508:25)
    at Module.require (internal/modules/cjs/loader.js:637:17)
    at require (internal/modules/cjs/helpers.js:22:18)
    at /usr/local/lib/node_modules/npm/bin/npm-cli.js:19:21
    at Object.<anonymous> (/usr/local/lib/node_modules/npm/bin/npm-cli.js:153:3)
    at Module._compile (internal/modules/cjs/loader.js:701:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:712:10)
    at Module.load (internal/modules/cjs/loader.js:600:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:539:12)
```

Run the following command:
```
sudo rm -rf /usr/local/lib/node_modules/npm
brew uninstall --force node
brew install node
```

&nbsp;
[top](#table-of-contents)
&nbsp;

### Resources
- [The XCUITest Driver for iOS](http://appium.io/docs/en/drivers/ios-xcuitest/index.html)
- [Setting up iOS Real Devices Tests with XCUITest](https://github.com/appium/appium-xcuitest-driver/blob/master/docs/real-device-config.md)
- [Appium XCUITest Driver Real Device Setup](http://appium.io/docs/en/drivers/ios-xcuitest-real-devices/)
- [Automating Mobile Gestures For iOS With WebDriverAgent/XCTest Backend](http://appium.io/docs/en/writing-running-appium/ios/ios-xctest-mobile-gestures/#automating-mobile-gestures-for-ios-with-webdriveragentxctest-backend)
- [Parallel iOS Tests](http://appium.io/docs/en/advanced-concepts/parallel-tests/#parallel-ios-tests)
- [Using Selenium Grid with Appium](http://appium.io/docs/en/advanced-concepts/grid/)
- [How To Set Up And Customize WebDriverAgent Server](https://github.com/appium/appium/blob/master/docs/en/advanced-concepts/wda-custom-server.md)
- [Medium - Appium XCUITest on Real iOS Devices](https://medium.com/@yash3x/appium-xcuitest-on-real-ios-devices-bd1ebe0dea55)
- [How to Build IPA file on Xcode 10](https://www.youtube.com/watch?v=w1rStFTTPrQ)

&nbsp;
[top](#table-of-contents)
&nbsp;
