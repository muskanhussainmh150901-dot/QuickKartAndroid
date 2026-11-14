# QuickKart Android starter

A starter Android app for the QuickKart Noida quick-commerce prototype.

## Included
- Kotlin + Jetpack Compose Android app
- Home screen with category filters and product search
- Sample grocery catalogue
- Add/remove cart quantities and cart total
- Demo checkout and demo order screen

## Open in Android Studio
1. Download and unzip this project.
2. Open Android Studio and choose **Open**.
3. Select the `QuickKartAndroid` folder.
4. Allow Gradle sync to finish.
5. Run on an Android emulator or a connected Android phone.

## Important
This is a UI prototype. It does not yet connect to a backend, real inventory,
customer accounts, maps/GPS, payment gateway, delivery partner app, or live order
tracking. Product names and prices are sample data. The 10–30 minute delivery
message is a target, not a guaranteed service level.

## Suggested next build stages
1. Backend/API and database (products, stock, customers, orders)
2. Admin dashboard and inventory tools
3. Payment gateway integration and COD workflow
4. Delivery partner app, GPS and order status updates
5. Security, testing, privacy policy and Play Store release preparation

## Mobile number + OTP login (Firebase Phone Auth)

The app now includes a phone-number login screen, OTP entry, Firebase phone
verification callbacks, authenticated session gating, and logout.

### One-time Firebase setup required before real OTP can work

1. Create a Firebase project at https://console.firebase.google.com/.
2. Add an Android app with package name `com.quickkart.app`.
3. Download that app's `google-services.json` and place it in `app/` (same folder as `app/build.gradle.kts`). Do not share this file publicly.
4. In Firebase Console, open **Authentication → Sign-in method** and enable **Phone**.
5. In Firebase project settings, add the app's SHA-1 and SHA-256 signing certificate fingerprints. For local debug builds, get them with `./gradlew signingReport` (or Android Studio's Gradle signingReport task).
6. For safe testing, configure Firebase Authentication test phone numbers and OTPs in the Firebase Console. Real SMS delivery is subject to Firebase limits, supported regions, and verification checks.
7. Sync Gradle and run the app. Enter the number in international format, e.g. `+91XXXXXXXXXX`.

Until `app/google-services.json` is added and Phone sign-in is enabled, the app intentionally displays a Firebase setup message instead of pretending to send a real OTP. Never hard-code OTPs or Firebase service credentials in the app.

### Build APK

After Firebase setup, open this folder in Android Studio, sync Gradle, then choose **Build → Build Bundle(s) / APK(s) → Build APK(s)**. The debug APK is normally generated at `app/build/outputs/apk/debug/app-debug.apk`.

This source archive is not itself an APK. A signed release APK also requires your own release signing key. Test authentication on a real device before launch.

## Build APK online using a phone (GitHub Actions)

This project includes `.github/workflows/android-apk.yml` for a cloud debug build.
1. Create a GitHub account and a new **public or private** repository named `QuickKartAndroid`.
2. In the repository, use **Add file → Upload files** and upload the extracted project contents (the files inside the `QuickKartAndroid` folder, including the hidden `.github` folder). Commit to the `main` branch.
3. Open the repository's **Actions** tab. Select **Build QuickKart Android APK** and tap **Run workflow** if it has not started automatically.
4. Wait for the run to finish successfully. Open that run, scroll to **Artifacts**, and download `QuickKart-debug-apk`.
5. Extract the downloaded artifact ZIP and install `app-debug.apk` on your Android phone.

This workflow builds a debug APK. For real SMS OTP, first add your own Firebase `google-services.json` to `app/`, enable Phone sign-in in Firebase, and configure the app's SHA fingerprints/test numbers. Do not publish Firebase configuration or signing keys in a public repository. A debug build without Firebase configuration will show the Firebase setup message and cannot send real OTPs.
