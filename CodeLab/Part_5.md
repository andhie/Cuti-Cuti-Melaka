# Cuti-Cuti Melaka - Part 5

## Background

We will be using Google Play Services API such as Google Maps and Fused Location.

## Creating Google Maps Activity

1. Create Google Maps Activity via the `New` -> `Activity` -> `Google` -> `Google Maps Activity`
2. Open the `app/src/debug/res/values/google_maps_api.xml`
3. Follow the link provided to enable Google Maps in your app.
4. After obtaining the API Key, replace the `YOUR_KEY_HERE` with your actual API Key.
  - It starts with "AIza"

## Start GoogleMapsActivity

1. In your `activity_tempat_detail.xml`, add a new row (similar design with Call row) below Call, use the `@drawable/ic_place` with the text "Show On Map".
2. When users click on "Show On Map", it should start `GoogleMapsActivity`.
3. Run your app to confirm you can see a Google Map with a pin in Sydney, Australia
4. Modify your start `GoogleMapsActivity` intent to pass your `Tempat`.
5. In your `GoogleMapsActivity`, retrieve the `Tempat` that was given to you via `getIntent()`
6. Once you have your `GoogleMap` object, create a pin with `@drawable/pin` (instead of default red pin) with the latitude and longitude in your `Tempat`. Set the pin title to your `Tempat` name.
7. Dont forget to move your `Camera` to the tourist attraction location

## ADVANCE: Sorting the Tempat list by distance

Making your app context aware helps the users a lot. By knowing the user's location, you can sort the list by distance from user. Users can easily figure out the nearest Tempat to them.

  - Refer to the official up-to-date documentation [Getting the Last Known Location
](https://developer.android.com/training/location/retrieve-current.html)
  - In Marshmallow (API 23), getting users location is a 'Dangerous' permission, you would have to ask for users permission.

1. Add permission in your `AndroidManifest.xml`
2. In your `MainActivity`, create a `GoogleApiClient` via its Builder and request for `FusedLocationApi` service from Google Play Services
3. Let your `MainActivity` implements  `GoogleApiClient.ConnectionCallbacks` and  `GoogleApiClient.OnConnectionFailedListener`
  - It should be similar to
  ```java
  public class MainActivity implements GoogleApiClient.ConnectionCallbacks,
        GoogleApiClient.OnConnectionFailedListener {

        }
  ```
4. There will be 3 new methods that you need to override, `onConnected`, `onConnectionSuspended` and `onConnectionFailed`
5. In the `onConnected` method, this is where you can start using any Google Play Services API. Before we get users location, we need to check if we have permission.
```java
if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION)
                == PackageManager.PERMISSION_GRANTED) {
    // have permission, get location
} else {
  // ask user for location permission
  requestPermissions(new String[]{Manifest.permission.ACCESS_COARSE_LOCATION}, 77);
}
```
5. Override the `onRequestPermissionsResult` method in your `MainActivity` where any permission request returns back here. Check the result to confirm if you have `PackageManager.PERMISSION_GRANTED` then proceed to get user location.
  - This is similar to `startActivityForResult` and its accompanying method `onActivityResult`
6. Use the `FusedLocationApi` to get the users last location.
  - `Location` may be null as users may not have location previously (e.g. turned off gps, just reboot phone)
  - If you are using emulator, launch the `DDMS` -> `Emulation Control`. Make sure you select the emulator on the left pane or your controls will be disabled. Then type in your latitude and longitude.
7. Use the `Location` and sort your `Tempat`
  - Your `Tempat` can implement the `Comparable<Tempat>` interface OR
  - Create a `Comparator<Tempat>` class and pass it to `Collections.sort(list, comparator)` method.
