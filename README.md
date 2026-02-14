# AlienAds SDK v2.0.0

[![](https://jitpack.io/v/yourusername/admobSdk-Sun-38.svg)](https://jitpack.io/#yourusername/admobSdk-Sun-38)
[![API](https://img.shields.io/badge/API-23%2B-brightgreen.svg?style=flat)](https://android-arsenal.com/api?level=23)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

Advanced AdMob SDK wrapper with mediation support for Android applications. Simplify your ad integration with powerful features and easy-to-use APIs.

## 🚀 Features

- ✅ **AdMob Integration** - Full support for Google AdMob (SDK 24.9.0)
- ✅ **Multiple Ad Formats** - Banner, Interstitial, Rewarded, Native, and Open Ads
- ✅ **Mediation Support** - Built-in mediation adapter support
- ✅ **UMP Consent** - User Messaging Platform (UMP) SDK 4.0.0 integrated
- ✅ **Easy Implementation** - Simple and intuitive API
- ✅ **Lifecycle Aware** - Automatic lifecycle management
- ✅ **Modern Android** - Supports Android 6.0+ (API 23+)
- ✅ **Latest SDK** - Built with Android SDK 36 (Android 16)

## 📋 Requirements

- **Minimum SDK:** API 23 (Android 6.0)
- **Target SDK:** API 36 (Android 16)
- **Compile SDK:** API 36
- **Java Version:** 17+

## 📦 Installation

### Step 1: Add JitPack repository

Add it in your root `build.gradle` at the end of repositories:

```gradle
allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

Or if you're using `settings.gradle` (Gradle 7.0+):

```gradle
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

### Step 2: Add the dependency

Add this to your app's `build.gradle`:

```gradle
dependencies {
    implementation 'com.github.yourusername:admobSdk-Sun-38:2.0.0'
}
```

### Step 3: Add AdMob App ID

Add your AdMob App ID to `AndroidManifest.xml`:

```xml
<manifest>
    <application>
        <meta-data
            android:name="com.google.android.gms.ads.APPLICATION_ID"
            android:value="ca-app-pub-xxxxxxxxxxxxxxxx~yyyyyyyyyy"/>
    </application>
</manifest>
```

## 🎯 Quick Start

### Initialize SDK

In your `Application` class or main `Activity`:

```java
// Initialize AlienAds SDK
InitializeAlienAds.LoadSDK();

// Initialize with AdMob
AliendroidInitialize.SelectAdsAdmob(this, selectBackupAds, backupInitialize);
```

### Banner Ads

```java
// Load banner ad
AlienBanner.LoadBanner(this, "ca-app-pub-3940256099942544/6300978111");
```

### Interstitial Ads

```java
// Load interstitial ad
AlienInterstitial.LoadInterstitial(this, "ca-app-pub-3940256099942544/1033173712");

// Show interstitial ad
AlienInterstitial.ShowInterstitial(this, new AlienInterstitial.OnInterstitialDismissed() {
    @Override
    public void onInterstitialDismissed() {
        // Ad dismissed, continue your flow
    }
});
```

### Open Ads (App Open Ads)

```java
// Load open ads
AlienOpenAds.LoadOpenAds("ca-app-pub-3940256099942544/3419835294", true);

// Show open ads
AlienOpenAds.AppOpenAdManager.showAdIfAvailable(this, new AlienOpenAds.OnShowAdCompleteListener() {
    @Override
    public void onShowAdComplete() {
        // Ad shown or failed, continue
    }
});
```

### Native Ads

```java
// Load native ad
AlienNative.LoadNative(this, "ca-app-pub-3940256099942544/2247696110", nativeAdView);
```

### Rewarded Ads

```java
// Load rewarded ad
AlienRewarded.LoadRewarded(this, "ca-app-pub-3940256099942544/5224354917");

// Show rewarded ad
AlienRewarded.ShowRewarded(this, new AlienRewarded.OnRewardedAdListener() {
    @Override
    public void onUserEarnedReward(int rewardAmount) {
        // User earned reward
    }
    
    @Override
    public void onRewardedAdClosed() {
        // Ad closed
    }
});
```

## 📱 Ad Formats

| Ad Format | Class | Description |
|-----------|-------|-------------|
| **Banner** | `AlienBanner` | Standard banner ads |
| **Interstitial** | `AlienInterstitial` | Full-screen ads |
| **Rewarded** | `AlienRewarded` | Reward-based video ads |
| **Native** | `AlienNative` | Native ads with custom layouts |
| **Open Ads** | `AlienOpenAds` | App open ads |

## 🔧 Advanced Configuration

### Mediation Support

AlienAds SDK supports mediation with various ad networks:

```java
// Configure mediation
AliendroidInitialize.SelectAdsAdmob(
    context,
    selectBackupAds,  // Backup ad network
    backupInitialize  // Backup initialization
);
```

### UMP Consent (GDPR/CCPA)

The SDK includes User Messaging Platform for consent management:

```java
// UMP is automatically handled by the SDK
// Consent dialog will show when required
```

### OneSignal Notifications

```java
// Load OneSignal for push notifications
AlienNotif.LoadOneSignal("your-onesignal-app-id");
```

## 📖 Documentation

### Test Ad Units

For testing, use these AdMob test ad unit IDs:

| Ad Format | Test Ad Unit ID |
|-----------|----------------|
| Banner | `ca-app-pub-3940256099942544/6300978111` |
| Interstitial | `ca-app-pub-3940256099942544/1033173712` |
| Rewarded | `ca-app-pub-3940256099942544/5224354917` |
| Native | `ca-app-pub-3940256099942544/2247696110` |
| App Open | `ca-app-pub-3940256099942544/3419835294` |

### ProGuard Rules

If you're using ProGuard/R8, add these rules:

```proguard
# AlienAds SDK
-keep class com.aliendroid.alienads.** { *; }
-keep class com.aliendroid.sdkads.** { *; }

# AdMob
-keep class com.google.android.gms.ads.** { *; }
-dontwarn com.google.android.gms.ads.**

# UMP
-keep class com.google.android.ump.** { *; }
-dontwarn com.google.android.ump.**
```

## 🔄 Migration Guide

### From v1.x to v2.0

Version 2.0 includes major updates:

- ✅ Updated to AdMob SDK 24.9.0
- ✅ Updated to UMP SDK 4.0.0
- ✅ Minimum SDK raised to API 23
- ✅ Target SDK updated to API 36
- ✅ Java 17 compatibility
- ✅ AndroidX libraries updated

**Breaking Changes:**
- Minimum SDK is now API 23 (was API 21)
- Java 17 required (was Java 8)

## 📊 Versions

| Version | AdMob SDK | UMP SDK | Min SDK | Target SDK | Release Date |
|---------|-----------|---------|---------|------------|--------------|
| 2.0.0 | 24.9.0 | 4.0.0 | 23 | 36 | Feb 2026 |
| 1.x.x | 23.3.0 | 3.0.0 | 21 | 34 | - |

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

```
Copyright 2026 AlienAds SDK

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## 🙏 Acknowledgments

- Google AdMob SDK
- Google User Messaging Platform
- AndroidX Libraries
- JitPack for easy distribution

## 📞 Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/admobSdk-Sun-38/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/admobSdk-Sun-38/discussions)

## 🌟 Show Your Support

Give a ⭐️ if this project helped you!

---

**Made with ❤️ by AlienDroid**
