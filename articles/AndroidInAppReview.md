###### IMPROVE THE ANDROID USER EXPERIENCE OF YOUR APP TODAY
## In-App Reviews have come to Android for Xamarin developers!
### You can now launch in-app reviews in Android using Xamarin.

Since the v1.8 release of Android's Play Core package in August 2020, Android users have been able to provide in-app reviews on Android for apps that implemented it. However, there were no binding libraries created for this, and so Xamarin developers were not able to implement this feature in Xamarin apps. But thanks to the recent update to this PlayCore nuget package, Xamarin developers are able to access implement it with ease.

In-app reviews greatly improve the User Experience as users dislike being taken outside the app. Apple had provided this feature since iOS 10.3 released in March 2017, so it was highly anticipated on Android.

{}
Native In-App Reviews are available on Android 

### Implementation

For Xamarin.Forms developers, there's two parts to implement this:

#### Core Project

The core code is pretty straight-forward. We first create an `IInAppReview` Interface through which we will communicate with the Renderer. Just replace NAMESPACE with your actual namespace:
```
namespace NAMESPACE
{
    public interface IInAppReview
    {
        void LaunchReview();
    }
}
```
You can either hook up the `Clicked` action of a Button control to launch the In-App Review, or use a Command to bind the click action and launch this code in your ViewModel using this:
```
var review = DependencyService.Get<NAMESPACE.IInAppReview>();
review.LaunchReview();
```

#### Android Project:
For the Android part, add the PlayCore Nuget package to your Android project, and then create the InAppReviewRenderer in your Droid project:
```
```

#### Testing
Testing in-app reviews is tricky on Android, just as it is on iOS. There are many limitations to being able to test your app as you can see here. Regardless of what you try, you won't be able to see the In-App review UI when distributed manually. You have to download the app from the Play Store, in order to see the UI. So, the easiest way to test this is by using Android's "Internal App Sharing"


---

Back story
Some of you might wonder how  I know about this, so I wanted to share the story to hopefully encourage you. I have subscribed to the Android subreddit through which I learn about the latest features. When I heard about the in-app reviews on Android, I was curious to implement it in my app too, but then I researched and learnt that Microsoft's Xamarin team would not create a support library for this package like they usually do. But luckily I found Patrick Getzman's library but it only implemented PlayCore v1.7.2. Since v1.8 is needed for in-app reviews, so I created an issue. 
22 days later, I had a deadline creeping, so I decided to procrastinate and find anything to do instead, so I decided to update that bindings library to v1.8. With many mouse scrolls and key taps, I followed this video by Jonathan Dick (LINK) and got the .AAR file for v1.8 from Android. Then, I was able to use the Java Android documentation along with the example already in Pat's repository to figure out the renderer too. After successfully figuring this article out, I decided to write this article to share my excitement.
