# Smart Toolkit - All in One

**Smart Toolkit** is a production-ready, modern Android utility application built with Flutter & Material 3. It bundles **10 essential offline and mostly-offline everyday utilities** into a unified, high-performance, responsive experience designed for Android phones and tablets.

---

## 🛠️ The 10 Essential Utilities

1. **Photo Compressor**:
   - Single & batch compression with custom quality slider (10% - 100%).
   - Presets: High Quality (85%), Medium (65%), Small Size (45%), Under 1 MB, Under 500 KB.
   - Shows original file size, compressed size, percentage saved, and before/after comparison.
   - Saves directly to local storage and supports native Android file sharing.

2. **Photo Resizer**:
   - Resize images by width, height, or scaling percentage.
   - Popular presets: 1920px (Full HD), 1280px (HD), 1080px (Square), 720px, 480px, WhatsApp DP (500x500), Profile Avatar (400x400), Email (800x600).
   - Aspect ratio lock toggle and instant dimension estimation.

3. **Watermark Photo**:
   - Add text watermarks with custom font size, color, opacity, and rotation (-45° to +45°).
   - Overlay logo/image watermarks with transparency.
   - Corner placement presets (Top-Left, Top-Right, Center, Bottom-Left, Bottom-Right).
   - Hardware-accelerated composite rendering with preview and export.

4. **Image to PDF**:
   - Convert single or multiple images into a multi-page PDF document.
   - Reorder pages via drag-and-drop, rotate pages by 90°, and delete unwanted pages.
   - Page formats: A4, US Letter, or Original image aspect ratio.
   - Portrait and Landscape orientation controls with quality compression.

5. **Document Scanner PDF**:
   - Capture paper documents with the camera or import from photos.
   - Document enhancement filters: Original, Enhanced (Color & contrast boost), Grayscale, High-contrast Black & White (thresholding).
   - Multi-page document compilation and one-click export to PDF.

6. **Video Compressor**:
   - On-device video compression with background processing (non-blocking UI).
   - Presets: High Quality, Medium Quality (Balanced), and Small Size.
   - Real-time progress percentage and cancellation support.
   - Compression savings calculation, local save, and instant sharing.

7. **QR Scanner**:
   - High-speed camera scanner with automatic recognition of URLs, Wi-Fi credentials, Email, Phone, and vCard Contacts.
   - Flashlight/torch toggle and front/back camera flip.
   - Direct action triggers (open link, dial phone, copy to clipboard).
   - Persistent local scan history with search and management.

8. **QR Generator**:
   - Generate offline QR codes for Website URLs, Plain Text, Wi-Fi configuration, Email, Phone, and vCard contacts.
   - Customizable foreground and background colors.
   - Adjustable QR dimensions and Error Correction Levels (L, M, Q, H).
   - Export as high-resolution PNG image and native share.

9. **Text to QR Code**:
   - Streamlined rapid generator for converting any text snippet or link into a QR code.
   - Color styling themes and single-tap Save/Share.

10. **File Size Calculator**:
    - Dual-standard conversion: Binary (1024) and Decimal (1000).
    - Real-time conversion across B, KB, MB, GB, and TB.
    - Built-in Download Time Estimator calculating hours, minutes, and seconds based on file size and internet connection speed (Mbps / MB/s).

11. **Unit Converter**:
    - 10 complete categories: Length, Weight, Temperature, Area, Volume, Speed, Time, Data, Pressure, Energy.
    - Two-way unit swapping and instant offline calculations.

---

## 🎨 Design & Architecture

- **Material 3 UI**: Follows Google Material Design 3 guidelines with rounded cards (16px), elevation tints, curated color palette, and smooth micro-animations.
- **Dynamic Theming**: Seamless Light, Dark, and System Default theme switching.
- **Privacy & Offline First**: All media processing runs locally on the device via Dart compute isolates. User photos, videos, and scanned files are NEVER uploaded to external servers.
- **Onboarding Flow**: 3-page introduction saved to persistent preferences so returning users go directly to the dashboard.
- **Favorites & Search**: Pin frequently used utilities and search through tools dynamically.

