# 🚀 Quick Start - AlienAds SDK

## 📦 Installation (1 minute)

### Add to `settings.gradle` or root `build.gradle`:
```gradle
maven { url 'https://jitpack.io' }
```

### Add to `app/build.gradle`:
```gradle
dependencies {
    implementation 'com.github.YOURUSERNAME:REPONAME:2.0.0'
}
```

### Add to `AndroidManifest.xml`:
```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-xxxxxxxxxxxxxxxx~yyyyyyyyyy"/>
```

---

## 🎯 Usage Examples

### Initialize (in Application or MainActivity)
```java
InitializeAlienAds.LoadSDK();
AliendroidInitialize.SelectAdsAdmob(this, selectBackupAds, backupInitialize);
```

### Banner Ad
```java
AlienBanner.LoadBanner(this, "YOUR_AD_UNIT_ID");
```

### Interstitial Ad
```java
// Load
AlienInterstitial.LoadInterstitial(this, "YOUR_AD_UNIT_ID");

// Show
AlienInterstitial.ShowInterstitial(this, new AlienInterstitial.OnInterstitialDismissed() {
    @Override
    public void onInterstitialDismissed() {
        // Continue your flow
    }
});
```

### App Open Ad
```java
// Load
AlienOpenAds.LoadOpenAds("YOUR_AD_UNIT_ID", true);

// Show
AlienOpenAds.AppOpenAdManager.showAdIfAvailable(this, 
    new AlienOpenAds.OnShowAdCompleteListener() {
        @Override
        public void onShowAdComplete() {
            // Ad shown or failed
        }
    });
```

### Rewarded Ad
```java
// Load
AlienRewarded.LoadRewarded(this, "YOUR_AD_UNIT_ID");

// Show
AlienRewarded.ShowRewarded(this, new AlienRewarded.OnRewardedAdListener() {
    @Override
    public void onUserEarnedReward(int rewardAmount) {
        // Give reward to user
    }
    
    @Override
    public void onRewardedAdClosed() {
        // Ad closed
    }
});
```

### Native Ad
```java
AlienNative.LoadNative(this, "YOUR_AD_UNIT_ID", nativeAdView);
```

---

## 🧪 Test Ad Unit IDs

| Ad Format | Test ID |
|-----------|---------|
| Banner | `ca-app-pub-3940256099942544/6300978111` |
| Interstitial | `ca-app-pub-3940256099942544/1033173712` |
| Rewarded | `ca-app-pub-3940256099942544/5224354917` |
| Native | `ca-app-pub-3940256099942544/2247696110` |
| App Open | `ca-app-pub-3940256099942544/3419835294` |

---

## 📋 Requirements

- Min SDK: **API 23** (Android 6.0+)
- Target SDK: **API 36** (Android 16)
- Java: **17+**

---

## 📚 Full Documentation

See `README.md` for complete documentation.

## 🐛 Issues?

See `TROUBLESHOOTING.md` for solutions.

## 🚀 Publishing?

See `PUBLISH_GUIDE.md` for GitHub/JitPack setup.
