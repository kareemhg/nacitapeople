# NACITA People — Android app (WebView wrapper)

This is a ready-to-build Android app that opens the NACITA People portal
(`https://nacitapeople.com/points/`) as a full-screen mobile app. It supports
login/session cookies, file uploads (attendance import, profile photo),
file downloads (Excel/PDF exports), pull-to-refresh, and the hardware Back
button for in-app navigation.

> The `.apk` itself is **not** included because it must be compiled with the
> Android SDK. Follow the steps below to produce the APK — it's one click in
> Android Studio.

---

## Option A — Build in Android Studio (recommended, ~10 min)

1. Install **Android Studio** (free): https://developer.android.com/studio
2. Unzip this folder somewhere, e.g. `C:\NacitaPeopleApp`.
3. Android Studio → **Open** → select that folder → wait for **Gradle sync**
   (it downloads the Android SDK + Gradle automatically the first time).
4. Build the installable APK:
   - **Build ▸ Build Bundle(s) / APK(s) ▸ Build APK(s)**
   - When it finishes, click **locate** in the popup.
   - The file is: `app/build/outputs/apk/debug/app-debug.apk`
5. Copy `app-debug.apk` to any Android phone and open it. Allow
   **Install from unknown sources** when prompted. Done.

The debug APK is fine for internal company distribution (sideloading).

## Option B — Command line

From the project folder, after Android Studio has set up the SDK once:

```
./gradlew assembleDebug            # Windows: gradlew.bat assembleDebug
```

Output: `app/build/outputs/apk/debug/app-debug.apk`

---

## Making a signed RELEASE APK (for wider distribution / Play Store)

1. In Android Studio: **Build ▸ Generate Signed Bundle / APK ▸ APK**.
2. Create a new **keystore** (keep the `.jks` file and passwords safe — you
   need the same key for every future update).
3. Choose **release**, finish. Output:
   `app/build/outputs/apk/release/app-release.apk`

(The project is pre-set to sign `release` with the debug key so it builds out
of the box; replace that with your own keystore for a real release — see the
commented `signingConfig` note in `app/build.gradle`.)

---

## Changing things

- **Portal URL / allowed host**: `app/src/main/java/com/nacita/people/MainActivity.java`
  — `START_URL` and `APP_HOST` at the top.
- **App name**: `app/src/main/res/values/strings.xml` (`app_name`).
- **App icon**: replace the PNGs in `app/src/main/res/mipmap-*` (or use
  Android Studio ▸ right-click `res` ▸ New ▸ Image Asset).
- **Brand colors / status bar**: `app/src/main/res/values/colors.xml`.

## Requirements
- Android Studio (bundles the Android SDK, build-tools, and a compatible JDK).
- Minimum phone: Android 6.0 (API 23) and up.
- The app loads the live site, so the phone needs internet; nothing is stored
  on a server by the app itself.
