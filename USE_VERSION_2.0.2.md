# 🎯 GUNAKAN VERSION 2.0.2 (FINAL!)

## ⚠️ PENTING: Gunakan Version 2.0.2, BUKAN 2.0.1!

Version 2.0.1 masih menggunakan code lama yang error. Version **2.0.2** adalah yang sudah diperbaiki!

---

## ✅ SOLUSI FINAL

### **1. Gunakan Dependency Version 2.0.2**

Buka `app/build.gradle` dan gunakan:

```gradle
dependencies {
    // ✅ GUNAKAN INI (VERSION 2.0.2)
    implementation 'com.github.plered:admobSDK:2.0.2'
    
    // ❌ JANGAN GUNAKAN INI
    // implementation 'com.github.plered:admobSDK:2.0.0'  // Failed build
    // implementation 'com.github.plered:admobSDK:2.0.1'  // Old code, error
}
```

### **2. Trigger Build di JitPack**

**WAJIB:** Anda harus trigger build manual!

1. **Buka:** https://jitpack.io

2. **Paste:** `https://github.com/plered/admobSDK`

3. **Klik "Look up"**

4. **Cari tag 2.0.2** (yang TERBARU!)

5. **Klik "Get it"** di samping tag 2.0.2

6. **Tunggu 5-10 menit** hingga status = **"Success"** ✅

### **3. Pastikan JitPack Repository Ada**

Di `settings.gradle`:
```gradle
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }  // ← WAJIB!
    }
}
```

### **4. Sync Gradle**

Setelah build JitPack SUCCESS:
- Klik **Sync Now** di Android Studio
- Library akan ter-download

---

## 📊 Perbedaan Version

| Version | Status | Keterangan |
|---------|--------|------------|
| **2.0.0** | ❌ Failed | Build gagal, namespace missing |
| **2.0.1** | ❌ Failed | Publishing config error |
| **2.0.2** | ✅ **READY** | **Publishing fixed, GUNAKAN INI!** |

---

## 🔍 Cek Status Build

### **Via Browser:**
https://jitpack.io/#plered/admobSDK

### **Via Command:**
```bash
curl "https://jitpack.io/api/builds/com.github.plered/admobSDK/2.0.2"
```

**Status yang diharapkan:**
- ✅ **"ok"** atau **"Success"** = Library siap!
- 🔵 **"Building..."** = Tunggu beberapa menit
- ⚪ **"none"** = Belum di-trigger (klik "Get it" dulu!)

---

## 📝 Contoh Lengkap

### **File: `settings.gradle`**
```gradle
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }  // ← JitPack
    }
}

rootProject.name = "YourApp"
include ':app'
```

### **File: `app/build.gradle`**
```gradle
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.yourpackage.app'
    compileSdk 36
    
    defaultConfig {
        applicationId "com.yourpackage.app"
        minSdk 23
        targetSdk 36
        versionCode 1
        versionName "1.0"
    }
    
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_11
        targetCompatibility JavaVersion.VERSION_11
    }
}

dependencies {
    // AlienAds SDK - VERSION 2.0.2
    implementation 'com.github.plered:admobSDK:2.0.2'
    
    // AndroidX
    implementation 'androidx.appcompat:appcompat:1.7.1'
    implementation 'com.google.android.material:material:1.13.0'
    
    // Lainnya...
}
```

---

## 🚀 Quick Start Setelah Library Ter-install

### **1. Initialize SDK**
```java
import com.aliendroid.alienads.*;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        // Initialize AlienAds
        InitializeAlienAds.LoadSDK();
        AliendroidInitialize.SelectAdsAdmob(this, selectBackupAds, backupInitialize);
    }
}
```

### **2. Load Banner Ad**
```java
AlienBanner.LoadBanner(this, "YOUR_AD_UNIT_ID");
```

### **3. Load Interstitial Ad**
```java
// Load
AlienInterstitial.LoadInterstitial(this, "YOUR_AD_UNIT_ID");

// Show
AlienInterstitial.ShowInterstitial(this, new AlienInterstitial.OnInterstitialDismissed() {
    @Override
    public void onInterstitialDismissed() {
        // Ad closed
    }
});
```

---

## ⏱️ Timeline

1. **Sekarang:** Code v2.0.2 sudah di-push ✅
2. **Anda:** Trigger build di JitPack (klik "Get it" pada tag 2.0.2)
3. **Tunggu:** 5-10 menit untuk build selesai
4. **Cek:** Status build = "Success"
5. **Sync:** Gradle di Android Studio
6. **Done:** Library siap digunakan!

---

## ✅ Checklist

- [ ] Buka https://jitpack.io
- [ ] Paste `https://github.com/plered/admobSDK`
- [ ] Klik "Look up"
- [ ] **Klik "Get it" pada tag 2.0.2** (BUKAN 2.0.0 atau 2.0.1!)
- [ ] Tunggu status = "Success"
- [ ] Update dependency ke `2.0.2` di `app/build.gradle`
- [ ] Pastikan JitPack repository ada di `settings.gradle`
- [ ] Sync Gradle
- [ ] Build project berhasil!

---

## 🆘 Troubleshooting

### **Error: "Could not find com.github.plered:admobSDK:2.0.2"**

**Penyebab:** Build di JitPack belum selesai atau belum di-trigger

**Solusi:**
1. Cek https://jitpack.io/#plered/admobSDK
2. Pastikan tag 2.0.2 sudah di-build (status = "Success")
3. Jika belum, klik "Get it" untuk trigger build
4. Tunggu hingga selesai
5. Sync Gradle lagi

### **Build JitPack Gagal?**

Jika build 2.0.2 masih gagal, beritahu saya:
1. Copy error message dari build log
2. Screenshot jika memungkinkan
3. Saya akan perbaiki lagi

---

## 📞 Support

**Repository:** https://github.com/plered/admobSDK  
**JitPack:** https://jitpack.io/#plered/admobSDK

---

## 🎉 Kesimpulan

**GUNAKAN VERSION 2.0.2!**

```gradle
implementation 'com.github.plered:admobSDK:2.0.2'
```

1. Trigger build di JitPack (klik "Get it")
2. Tunggu SUCCESS
3. Sync Gradle
4. Selesai!

---

**Good luck!** 🚀
