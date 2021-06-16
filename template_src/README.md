# Apollo mobile APPs

## Required Preinstalled Software

1. NPM 6.5.0
2. NVM 11.8.0
3. Gradle 5.5.1 or higher
4. Android SDK API Level 28 or higher
5. Android NDK - android-ndk-r20
6. Cordova 9.0.0 (cordova-lib@9.0.1)
7. Java 8 (1.8.0_172)
8. HOMEBREW_VERSION: 2.1.10 (for Mac)

## Required Programms

1. Terminal/Command line
2. Android Studio 3.4
3. Xcode 10.3

## How to build apps
`cordova platform rm ios && cordova platform add ios@5.1.1 &&  cordova build ios &&  cordova run ios`
`cordova platform rm android && cordova platform add android &&  cordova build android &&  cordova run android`

1. Create an empty folder on your device and clone Apollo Web wallet repo's stable branch (for example - master) - git clone https://bitbucket.org/firstbridge_company/web-wallet/src/master/
2. Move to git folder `cd web-wallet`
3. Remove node modules before each build `rm -rf node_modules`
4. Install node modules - `npm install` or `yarn install`
4. Create production build `npm run build`
5. Create an empty folder on your device and clone this repository - git clone https://firsfbridge@bitbucket.org/firsfbridge/apollo-mobile-apps.git
6. Move to git folder `cd apollo-mobile-apps`
7. Copy all contents from the build folder in web-wallet repo and pase it to the www folder in apollo-mobile-apps repo
8. Move to apollo-mobile-apps folder

9. Run app building commands `cordova build android` and `cordova build ios`

### Android build

#### Command line - Cordova build

1. Run one of the following commands to get an .apk file
```
Possible commands for Android build:

Cordova build - `cordova build android` - builds app-debug.apk file

Gradle based builds:
* Build app-debug.apk cordova build android -- --gradleArg=-PcdvBuildMultipleApks=true --info
* Build unsigned app-release.apk cordova build android --release --gradleArg=-PcdvBuildMultipleApks=true --info
* Create a debug bundle - go to /platfrorms folder run ./gradlew bundleDebug
* Create an unsigned release bundle - go to /platfrorms folder run ./gradlew bundleRelease

> Bundles have .aab file extension
```
10. Check Android build results here - /ApolloWallet/platforms/android/app/build/outputs/apk/
11. Manually install .apk to your android device

#### Android studio

1. Download and install Android studio from https://developer.android.com/studio/index.html, start it
2. Open a new project from `/platforms/android/` folder
3. Create an Android virtual device (AVD)
4. Set an NDK location in Project structure
5. Build and run the project on the choosen AVD

Optional - import apk file

1. Click `File` and choose `Profile or Debug APK`
2. Choose your apk and run it

### iOS build

1. Start xCode and open `/platforms/ios`
2. Choose a device (not iOS generic device)
3. Run build

### iOS .ipa build and testing on real iphone device

1. Run cordova build ios --device --buildFlag="-UseModernBuildSystem=0" to generate .ipa file
2. Open Xcode, connect your iphone by USB and add your device Product->Destination->your device
3. Open /platforms/ios/build/device and drag&drop .ipa file to your phone displayed in Xcode
4. Approve your app in iphone settings - general/device control/your account/your app
5. Launch the app on your iphone

### OSX build

1. Add OSX platform - cordova platform add osx
2. Run cordova build osx --device --buildFlag="-UseModernBuildSystem=0"
3. Open /platforms/osx/build and start the app

### OSX .dmg debug build

1. Add cordova-electon platform - cordova platform add cordova-electron
2. Build .dmg file - cordova build cordova-electron
3. Open /platforms/cordova-electron/build and run .dmg file

##### References and known issues

Not all licenses are signed - https://stackoverflow.com/questions/39760172/you-have-not-accepted-the-license-agreements-of-the-following-sdk-components
```
Run ./sdkmanager --licenses and sign all licenses
Run build in Android stuudio and sign all licenses in it's interface
```

No toolchains found in the NDK toolchains folder for ABI with prefix: mips64el-linux-android
```
Open /platforms/android/build.gradle and modify classpath value to this `classpath 'com.android.tools.build:gradle:3.4.2`
Possible solution - https://georgik.rocks/android-studio-ndk-could-not-start-mips64el-linux-android-strip/
```

Minimum supported Gradle version is 4.4. Current version is 4.1. If using the gradle wrapper, try editing the distributionUrl in
```
Open /platforms/android/cordova/lib/builders/GradleBuilder.js and modify `var distributionUrl` on line 251 to `https\\://services.gradle.org/distributions/gradle-5.6-all.zip`
```

System variables and PATH aren't set - https://gist.github.com/patrickhammond/4ddbe49a67e5eb1b9c03
```
* Run the followind commands in command line: 

export ANDROID_HOME=/usr/local/share/android-sdk
export ANDROID_NDK_HOME=/usr/local/share/android-ndk
export ANDROID_PLATFORM_TOOLS=/usr/local/share/android-sdk/tools/bin
export ANDROID_PLATFORMS=/usr/local/share/android-sdk/tools/bin
export ANDROID_SDK_ROOT=/usr/local/share/android-sdk

export PATH=$ANT_HOME/bin:$PATH
export PATH=$MAVEN_HOME/bin:$PATH
export PATH=$GRADLE_HOME/bin:$PATH
export PATH=$ANDROID_HOME/tools:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/build-tools/19.1.0:$PATH

brew update
```

repositories.cfg could not be loaded
* Run the following in the command line:
```
touch ~/.android/repositories.cfg
sdkmanager "build-tools;26.0.1" --verbose
```

Could not find method leftShift() while building the app in Android Studio
```
https://stackoverflow.com/questions/55793095/could-not-find-method-leftshift-for-arguments-after-updating-studio-3-4
Replace `task cdvPrintProps <<` with `task cdvPrintProps doLast`
```

NPM Build errors
```
1. Install nvm (https://github.com/nvm-sh/nvm) to change node version

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash

2. Download version 11.8.0
nvm install 11.8.0

3. Set it as default
nvm alias default 11.8.0

4. Switch to it
nvm use default

5. Remove node modules
rm -rf node_modules/

6. Install node modules
npm/yarn install
```

Key store passwords:
`Apollo1!`