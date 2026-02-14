# Potential Issues & Quick Fixes

## 🔴 Common Build Errors

### 1. Gradle Sync Failed - AGP Version Mismatch
```
Error: This version of the Android Support plugin for IntelliJ IDEA (or Android Studio) 
cannot open this project, please retry with version 2021.1.1 or newer.
```

**Solusi:**
- Update Android Studio ke versi terbaru (minimal Iguana 2023.2.1)
- Atau downgrade AGP jika tidak bisa update Android Studio

---

### 2. Duplicate Class Error
```
Error: Duplicate class com.google.android.gms.internal.xxx found in modules
```

**Solusi:** Tambahkan di `app/build.gradle`:
```gradle
android {
    // ... existing config
    
    packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/LICENSE.txt'
        exclude 'META-INF/NOTICE'
        exclude 'META-INF/NOTICE.txt'
    }
}

configurations.all {
    resolutionStrategy {
        force 'com.google.android.gms:play-services-basement:18.3.0'
    }
}
```

---

### 3. Manifest Merger Error - android:exported
```
Error: Manifest merger failed : Apps targeting Android 12 and higher are required 
to specify an explicit value for `android:exported`
```

**Solusi:** Tambahkan `android:exported="true"` atau `"false"` di semua `<activity>`, `<service>`, `<receiver>` di AndroidManifest.xml

Sudah diterapkan di manifest, tapi jika ada error, tambahkan:
```xml
<activity
    android:name=".YourActivity"
    android:exported="true">  <!-- atau false -->
</activity>
```

---

### 4. Resource Not Found - android:attr/lStar
```
Error: AAPT: error: resource android:attr/lStar not found.
```

**Solusi:** Pastikan `compileSdk 36` (sudah diterapkan)

---

### 5. Java Version Mismatch
```
Error: Unsupported class file major version 61
```

**Solusi:** Update Java compatibility di `build.gradle`:
```gradle
android {
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_17
        targetCompatibility JavaVersion.VERSION_17
    }
}
```

Jika masih error, tambahkan di `gradle.properties`:
```properties
org.gradle.jvmargs=-Xmx4096m -XX:MaxMetaspaceSize=1024m
```

---

## 🟡 Runtime Issues

### 6. AdMob Ads Not Loading
```
Error: The Google Mobile Ads SDK was initialized incorrectly
```

**Solusi:**
1. Pastikan `com.google.android.gms.ads.APPLICATION_ID` ada di AndroidManifest.xml
2. Inisialisasi AdMob di Application class:
```java
MobileAds.initialize(this, initializationStatus -> {});
```

---

### 7. UMP Consent Dialog Not Showing
```
Error: ConsentInformation.requestConsentInfoUpdate failed
```

**Solusi:**
1. Pastikan UMP SDK versi 4.0.0 (sudah diterapkan)
2. Test dengan test device ID:
```java
ConsentDebugSettings debugSettings = new ConsentDebugSettings.Builder(this)
    .setDebugGeography(ConsentDebugSettings.DebugGeography.DEBUG_GEOGRAPHY_EEA)
    .addTestDeviceHashedId("YOUR_TEST_DEVICE_ID")
    .build();
```

---

### 8. WorkManager Not Working
```
Error: WorkManager is not initialized properly
```

**Solusi:** Tambahkan di AndroidManifest.xml:
```xml
<provider
    android:name="androidx.startup.InitializationProvider"
    android:authorities="${applicationId}.androidx-startup"
    android:exported="false"
    tools:node="merge">
    <meta-data
        android:name="androidx.work.WorkManagerInitializer"
        android:value="androidx.startup"
        tools:node="remove" />
</provider>
```

Lalu inisialisasi manual di Application class:
```java
WorkManager.initialize(
    this,
    new Configuration.Builder().build()
);
```

---

### 9. Multidex Error on Older Devices
```
Error: java.lang.NoClassDefFoundError: Failed resolution of: Landroidx/multidex/MultiDex
```

**Solusi:** Pastikan Application class extends MultiDexApplication:
```java
public class MyApplication extends MultiDexApplication {
    @Override
    protected void attachBaseContext(Context base) {
        super.attachBaseContext(base);
        MultiDex.install(this);
    }
}
```

---

## 🟢 Performance Issues

### 10. Slow Build Time
**Solusi:** Tambahkan di `gradle.properties`:
```properties
org.gradle.jvmargs=-Xmx4096m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.caching=true
org.gradle.configureondemand=true
android.useAndroidX=true
android.enableJetifier=false
```

---

### 11. Large APK Size
**Solusi:** Enable ProGuard/R8 di `build.gradle`:
```gradle
buildTypes {
    release {
        minifyEnabled true
        shrinkResources true
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
}
```

Tambahkan di `proguard-rules.pro`:
```proguard
# AdMob
-keep class com.google.android.gms.ads.** { *; }
-dontwarn com.google.android.gms.ads.**

# UMP
-keep class com.google.android.ump.** { *; }
-dontwarn com.google.android.ump.**
```

---

## 🔵 Migration Issues

### 12. Deprecated API Usage
Jika ada warning tentang deprecated APIs, update code:

**Lama:**
```java
// Deprecated
startActivityForResult(intent, REQUEST_CODE);
```

**Baru:**
```java
// Modern approach
ActivityResultLauncher<Intent> launcher = registerForActivityResult(
    new ActivityResultContracts.StartActivityForResult(),
    result -> {
        // Handle result
    }
);
launcher.launch(intent);
```

---

### 13. Material Components Theme Error
```
Error: The style on this component requires your app theme to be Theme.MaterialComponents
```

**Solusi:** Update `themes.xml`:
```xml
<style name="Theme.MyApplication" parent="Theme.MaterialComponents.DayNight.DarkActionBar">
    <!-- Your theme attributes -->
</style>
```

---

## 🛠️ Quick Commands

### Clean & Rebuild
```bash
./gradlew clean
./gradlew build --refresh-dependencies
```

### Check Dependencies
```bash
./gradlew app:dependencies
```

### Check for Updates
```bash
./gradlew dependencyUpdates
```

### Generate Debug APK
```bash
./gradlew assembleDebug
```

### Generate Release APK
```bash
./gradlew assembleRelease
```

---

## 📞 Emergency Rollback

Jika update menyebabkan masalah kritis, rollback dengan:

### 1. Revert Gradle Files
```bash
git checkout HEAD -- build.gradle app/build.gradle AlienAdsV2/build.gradle gradle/wrapper/gradle-wrapper.properties
```

### 2. Manual Rollback Values
Jika tidak menggunakan Git, kembalikan ke:
- AGP: `7.0.0`
- Gradle: `7.2`
- compileSdk: `34`
- targetSdk: `34`
- minSdk: `21`
- AndroidX libraries: versi lama (lihat UPDATE_NOTES.md)

---

## 🎯 Testing Checklist

Setelah fix error, test:

- [ ] App builds successfully
- [ ] App installs on device
- [ ] App launches without crash
- [ ] All activities accessible
- [ ] AdMob ads display correctly
- [ ] No memory leaks
- [ ] No ANR (Application Not Responding)
- [ ] Background tasks work
- [ ] Permissions granted properly

---

**Last Updated:** 14 Februari 2026
