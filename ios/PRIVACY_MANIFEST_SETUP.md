# iOS Privacy Manifest Setup

The PrivacyInfo.xcprivacy file has been created but needs to be manually added to the Xcode project.

## Steps to Add Privacy Manifest to Xcode Project:

1. Open `ios/Runner.xcodeproj` in Xcode
2. Right-click on the `Runner` folder in the project navigator
3. Select "Add Files to Runner..."
4. Navigate to and select `ios/Runner/PrivacyInfo.xcprivacy`
5. Make sure "Copy items if needed" is **unchecked**
6. Make sure the target "Runner" is **checked**
7. Click "Add"

## What This File Does:

The PrivacyInfo.xcprivacy file declares:
- No tracking of users
- Required API usage reasons for common iOS APIs used by Flutter:
  - **File Timestamp API (C617.1)**: Accessing file modification times
  - **UserDefaults API (CA92.1)**: Storing app preferences
  - **Disk Space API (E174.1)**: Checking available storage
  - **System Boot Time API (35F9.1)**: Used by audio/media frameworks

## Why This Is Required:

Starting in 2024-2025, Apple requires all apps to include a privacy manifest file when using certain APIs or third-party SDKs. This is enforced for App Store submissions as of 2026.

For more information, see:
- [Apple Developer: Privacy Manifest](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files)
- [Flutter Privacy Manifest Support](https://github.com/flutter/flutter/issues/143232)

## Additional Notes:

After adding the file to Xcode:
1. Run `pod install` in the `ios` directory to update dependencies
2. Build the project to ensure everything compiles correctly
3. When submitting to App Store, ensure all third-party dependencies also have privacy manifests
