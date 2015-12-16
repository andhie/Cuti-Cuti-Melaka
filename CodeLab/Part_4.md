# Cuti-Cuti Melaka - Part 4


## Background

In this session, you will store the Tempat data on a permanent storage such as SQLite Database

## Creating Tables

1. Create a new Java file named `MyDatabaseHelper.java`
2. Then make it `extends SQLiteOpenHelper`
3. Implement the `onCreate(SQLiteDatabase)` method by creating a table to store the `Tempat` data.
  - Give the table a name, `table_tempat`
  - Create columns that matches your `Tempat.java` model and declare appropriate data type for SQLITE

## Modify your IntentService

We will modify `FetchTempatService` to send a broadcast that there is new data instead of passing the whole JSON string in the Intent. Note that, in Android, there is a 1MB limit for passing data, or your will get  `!!! FAILED BINDER TRANSACTION !!!`. One solution this approach it to store the data somewhere (e.g. database, files) and let the next Activity know where to find it.

1. In order to store every `Tempat` attributes into the database, we would need to read the JSON string and store it according to the appropriate database column.
  - Consider creating a static function util for JSON parsing
  ```java
  public class TempatUtil {
    public static List<Tempat> parseJson(String json) {
      // move your JSONObject and JSONArray code here
      // and return List<Tempat>
    }
  }
  ```
2. Modify your broadcast `Intent` not to send the JSON string.

## Modify BroadcastReceiver in MainActivity

1. Make similar adjustments to in your `MainActivity`'s `BroadcastReceiver` to not read the JSON string data.

## Modify AsyncTask to read database

 1. Inside `doInBackground`, remove any existing JSON parsing code. Add the database code to get our Tempat.
 2. Querying the database will return in a `Cursor` object. Loop thru the `Cursor` and read each row info
 3. By the end of `doInBackground`, it should still return a `List<Tempat>`
