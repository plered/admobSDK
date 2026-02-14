# Update SDK ke Android 36 - 14 Februari 2026

## 🎯 Ringkasan Perubahan

Proyek telah diperbarui dari Android SDK 34 ke SDK 36 (Android 16 "Baklava") dengan semua dependencies terbaru.

---

## 📦 Perubahan SDK & Build Tools

### Android SDK
- **compileSdk:** 34 → **36**
- **targetSdk:** 34 → **36**
- **minSdk:** 21 → **23** (Android 6.0+)

### Build Tools
| Tool | Versi Lama | Versi Baru | Tanggal Rilis |
|------|-----------|-----------|---------------|
| Android Gradle Plugin | 7.0.0 | **9.0.1** | Januari 2026 |
| Gradle Wrapper | 7.2 | **9.1** | - |

---

## 📚 Update AndroidX Libraries

### App Module (`app/build.gradle`)
| Library | Versi Lama | Versi Baru | Tanggal Rilis |
|---------|-----------|-----------|---------------|
| androidx.appcompat | 1.4.1 | **1.7.1** | Juni 2025 |
| androidx.work:work-runtime | 2.7.1 | **2.11.1** | Januari 2026 |
| androidx.multidex | 2.0.1 | **2.0.1** | (tidak berubah) |
| com.google.android.material | 1.6.1 | **1.13.0** | - |
| androidx.constraintlayout | 2.1.4 | **2.2.1** | Februari 2025 |

### AlienAdsV2 Module (`AlienAdsV2/build.gradle`)
| Library | Versi Lama | Versi Baru | Tanggal Rilis |
|---------|-----------|-----------|---------------|
| androidx.appcompat | 1.4.1 | **1.7.1** | Juni 2025 |
| com.google.android.material | 1.6.0 | **1.13.0** | - |
| androidx.lifecycle:lifecycle-process | 2.5.1 | **2.10.0** | November 2025 |
| androidx.multidex | 2.0.1 | **2.0.1** | (tidak berubah) |
| play-services-ads (AdMob) | 23.3.0 | **24.9.0** | Desember 2025 |
| user-messaging-platform (UMP) | 3.0.0 | **4.0.0** | Oktober 2025 |

---

## 🔧 File yang Dimodifikasi

1. ✅ `build.gradle` (root)
   - Update AGP ke 9.0.1
   - Hapus jcenter() (sudah shutdown)

2. ✅ `gradle/wrapper/gradle-wrapper.properties`
   - Update Gradle wrapper ke 9.1

3. ✅ `app/build.gradle`
   - Update compileSdk, minSdk, targetSdk
   - Update semua AndroidX dependencies

4. ✅ `AlienAdsV2/build.gradle`
   - Update compileSdk, minSdk, targetSdk
   - Update semua AndroidX dependencies
   - Update AdMob & UMP SDK

---

## ⚠️ Breaking Changes & Catatan Penting

### 1. Minimum SDK Naik ke API 23
**Dampak:** Aplikasi tidak lagi support Android 5.0 dan 5.1
- **Sebelum:** minSdk 21 (Android 5.0 Lollipop)
- **Sekarang:** minSdk 23 (Android 6.0 Marshmallow)
- **Alasan:** Banyak AndroidX libraries terbaru (WorkManager 2.11+, Lifecycle 2.10+, Material 1.13+) memerlukan minimum API 23

**Statistik:** Per 2026, Android 6.0+ mencakup ~99% pengguna aktif

### 2. Target SDK 36 - Persyaratan Google Play
- Google Play akan **WAJIB** target API 36+ mulai **31 Agustus 2026**
- Update ini memastikan aplikasi Anda siap untuk persyaratan tersebut

### 3. Perubahan Behavior Android 16 (API 36)
Beberapa perubahan behavior yang perlu diperhatikan:
- **Privacy & Security:** Enhanced permission controls
- **Performance:** Improved background task restrictions
- **Notifications:** Stricter notification policies

### 4. JCenter Dihapus
- Repository `jcenter()` sudah shutdown dan dihapus dari build.gradle
- Semua dependencies sekarang menggunakan `mavenCentral()` dan `google()`

### 5. AGP 9.0 Breaking Changes
- Beberapa API deprecated di AGP 7.x sekarang dihapus
- Build configuration mungkin perlu penyesuaian

---

## 🚀 Langkah Selanjutnya

### 1. Sync & Build Proyek

#### Di Android Studio:
```
1. File → Invalidate Caches / Restart
2. File → Sync Project with Gradle Files
3. Build → Clean Project
4. Build → Rebuild Project
```

