# KK Scanner — Android cloud build

This repository packages the supplied KK Scanner static web app inside a Capacitor Android shell.

## What the workflow produces

- Always: a **debug APK** for installation/testing (`app-debug.apk`).
- After configuring the four signing secrets: a **signed release APK** and **signed AAB** suitable for Play Console review/upload.

An AAB is not generated as a Play-ready signed artifact until a persistent upload/release keystore is configured. Keep that keystore and its passwords backed up securely. Do not commit the keystore or passwords to the repository.

## Build from a phone

1. Create a **private** GitHub repository named `KK-Scanner`.
2. Extract this ZIP and upload all its contents (including the hidden `.github` folder) to the repository root. In GitHub mobile browser, enable desktop site if needed.
3. Open **Actions** → **Build KK Scanner Android** → **Run workflow**.
4. Wait for the workflow to finish. Open the run and download `kk-scanner-android-build` under Artifacts. The debug APK is for testing only.
5. Before Play Store release, create a persistent Android keystore and add these repository Actions secrets: `ANDROID_KEYSTORE_BASE64`, `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_ALIAS`, `ANDROID_KEY_PASSWORD`. Then run the workflow again; it will produce signed release APK and AAB.

## Important app checks

The source uses the browser camera (`getUserMedia`) and IndexedDB. Test camera permission, image capture, PDF export, backup/restore, offline startup, and privacy-policy navigation on a real Android device. This ZIP is a build scaffold, not proof that every native WebView feature has passed device testing.

Package ID is `com.kk.scanner`. Choose it carefully: changing it after publishing creates a different Play Store app.
