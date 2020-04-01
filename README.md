[![GitHub license](https://img.shields.io/github/license/mintware-de/flutter_barcode_reader.svg)](https://github.com/mintware-de/flutter_barcode_reader/blob/master/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/mintware-de/flutter_barcode_reader)](https://github.com/mintware-de/flutter_barcode_reader/stargazers)
[![Pub](https://img.shields.io/pub/v/barcode_scan.svg)](https://pub.dartlang.org/packages/barcode_scan)
[![GitHub forks](https://img.shields.io/github/forks/mintware-de/flutter_barcode_reader)](https://github.com/mintware-de/flutter_barcode_reader/network)

Fork of :
Hacked so full binary QR codes are returned in iOS (as they are in Android).
Previously they were truncated at the first 0x00 byte.
void startScan() in Classes/BarcodeScannerViewController.m modified so the full QR code is to be returned.
In older ios versions, the data may be available but it is probably a bad idea to access it this way.
There seems to be a 4 byte header and 20 bytes extra at the end. I've stripped off the header but left the 20 bytes at the end (for now).

# Barcode Scanner

A flutter plugin for scanning 2D barcodes and QR codes. 

This provides a simple wrapper for two commonly used iOS and Android libraries:

iOS: https://github.com/mikebuss/MTBBarcodeScanner

Android: https://github.com/dm77/barcodescanner

### Features
- [x] Scan 2D barcodes
- [x] Scan QR codes
- [x] Control the flash while scanning
- [x] Permission handling

## Getting Started

### Android
For Android, you must do the following before you can use the plugin:

* Add the camera permission to your AndroidManifest.xml
     
     `<uses-permission android:name="android.permission.CAMERA" />`

* This plugin is written in Kotlin. Therefore, you need to add Kotlin support to your project. See [installing the Kotlin plugin](https://kotlinlang.org/docs/tutorials/kotlin-android.html#installing-the-kotlin-plugin).

Edit your project-level build.gradle file to look like this:
```groovy
buildscript {
    ext.kotlin_version = '1.3.61'
    // ...
    dependencies {
        // ...
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
// ...
```

Edit your app-level build.gradle file to look like this:

```groovy
apply plugin: 'kotlin-android'
// ...
dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    // ...
}
```

Now you can depend on the barcode_scan plugin in your pubspec.yaml file:

```yaml
dependencies:
    # ...
    barcode_scan: any
```
Click "Packages get" in Android Studio or run `flutter packages get` in your project folder.

### iOS
To use on iOS, you must add the the camera usage description to your Info.plist

```xml
<dict>
    <!-- ... -->
    <key>NSCameraUsageDescription</key>
    <string>Camera permission is required for barcode scanning.</string>
    <!-- ... -->
</dict>
```


## Common problems
### Android "Could not find org.jetbrains.kotlin:kotlin-stdlib-jre..."
Change `org.jetbrains.kotlin:kotlin-stdlib-jre` to `org.jetbrains.kotlin:kotlin-stdlib-jdk`
([StackOverflow](https://stackoverflow.com/a/53358817))
