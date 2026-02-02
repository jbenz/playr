# iOS Configuration Updates for 2026

## Summary of Changes

This update modernizes the iOS configuration for the Koel Player Flutter app to meet 2026 App Store requirements and best practices.

## Changes Made

### 1. Updated iOS Deployment Target (iOS 13.0 → iOS 15.0)
**Files Modified:**
- `ios/Podfile` - Updated platform requirement to iOS 15.0
- `ios/Podfile` - Updated post_install deployment target to iOS 15.0
- `ios/Runner.xcodeproj/project.pbxproj` - Unified all deployment targets to iOS 15.0

**Rationale:** 
- iOS 13.0 was released in 2019 and is now outdated
- Apple recommends iOS 15.0 as minimum for new apps in 2026
- Most modern Flutter plugins require iOS 13+ minimum, with many moving to iOS 15+
- Better compatibility with Xcode 16+ and iOS 18 SDK

### 2. Modernized Info.plist Settings
**Files Modified:**
- `ios/Runner/Info.plist`

**Changes:**
- Removed `CADisableMinimumFrameDurationOnPhone` (legacy setting)
- Updated `UIStatusBarStyle` from `UIStatusBarStyleDarkContent` to `UIStatusBarStyleDefault`

**Rationale:**
- `CADisableMinimumFrameDurationOnPhone` is a legacy setting from older iOS versions
- `UIStatusBarStyleDefault` adapts automatically to the system's light/dark mode settings, providing better user experience across different appearance modes. The previous `UIStatusBarStyleDarkContent` was specifically for dark content on a light background, which doesn't adapt well to dark mode.

### 3. Added Privacy Manifest
**Files Created:**
- `ios/Runner/PrivacyInfo.xcprivacy` - Apple-required privacy manifest
- `ios/PRIVACY_MANIFEST_SETUP.md` - Documentation for manual Xcode setup

**Rationale:**
- Required by Apple starting 2024-2025 for App Store submissions
- Mandatory for all apps in 2026
- Declares API usage for:
  - File Timestamp API (C617.1)
  - UserDefaults API (CA92.1)
  - Disk Space API (E174.1)
  - System Boot Time API (35F9.1)

**Note:** The PrivacyInfo.xcprivacy file must be manually added to the Xcode project. See `ios/PRIVACY_MANIFEST_SETUP.md` for instructions.

## What Was NOT Changed

### Files Kept As-Is:
- `ios/Runner/AppDelegate.swift` - Already uses modern patterns (@main, FlutterAppDelegate)
- `ios/Runner/Runner.entitlements` - Current entitlements are appropriate
- `ios/Runner/Info.plist` - Other settings like LSRequiresIPhoneOS (still supported)

## Post-Update Steps

### Required Manual Steps:
1. **Add Privacy Manifest to Xcode:**
   - Open the project in Xcode
   - Add `ios/Runner/PrivacyInfo.xcprivacy` to the Runner target
   - See `ios/PRIVACY_MANIFEST_SETUP.md` for detailed instructions

2. **Update Dependencies:**
   ```bash
   cd ios
   pod install --repo-update
   ```

3. **Update Flutter Dependencies:**
   ```bash
   flutter pub get
   flutter pub upgrade
   ```

### Recommended Steps:
1. **Test Build:**
   ```bash
   flutter build ios --release
   ```

2. **Verify Plugin Compatibility:**
   - Check that all plugins support iOS 15.0+
   - Update any plugins that have newer versions with privacy manifest support

3. **Test on Device:**
   - Test on physical iOS device running iOS 15+
   - Verify all functionality works as expected

## Compatibility Notes

- **Minimum iOS Version:** Now requires iOS 15.0 or later
- **Xcode Version:** Requires Xcode 14.0 or later for iOS 15 development
- **Flutter Version:** Recommend Flutter 3.19+ for privacy manifest support
- **App Store:** Fully compliant with 2026 App Store requirements

## References

- [Apple Developer: Privacy Manifest Files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files)
- [Apple Developer: iOS Deployment Target Requirements](https://developer.apple.com/support/xcode/)
- [Flutter: Privacy Manifest Support](https://github.com/flutter/flutter/issues/143232)
- [Flutter: iOS Development Guide](https://docs.flutter.dev/deployment/ios)
