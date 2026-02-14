# 📦 Panduan Publish ke GitHub & JitPack

Panduan lengkap untuk mempublikasikan AlienAds SDK ke GitHub dan membuatnya tersedia via JitPack.

---

## 📋 Persiapan

### ✅ File yang Sudah Disiapkan

Saya telah membuat file-file berikut untuk Anda:

1. ✅ `.gitignore` - Mengabaikan file yang tidak perlu di Git
2. ✅ `README.md` - Dokumentasi lengkap untuk GitHub
3. ✅ `LICENSE` - Apache License 2.0
4. ✅ `jitpack.yml` - Konfigurasi JitPack
5. ✅ `AlienAdsV2/build.gradle` - Sudah ditambahkan maven-publish plugin

---

## 🔧 Langkah 1: Edit Konfigurasi

### A. Edit `AlienAdsV2/build.gradle`

Buka file `AlienAdsV2/build.gradle` dan **ganti placeholder** berikut:

```gradle
// Di bagian publishing configuration (baris ~48-85)

groupId = 'com.github.GANTI_USERNAME_GITHUB_ANDA'  // ← GANTI INI
artifactId = 'alienads'  // Bisa diganti sesuai keinginan
version = '2.0.0'  // Versi library Anda

pom {
    name = 'AlienAds SDK'
    description = 'Advanced AdMob SDK wrapper with mediation support for Android'
    url = 'https://github.com/GANTI_USERNAME/GANTI_REPO_NAME'  // ← GANTI INI
    
    developers {
        developer {
            id = 'GANTI_USERNAME_ANDA'  // ← GANTI INI
            name = 'GANTI_NAMA_ANDA'    // ← GANTI INI
            email = 'GANTI_EMAIL_ANDA'  // ← GANTI INI
        }
    }
    
    scm {
        connection = 'scm:git:git://github.com/USERNAME/REPO.git'  // ← GANTI INI
        developerConnection = 'scm:git:ssh://github.com/USERNAME/REPO.git'  // ← GANTI INI
        url = 'https://github.com/USERNAME/REPO'  // ← GANTI INI
    }
}
```

**Contoh setelah diganti:**
```gradle
groupId = 'com.github.johndoe'
url = 'https://github.com/johndoe/alienads-sdk'

developers {
    developer {
        id = 'johndoe'
        name = 'John Doe'
        email = 'john.doe@example.com'
    }
}

scm {
    connection = 'scm:git:git://github.com/johndoe/alienads-sdk.git'
    developerConnection = 'scm:git:ssh://github.com/johndoe/alienads-sdk.git'
    url = 'https://github.com/johndoe/alienads-sdk'
}
```

### B. Edit `README.md`

Ganti semua `yourusername` dengan username GitHub Anda:

```markdown
[![](https://jitpack.io/v/USERNAME/REPO.svg)](https://jitpack.io/#USERNAME/REPO)

## Installation
dependencies {
    implementation 'com.github.USERNAME:REPO:2.0.0'
}
```

---

## 🚀 Langkah 2: Upload ke GitHub

### Opsi A: Menggunakan Git Command Line

1. **Buka Terminal/Command Prompt** di folder proyek:
   ```bash
   cd d:\Android\admobSdk-Sun-38
   ```

2. **Initialize Git repository:**
   ```bash
   git init
   ```

3. **Add semua file:**
   ```bash
   git add .
   ```

4. **Commit pertama:**
   ```bash
   git commit -m "Initial commit - AlienAds SDK v2.0.0"
   ```

5. **Buat repository di GitHub:**
   - Buka https://github.com/new
   - Repository name: `alienads-sdk` (atau nama lain)
   - Description: `Advanced AdMob SDK wrapper for Android`
   - **JANGAN** centang "Initialize with README" (sudah ada)
   - Klik **Create repository**

6. **Link ke GitHub repository:**
   ```bash
   git remote add origin https://github.com/USERNAME/REPO_NAME.git
   git branch -M main
   git push -u origin main
   ```

7. **Buat Release Tag (PENTING untuk JitPack):**
   ```bash
   git tag -a 2.0.0 -m "Release version 2.0.0"
   git push origin 2.0.0
   ```

