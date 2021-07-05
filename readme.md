Requirements
(if requirements without version - recommend latest)
For electron build:

Node.js 14+
Python 2.7.10+
At the package.json of the root project
```
  "homepage": "./",
```
special point for platforms:
Windows: Windows SDK 10.0.15063.468. 
Mac: Xcode and RedHat Build Support

For android build:
```
Java Development Kit (JDK)
Gradle
Android SDK

environment variables - JAVA_HOME, ANDROID_SDK_ROOT 
```
For ios build:
```
xcode
cocoapods (1.8.0+ or latest)
```


How to add it to the project
dist directory is requirement cordova other options

```
cordova create cordova com.apollo.currency Apollo --template https://github.com/RomanFirstBridge/template
```

you can add to the package.json file command 

```
"build:android: ./cordova/android",
"build:electron: ./cordova/electron"
```

App work without proxy, so to the config file you need to add the conditions for correct request works.
```
  server: window.cordova ? 'your url or var' : '',
```