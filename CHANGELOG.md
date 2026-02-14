# Changelog

All notable changes to AlienAds SDK will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-02-14

### 🎉 Major Release - Android 16 Support

This is a major update with significant improvements and modernization.

### ✨ Added
- Support for Android SDK 36 (Android 16 "Baklava")
- Updated to Google Mobile Ads SDK 24.9.0 (from 23.3.0)
- Updated to User Messaging Platform SDK 4.0.0 (from 3.0.0)
- Java 17 compatibility
- Maven publishing support for JitPack
- Comprehensive documentation (README, LICENSE, guides)
- Gradle build optimizations (parallel, caching)
- Enhanced ProGuard rules

### 🔄 Changed
- **Minimum SDK raised from API 21 to API 23** (Android 6.0+)
- **Target SDK updated from 34 to 36** (Android 16)
- **Compile SDK updated from 34 to 36**
- **Java compatibility from 8 to 17**
- Android Gradle Plugin updated from 7.0.0 to 9.0.1
- Gradle wrapper updated from 7.2 to 9.1.0
- AndroidX AppCompat updated from 1.4.1 to 1.7.1
- Material Components updated from 1.6.x to 1.13.0
- Lifecycle components updated from 2.5.1 to 2.10.0
- WorkManager updated from 2.7.1 to 2.11.1
- ConstraintLayout updated from 2.1.4 to 2.2.1
- JVM memory allocation increased from 2GB to 4GB
- Removed deprecated jcenter() repository

### 🚨 Breaking Changes
- **Dropped support for Android 5.0 and 5.1** (API 21-22)
  - Reason: Latest AndroidX libraries require API 23+
  - Impact: ~1% of users (as of 2026)
- **Requires JDK 17 or higher**
  - Reason: AGP 9.0+ requirement
  - Migration: Update Android Studio or use embedded JDK
- **Removed jcenter() repository**
  - Reason: JCenter has been shut down
  - Impact: All dependencies now use mavenCentral()

### 🐛 Fixed
- Gradle sync issues with newer Android Studio versions
- Build performance improvements
- Memory allocation issues with large projects
- Compatibility issues with latest AndroidX libraries

### 📚 Documentation
- Added comprehensive README.md
- Added PUBLISH_GUIDE.md for GitHub/JitPack publishing
- Added TROUBLESHOOTING.md for common issues
- Added UPGRADE_GUIDE.md for migration from v1.x
- Added Apache License 2.0
- Added this CHANGELOG.md

### 🔧 Technical Details
- AdMob SDK 24.9.0 includes:
  - Bug fixes and performance improvements
  - Enhanced ad loading mechanisms
  - Better error handling
- UMP SDK 4.0.0 includes:
  - New `setConsentSyncId()` API
  - Improved consent flow
  - Better GDPR/CCPA compliance

### 📊 Dependencies Summary
| Dependency | Old Version | New Version |
|------------|-------------|-------------|
| AdMob SDK | 23.3.0 | 24.9.0 |
| UMP SDK | 3.0.0 | 4.0.0 |
| AppCompat | 1.4.1 | 1.7.1 |
| Material | 1.6.x | 1.13.0 |
| Lifecycle | 2.5.1 | 2.10.0 |
| WorkManager | 2.7.1 | 2.11.1 |
| ConstraintLayout | 2.1.4 | 2.2.1 |

### 🎯 Google Play Compliance
- ✅ Ready for Google Play target SDK 36 requirement (deadline: August 31, 2026)
- ✅ Compliant with latest privacy policies
- ✅ UMP SDK 4.0.0 for proper consent management

### 🔮 Future Compatibility
- Compatible with Android 17 (API 37) Beta
- Ready for Google Mobile Ads Next-Gen SDK (when GA in July 2026)

---

## [1.x.x] - Previous Versions

### Legacy Version Details
- AdMob SDK: 23.3.0
- UMP SDK: 3.0.0
- Minimum SDK: API 21 (Android 5.0)
- Target SDK: API 34 (Android 14)
- Java: Version 8

### Known Issues in v1.x
- Not compatible with Android SDK 36
- Missing latest AdMob features
- Performance issues with large projects
- Deprecated jcenter() repository

---

## Migration Guide

### From v1.x to v2.0.0

**Step 1: Update Dependencies**
```gradle
// Old
implementation 'com.github.username:repo:1.x.x'

// New
implementation 'com.github.username:repo:2.0.0'
```

**Step 2: Update Build Configuration**
```gradle
android {
    compileSdk 36  // was 34
    
    defaultConfig {
        minSdk 23  // was 21 - BREAKING CHANGE
        targetSdk 36  // was 34
    }
    
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_17  // was VERSION_1_8
        targetCompatibility JavaVersion.VERSION_17
    }
}
```

**Step 3: Update Gradle**
- AGP: 9.0.1 (was 7.0.0)
- Gradle: 9.1.0 (was 7.2)
- JDK: 17+ (was 8)

**Step 4: Test Thoroughly**
- Test all ad formats
- Test on Android 6.0+ devices
- Verify UMP consent dialog
- Check for any deprecated API usage

**No Code Changes Required!**
- All AlienAds APIs remain the same
- No breaking changes in SDK usage
- Only build configuration updates needed

---

## Versioning Strategy

We follow [Semantic Versioning](https://semver.org/):

- **MAJOR** version (X.0.0): Incompatible API changes or breaking changes
- **MINOR** version (0.X.0): New features, backward compatible
- **PATCH** version (0.0.X): Bug fixes, backward compatible

---

## Support

- **Issues:** [GitHub Issues](https://github.com/yourusername/admobSdk-Sun-38/issues)
- **Discussions:** [GitHub Discussions](https://github.com/yourusername/admobSdk-Sun-38/discussions)
- **Documentation:** See README.md and guides

---

[2.0.0]: https://github.com/yourusername/admobSdk-Sun-38/releases/tag/2.0.0
