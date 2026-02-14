# ⚠️ ERROR: Version 2.0.0 Tidak Tersedia

## 🔴 Masalah

Anda menggunakan version **2.0.0** yang **GAGAL BUILD** di JitPack.

```gradle
// ❌ JANGAN GUNAKAN INI
implementation 'com.github.plered:admobSDK:2.0.0'
```

## ✅ Solusi: Gunakan Version 2.0.1

Version **2.0.1** adalah versi yang sudah diperbaiki dan siap untuk JitPack.

### **Langkah 1: Update Dependency**

Buka file `app/build.gradle` dan **ganti version**:

```gradle
dependencies {
    // ❌ Hapus ini:
    // implementation 'com.github.plered:admobSDK:2.0.0'
    
    // ✅ Gunakan ini:
    implementation 'com.github.plered:admobSDK:2.0.1'
}
```

### **Langkah 2: Trigger Build di JitPack**

Ada 2 cara:

#### **Cara A: Via Website (Recommended)**

1. Buka: **https://jitpack.io**
2. Paste: `https://github.com/plered/admobSDK`
3. Klik **"Look up"**
4. Cari tag **2.0.1** di list
5. Klik **"Get it"** di samping tag 2.0.1
6. Tunggu build selesai (5-10 menit)
7. Status akan berubah menjadi **"Success"** (hijau)

#### **Cara B: Auto-Trigger (Langsung Sync)**

1. Update dependency ke 2.0.1 (seperti di atas)
2. Sync Gradle di Android Studio
3. JitPack akan **otomatis** mulai build
4. Tunggu beberapa menit
5. Sync lagi jika perlu

---

## 📝 Contoh Lengkap

### **File: `settings.gradle` atau root `build.gradle`**

Pastikan JitPack repository sudah ditambahkan:

```gradle
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }  // ← Pastikan ada ini
    }
}
```

Atau jika menggunakan root `build.gradle`:

```gradle
allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }  // ← Pastikan ada ini
    }
}
```

### **File: `app/build.gradle`**

```gradle
dependencies {
    // AlienAds SDK
    implementation 'com.github.plered:admobSDK:2.0.1'  // ✅ Version 2.0.1
    
    // Dependencies lainnya...
    implementation 'androidx.appcompat:appcompat:1.7.1'
    // dll...
}
```

---

## 🔍 Cek Status Build

### **Via Browser:**
Buka: https://jitpack.io/#plered/admobSDK

Anda akan lihat:
- ✅ **Success** (hijau) = Build berhasil, library siap digunakan
- 🔵 **Building...** (biru) = Sedang build, tunggu beberapa menit
- ❌ **Error** (merah) = Build gagal (beritahu saya jika ini terjadi)

### **Via Command Line:**
```bash
curl "https://jitpack.io/api/builds/com.github.plered/admobSDK/2.0.1"
```

---

## ⏱️ Berapa Lama Build?

- **First build:** 5-10 menit (download dependencies, compile, dll)
- **Subsequent builds:** Lebih cepat (menggunakan cache)

---

## 🚨 Jika Masih Error

### Error: "Could not find com.github.plered:admobSDK:2.0.1"

**Penyebab:**
- Build di JitPack belum selesai
- Build di JitPack gagal

**Solusi:**
1. Cek status build di https://jitpack.io/#plered/admobSDK
2. Jika status **"Building..."** → Tunggu hingga selesai
3. Jika status **"Error"** → Beritahu saya error message-nya
4. Jika status **"Success"** → Sync Gradle lagi

### Error: "Failed to resolve: com.github.plered:admobSDK:2.0.1"

**Solusi:**
1. Pastikan JitPack repository sudah ditambahkan
2. Invalidate caches: `File → Invalidate Caches / Restart`
3. Sync Gradle lagi

---

## 📊 Perbedaan Version

| Version | Status | Keterangan |
|---------|--------|------------|
| **2.0.0** | ❌ Failed | Build gagal di JitPack, **JANGAN GUNAKAN** |
| **2.0.1** | ✅ Ready | Build berhasil, **GUNAKAN INI** |

---

## ✅ Checklist

Sebelum sync Gradle:

- [ ] JitPack repository sudah ditambahkan di `settings.gradle` atau root `build.gradle`
- [ ] Dependency sudah diubah ke version **2.0.1** (bukan 2.0.0)
- [ ] Build di JitPack sudah **SUCCESS** (cek di https://jitpack.io/#plered/admobSDK)
- [ ] Invalidate caches jika perlu

---

## 🎯 Quick Fix

**Langsung copy-paste ini:**

```gradle
// settings.gradle
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}

// app/build.gradle
dependencies {
    implementation 'com.github.plered:admobSDK:2.0.1'
}
```

Lalu:
1. Sync Gradle
2. Tunggu build JitPack selesai (5-10 menit)
3. Sync lagi jika perlu

---

## 📞 Butuh Bantuan?

Jika masih error setelah menggunakan 2.0.1, beritahu saya:
1. Error message lengkapnya
2. Status build di JitPack (Success/Building/Error)
3. Screenshot jika memungkinkan

---

**TL;DR:**
- ❌ Jangan gunakan `2.0.0`
- ✅ Gunakan `2.0.1`
- 🌐 Trigger build di https://jitpack.io
- ⏱️ Tunggu 5-10 menit
- 🔄 Sync Gradle lagi
