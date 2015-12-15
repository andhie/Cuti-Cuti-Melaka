# Cuti-Cuti Melaka - Part 2

Start Part 2 by download resources required for this section

  - Download [Part 2 of CodeLab Resource](https://github.com/andhie/Cuti-Cuti-Melaka/raw/master/CodeLab%20Resources/CodeLab%20-%20Part%202.zip)

## Add an ImageView into your list item

Images are a quick way for users understanding a context. e.g. photo of your friend instead of name.

1. In `list_item_tempat.xml`, add an ImageView at the left side of the existing Name and Address `TextView`
2. Set a fixed height on the ImageView, 40dp x 40dp. With 16dp space from the `TextView`
3. Set the ImageView to display the `@drawable/tempat`

## Reacting to user clicking

1. Implement `OnItemClickListener` and set it on your `ListView`
2. In the `onItemClicked()` callback, do a simple Toast for now.

## Getting data from the Internet

1. Add the Internet permission in your `AndroidManifest.xml`
2. Create or subclass an `AsyncTask`
3. Inside `doInBackground()` method, use `HttpURLConnection` to fetch JSON data on Cuti-Cuti Melaka. Returns a list of Tempat
   - Url : https://github.com/andhie/Cuti-Cuti-Melaka/raw/master/data/data.json
4. Read the `InputStream` and build a `String` using `StringBuilder` class
5. Parse the JSON string using `JSONArray` and `JSONObject`
6. `onPostExecute(List<Tempat>)`, add the list to your adapter

```java
new AsyncTask<Void, Void, List<Tempat>>() {
    @Override
    protected List<Tempat> doInBackground(Void... params) {
        return null; // todo return our List<Tempat>
    }

    @Override
    protected void onPostExecute(List<Tempat> tempatList) {
        // todo
    }
}.execute();
```

## Tempat Detail screen

When users click on a Tempat list item, we want to start a new screen that displays more info about the specific Tempat

1. Create a new 'Empty Activity', call it `TempatDetailActivity`
2. Change your `MainActivity`'s `onItemClicked` to launch the new `TempatDetailActivity` screen
3. Display the `@drawable/famosa` at the top. Set its width `match_parent`, height: `wrap_content`. Adjust `android:scaleType` accordingly.
4. Display the Tempat Name, Address, Description and Telephone number.
5. The telephone number should be displayed with the `@drawable/ic_call`
6. When users click on the telephone number, launch the Telephony app on the device.
  - Hint : Use `Intent.ACTION_DIAL`

# ADVANCED

## ActionMode

`ActionMode` is the recommended method to display extra options when user perform long click.

1. Try to implement `ActionMode` with `ActionMode.Callback`
2. Start ActionMode when user long clicks on a Tempat item in your `ListView`.
3. Offer a Share option (share info e.g. Name, Address of this Tempat)
  - Use `Intent.ACTION_SEND` or simply use ShareCompat.IntentBuilder
