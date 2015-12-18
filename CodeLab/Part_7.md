# Cuti-Cuti Melaka - Part 7

## Background

In this session, we will be adding some animation to our app. We will be animating our list item's `Tempat` image to into the new position inside `TempatDetailActivity`

> Meaningful transitions

>Motion design can effectively guide the user’s attention in ways that both inform and delight. Use motion to smoothly transport users between navigational contexts, explain changes in the arrangement of elements on a screen, and reinforce element hierarchy.

> Source : https://www.google.com/design/spec/animation/meaningful-transitions.html

## Creating transitions

You may refer to the Sub-Section [Start an activity using transitions](https://developer.android.com/training/material/animations.html#Transitions)

1. In your `list_item_tempat.xml` give an `@+id` to your `ImageView`
2. In your `activity_tempat_detail.xml`'s `ImageView` where it displays the hero image of a Tempat, add a new attribute `android:transitionName="hero"`
3. Modify your start detail activity `Intent` to pass a `Bundle` related to our information
  - Note: `Activity` transition only works for Lollipop onwards. This API appears in API21+
  - For compatibility purposes, we will make use of `ActivityCompat` and `ActivityOptionsCompat` from the v4 Android Support Library
    - If you see any "\*Compat" such as `NotificationCompat` it means that for non-supported Android versions, there will be no-operation
4. Before `startActivity`, create our Animation bundle using `ActivityOptionsCompat#makeSceneTransitionAnimation(Activity activity, View sharedElement, String sharedElementName)`.
  - Our sharedElement is our ImageView, find and pass in that
  - Our sharedElementName is the `android:transitionName="hero"` that was declared in the Detail Activity
  - This would make the system to understand that:
    1. Our starting element is list item's `ImageView`
    2. It is suppose to animate into an end result that has the matching sharedElementName  
5. Use `ActivityCompat#startActivity(Activity activity, Intent intent, Bundle options)` to pass in our create Animation bundle and start our `TempatDetailActivity`

## Display simple Animations for older devices

Since Activity Transitions are only available in API 21+, we could also enhance our screen animation that are available on older Android versions. We will be doing a Scale Up Animation when starting our Detail Activity

1. To figure out what Android version our app is running on user device, we can use `Build.VERSION.SDK_INT` which would return the API level e.g. 23 for Android Marshmallow
  - In general
  ```java
  if (Build.VERSION.SDK_INT < Build.VERSION_CODES.LOLLIPOP) {
        // we are not on Lollipop, use older API
  } else {
        // we are running at least Lollipop, can use new Lollipop API
  }
  ```
2. For Android versions runnning lesser than Lollipop, use the `ActivityOptionsCompat#makeScaleUpAnimation(View source, int startX, int startY, int startWidth, int startHeight)` to create your Animation Bundle
3. Continue using `ActivityCompat#startActivity(Activity activity, Intent intent, Bundle options)` and pass our Scale Up Animation bundle.