### Opsi B: Menggunakan GitHub Desktop

1. **Download & Install GitHub Desktop:**
   - https://desktop.github.com/

2. **Buka GitHub Desktop**

3. **Add Repository:**
   - File → Add Local Repository
   - Pilih folder: `d:\Android\admobSdk-Sun-38`
   - Klik "create a repository"

4. **Commit:**
   - Summary: `Initial commit - AlienAds SDK v2.0.0`
   - Klik **Commit to main**

5. **Publish ke GitHub:**
   - Klik **Publish repository**
   - Name: `alienads-sdk`
   - Description: `Advanced AdMob SDK wrapper for Android`
   - **Uncheck** "Keep this code private" (untuk JitPack)
   - Klik **Publish repository**

6. **Buat Release Tag:**
   - Di GitHub Desktop: Repository → Create Tag
   - Tag: `2.0.0`
   - Klik **Create Tag**
   - Push tag: Repository → Push

### Opsi C: Menggunakan Android Studio

1. **Enable Version Control:**
   - VCS → Enable Version Control Integration
   - Pilih **Git**

2. **Add Files:**
   - VCS → Git → Add

3. **Commit:**
   - VCS → Commit
   - Commit message: `Initial commit - AlienAds SDK v2.0.0`
   - Klik **Commit**

4. **Share to GitHub:**
   - VCS → Import into Version Control → Share Project on GitHub
   - Repository name: `alienads-sdk`
   - Klik **Share**

5. **Create Tag:**
   - VCS → Git → Tag
   - Tag name: `2.0.0`
   - Klik **Create Tag**
   - VCS → Git → Push → Push Tags

---

## 📦 Langkah 3: Publish ke JitPack

### A. Trigger JitPack Build

1. **Buka JitPack:**
   - https://jitpack.io

2. **Masukkan GitHub URL:**
   - Paste: `https://github.com/USERNAME/REPO_NAME`
   - Klik **Look up**

3. **Pilih Version:**
   - Akan muncul tag `2.0.0`
   - Klik **Get it**

4. **Tunggu Build:**
   - JitPack akan mulai build
   - Status akan berubah dari "Building..." → "Success" (hijau)
   - Jika gagal (merah), klik "Log" untuk lihat error

### B. Verifikasi Build Success

Jika build **SUCCESS** ✅, Anda akan lihat:
- Badge hijau dengan tulisan "Success"
- Instruksi instalasi muncul

Jika build **FAILED** ❌, lihat bagian Troubleshooting di bawah.

---

## 🎯 Langkah 4: Test Library

### A. Buat Project Baru untuk Testing

1. **Buat project Android baru**

2. **Tambahkan JitPack repository** di `settings.gradle`:
   ```gradle
   dependencyResolutionManagement {
       repositories {
           google()
           mavenCentral()
           maven { url 'https://jitpack.io' }
       }
   }
   ```

3. **Tambahkan dependency** di `app/build.gradle`:
   ```gradle
   dependencies {
       implementation 'com.github.USERNAME:REPO_NAME:2.0.0'
   }
   ```

4. **Sync Gradle**

5. **Test import:**
   ```java
   import com.aliendroid.alienads.AlienBanner;
   import com.aliendroid.alienads.AlienInterstitial;
   // dll
   ```

Jika berhasil import, **SELAMAT!** 🎉 Library Anda sudah tersedia di JitPack!

---

## 🔄 Update Version (Release Baru)

Ketika ingin release versi baru:

### 1. Update Version di Code

Edit `AlienAdsV2/build.gradle`:
```gradle
version = '2.1.0'  // Update version number
```

### 2. Commit Changes

```bash
git add .
git commit -m "Update to version 2.1.0"
git push
```

### 3. Create New Tag

```bash
git tag -a 2.1.0 -m "Release version 2.1.0"
git push origin 2.1.0
```

### 4. Rebuild di JitPack

- Buka https://jitpack.io/#USERNAME/REPO_NAME
- Tag `2.1.0` akan muncul otomatis
- Klik **Get it** untuk trigger build

---

## ⚠️ Troubleshooting JitPack

### Error: "Could not find com.github.USERNAME:REPO:2.0.0"

