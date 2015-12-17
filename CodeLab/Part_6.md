# Cuti-Cuti Melaka - Part 6

Start Part 6 by download resources required for this section

  - Download [Part 6 of CodeLab Resource](https://github.com/andhie/Cuti-Cuti-Melaka/raw/master/CodeLab%20Resources/CodeLab%20-%20Part%206.zip)
  - Inside the res, we now have a new ic_launcher as our app icon

## Background

We will have an About Activity that describes Melaka history. This screen also provides the ability for Text-To-Speech (TTS)

## Main Activity

We will be accessing `AboutActivity` via a Menu options in `MainActivity` ActionBar

1. Create a menu XML in `res/menu_main.xml`
2. Create a menu item in the XML. it should `never` be shown in the ActionBar. It has a title `About Us`. Give it an ID `@+id/action_about_us`
  - Since we are using AppCompat, we need to use `app:showAsAction` instead of `android:showAsAction`
3. In your `MainActivity`, inflate `R.menu.menu_main` in the `Activity`'s `onCreateOptionsMenu`
4. Also override `onOptionsItemSelected` to handle `R.id.action_about_us` which should launch our new  `AboutActivity`

## About Activity

We will trigger a TTS via a menu options

1. Create an new `Activity`, named `AboutActivity`
2. In this activity, it only contains a single `TextView`
3. Set this `TextView` to display the string `@string/about_us`
4. Create a menu, `res/menu_about_us`
5. Create a menu item, set it to `always` show in the ActionBar, with title `Speak`, an ID of `@+id/action_speak` and an icon of `@drawable/ic_tts`
6. Inflate the menu and handle speak item selected by speaking the content of About Us
7. Implement any callback as appropriate to support TTS.
