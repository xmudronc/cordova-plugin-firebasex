# Version 6.0.2
* (Android) Improved exception handling to prevent app crashes due to plugin exceptions.
Document caveats of received message payload when notification message is received while app is not running on Android.
Further resolves [#52](https://github.com/dpa99c/cordova-plugin-firebasex/issues/52).

# Version 6.0.1
* (Android) Expose notification message properties in message object sent to onMessageReceived().
Ensure message is always sent to onMessageReceived(), regardless if it was tapped.
Resolves [#52](https://github.com/dpa99c/cordova-plugin-firebasex/issues/52).


# Version 6.0.0
* *BREAKING CHANGES*
    * `onMessageReceived()` is now called when a message is received (data or notification) AND when a system notification is tapped (whether app is running or not)
    * Resolves [#48](https://github.com/dpa99c/cordova-plugin-firebasex/issues/48).
    * The `tap` parameter passed to `onMessageReceived()` is only set if a system notification is tapped
        * If the system notification was tapped while the app is running in the foreground, the value will be `tap: "foreground"`
        * If the system notification was tapped while the app is not running / in the background, the value will be `tap: "background"`     

# Version 5.0.0
* *BREAKING CHANGES*
    * `onNotificationOpen()` renamed to `onMessageReceived()`
    * Changed key names for custom notification properties in FCM data messages to display system notifications in foreground.
    * Message payload is always delivered to `onMessageReceived()` for both data and notification messages.
    * `messageType` key indicates type of FCM message: `notification` or `data`
    * `tap` is only set when `messageType` is `notification`
    * Explicit dependency on `cordova-plugin-androidx-adapter` since Android implementation uses AndroidX so is incompatible with Android Support Library.
    * Set `remote-notification` background mode in native Xcode project for iOS.
    * Reworked plugin documentation.
* Support customisable display of system notifications while app is in foreground for both notification and data messages (both Android & iOS).
* Set default color accent and notification channel for FCM notifications.
* Add support for default and custom notification channels for Android 8+
    * Customise importance, visibility, LED light, badge number, notification sound and vibration pattern 
* Calling `logError()` on Android now also logs to native logcat (as well as a non-fatal error to remote Crashlytics service).
* Fix `logError()` on iOS to log non-fatal error to remote Crashyltics service.
* Implement stubs for `hasPermission()` and `grantPermission()` on Android so they both return true in to the success callback.
* Rationalise permission check/request on iOS.
* Remove legacy support for iOS 9 and below.
* Support overridable default color accent for Android notification icons via `ANDROID_ICON_ACCENT` plugin variable.
    
# Version 4.0.0
* *BREAKING CHANGE:* set min supported versions to `cordova@9` and `cordova-ios@5`.
    * Drop dependency on cordova-plugin-cocoapodsx to install pod dependencies.
    * Instead  update plugin.xml to use podspec formatting as required by cordova-ios@5.
    * Remove iOS plugin variables as these are not (currently) supported by cordova-ios@5
    * Resolves [#22](https://github.com/dpa99c/cordova-plugin-firebasex/issues/22).

# Version 3.0.8
* \[iOS\] Add support for stripping debug symbols for libraries included via Cocoapods. Resolves [#28](https://github.com/dpa99c/cordova-plugin-firebasex/issues/28).

# Version 3.0.7
* \[iOS\] Ensure runpath search path contains `$(inherited)` to avoid build warnings/issues. Resolves [#25](https://github.com/dpa99c/cordova-plugin-firebasex/issues/25).

# Version 3.0.6
* Update iOS to Firebase SDK v6.3.0 (from v5.20.2) - major version increment so update source code for breaking changes to API. Resolves [#9](https://github.com/dpa99c/cordova-plugin-firebasex/issues/9).
* Add support for NDK crashlytics on Android. Resolves [#17](https://github.com/dpa99c/cordova-plugin-firebasex/issues/17).

# Version 3.0.5
* Bump min version of cordova-plugin-cocoapod-supportx to 1.7.2 which fixes bug when using a plugin variable to specify the `ios-min-version` in `<pods-config>`

# Version 3.0.4
* Bump min version of cordova-plugin-cocoapod-supportx to 1.7.1 which supports using a plugin variable to specify the `ios-min-version` in `<pods-config>`

# Version 3.0.3
* Implement didReceiveRegistrationToken delegate for iOS. Resolves [#16](https://github.com/dpa99c/cordova-plugin-firebasex/issues/16).
* Document dependency on Cocoapods. Resolves [#15](https://github.com/dpa99c/cordova-plugin-firebasex/issues/15).
* Make min iOS version configurable. Resolves [#14](https://github.com/dpa99c/cordova-plugin-firebasex/issues/14).


# Version 3.0.2
* Update legacy Xpath reference to `<application>` element in `AndroidManifest.xml`

# Version 3.0.1
* Bump default iOS Firebase SDK version to 5.20.2 (https://firebase.google.com/support/release-notes/ios#version_5202_-_april_10_2019). Resolves [#8](https://github.com/dpa99c/cordova-plugin-firebasex/issues/8).

# Version 3.0.0
* Reapply: Support user-overriding of default Android Gradle & iOS Cocoapods versions using plugin variables.

# Version 2.1.2
* Revert: Support user-overriding of default Android Gradle & iOS Cocoapods versions using plugin variables.
    * Since it's not working on iOS due to Cocoapods plugin dependency.
    * Need to fix that plugin to handle plugin variables then reinstate this change in a major version release.

# Version 2.1.1
* Support user-overriding of default Android Gradle & iOS Cocoapods versions using plugin variables.

# Version 2.1.0
* Update Android source to use AndroidX class names and adds dependency on [cordova-plugin-androidx](https://github.com/dpa99c/cordova-plugin-androidx) for forward compatibility with future versions of Firebase libraries on Android.
    * Note: if you include other plugins in your project which reference the legacy Android Support Library, you'll still need to include [cordova-plugin-androidx-adapter](https://github.com/dpa99c/cordova-plugin-androidx-adapter) in your project to dynamically patch them.
* Pins Firebase and Crashlytics Gradle dependencies to latest major version (to prevent build failures due to unexpected changes in subsequent major versions).
* Set minimum supported versions to `cordova@8+`, `cordova-android@8+`, `cordova-ios@4+`.

# Version 2.0.7
* Merge [PR #7](https://github.com/dpa99c/cordova-plugin-firebasex/pull/7): use `<pod>` instead of deprecated `<<framework type="podspec">`. Resolves [#5](https://github.com/dpa99c/cordova-plugin-firebasex/issues/5).

# Version 2.0.6
* Use Cocoapods to satisfy iOS Firebase SDK (rather than bundling with plugin). See https://github.com/arnesson/cordova-plugin-firebase/pull/972.
* Add support for logMessage() and sendCrash() functions (ported from cordova-fabric-plugin)
* Bump version of Crashlytics library on Android to current latest (v2.9.8 - Dec 2018)
* Bump Firebase SDK versions in iOS PodSpecs to latest version (v5.15.0)
* Remove redundant build-extras.gradle
* Set minimum iOS version to 9.0 in podspec
* Remove unnecessary extra <config-file> block which can lead to race condition
* Fixes issues cause by Firebase SDK updates on 5 April 2019 (https://firebase.google.com/support/release-notes/android#update_-_april_05_2019) which removed deprecated API features causing Android build failures.
See https://github.com/arnesson/cordov 
* Fix compatibility with cordova@9 CLI
* Add explicit dependency on cordova-lib to prevent build error on iOS. Fixes #2.

---> **FORKED FROM `cordova-plugin-firebase` AS `cordova-plugin-firebasex`** <---

# Version 2.0.5

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/897">#897</a>: Fixed issue with after_prepare hook not copying required files

# Version 2.0.4

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/866">#866</a>: Fixed issue with loading .plist file on some iOS devices

# Version 2.0.3

### Features
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/874">#874</a>: Added new api `setCrashlyticsUserId` which allows setting Crashlytics user identifier
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/861">#861</a>: Updated `verifyPhoneNumber` api on android to add the following properties to the returned object:
   - `code` - sms code
   - `verified` - whether or not the verification was successful

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/869">#869</a>: Replace add/remove hooks with install/uninstall hooks to ensure proper configuration of the plugin
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/870">#870</a>: Add error handling to `fetch` api on iOS

# Version 2.0.2

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/837">#837</a>: Fixed android build

# Version 2.0.1

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/836">#836</a>: Fixed Crashlytics on iOS
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/830">#830</a>: Fixed initialization of firebase services

# Version 2.0.0

### Features
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/796">#796</a>: Update Firebase SDK Version to 5.x

### Bug Fixes
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/822">#822</a>: Can't use initFirebase() on 1.1.3 [Firebase isn't initialized]
- <a href="https://github.com/arnesson/cordova-plugin-firebase/issues/827">#827</a>: doc missing: initFirebase call needed before anything
- <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/824">#824</a>: Removed initRemoteConfig method

# Version 1.1.4 (deprecated)

This version has been deprecated due to complications with PR <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/784">#784</a>

# Version 1.1.3 (deprecated)

This version has been deprecated due to complications with PR <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/784">#784</a>

# Version 1.1.2 (deprecated)

This version has been deprecated due to complications with PR <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/784">#784</a>

# Version 1.1.1 (deprecated)

This version has been deprecated due to complications with PR <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/784">#784</a>

# Version 1.1.0 (deprecated)

This version has been deprecated due to complications with PR <a href="https://github.com/arnesson/cordova-plugin-firebase/pull/784">#784</a>

# Version 1.0.5

To force cordova to use this version, add the following to your project's config.xml:
```
<plugin name="cordova-plugin-firebase" spec="1.0.5" />
```
or by running:
```
cordova plugin add cordova-plugin-firebase@1.0.5 --save
```
