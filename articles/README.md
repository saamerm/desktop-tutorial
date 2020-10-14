###### IMPROVE THE ANDROID USER EXPERIENCE OF YOUR APP TODAY
## In-App Reviews have come to Android for Xamarin developers!
### You can now launch in-app reviews in Android using Xamarin.

Since the v1.8 release of Android's Play Core library in August 2020, Android users have been able to provide in-app reviews on Android. However, there was no bindings library created for this version of Play Core, and so Xamarin developers were not able to implement this feature in Xamarin apps. But thanks to the recent update to [this PlayCore library](https://github.com/PatGet/XamarinPlayCoreUpdater), Xamarin developers are able to implement it successfully.

In-App Reviews greatly improve the User Experience as users dislike being taken outside their app. Apple had provided this feature since iOS 10.3 released in March 2017, so it was highly anticipated on Android.

<img width="705" alt="Screenshots showing In-App Reviews on a Xamarin Android app" src="https://user-images.githubusercontent.com/8262287/93619419-8802e580-f9a6-11ea-9c80-920f8a3fb196.png">

### Implementation

Since [James Montemagno](https://twitter.com/JamesMontemagno) already has a popular [Store Review Plugin](https://www.nuget.org/packages/Plugin.StoreReview/), we partnered with him to make the feature more accessible through his Nuget. So implementing this in your app is now a piece of cake! 

##### Step 1 - Add the nuget
For Xamarin Native or Xamarin.Forms developers, just add v3 of the "Plugin StoreReview" nuget ([instructions](https://docs.microsoft.com/en-us/visualstudio/mac/nuget-walkthrough)) to your Core, Droid and iOS projects, and this also adds the Play Core bindings library.

##### Step 2 - Call `RequestReview()`
Then, you can either hook up the `Clicked` action of a Button control to launch the In-App Review, or use a Command to bind the click action and launch this code in your ViewModel using this:
```
await Plugin.StoreReview.CrossStoreReview.Current.RequestReview(false);
```

##### Step 3 - Add the proguard
If you use the plugin with Link all, Release Mode and ProGuard/r8 enabled, you have to do add the following in the [proguard file](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/release-prep/proguard) in your android project and add the following: 
```
-keep class com.google.android.play.core.common.PlayCoreDialogWrapperActivity
-keep class com.google.android.play.core.review.** { *; }
-keep class com.google.android.play.core.tasks.** { *; }
```

Alternatively, you can just add the latest [PlayCore Nuget package](https://www.nuget.org/packages/PlayCore/) directly to your Android project, and as you can see in [this PR](https://github.com/PatGet/XamarinPlayCoreUpdater/pull/5), create a Custom Renderer and then add this [`InAppReviewService.cs`](https://gist.github.com/saamerm/bc3f7bd9e96bd4b027ddfaec3a0876a8) to your Droid project.

#### Testing
Testing in-app reviews is tricky on Android, just as it is on iOS. There are many limitations to being able to test your app as you can [see here](https://developer.android.com/guide/playcore/in-app-review/test). Regardless of what you try, you won't be able to see the In-App review UI when built and distributed manually. You have to download the app from the Play Store, in order to see the UI. So, the easiest way to test this is by using Android's "Internal App Sharing". 

---

#### Back story
Some of you might wonder how  I figured this out, so I wanted to share the story to encourage you to contribute as well. I subscribed to the [Android subreddit](https://www.reddit.com/r/androiddev/) through which I learn about the latest features. When I heard about the in-app reviews on Android, I was curious to implement it in my app too, but then I researched and learnt that Microsoft's Xamarin team would [not create a support package for this Android library](https://github.com/xamarin/GooglePlayServicesComponents/issues/221) like they usually do. Luckily I found [Patrick Getzman](https://github.com/PatGet)'s nuge,t but it only implemented PlayCore v1.7.2. Since v1.8 is needed for in-app reviews, so I [created an issue](https://github.com/PatGet/XamarinPlayCoreUpdater/issues/2). 

22 days later, I had a deadline creeping, so I decided to procrastinate and find anything to do instead, and that's when I decided to update that bindings library to v1.8. With many mouse scrolls and key taps, I followed [this video](https://www.youtube.com/watch?v=NyqxScrnJKw) by Jonathan Dick and got the .AAR file for v1.8 [from Android](https://developer.android.com/guide/playcore#native). Then, I was able to use the [Official Android documentation](https://developer.android.com/guide/playcore/in-app-review/kotlin-java#java), the example in [Pat's repository](https://github.com/PatGet/XamarinPlayCoreUpdater), and lots of trial and error to figure out the native service too. If you use this in your apps, please share screenshots with [me](https://twitter.com/saamerm), or you can just say Hi!
