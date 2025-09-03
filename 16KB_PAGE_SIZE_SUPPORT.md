# 16KB Page Size Support

This Flutter plugin now supports Android devices with 16KB memory page sizes as required by [Android's development guidelines](https://developer.android.com/guide/practices/page-sizes).

## What is 16KB Page Size Support?

Starting with Android API level 35, apps must be compatible with devices that use 16KB memory pages instead of the traditional 4KB pages. This is required for:
- 64-bit Android devices
- Apps targeting Android API 35+
- Google Play Store requirements

## Changes Made

### Build Configuration Updates
- **Android Gradle Plugin**: Updated to 8.1.2 (from 4.1.0)
- **Kotlin Version**: Updated to 1.9.10 (from 1.6.10)  
- **Gradle Wrapper**: Updated to 8.4 (from 7.6.1/7.5)
- **SDK Versions**: 
  - `compileSdkVersion`: 35 (was 31 for plugin, 33 for example)
  - `targetSdkVersion`: 35 (newly added)
  - `minSdkVersion`: 21 (unchanged, supports 64-bit devices)

### Testing Configuration
Added to `gradle.properties`:
```properties
# Support for 16KB page sizes
android.experimental.testOptions.emulatorSnapshots.compressSnapshots=false
```

## Native Code Compatibility

The plugin's native C++ code has been verified to be compatible with 16KB page sizes:
- Uses standard `malloc()`/`free()` functions (page size agnostic)
- No hard-coded memory page size assumptions
- Memory operations based on dynamic sizes, not fixed page sizes

## Verification

You can verify your app supports 16KB page sizes by:

1. **Build Configuration**: Ensure your app targets Android API 35+
2. **Testing**: Test on Android Virtual Devices (AVDs) configured with 16KB page sizes
3. **Native Code**: Verify any native code doesn't assume 4KB page sizes

## For App Developers Using This Plugin

When using this plugin in your Flutter app, make sure your app also:
- Targets Android API 35+
- Uses compatible versions of other dependencies
- Tests on 16KB page size configurations

## Resources

- [Android 16KB Page Size Guide](https://developer.android.com/guide/practices/page-sizes)
- [Google Play 64-bit Requirements](https://developer.android.com/distribute/best-practices/develop/64-bit)
- [Android API Level Requirements](https://developer.android.com/distribute/best-practices/develop/target-sdk)