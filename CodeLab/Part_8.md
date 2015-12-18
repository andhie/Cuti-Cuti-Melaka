# Cuti-Cuti Melaka - Part 8

Start Part 8 by download resources required for this section

  - Download [Part 8 of CodeLab Resource](https://github.com/andhie/Cuti-Cuti Melaka/raw/master/CodeLab%20Resources/CodeLab%20-%20Part%208.zip)

## Background

We will be adding a watch a feature for users to watch a intro video about Cuti-Cuti Melaka.

## About Activity.

1. In the `activity_about.xml`, add a Button before the About Us TextView with `@drawable/pin` and the text "Watch Video".
2. Clicking on this Video should launch a new `WatchVideoActivity.java`

## WatchVideoActivity

1. Create a new `Activity`, named `WatchVideoActivity`.
2. In the XML layout, add a `VideoView`, set it to `match_parent` for both layout width and height. Give it an `@+id`
3. Find the `VideoView` in your Java code
4. Find out how to load a video from your local resource directory (Hint: search on StackOverFlow)
5. Don't forget to `setMediaController` on the `VideoView` in order to get the "Play" and "Stop" button
6. The video should also start playing immediately
