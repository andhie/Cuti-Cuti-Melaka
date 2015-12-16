# Cuti-Cuti Melaka - Part 3

Start Part 3 by download resources required for this section

  - Download [Part 3 of CodeLab Resource](https://github.com/andhie/Cuti-Cuti-Melaka/raw/master/CodeLab%20Resources/CodeLab%20-%20Part%203.zip)

## Background

The whole architecture after the end of this lesson will be:

  1. `Activity` start the `FetchTempatService` (an `IntentService`) where it will connect to the internet and read the data.
  2. `FetchTempatService` will use `LocalBroadcastManager` to broadcast the data back to the `Activity`
  3. Activity will have a `BroadcastReceiver` to listen to the broadcast message.
  4. Upon receiving the data, you should start the `AsyncTask` that process the JSON data into actual `List<Tempat>` and add it to your `CustomAdapter`

## IntentService instead of AsyncTask

AsyncTask continues to run even after Activity is destroyed, holding a reference to any Views (such as onPostExecute, `TextView#setText()` is used) will indirectly leaks the whole Activity.

1. Right-click on the src folder, `New` -> `Service` -> `Service (IntentService)`
2. Open your `AndroidManifest.xml` and confirm your service is declared.
  - Note: If you did not declare your Service, it will not run.
  ```xml
  <service android:name=".FetchTempatService" />
  ```
3. Note that in FetchTempatService.java actually `extends IntentService`. Write your code in `onHandleIntent()` method
4. Move parts of the `AsyncTask` code that related to fetching data from Internet until the point we get the JSON string (i.e `HttpURLConnection` related).
  - We will be sending this JSON `String` back to the Activity via `LocalBroadcastManager` later

## Modify AsyncTask to only handle JSON parsing

1. Your `AsyncTask` should only be left with JSON string parsing code (i.e. `JSONObject` and `JSONArray`). It should still return `List<Tempat>` in `doInBackground()` method.
2. Modify your `AsyncTask` to accept a `String` type, indicated by the 1st data-type inside <>. Such as `extends AsyncTask<String, Void, List<Tempat>>`

## Creating a BroadcastReceiver

1. Create or subclass a `BroadcastReceiver`, name it `MyBroadcastReceiver`
2. In the `onReceive()` method, get the JSON String data from the `Intent` given. You can use the key "Tempat_json". Start our AsyncTask by passing the JSON String into the AsyncTask execute().
`new CustomAsyncTask.execute(TempatJsonString)`
  - Later, You will be sending a broadcast by creating an `Intent` where you already already did `putExtras("Tempat_json", TempatJsonString)`
3. Declare a global variable for `MyBroadcastReceiver`
  - For example
  ```java
  BroadcastReceiver broadcastReceiver = new MyBroadcastReceiver();
  ```
4. Use the `LocalBroadcastManager` to register `MyBroadcastReceiver` with a `new IntentFilter("ACTION_DATA_GET")`
  - Register in `Activity`'s `onStart()` method
  - Unregister in `Activity`'s `onStop()`
  - You may refer to [how to use LocalBroadcastManager?](https://stackoverflow.com/questions/8802157/how-to-use-localbroadcastmanager) on StackOverFlow

## Sending broadcast from IntentService

1. Use the `LocalBroadcastManager` to send (broadcast) an Intent with `"ACTION_DATA_GET"` as your Action. Put the JSON string that you get from `HttpURLConnection` into the Intent via `putExtras("Tempat_json", TempatJsonString)`

## Starting your IntentService

1. In your `Activity`'s `onCreate()` method, use `startService()` to start the `FetchTempatService`
