# expo-location-bare

This repo demonstrates a simple example of expo-location as specified in [https://docs.expo.dev/versions/latest/sdk/location/](official documentaion)

## Purpose
Purpose of this repo is to show that expo location always includes the `com.google.android.gms.permission.ACTIVITY_RECOGNITION` example even though official documentation 
does not state it.

## Plausible cause:
Debugging shows that permission `com.google.android.gms.permission.ACTIVITY_RECOGNITION` is added to the AndroidManifest.xml by dependecy 'io.nlopez.smartlocation:library:3.2.11'

This dependecy is added in expo location in [build.gradle](https://github.com/expo/expo/blob/d2cedae3ac78718bfe8dcac6f0375412c7c178ff/packages/expo-location/android/build.gradle#L73)

Permission `com.google.android.gms.permission.ACTIVITY_RECOGNITION` is added in the [smart-location-lib](https://github.com/mrmans0n/smart-location-lib/blob/v3.x/library/src/main/AndroidManifest.xml)
for geo-fencing features

## Steps to reproduce:
1. clone this repo
2. run `npm install`
3. run `eas build --platform android --profile dev` --> you may need to login to expo
4. Wait for the build to finish
5. Download the resulting apk
6. Inspect the permissions of resulting apk. e.g `aapt d permissions YOUR_APK_FILE_HERE'` 
7. Resulting permissions are 
```
package: com.hamdanis.expolocationbare
uses-permission: name='android.permission.ACCESS_COARSE_LOCATION'
uses-permission: name='android.permission.ACCESS_FINE_LOCATION'
uses-permission: name='android.permission.FOREGROUND_SERVICE'
uses-permission: name='android.permission.INTERNET'
uses-permission: name='android.permission.READ_EXTERNAL_STORAGE'
uses-permission: name='android.permission.SYSTEM_ALERT_WINDOW'
uses-permission: name='android.permission.VIBRATE'
uses-permission: name='android.permission.WRITE_EXTERNAL_STORAGE'
uses-permission: name='android.permission.ACCESS_NETWORK_STATE'
uses-permission: name='com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE'
uses-permission: name='com.google.android.providers.gsf.permission.READ_GSERVICES'

```
