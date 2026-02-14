# Update SDK AdMob - 14 Februari 2026

## Perubahan yang Dilakukan

### 1. Google Mobile Ads SDK (AdMob)
- **Versi Lama:** 23.3.0
- **Versi Baru:** 24.9.0
- **Tanggal Rilis:** Desember 2025
- **Perubahan:**
  - Bug fixes dan performance improvements
  - Peningkatan stabilitas iklan
  - Optimasi request latency

### 2. User Messaging Platform (UMP) SDK
- **Versi Lama:** 3.0.0
- **Versi Baru:** 4.0.0
- **Tanggal Rilis:** 31 Oktober 2025
- **Perubahan:**
  - Penambahan API `setConsentSyncId()`
  - Peningkatan minimum Android API level ke 23
  - Peningkatan manajemen consent pengguna

## File yang Dimodifikasi
- `AlienAdsV2/build.gradle`

## Langkah Selanjutnya

### Di Android Studio:
1. Buka proyek di Android Studio
2. Klik **File → Sync Project with Gradle Files**
3. Tunggu hingga proses sync selesai
4. Build proyek untuk memastikan tidak ada error

### Via Command Line (jika Java sudah terinstall):
```bash
cd d:\Android\admobSdk-Sun-38
./gradlew clean build
```

## Catatan Penting

### Kompatibilitas
- Minimum Android API Level: 23 (Android 6.0)
- Target SDK: 34
- Compile SDK: 34

### Breaking Changes
Tidak ada breaking changes yang signifikan antara versi 23.3.0 ke 24.9.0, namun disarankan untuk:
1. Testing iklan banner, interstitial, dan rewarded ads
2. Verifikasi consent dialog UMP masih berfungsi dengan baik
3. Testing di berbagai versi Android (minimal API 23+)

### SDK Next-Gen (Opsional)
Google telah mengumumkan **Google Mobile Ads Next-Gen SDK** yang sedang dalam Open Beta (v0.23.0-beta01). SDK ini akan GA pada Juli 2026 dengan fitur:
- Performa lebih baik dengan reduced latency
- Ukuran aplikasi lebih kecil
- Dukungan Kotlin modern
- Release cycle lebih cepat

Untuk saat ini, versi stabil 24.9.0 adalah pilihan yang tepat untuk production.

## Referensi
- [Google Mobile Ads SDK Release Notes](https://developers.google.com/admob/android/rel-notes)
- [UMP SDK Release Notes](https://developers.google.com/ump/android/release-notes)