---

## 💰 AdMob Monetization Setup

The app is built with a non-intrusive AdMob strategy compliant with Google Play policies:
- **Banner Ads**: Displayed at the bottom of the home screen and utility screens.
- **Interstitial Ads**: Shown occasionally after significant completed operations (rate-limited, never interrupting active user actions).
- **Rewarded Ads**: Optional VIP unlock mechanism for advanced operations.

### Configuring AdMob IDs

By default, the project uses **Google's official Test Ad Unit IDs** to ensure zero policy violations and crash-free local development.

To switch to your production AdMob IDs:

1. **Ad Units (`lib/ads/ad_helper.dart`)**:
   Open `lib/ads/ad_helper.dart` and replace the placeholder IDs:
   ```dart
   class AdHelper {
     // Set to false for production Play Store release
     static const bool isTestMode = false;

     static const String _prodBannerId = 'ca-app-pub-XXXXXXXXXXXXXXXX/YYYYYYYYYY';
     static const String _prodInterstitialId = 'ca-app-pub-XXXXXXXXXXXXXXXX/YYYYYYYYYY';
     static const String _prodRewardedId = 'ca-app-pub-XXXXXXXXXXXXXXXX/YYYYYYYYYY';
   }
   ```

2. **Android Application ID (`android/app/src/main/AndroidManifest.xml`)**:
   Update the AdMob App ID meta-data tag:
   ```xml
   <meta-data
       android:name="com.google.android.gms.ads.APPLICATION_ID"
       android:value="ca-app-pub-XXXXXXXXXXXXXXXX~YYYYYYYYYY"/>
   ```

---

## 📱 Permissions

The application requests only necessary permissions at runtime:
- `CAMERA`: Used exclusively for QR scanning and Document Scanner image capture.
- `READ_MEDIA_IMAGES` / `READ_MEDIA_VIDEO` / `READ_EXTERNAL_STORAGE`: Used to select photos/videos for compression, resizing, and watermarking.
- `INTERNET`: Required for Google AdMob SDK.

---

## 🚀 How to Build & Run

### Prerequisites
- Flutter SDK (v3.24+ recommended, tested on Flutter 3.47 / Dart 3.13)
- Android SDK (API 34/35)
- Java 17

### 1. Install Dependencies
```bash
flutter pub get
```

### 2. Verify Code Quality
```bash
flutter analyze
flutter test
```

### 3. Run Locally in Debug Mode
```bash
flutter run
```

### 4. Build Release APK
```bash
flutter build apk --release
```
The output APK will be located at:
`build/app/outputs/flutter-apk/app-release.apk`

### 5. Build Release Android App Bundle (AAB) for Google Play
```bash
flutter build appbundle --release
```
The output AAB will be located at:
`build/app/outputs/bundle/release/app-release.aab`

---

## 📦 Google Play Store Publishing Guide

1. **Create Keystore for App Signing**:
   ```bash
   keytool -genkey -v -keystore my-release-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
   ```
2. **Configure `android/key.properties`**:
   ```properties
   storePassword=<your-password>
   keyPassword=<your-password>
   keyAlias=my-key-alias
   storeFile=<path-to-my-release-key.jks>
   ```
3. **Set Production AdMob IDs**: Update `lib/ads/ad_helper.dart` (`isTestMode = false`) and `AndroidManifest.xml`.
4. **Build Bundle**: Run `flutter build appbundle --release`.
5. **Upload to Google Play Console**:
   - Create app on [Google Play Console](https://play.google.com/console).
   - Upload `app-release.aab`.
   - Provide Privacy Policy URL (copy from in-app Privacy Policy screen).
   - Complete Data Safety form indicating photos/videos are processed locally on device and advertising ID is used by Google Mobile Ads.
   - Submit for review!

---

## 📄 License

Smart Toolkit - All in One Utility Application. All rights reserved.
