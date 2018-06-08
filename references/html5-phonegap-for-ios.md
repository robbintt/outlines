# HTML5 

## Use PhoneGap to build a html5 app to iOS

I read somewhere that phonegap CLI is easier once you downaload the ios and android SDKs.

### Issues (All heresay at this point)

These issues are mostly around game dev focusing on 60fps games.

There is less criticism for business apps.

- a lot of intermittent problems (sound issues, android issues)
- issues with having a high number of elements
- issues on phones older than iphone 6 and similar android generations
- may not use canvas and webgl due to the type of iphone browser emulation?
    - 


### Alternatives for game dev


1. Get an apple developer account - individual is faster
	1. [enroll](https://developer.apple.com/programs/enroll/)
		- you have to pay $99 + tax (no tax if you have a ADUNS, TIN)
		- individual can do apple ID
		- company can use ADUNS number to get company apple id
		- other requirements listed at the link (above)
1. Get an apple iOS signing certificate
	1. lots to this, follow [phonegap instructions](http://docs.phonegap.com/phonegap-build/signing/ios/)
1. Build the app in phonegap
	- attach the github link, it will build
	- i have no idea what the app needs to build properly... lol
1. Download the `.ipa` file!
	- iPhone apps are `.ipa` files, cool.
1. Install `Apple Configurator 2` by Apple (in the app store)
	- This can be used to configure apple devices
	- Drag the `.ipa` file onto `Apple Configurator 2`
1. Open the app by pressing the new icon on your phone


### Future - TestFlight

It would be nice to distribute beta apps to testers via TestFlight

Resource: https://medium.com/@dmathewwws/steps-to-put-your-app-on-testflight-and-then-the-ios-app-store-10a7996411b1


# How to set up a HTML5 project to work on Phonegap/iOS

Ionic has some sort of [descriptive (html-like) language for native-like components](https://ionicframework.com/docs/api/components/list/List/). Ionic also has released `capacitor` which is similar to `cordova`. The `phonegap` project is also based on `cordova`.

1. Install `phonegap` for macos.
	- also checkout `phonegap-cli`
1. Open `phonegap` and make a `new project`
1. (build your app in this project template, using phaser.js?)




# Guidelines for what Apple will accept as a mobile app

Found [here](https://www.joshmorony.com/the-step-by-step-guide-to-publishing-a-html5-mobile-application-on-app-stores/)

> If you’re building an application to be distributed through the Apple and Google Play app stores, you need to play by their rules. Make sure you comply with the Apple App Store Review Guidelines and the Google Play Developer Program Policies. This is where the benefit of distributing your application as a Progressive Web Application comes in – using the open web means we don’t need to jump through somebody else’s hoops.

> Apple especially can be a bit fickle with their application of the guidelines, but if you break any of them (sometimes even if you don’t) your application may be rejected and you will have to fix the problem and resubmit. Here are a few gotchas to watch out for that might see your application be rejected:

> Your app is more like a web page than a mobile application

> You don’t handle online/offline states

> Your app is slow or unresponsive

> Your application doesn’t make use of native features (i.e. there isn’t really a reason for it to be > distributed as a native app instead of a website)