#### Via Command Line:
```bash
cd d:\Android\admobSdk-Sun-38
./gradlew clean build
```

### 2. Testing Wajib

#### A. Functional Testing
- ✅ Test semua fitur utama aplikasi
- ✅ Test navigasi antar activity
- ✅ Test background tasks (WorkManager)

#### B. AdMob Testing
- ✅ Banner ads loading & display
- ✅ Interstitial ads loading & display
- ✅ Rewarded ads (jika ada)
- ✅ Native ads (jika ada)
- ✅ UMP consent dialog

#### C. Permission Testing
- ✅ Runtime permissions (Android 6.0+)
- ✅ Network state access
- ✅ Ad ID permission

#### D. Device Testing
- ✅ Test di Android 6.0 (API 23) - minimum
- ✅ Test di Android 14/15/16 (API 34-36) - target
- ✅ Test di berbagai ukuran layar

### 3. Kemungkinan Error & Solusi

#### Error: "Manifest merger failed"
**Solusi:** Tambahkan di AndroidManifest.xml:
```xml
<application
    android:exported="true/false"
    tools:replace="android:exported">
```

#### Error: "Duplicate class found"
**Solusi:** Tambahkan di build.gradle:
```gradle
configurations.all {
    exclude group: 'com.google.android.gms', module: 'play-services-basement'
}
```

#### Error: "AAPT: error: resource android:attr/lStar not found"
**Solusi:** Update compileSdk ke 36 (sudah dilakukan)

#### Error: Build gagal dengan AGP 9.0
**Solusi:** Pastikan Gradle wrapper sudah 9.1+ (sudah dilakukan)

---

## 📱 Kompatibilitas

### Minimum Requirements
- **Android Version:** 6.0 Marshmallow (API 23)
- **Google Play Services:** Latest
- **Java Version:** 8 (sudah dikonfigurasi)

### Target & Compile
- **Target SDK:** 36 (Android 16)
- **Compile SDK:** 36 (Android 16)

### Device Coverage
- Android 6.0 - 16+ (~99% pengguna)

---

## 🔮 Informasi Tambahan

### Android 17 (API 37) - Coming Soon
- Android 17 "Cinnamon Bun" Beta 1 dirilis 13 Februari 2026
- GA diperkirakan pertengahan 2026
- Pertimbangkan untuk update ke API 37 setelah stable

### Google Mobile Ads Next-Gen SDK
- SDK Next-Gen sedang dalam Open Beta (v0.23.0-beta01)
- GA dijadwalkan Juli 2026
- Fitur: Performa lebih baik, ukuran lebih kecil, Kotlin native
- **Rekomendasi:** Tunggu hingga GA untuk production

---

## 📋 Checklist Deployment

Sebelum deploy ke production:

- [ ] Sync Gradle berhasil tanpa error
- [ ] Build berhasil (debug & release)
- [ ] Semua unit tests passed
- [ ] UI tests passed
- [ ] AdMob ads tampil dengan benar
- [ ] UMP consent dialog berfungsi
- [ ] Test di minimal 3 device berbeda
- [ ] Test di Android 6.0 (minimum SDK)
- [ ] Test di Android 14+ (target SDK)
- [ ] ProGuard rules updated (jika ada)
- [ ] App size tidak meningkat signifikan
- [ ] Performance tidak menurun
- [ ] Crash rate normal di Firebase/Crashlytics

---

## 📞 Troubleshooting

Jika mengalami masalah:

1. **Clean & Rebuild:**
   ```bash
   ./gradlew clean
   ./gradlew build --refresh-dependencies
   ```

2. **Invalidate Caches:**
   - Android Studio → File → Invalidate Caches / Restart

3. **Check Gradle Daemon:**
   ```bash
   ./gradlew --stop
   ./gradlew build
   ```

4. **Update Android Studio:**
   - Pastikan menggunakan Android Studio terbaru
   - Minimum: Android Studio Iguana atau lebih baru

---

## 📚 Referensi

- [Android 16 Release Notes](https://developer.android.com/about/versions/16)
- [AGP 9.0 Release Notes](https://developer.android.com/build/releases/gradle-plugin)
- [AndroidX Release Notes](https://developer.android.com/jetpack/androidx/versions)
- [Google Mobile Ads SDK](https://developers.google.com/admob/android/rel-notes)
- [Target SDK Requirements](https://support.google.com/googleplay/android-developer/answer/11926878)

---

**Update Date:** 14 Februari 2026  
**Updated By:** Antigravity AI Assistant  
**Status:** ✅ Ready for Testing
