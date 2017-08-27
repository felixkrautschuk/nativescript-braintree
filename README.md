[![npm](https://img.shields.io/npm/v/nativescript-braintree.svg)](https://www.npmjs.com/package/nativescript-braintree)
[![npm](https://img.shields.io/npm/dt/nativescript-braintree.svg?label=npm%20downloads)](https://www.npmjs.com/package/nativescript-braintree)

# nativescript-braintree

Braintree Payment NativeScript plugin for Android. Detail information here: https://developers.braintreepayments.com/start/hello-client/android/v2

You will need a Server to Generate a client token. You can follow here:
https://developers.braintreepayments.com/start/hello-server/php 

Note: Your app's package ID should be lowercase letters. If your package contains underscores, the underscores should be removed. Detail: https://developers.braintreepayments.com/guides/client-sdk/setup/android/v2#browser-switch-setup

For iOS (Important)
===================
For Paypal must need to follow: https://developers.braintreepayments.com/guides/client-sdk/setup/ios/v4#register-a-url-type

## Platforms
Android

iOS ( iOS 9+)

## Installation

```javascript
tns plugin add nativescript-braintree
```

## Usage 
	
```javascript
    import { Braintree } from 'nativescript-braintree';
    private braintree: Braintree;

    this.braintree = new Braintree();
     let token = token; //Get the token from server. https://developers.braintreepayments.com/start/hello-server/php

     this.braintree.startPayment(token).then(()=>{
       console.dir(this.braintree.output);
       alert(this.braintree.output.msg);
       // Now you have nonce. So you can push it to server :)
     }).catch(()=>{
       console.dir(this.braintree.output);
       alert(this.braintree.output.msg);
     })
```

## Common Issues:

1) Error during build for Android

`Could not find com.android.support:design:26.0.0.`

Add following lines in your main `app.gradle` file.

```
allprojects {
    repositories {
        jcenter()
        maven {
            url 'https://maven.google.com'
        }
    }
}

```
ref: https://stackoverflow.com/questions/44500176/setting-up-gradle-for-api-26-android


`AAPT: No resource found that matches the given name: attr 'android:keyboardNavigationCluster'.`

Update sdk version and tools in gradle `compileSdkVersion 26` `buildToolsVersion "26.0.1"`

ref: https://stackoverflow.com/a/45310170/1281864

So my `app.gradle` looks like this (https://github.com/jibon57/nativescript-braintree/blob/master/demo/app/App_Resources/Android/app.gradle):

```
allprojects {
    repositories {
        jcenter()
        maven {
            url 'https://maven.google.com'
        }
    }
}
android {  
  defaultConfig {  
    generatedDensities = []
    applicationId = "com.yourcompany.yourapp" // this should be your app id
  }  
  aaptOptions {  
    additionalParameters "--no-version-vectors"  
  }
  compileSdkVersion 26
  buildToolsVersion "26.0.1"
} 

```
    
## License

Apache License Version 2.0, January 2004
