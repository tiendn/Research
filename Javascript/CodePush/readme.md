# [react-native-code-push](https://github.com/Microsoft/react-native-code-push/blob/master/docs/multi-deployment-testing-ios.md) - Update 01/08/2018

## Installation
Step by step:

* Install npm and link: https://github.com/Microsoft/code-push/tree/master/cli#installation
* Add `public key` and `deployment key` with multiple testing (1)
    * iOS: https://github.com/Microsoft/react-native-code-push/blob/master/docs/multi-deployment-testing-ios.md
    
    * Android: https://github.com/Microsoft/react-native-code-push/blob/master/docs/multi-deployment-testing-android.md
* Import library in JS code: https://github.com/Microsoft/react-native-code-push#plugin-usage

## Usage
Releasing updates: https://github.com/Microsoft/code-push/tree/master/cli#releasing-updates-react-native

Command line build popular: (this will make release to `STAGING`)
* iOS: 

        code-push release-react MyApp-iOS ios
* Android: 

        code-push release-react MyApp-Android android

Change `STAGING` INTO `PRODUCTION` use this: 

    code-push promote APP_NAME_HERE Staging Production

In fact, when setup like (1): 

* With **Stagging build**, app will be build with **Release Configuration** and `STAGGING` key. So your device will sync with `STAGGING` deployment

* With **Release build**, app will be build with **Release Configuration** and `PRODUCTION` key. So your device will sync with `PRODUCTION` development

## Debug
https://github.com/Microsoft/react-native-code-push#debugging--troubleshooting

Note that by default, React Native logs are disabled on iOS in release builds, so if you want to view them in a release build, you need to make the following changes to your `AppDelegate.m` file:

1. Add an `#import <React/RCTLog.h>` statement. For RN < v0.40 use: #import "RCTLog.h"

2. Add the following statement to the top of your `application:didFinishLaunchingWithOptions` method:
    ```objective-c
    RCTSetLogThreshold(RCTLogLevelInfo);
    ```


## Questions
1. What different between Staging and Production ?

    It just another version build. If your app build with `STAGGING` key, any `STAGGING` will be sync with your app, but not `PRODUCTION` and vice versa.
2. If don't provide `CodePushDevelopmentKey`, what problem?

    The error messageg here: 
    
        [CodePush] 400: An update check must include a valid deployment key - please check that your app has been configured correctly. To view available deployment keys, run 'code-push deployment ls <appName> -k'