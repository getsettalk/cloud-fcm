
# How to use firebase Cloud Messaging (FCM)
FCM is a `cost free` service, allowing for server-device and device-device communication. The React Native Firebase Messaging module provides a simple JavaScript API to interact with FCM(send notification)


🔗 you can read here  [full details](https://rnfirebase.io/)

## 🌤 Steps to Use FCM

Before `getting started`, the documentation assumes you are able to create a project with React Native and that you have an active Firebase project. If you do not meet these prerequisites, follow the links below:

- [React Native - Setting up the development environment](https://reactnative.dev/docs/environment-setup)
- [Create a new Firebase project](https://console.firebase.google.com/)

`Additionally`, current versions of firebase-ios-sdk have a minimum Xcode requirement of 14.1, which implies a minimum macOS version of 12.5 (macOS Monterey).


# Installation for React Native CLI projects
Installing React Native Firebase to a RN CLI project requires a few steps; installing the NPM module, adding the `Firebase config` files & rebuilding your application.

##  ✔ 1. Install via NPM
#### Using npm
```
npm install --save @react-native-firebase/app

```


#### Using Yarn
```
yarn add @react-native-firebase/app
```

The `@react-native-firebase/app` module must be installed before using any other Firebase service.


## ✔ 2. React Native CLI - Android Setup
To allow the Android app to securely connect to your Firebase project, a configuration file must be downloaded and added to your project.

On the Firebase console, `add a new Android` application and enter your projects details. 

➡ to generate a certificate run `cd android` && `./gradlew signingReport`.

👍 Download the` google-services.json` file and place it inside of your project at the following location: `/android/app/google-services.json`.

### 🟢 Configure Firebase with Android credentials
First, add the `google-services` plugin as a dependency inside of your `/android/build.gradle `file:

```
buildscript {
  dependencies {
    // ... other dependencies
    classpath 'com.google.gms:google-services:4.4.0'
    // Add me only above one line ---⬆⬆
  }
}
```

✔ Lastly, execute the plugin by adding the following to your `/android/app/build.gradle` file:

```
apply plugin: 'com.android.application'
apply plugin: 'com.google.gms.google-services' // ⬅ <- Add this line
```
## ✔ 3 . Autolinking & rebuilding

 to rebuild your apk for android:
 ```
 npx react-native run-android
 ```

` ✔✔ Now we have successfully installed Firebase configuration , now you can use other features of firebase to use that`

# 🟢🟢 Now  install Cloud Messaging For Send Notification


#### Install the messaging module
```
yarn add @react-native-firebase/messaging
```

### Uses : 
- Android - Requesting permissions

```
 import {PermissionsAndroid} from 'react-native';
  PermissionsAndroid.request(PermissionsAndroid.PERMISSIONS.POST_NOTIFICATIONS);
  ```

  ### Getting FCM Token:

  use this function to get fcm device token 

  ```
  async function requestFCMToken() {
    try {
      const fcmToken = await messaging().getToken();
      if (fcmToken) {
        // console.log('FCM Token:', fcmToken);
        return fcmToken;
        // Use or send the FCM token as needed (e.g., for push notifications)
      } else {
        console.log('No FCM token available.');
        return null; // Return a default value if no token is available
      }
    } catch (error) {
      console.error('Error fetching FCM token:', error);
      return null; // Return a default value if no token is available
    }
  }
  ```

  ===> uses: must be call that function inside async
  ```
const  fcmTokem  = await requestFCMToken();
console.log(fcmTokem)
```



### unsubscribe it in App.js

```
 useEffect(() => {
    const unsubscribe = messaging().onMessage(async remoteMessage => {
    console.log("FCM Arrived:", remoteMessage)
    alert('A new FCM message arrived! Forground :', JSON.stringify(remoteMessage));


    return unsubscribe;
  }, [])
  ```



  ###### Now you send notification using `fcmTokem` and `ServerKey`



## 🟢✔ where and how to test 

`Go to this Website` [test2fcm](https://getsettalk.github.io/test2fcm/), where you can test notification `free` `unlimited`. its fully customizable.

https://getsettalk.github.io/test2fcm/

![image](https://github.com/getsettalk/cloud-fcm/assets/49394996/b3a63e51-3d10-44c4-8523-a623722502a2)()





**💖🟢 its work fine with [https://notifee.app/](https://notifee.app/)**



