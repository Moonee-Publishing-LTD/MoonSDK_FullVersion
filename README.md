&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![LOGO](images/logo.png) 


# Monetization Guide
Welcome, developers, to the full version of the Moon SDK! 🌕

Exciting news awaits as we transition to the Moonee SDK. If you were using the Moonlight SDK previously, kindly remove it and make the switch to this upgraded version.

In this journey, we're implementing MAX as the central mediator for all monetization partners, streamlining the process while also empowering you to leverage your own monetization products.

Let's embark on this enhanced development experience together! 🚀



#
#### Current Version: 1.4.1(Released: 23/12/2024)

In this version, we've made the following updates:

- iOS CMP update
- Collecting additional data for analytics: produce-consume data in level events
- Added listeners events for high revenue ads
- New event - 'segmentation' that has a new token - on function usege is needed, automatically collected by the SDK.

Note: The inspector is asking you for a session toke, please leave it empty for now.

# Table of Contents
<details>
  <summary></summary>

1. [System Requirements](#system-requirements)
2. [Downloading MOON SDK](#downloading-moon-sdk)
3. [Setting Up Moon SDK](#setting-up-moon-sdk)
4. [Initialization](#initialization)
5. [Displaying Ads](#displaying-ads)  
   A. [Rewarded Video Ads](#rewarded-video-ads-api)  
   B. [Interstitial Ads](#interstitial-ads-api)  
   C. [Banner Ads](#banner-ads-api)
6. [Events](#events)  
  A. [Progression events](#progression-events)  
  B. [In-app purchase (IAP) Events](#in-app-purchase-iap-events)  
  C. [Segmentation Events](#segmentation-events)  
  D. [Custom Events](#custom-events)  
7. [Firebase Configuration](#firebase-configuration)
8. [CMP - GDPR Consent](#cmp---gdpr-consent)
9. [In-Game Fonts](#in-game-fonts)
10. [Rate Us View](#rate-us-view)
11. [Platform Configuration - If Not Yet Added](#platform-configuration---if-not-yet-added)  
    A. [Facebook](#facebook)  
    B. [Game Analytics](#game-analytics)
12. [DATA Safety](#data-safety)  
      A. [Android](#android)  
      B. [iOS](#ios)  
      C. [Facebbok Data Checkup](#facebbok-data-checkup)  
13. [Testing](#testing)
14. [Common Issues](#common-issues)

</details>


## System Requirements
<details>
  <summary></summary>
  
  - Unity Editor 2022 LTS version
  - Android:
    - Minimum SDK: Lollipop 5.0 (API 22)
    - Scripting backend: IL2CPP
  - iOS:
    - Target minimum iOS Version: 13.0
    - Scripting backend: IL2CPP
  - Stores:
    - In order for us to have the optimal monetization, we will need you to add our web link in the stores:[https://moonee.io](#https://moonee.io)
    - On Google play it’s under Store Settings -> Website
    - On App Store it’s under Marketing URL in an App Version

      
</details>


## Downloading MOON SDK
<details>
  <summary></summary>

  The current version of the MOON SDK is version 1.4.0.3    
  Slack bot is sending the link if you will type `FULL_SDK` 
  
</details>
  

## Setting Up Moon SDK
<details>
  <summary></summary>

  1. Import MoonSDK.unitypackage into your unity project.
  
  2. Please note, that our SDK uses some iAP features, so iAP package should be installed from the package manager
  
  3. The MoonSDKScene must be the first in the list in the build settings, after initialization it will load the next scene in the list (with index 1).

     ![MoonSDKScene](images/MoonSDKScene.png)
     
  4. Open MoonSDK settings and fill in all app keys for analytics and advertising services, Please ensure you add **all** of them and **copy/paste** them to the correct location in the inspector.
  5. Press Check and Sync Settings button  
     **Note:Make sure to copy/paste the tokens/ad IDs and not type them manually to avoid mistakes.**
    
     ![SyncSettings](images/SyncSettingsNew.png)

     
</details>
 
## Initialization
<details>
  <summary></summary>
Moon SDK is initialized automatically from the Moon SDK scene.
</details>

## Displaying Ads
<details>
  <summary></summary>

MoonSDK does support the following ad formats:

A. [Rewarded Video Ads](#rewarded-video-ads-api)  
B. [Interstitial Ads](#interstitial-ads-api)  
C. [Banner Ads](#banner-ads-api)

To use the advertisement manager add the following namespace: 
      using `Moonee.MoonSDK.Internal.Advertisement;`


### Rewarded video ads API:
<details>
  <summary>Expand</summary>

#### Showing a Rewarded Video:
Use the following method to display a rewarded video in your game:

```csharp

AdvertisementManager.ShowRewardedAd(
    () => 
    {
        // Ad start logic
    },
    () =>
    {
        // Ad finish logic
    },
    () =>
    {
        // Ad fail logic - show pop up that ad is not ready. 
    },
    () =>
    {
        // Reward logic
    },
    "rewardedVideoName" // Add Rewarded Video Name here!
);
```


---

#### Displaying High-Income Ads (Listeners events):
There are two important events in the AdvertisementManager class:

AdvertisementManager.OnHighSegmentationInterstitialReadyEventHandler;
AdvertisementManager.OnMediumSegmentationInterstitialReadyEventHandler;
AdvertisementManager.OnHighSegmentationRewardedVideoReadyEventHandler;
AdvertisementManager.OnMediumSegmentationRewardedVideoReadyEventHandler;

These events are called as soon as the high-income ad is loaded and ready to display, use these events to trigger high-income ads as soon as you can in your game. Note that when AdvertisementManager.OnHighSegmentationInterstitialReadyEventHandler is called, the interstitial ad timer is reset, the ads are ready to be shown immediately.

---

#### Key Notes:
1. **Always include the Rewarded Video Name**: When calling `ShowRewardedAd()`, ensure that you provide the correct video name (e.g., `"RV_more_coins"`). Missing the video name can cause issues with tracking.
2. **Handling interstitial ads**: If you notice that interstitial ads are being shown instead of rewarded videos, this is expected. The SDK might optimize revenue by choosing a more suitable ad format based on various factors.
3. **For High-income ads**, ensure that `OnHighSegmentationRewardedVideoReadyEventHandler` is set up and used to display these ads quickly. Note the method for interstitial high income is differnt than Rewarded Video.


</details>

  ### Interstitial ads API:
<details>
  <summary>Expand</summary>

#### Showing Interstitial ads:
Use the following method to display an interstitial in your game:

```csharp
       float AdvertisementManager.InterstitialTimer {get; private set;}
       double timeLeftForNextAd = AdvertisementManager.InterstitialTimer;

       AdvertisementManager.ShowInterstitial(
        () =>
        {
            //Ad start logic
        },
        () =>
        {
            //Add finish logic
        },
        () =>
        {
            //Ad fail logic - show pop up that ad is not ready. 
        });
```
---


#### Key Notes:
1. For High-income ads, ensure that `AdvertisementManager.OnHighSegmentationInterstitialReadyEventHandler` is set up and used to display these ads quickly.
2. When `AdvertisementManager.OnHighSegmentationInterstitialReadyEventHandler` is called, the interstitial ad timer is reset, and the ads are immediately ready to be shown.

</details>

  ### Banner Ads API:
<details>
  <summary>Expand</summary>

      AdvertisementManager.ShowBanner()
      
      AdvertisementManager.HideBanner();
      
</details>

</details>

## Events
<details>
  <summary></summary>
  
A. [Progression events](#progression-events)  
B. [In-app purchase (IAP) Events](#in-app-purchase-iap-events)  
C. [Segmentation Events](#segmentation-events)  
D. [Custom Events](#custom-events) 


---

### Progression Events

<details>
  <summary></summary>
  
**Level Progression Events:**  
We utilize two key events related to game level progression: `LevelDataStartEvent` and `LevelDataCompleteEvent`. These events are sent to Adjust and Game Analytics.

- `LevelDataStartEvent` is triggered at the beginning of the level.
- `LevelDataCompleteEvent` is triggered at the end of the level and contains all data related to the player's actions during the level.

The `LevelDataStartEvent` includes information about the time spent between levels (engagement time), while the `LevelDataCompleteEvent` contains data on everything that happened during the level.

The image below represents the event flow:  
![levels_order](images/levels_order.png)


#### **`LevelDataStartEvent`**  
This event is sent at the beginning of a level and includes data on the engagement time between levels. The following parameters are included:

1. **`levelNumber`** - Indicates the current level number.  
   - **Example:** If the player is starting level 3, send `3`.

2. **`coinsAmount`** – The player's current **balance** of the main currency.  
   - **Example:** If a player ended the last level with 30 coins and didn't spend any, send `30`. If the player had 30 coins but spent 15 in the store, send `15`.  
   - **Detailed scenario:** If I played level 1, during the level got 10 and lost 5. In the complete screen, I was given 2 more coins. You should send: `10-5+2 = 7`. If the player starts level 1 with 0 coins, send `0`.

3. **`producedCoinsAmount`** – The total number of coins earned during the **previous level** or **between** levels.  
   - **Example:** If the player earned 20 coins for completing a task and 10 coins from a bonus reward, send `30`. If no coins were produced, send `0`.

4. **`consumedCoinsAmount`** – The total number of coins spent during the **previous level** or **between** levels.  
   - **Example:** If the player spent 15 coins on an upgrade and 5 coins on a power-up, send `20`. If no coins were spent, send `0`. 

5. **`purchaseIDs`** – The IDs of in-app purchases made before starting this level, since the last time this event was sent.

Use the following function to send this event:

```csharp
MoonSDK.SendLevelDataStartEvent(levelIndex, coinsAmount,producedCoinsAmount,consumedCoinsAmount, purchaseIDs);
```

---

#### **`LevelDataCompleteEvent`**  
This event is sent at the end of a level and contains the following information:

1. **`levelNumber`** - Indicates the current level number.  
   - **Example:** If the player finishes level 5, send `5`.

2. **`result`** - Represents the outcome of the level.  
   - **Example:** Send `"win"` if the player completes the level successfully, or `"fail"` if they fail to complete it.

3. **`isContinueLevel`** - A boolean indicating whether the player continued the level from where they left off (`true`) or started it from the beginning (`false`).  
   - **Example:** If the player used a revive to continue the level, send `true`. If the level was played from the start, send `false`. For games without such features, this should default to `false`.

4. **`coinsAmount`** – Represents the player's current soft currency balance when the level ends.  
   - **Example:** If the player started with 10 coins, earned 20 coins, and spent 5 coins during the level, send `25` (`10 + 20 - 5`). If the player ends the level with no currency, send `0`.

5. **`producedCoinsAmount`** – The total number of coins earned during the level.  
   - **Example:** If the player earned 10 coins from rewards and 5 coins from bonuses, send `15`. If no coins were earned, send `0`.

6. **`consumedCoinsAmount`** – The total number of coins spent during the level.  
   - **Example:** If the player spent 5 coins on a power-up and 3 coins on an in-game item, send `8`. If no coins were spent, send `0`.

7. **`moves`** – Represents the number of moves made by the player during the level.  
   - **Example:** If the player made 25 moves before completing or failing the level, send `25`. If moves are not tracked in your game, this parameter can be omitted or set to `0`. 

8. **`customParameters`** – A `Dictionary<string, string>` where custom parameters can be tracked.  
   - **Key:** Represents the name of the custom parameter.  
   - **Value:** Represents the value of the parameter.  
   - **Example:** 
     ```json
     {
       "difficulty": "hard",
       "timeOfDay": "evening",
       "powerUpsUsed": "3"
     }
     ``` 
   Use this field to include additional game-specific data, such as the level's difficulty, the time of day the level was played, or any other relevant information. If no custom parameters are needed, send an empty dictionary. 

Use the following function to send this event:

```csharp
MoonSDK.SendLevelDataCompleteEvent(LevelStatus.complete, levelNumber, LevelResult.win, isContinueLevel, coinsAmount, producedCoinsAmount,consumedCoinsAmount, moves, customParamsDictionary);
```

---

#### **In-Game Store**  
For tracking player interactions with the in-game store, use the following functions:

```csharp
MoonSDK.OpenInGameStore(); // Execute when user opens the store
MoonSDK.CloseInGameStore(); // Execute when user closes the store
```

---

#### **Rewarded Video Ads**  
Remember to add every Rewarded Video used in the game. Append `"rewardedVideoName"` to the function as described in the [Rewarded Video Ads API section](#rewarded-video-ads-api).

---

**Important Notes:**
- **A.** Ensure that a token is sent to Adjust for *each event*.
- **B.** Double-check that there are no spaces before or after the token.
- **C.** Always **copy/paste** the tokens to avoid errors.

</details>

--- 


### In-app purchase (IAP) Events:
<details>
  <summary></summary>
  
To accurately monitor in-app purchase (IAP) revenue through Adjust, ensure you've configured the Adjust app token and the IAP revenue event token within the Moon SDK settings.  
Go to receipt Validation Obfuscator , **paste** the google public key of your app and press **“Obfuscate Google Play License Key”**.  
Please ensure that the event is triggered from every available location where the product can be purchased. If users have the option to buy from both the in-game store and a popup, make sure the event is sent in both scenarios.  
If you don't have an in app in the game, send `string.Empty`

In-app purchase (IAP) Event contains the following parameters:
1. `purchaseEventArgs` - 
2. `iAPType` - Refer to the different types of in-app purchaseS:
    A. `product` - A one-time purchase.
    B. `Subscription` - A product that allows users to purchase content for a defined period.   
3. `levelNunmber` -  Specifies the level where the in-app purchase was made.

After each successful purchase you need to send event to adjust:

      MoonSDK.TrackAdjustRevenueEventAsync(args, subsription, "4");

![obfuscation](images/obfuscation.png)

</details>

---

### Segmentation Events
<details>
  <summary></summary>

  These are automatically collected events by the MOON SDK, you don't need to use any function.
  The only thing that you should do is use the event token in the right place in the inspector. 
</details>

---

### Custom Events
<details>
  <summary></summary>
The following is only for advance games, that have a need for custom events:  
With Moon SDK you can send custom events to various analytics services
  
      MoonSDK.TrackCustomEvent("Event name", [Dictionary <string, object> eventProperties = null],
      [string type = null],
      [List < MoonSDK.AnalyticsProvider> analyticsProviders = null])
      
Call this method to track any custom event you want.  
eventName = the name of the event to track.  
Exsample:  
      
      MoonSDK.TrackCustomEvent("Event name", MoonSDK.AnalyticsProvider.Firebase);
  
</details>

---

</details>


## Firebase Configuration
<details>
  <summary></summary>

**We utilize Firebase for two primary purposes:**

1. User Acquisition: To facilitate proper integration within Google platforms, event data needs to be stored in Firebase.
2. A/B Testing via Remote Config: This powerful tool enables remote modification of parameters.

**Workflow:**

1. A designated team member, typically the Product Manager, will initiate a Firebase project for your game (do not create one yourself, as it may lead to improper UA usage).
2. You will receive configuration files (google-services.json for Android and GoogleService-Info.plist for iOS).
3. Integrate these files into your Unity project following the instructions provided below.


  
![UnityFirebase](images/AddingFirebaseToUnity.png)
![AssetesStreaming](images/AssetesStreamings.png)

**Firebase Remote Config** 

Moon SDK by default uses some default remote config values:
1. `int_grace_time`: Interstitials time grace - time grace untill first interstitial.
2. `int_grace_level`: Interstitials level grace - level grace untill first interstitial.
3. `cooldown_between_INTs`: Cooldown Between Interstitials -  timer (in seconds) for spaces between INTs.
4. `cooldown_after_RVs`: Cooldown After Rewarded Videos- time (in seconds) for INT AFTER watching a Rewarded video.( Replace cooldown_between_int ).
5. `show_int_if_fail`: Show Interstitial If Fail 	
`True`: player gets ads after each level, regardless of success status,
`False`:  player gets ads after success levels only.
6. `int_in_stage`: Interstitials In Stage,
`True`: player gets ads during stages
`False`: player gets ads after stages only

**Default values:**
`int_grace_time`: 0 sec
`int_grace_level`" 1
`cooldown_between_INTs`: 20 sec
`cooldown_after_RVs`: 20 sec
`show_int_if_fail`: False
`int_in_stage`: False

Note that `int_sessions_grace`, `cooldown_between_INTs`, `cooldown_after_RVs` are managed automatically by Moon SDK and you don’t need to do anything with that, but the rest values you need to check before showing ads.


        if(currentLevel > RemoteConfigValues.int_grace_level)
        {
            AdvertisementManager.ShowInterstitial();
        }



       if(RemoteConfigValues.Show_int_if_fail == true)
        {
            AdvertisementManager.ShowInterstitial();
        }


       if(RemoteConfigValues.INT_in_stage == true)
        {
            AdvertisementManager.ShowInterstitial();
        }

</details>

## CMP - GDPR Consent
<details>
  <summary></summary>
We utilize a CMP (Consent Management Platform) solution to obtain consent from users.   
Effective CMP implementations can potentially boost the value of users engaging with the game, potentially adding up to 50% of the ad's worth.
  
To use CMP in your project you need to fill in the Adjust Consent Token:  
![consentToken](images/consentToken.png)    

Consent precedes any other aspect of the SDK and the tutorial. We are dedicated to compliance with the highest regulatory standards in Europe, as outlined by the GDPR enforced by the IAB. Therefore, we are unable to implement the best practice of obtaining consent after the tutorial.
The CMP popup appears as follows: 
<details>
 <summary>ConsentPopUp</summary>
  
![welcome](images/welcome.png) 

</details>

Below you will find a code example how to pop up the consent window from your game,you will need to mute sounds and stop any ad timers.   
Create a consent button in settings screen in your game.  

![consentSetting](images/consent_setting.png)    


      private void ConsentsButtonPressed()
    {
        CMP.OpenSettingsScreen();
        CMP.eventHandler += OnConsentsChangesEventListener; // Don't forget to unsubscribe, you can use OnDestroy method for example
        // AdvertisementManager.PauseInterstitialTimer();
        // AudioController.PauseMusic(true);
    }
    private void OnConsentsChangesEventListener(int id, TCData TCData, bool isSuccess)
    {
        //AdvertisementManager.ResumeInterstitialTimer();
        //AudioController.PauseMusic(false);
    }

Check if the user is in the GDPR country

    if(!CheckGDPRCountry.CheckCountryForGDPR())
        {
    //Disable cmp pop-up
        } 

        
</details>  

## In-Game Fonts
<details>
  <summary></summary>  
In terms of in-game fonts, they must be official fonts from Google Fonts or Liberation Sans from Unity. Follow these steps to ensure compliance with font licensing:

1. Use only fonts from the Google Fonts library or Liberation Sans from Unity.
2. After selecting the relevant font, ensure you have the license for the game code as a text file.
3. Rename the license file to the following format: `Fontname_license.txt`.
4. Place both the font file and its license file in the Fonts directory of your project.
5. The most common font licenses are OFL (Open Font License) and Apache License.
6. Copy everything in the StreamingAssets directory to add a new licensed font, which will be automatically added to the build.
7. Fonts from Google Fonts can be used for both Android and iOS games. You can find them at [Google Fonts](https://fonts.google.com/).
8. Unity typically has two built-in fonts:
   * Liberation Sans (free to use)
   * Arial (note: Arial is not free to use)
9. Refer to the following guides for embedding custom fonts in games:
   * Unity - Manual: [Font Assets](https://docs.unity3d.com/Manual/class-Font.html).

By adhering to these guidelines, you ensure that your game uses licensed fonts responsibly and legally.

</details>

## Rate Us View
<details>
  <summary></summary>
  
You can open rate us screen using code example below

     MoonSDK.OpenRateUsScreen();

The SDK rate us logic is just a default one, You can overwrite it with your own UI and logic.
     
</details>

 ## Platform Configuration - If Not Yet Added
 
 <details>
  <summary></summary>
   
A. [Facebook](#facebook)  
B. [Game Analytics](#game-analytics)

### Facebook
 <details>
  <summary></summary>
   
#### 1: Creating a game in the [Facebook UI](https://developers.facebook.com/apps)

#### 2: Create an app

The following manual by Meta explains how to create an app: [Manual](https://developers.facebook.com/docs/development/create-an-app/)

When you need to choose the type of the app, choose "Other" > "Gaming app".

#### 3: Go to Settings > Basic and fill the needed info

#### 4: Create a valid privacy policy and User data deletion

  A. Create Privacy policy on: [this link](https://app-privacy-policy-generator.firebaseapp.com/)  
  B. After creating, download it and open it on Google Docs.  
  C. Under "File" choose "Publish to the web" and it will create you a Privacy Policy link.  
  D. Insert the created link on Both privacy policy and User data deletion sections, and choose the needed Category and Sub-Category (Hyper Casual, Hybrid etc.).
![Basic](images/facebookBasic.png)
#### 5: Choose and add your platform

  A. Android: fill the package name (it’s the bundle), and on iOS fill App’s ID and Bundle ID.  
  B. Other sections or to confirm ownership are not mandatory so don’t worry about it!  
  C. Click “Save Changes”.
  ![Android](images/Android.png)

#### 6: Activate your app

Make sure to set the status on the first row to "Live".
![live app](images/liveAppMeta.png)

#### 7: Add Moonee’s Ad Account ID

For us to be able to test your game, we need to connect it to our Ad Account:  
  a. Go to Settings -> Advanced and fill the needed info:  
  b. Scroll down to the section “Advertising Accounts” and insert Moonee’s Ad Account ID:`267507499172466`.
![account](images/AccountID.png)
#### 8: Verify data

You can download + open the app and check on FB Developer main dashboard if you’re seeing data of last date installs.

#### 9: Share in the Slack channel your FB App ID.

  </details>  

### Game Analytics
 <details>
  <summary></summary>

1. Create a Game analytics account and asset using this [link](https://tool.gameanalytics.com/login?redirect=%252F).
2. If your game is level-based, make sure to have the events:
   - `Start`
   - `Complete`
   - `Fail`
3. Make sure to have the level events naming in the format:
   - `Level0001`
   - `Level0002`
   (Make sure to start from level 0001 and not from 0000)
4. Grant us Admin access to the app on Game Analytics: 
   - Settings -> Users -> Invite users -> for this user erez@moonee.io
  </details>

 </details>

## Testing
<details>
  <summary></summary>

Get check for the following:
  - We get the following events:
    - `levelDataStart`
    - `levelDataComplete` events from the app
    - `consent` event
  - Test the build on a device in addition to the editor. Editor itself is not a sufficient environment.
</details>

## DATA Safety
<details>
  <summary></summary>

### Android
<details>
  <summary></summary>
To complete the Data Safety form required by the Google Store, please adhere to the following steps:

Access the Google Play Console for your application.
Navigate to the "Data safety" section within the console.
Answer the questions as below:  

**Overview:**  
Please read the following instructions carefully to ensure that you are not collecting data beyond the parameters outlined below. If, however, you find that you are inadvertently collecting additional data, please promptly contact us for further assistance. It is essential to adhere strictly to the specified data collection guidelines to maintain compliance and transparency with our policies.  

**Data collection and security:**  
Does your app collect or share any of the required user data types? _Yes_
  - Is all of the user data collected by your app encrypted in transit? _Yes_
  - Which of the following methods of account creation does your app support? _My app does not allow users to create an account_
  - Do you provide a way for users to request that their data is deleted? (Optional) _No_ 

**Data types:**  
Select all of the user data types collected or shared by your app.
- Location: _None_
- Personal info: _None_
- Financial info: _None_
- Health and fitness: _None_
- Messages: _None_
- Photos and videos: _None_
- Audio files: _None_
- Files and docs: _None_
- Calendar: _None_
- Contacts: _None_
- App activity: App interactions (Information about how a user interacts with your app. For example, the number of times they visit a page, or what they tap on.)
- Web browsing: _None_
- App info and performance: Crash logs
- Device or other IDs: Device or other IDs

**Data usage and handling** _Manage in the errow for both types:_

App Activity / App interactions:
  - Is this data collected, shared, or both? _Collected_
  - Is this data processed ephemerally? _Yes, this collected data is processed ephemerally_
  - Is this data required for your app, or can users choose whether it's collected? _Data collection is required_
  - Why is this user data collected? App functionality, Analytics, Advertising or marketing

Device or other IDs:
  - Is this data collected, shared, or both? _Collected_
  - Is this data processed ephemerally? _Yes, this collected data is processed ephemerally_
  - Is this data required for your app, or can users choose whether it's collected? _Data collection is required_
  - Why is this user data collected? _App functionality, Analytics, Advertising or marketing_
    
**Preview:**  
See that all of the above is correct, and press save.
If you can't see the save button, there are 3dots there, that "save" is one othe options in them.

</details>


### iOS
<details>
  <summary></summary>
To complete the Data Safety form required by the App Store, please adhere to the following steps:

Access the App Play Connect for your application.
Navigate to the "App Privacy" section within the console.
Answer the questions as below:  

**Privacy Policy**  
User Privacy Choices URL: Please provide Moonne's URL: https://moonee.io/privacy-policy/

**Data Collection**  
Do you or your third-party partners collect data from this app? _Yes, we collect data from this app_

**Data Types**  
- Contact Info: _None_
- Health & Fitness: _None_
- Financial Info: _None_
- Location: _None_
- Sensitive Info: _None_
- Contacts: _None_
- User Content: _None_
- Browsing History: _None_
- Search History: _None_
- Identifiers: _Device ID_
- Usage Data: _Product Interaction,Advertising Data_
- Diagnostics: _Crash Data, Performance Data_
- Surroundings: _None_
- Body: _None_
- Other Data: _None_


Identifiers/ Device ID:
- Indicate how device IDs collected from this app are being used by you or your third-party partners? _Third-Party Advertising,Developer’s Advertising or Marketing_
- Are the device IDs collected from this app linked to the user’s identity? _No, device IDs collected from this app are not linked to the user’s identity_
- Do you or your third-party partners use device IDs for tracking purposes? _Yes, we use device IDs for tracking purposes_

Usage Data/ Product Interaction:
- Indicate how Product Interaction collected from this app are being used by you or your third-party partners? _Third-Party Advertising, Developer’s Advertising or Marketing, Analytics,Product Personalization, App Functionality_
- Are the Product Interaction data collected from this app linked to the user’s identity? _No, Product Interaction data collected from this app are not linked to the user’s identity_
- Do you or your third-party partners use device IDs for tracking purposes? _Yes, we use device IDs for tracking purposes_

Usage Data/ Advertising Data:
- Indicate how Advertising Data collected from this app are being used by you or your third-party partners? _Third-Party Advertising,Developer’s Advertising or Marketing, Analytics,Product Personalization, App Functionality_
- Are the Advertising Data collected from this app linked to the user’s identity? _No, Advertising Data collected from this app are not linked to the user’s identity_
- Do you or your third-party partners use Advertising Data for tracking purposes? _Yes, we use Advertising Data for tracking purposes_

Diagnostics/ Crash Data:
- Indicate how crash data collected from this app are being used by you or your third-party partners? _Developer’s Advertising or Marketing, Analytics_
- Are the crash data collected from this app linked to the user’s identity? _No, crash data collected from this app are not linked to the user’s identity_
- Do you or your third-party partners use crash data for tracking purposes? _Yes, we use crash data for tracking purposes_

Diagnostics/ Performance Data:
- Indicate how performance data collected from this app are being used by you or your third-party partners? _Third-Party Advertising, Developer’s Advertising or Marketing, Analytics,Product Personalization, App Functionality_
- Are the performance data collected from this app linked to the user’s identity? _No, performance data collected from this app are not linked to the user’s identity_
- Do you or your third-party partners use performance data for tracking purposes? _Yes, we use performance data for tracking purposes_

</details>  

### Facebbok Data checkup 
<details>
  <summary></summary>
  
In case the Facebook UI is asking to craete data check up, use the following:  
Go to [https://developers.facebook.com/]  
Sign in and go to the app, the Data checkup will pop up  
1. Click on your app and press next  
![FB1](images/FB1.png)  
2. Under Do you have data controller choose No, Add data processor  
![FB2](images/FB2.png)  
3. Insert Moonee Publishing LTD as your data processor. From the category choose Advertising and Analytics and measurement. From the list of countries choose Israel and Poland  
![FB3](images/FB3.png)  
![FB4](images/FB4.png)  
4. For Have you provided the personal data of user to public authorities choose No, and for Which of the following processes do you have in place choose Required review of the legality of these requests and press next/  
![FB5](images/FB5.png)  
5. Tick all the boxes and press next.  
![FB6](images/FB6.png)  
6. Insert the Google Play store link and fill in the answers to the rest of the questions as following:  
![FB7](images/FB7.png)  
7. Same for iOS, insert the App Store link and fill in the answesr to the rest of the questions as following:  
![FB8](images/FB8.png)  
8. Tick the box and finish the checkup  
![FB9](images/FB9.png)  

</details>
</details>

## Common Issues
<details>
  <summary></summary>  
Commen issues can be found here as well as in the "issue" section.  
Please add your comments there as well, to allow other to gain from it.  

**Importnat comments:**
1. Please remove External Dependency manager folder from the project and import the latest one.
2. After adding the keys and tokens, make sure **not** to disable the checkmarks for the basic.
3. Plaese copy/paste the keys without space to avoid mistakes
4. Use both methods of progression events: to Adjust and to Game Analytics. Soon we will be changing it to one method sending to both platforms.
5. When updating the SDK version, pleaese remove MoonSDK folder and after that import the new package.
6. If you don't have an in app in the game, send string.Empty  
7. If IAP event is arriving, but missing the level_name or number (depend on SDK version, reimport the package as shown in the picture below.
![reimportPackage](images/reimportPackage.png)
8. The SDK rate us logic is just a default one, You can overwrite it with your own UI and logic.
9. `PurchaseEventArg`s error:You need to install iAP plugin via package manager.
10. `NewtonSoft` error: import `NewtonSoft.Json.dll` library under plugins folder
11. If you see interstitial ads being displayed instead of rewarded videos, this is intentional. In some cases, the SDK will identify a more revenue-optimizing option and utilize it.
   
</details>

# Good Luck! 


