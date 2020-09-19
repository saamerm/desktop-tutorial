###### IMPROVE THE ANDROID USER EXPERIENCE OF YOUR APP TODAY
## In-App Reviews have come to Android for Xamarin developers!
### You can now launch in-app reviews in Android using Xamarin.

Since the v1.8 release of Android's Play Core package in August 2020, Android users have been able to provide in-app reviews on Android for apps that implemented it. However, there were no binding libraries created for this, and so Xamarin developers were not able to implement this feature in Xamarin apps. But thanks to the recent update to this PlayCore nuget package, Xamarin developers are able to access implement it with ease.

In-app reviews greatly improve the User Experience as users dislike being taken outside the app. Apple had provided this feature since iOS 10.3 released in March 2017, so it was highly anticipated on Android.

<img width="705" alt="Screenshots showing In-App Reviews on a Xamarin Android app" src="https://user-images.githubusercontent.com/8262287/93619419-8802e580-f9a6-11ea-9c80-920f8a3fb196.png">

### Implementation

For Xamarin.Forms developers, there's two parts to implement this:

#### Core Project

The core code is pretty straight-forward to implement. We first create an `IInAppReview.cs` Interface through which we will communicate with the Renderer. Just replace NAMESPACE with your actual namespace:
```
namespace NAMESPACE
{
    public interface IInAppReview
    {
        void LaunchReview();
    }
}
```
Then, you can either hook up the `Clicked` action of a Button control to launch the In-App Review, or use a Command to bind the click action and launch this code in your ViewModel using this:
```
var review = DependencyService.Get<NAMESPACE.IInAppReview>();
review.LaunchReview();
```

#### Android Project:
For the Android part, add the [PlayCore Nuget package](https://www.nuget.org/packages/PlayCore/) to your Android project, and then add the Custom Renderer for the IInAppReview interface, naming it as [`InAppReviewRenderer.cs`](https://gist.github.com/saamerm/bc3f7bd9e96bd4b027ddfaec3a0876a8) in your Droid project.

#### Testing
Testing in-app reviews is tricky on Android, just as it is on iOS. There are many limitations to being able to test your app as you can [see here](https://developer.android.com/guide/playcore/in-app-review/test). Regardless of what you try, you won't be able to see the In-App review UI when built and distributed manually. You have to download the app from the Play Store, in order to see the UI. So, the easiest way to test this is by using Android's "Internal App Sharing"


---

#### Back story
Some of you might wonder how  I figure this out, so I wanted to share the story to hopefully encourage you. I have subscribed to the [Android subreddit](https://www.reddit.com/r/androiddev/) through which I learn about the latest features. When I heard about the in-app reviews on Android, I was curious to implement it in my app too, but then I researched and learnt that Microsoft's Xamarin team would [not create a support package for this Android library](https://github.com/xamarin/GooglePlayServicesComponents/issues/221) like they usually do. But luckily I found [Patrick Getzman](https://github.com/PatGet)'s nuget but it only implemented PlayCore v1.7.2. Since v1.8 is needed for in-app reviews, so I [created an issue](https://github.com/PatGet/XamarinPlayCoreUpdater/issues/2). 

22 days later, I had a deadline creeping, so I decided to procrastinate and find anything to do instead, so I decided to update that bindings library to v1.8. With many mouse scrolls and key taps, I followed [this video](https://www.youtube.com/watch?v=NyqxScrnJKw) by Jonathan Dick (LINK) and got the .AAR file for v1.8 [from Android](https://developer.android.com/guide/playcore#native). Then, I was able to use the [Official Android documentation](https://developer.android.com/guide/playcore/in-app-review/kotlin-java#java), the example already in [Pat's repository](https://github.com/PatGet/XamarinPlayCoreUpdater), along with lots of trial and error to figure out the renderer too. I will also be presenting this in October's [Rochester Xamarin meetup](https://twitter.com/rocxamarin). If you use this in your apps, please share screenshots with [me](https://twitter.com/rocxamarin), or you can just say Hi!
