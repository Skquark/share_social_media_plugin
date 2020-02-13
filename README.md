
[![N|Social media](https://i.ibb.co/QYMBDZ5/share.png)](https://ibb.co/kqXnmpd)

Share social media plugin

## Getting Started

This project is a starting point for a Flutter
[plug-in package](https://flutter.dev/developing-packages/),
a specialized package that includes platform-specific implementation code for
Android and/or iOS.

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.


Share text in your social media.

  - Line (Android / iOS)
  - Twitter (Android / iOS)
  - Instagram (coming)

### Example

Share in Line.

```dart
 await ShareSocialMediaPlugin.shareLine("My share text");
```

Share in Twitter
```dart
//Set keys
final twitterLogin = new ShareSocialMediaPlugin(
      consumerKey: "consumerKey",
      consumerSecret: 'consumerSecret');

          onPressed: () async{
                      if (Platform.isAndroid) {
                        twitterLogin.shareTwitter("ありがとう");
                      } else if (Platform.isIOS) {
                        var sessionTwitter = await twitterLogin.currentSessionIOS();
                        var tweet = await twitterLogin.shareTwitteriOS(sessionTwitter["outhToken"], sessionTwitter["oauthTokenSecret"],
                            "ありがとう", twitterLogin.consumerKey, twitterLogin.consumerSecret);
                        print(tweet.body.toString());
                      }
                    },
```
**Note For iOS Twitter
In plist
add:
```
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>TwitterLoginSampleOAuth</string>
			</array>
		</dict>
	</array>

```
Add in your Delegate

ios/Runner/AppDelegate.swift

```swift
 import OAuthSwift

 @UIApplicationMain
 @objc class AppDelegate: FlutterAppDelegate {
   override func application(
     _ application: UIApplication,
     didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
   ) -> Bool {
     GeneratedPluginRegistrant.register(with: self)
     return super.application(application, didFinishLaunchingWithOptions: launchOptions)
   }
     //Add this
     override func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
        if (url.host == "oauth-callback") {
           OAuthSwift.handle(url: url)
         }else{
           OAuthSwift.handle(url: url)
         }
         return true
     }
 }

```


!IMPORTANT

In your developer.twitter.com app , you need add the next callback

-TwitterLoginSampleOAuth://

-twittersdk://


### Instagram- Share stories
(Only android )

Read some image from flutter assets
```dart
 RaisedButton(
              onPressed: () async {
                  await ShareSocialMediaPlugin.shareInstagram("hello","assets/nofumar.jpg");
              },
              child: Text('Share in Instagram', style: TextStyle(fontSize: 20)),
            )

```

Public image from album phone
```dart
 RaisedButton(
              onPressed: () async {
                 await ShareSocialMediaPlugin.shareInstagramAlbum();
              },
              child: Text('Share in Instagram from album', style: TextStyle(fontSize: 20)),
            )

```

(For any case add this code in your AndroidManifest.xml)

android/app/src/main/AndroidManifest.xml

```xml
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

In some days for iOS! wait!
Thank you!!




Thank you for your repo
https://github.com/bodnarrr/flutter_twitter_login/blob/master/android/src/main/java/com/bodnarrr/fluttertwitterlogin/fluttertwitterlogin/TwitterLoginPlugin.java