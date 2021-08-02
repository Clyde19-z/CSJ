# MoPub Custom Event Adapter for CSJ Ad Network

> Please set [MoPub](https://developers.mopub.com/publishers/ios/integrate/) in your app first.

* Required Steps for integration
  * [Setup Pangle platform](#setup-pangle)
  * [Add Pangle to MoPub's mediation](#add-pangle)
    * [Adapters for different ad formats](#adapter-file)
  * [Initialize Pangle SDK and adapters](#import-pangle)
    * [Pangle SDK's integration and initialize](#import-sdk)
    * [Embed Pangle adapters](#import-adapter)

<a name="setup-pangle"></a>
## Setup Pangle Platform
### Create a Pangle account

- Please create a [Pangle account](https://www.pangleglobal.com) if you do no have one.


### Create an application and placements in Pangle

- Click `Apps` -> `+ Add App` to create a app for mediation.
<br>
<img src="./pics/create-app-home.png" alt="drawing" width="400"/>
<br>
<img src="./pics/create-app.png" alt="drawing" width="300"/>

<a name="app-id"></a>
- You will get an app with its `app ID`.
<br>
<img src="./pics/app-id.png" alt="drawing" width="400"/>



### Create Ad Placement
- Click `Ad Placements` -> `+ Add Ad Placement` to create the placement for mediation.
<br>
<img src="./pics/create-placement.png" alt="drawing" width="400"/>

- Select the ad's type for your app and finish the create.
<br>
<img src="./pics/ad-type.png" alt="drawing" width="400"/>

<a name="placementID"></a>
- You will get a placement with its `placement ID`.
<br>
<img src="./pics/placement-id.png" alt="drawing" width="400"/>


<a name="add-pangle"></a>
## Add Pangle to MoPub's mediation

### Create Order 
- Click `Order` -> `Create Order` to create a new order. If you already have an existing order, please move to the next step.

### Create Line Item

- Click `New Line Item` to create a line item.
<br>
<img src="./pics/add-mediation.png" alt="drawing" width="400"/>


- Select `Network Line Item` to the field `Type & Priority` 
<br>
<img src="./pics/ad-format.png" alt="drawing" width="400"/>

- Select `Custom SDK Network` to the field `Network`


- Add adapter's class name to Class Name.
    - **Class Name**: the adapter class's name , for example,`BUDAdmob_RewardCustomEventAdapter`

- Add `{"app_id":"your app id", "ad_placement_id":"your placement id"}` to Parameter.
    - **Parameter**: Add {"app_id":"[your app id](#app-id)", "ad_placement_id":"[your placement id](#placementID)"} to Parameter , for example,`{"app_id":"5000546", "ad_placement_id":"946411987"}`
<br>
<img src="./pics/mediation-param.png" alt="drawing" width="400"/>

  - **Please make sure to use JSON to set Parameter. Or you need to customize adapter yourself.**

<a name="adapter-file"></a>
### Class name for different ad formats
- Reward Video Ads:`CSJRewardedVideoCustomEvent`
- Interstitial(Fullscreen Video) Ads:`CSJInterstitialCustomEvent`
- Banner Ads:`CSJBannerCustomEvent`
- Native Ads:`CSJNativeCustomEvent`


- Embed your MoPub Ad Placement for this line item.
<br>
<img src="./pics/add-custom-event.png" alt="drawing" width="400"/>

<a name="import-pangle"></a>
## Initialize CSJ SDK and Adapter

<a name="import-sdk"></a>
### Import and Init CSJ SDK
Add the information as follows in Podfile, and using `pod install` to intergrate.
```
pod 'Ads-Global'
```

Initialize Pangle with the APP ID as the argument. Unless there is a particular reason, stipulate as

**UIApplicationDelegate application(_:didFinishLaunchingWithOptions:)**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

    BUAdSDKManager.setAppID("your_app_id")

    return true
}
```

Please refer to [Integrate Pangle SDK](https://www.pangleglobal.com/help/doc/6034ac60511c57004360ff72)
and [Initialize Pangle SDK](https://www.pangleglobal.com/help/doc/6034ac73511c57004360ff76) for manual integration and more information.

<a name="import-adapter"></a>
### Embed Pangle Adapters
- Click `SDK Integration` -> `SDK download`, you can download adapters for different ad formats from your Pangle platform.
<br>
<img src="./pics/mediation.png" alt="drawing" width="400"/>
<br>
<img src="./pics/adapter-download.png" alt="drawing" width="400"/>

Please unzip the file and add adapter files from iOS folder into your application project. They can be used with no code changes. Also you can customize it for your use case.
* You need to add `BUDAdmob_NativeFeedAd.h` and `BUDAdmob_NativeFeedAd.m`  into your project to support native ad's adapter [mapping](https://developers.google.com/admob/ios/native/native-custom-events#map_native_ads).


<img src="./pics/adapter-files.png" alt="drawing" width="400"/>

<a name="adapter-swift"></a>
## About Swift
- If your project is based on Swift, please add adapter's header file into your bridge-header file.
<br>
<img src="./pics/bridge-header.png" alt="drawing" width="400"/>

<a name="adapter-demo"></a>
## Demo
- You can find simple use cases from [Demo](https://github.com/bytedance/Bytedance-UnionAD/tree/master/Demo).