**Penyebab:**
- Repository masih private
- Tag belum di-push
- Build JitPack gagal

**Solusi:**
1. Pastikan repository **PUBLIC**
2. Cek tag sudah ada: `git tag -l`
3. Push tag: `git push origin 2.0.0`
4. Trigger build di JitPack

---

### Error: "Build Failed" di JitPack

**Klik "Log" di JitPack untuk lihat error detail.**

**Error Umum & Solusi:**

#### 1. "Could not find com.android.tools.build:gradle:9.0.1"
**Solusi:** JitPack mungkin belum support AGP 9.0.1

Edit `build.gradle` (root) untuk JitPack:
```gradle
dependencies {
    classpath "com.android.tools.build:gradle:8.3.2"  // Downgrade untuk JitPack
}
```

Edit `gradle/wrapper/gradle-wrapper.properties`:
```properties
distributionUrl=https\://services.gradle.org/distributions/gradle-8.4-bin.zip
```

Commit dan push lagi.

#### 2. "Unsupported class file major version"
**Solusi:** Sudah diatasi dengan `jitpack.yml` (JDK 17)

#### 3. "Task 'install' not found"
**Solusi:** Sudah diatasi dengan `maven-publish` plugin

---

### Error: "No such module 'AlienAdsV2'"

**Penyebab:** JitPack tidak tahu module mana yang harus di-build

**Solusi:** Buat file `build.gradle` di root dengan:
```gradle
// Di root build.gradle, tambahkan:
task install(dependsOn: ':AlienAdsV2:publishToMavenLocal')
```

---

## 📊 Monitoring

### Cek Status Build

- **JitPack Dashboard:** https://jitpack.io/#USERNAME/REPO_NAME
- **Build Log:** Klik "Log" di samping version
- **Download Stats:** Lihat berapa kali library di-download

### Badge untuk README

Tambahkan badge di `README.md`:
```markdown
[![](https://jitpack.io/v/USERNAME/REPO.svg)](https://jitpack.io/#USERNAME/REPO)
[![](https://jitpack.io/v/USERNAME/REPO/month.svg)](https://jitpack.io/#USERNAME/REPO)
```

---

## 🎯 Best Practices

### 1. Semantic Versioning

Gunakan format: `MAJOR.MINOR.PATCH`
- **MAJOR:** Breaking changes (2.0.0 → 3.0.0)
- **MINOR:** New features, backward compatible (2.0.0 → 2.1.0)
- **PATCH:** Bug fixes (2.0.0 → 2.0.1)

### 2. Changelog

Buat file `CHANGELOG.md`:
```markdown
# Changelog

## [2.0.0] - 2026-02-14
### Added
- Updated to AdMob SDK 24.9.0
- Updated to UMP SDK 4.0.0
- Support for Android SDK 36

### Changed
- Minimum SDK raised to API 23
- Java 17 compatibility

### Breaking Changes
- Dropped support for Android 5.x
```

### 3. Documentation

- Update `README.md` setiap ada perubahan API
- Tambahkan contoh code yang jelas
- Dokumentasikan breaking changes

### 4. Testing

- Test library di project lain sebelum release
- Pastikan semua ad formats berfungsi
- Test di berbagai Android versions

---

## 📞 Support

Jika ada masalah:

1. **Cek JitPack Log** untuk error detail
2. **Lihat TROUBLESHOOTING.md** untuk solusi umum
3. **GitHub Issues:** Buat issue di repo Anda

---

## ✅ Checklist Publish

Sebelum publish, pastikan:

- [ ] Semua placeholder di `build.gradle` sudah diganti
- [ ] `README.md` sudah di-update dengan username yang benar
- [ ] Repository di GitHub sudah PUBLIC
- [ ] Tag version sudah dibuat dan di-push
- [ ] Build di JitPack SUCCESS (hijau)
- [ ] Library bisa di-import di project test
- [ ] Dokumentasi lengkap dan jelas

---

**Selamat! SDK Anda sekarang tersedia untuk publik via JitPack!** 🎉

Orang lain bisa menggunakan library Anda dengan:
```gradle
implementation 'com.github.USERNAME:REPO:2.0.0'
```
