# Ghost Hunter Pro

Native Android evidence-led field investigation recorder. Full product direction and safety/credibility requirements are in [`PRODUCT_SPEC.md`](PRODUCT_SPEC.md).

## Implemented

- Runtime discovery and live display for magnetometer, accelerometer, gyroscope, ambient light, and barometer when available; timestamped raw sensor log, foreground pause-gap markers, and local session history.
- Live environmental-change warning: after a ten-second in-session magnetometer baseline, three consecutive readings at least max(12 µT, 5 baseline standard deviations) away from the reference show a banner and toast, and add a timestamped event to the session log. The warning explicitly describes a sensor change, lists common interference/movement explanations, and is not a paranormal verdict. A 30-second cooldown prevents alert spam.
- Timestamped investigator observations, session/case/site/team roster details, local audio recording (explicit runtime microphone permission), and photo/video capture through the Android camera app to user-visible media storage.
- Five-second magnetometer quality check and documented software baseline; not certified calibration.
- PDF investigation report with case/device/method metadata, timeline events, descriptive first-axis sensor statistics, media index, limitations, and no automated paranormal verdict.
- CSV export and ZIP case-bundle export with original local audio and referenced camera media, report, and SHA-256 integrity manifest. Bundle export offers Android's system share sheet.
- Local-first, no account and no network requirement; no paranormal detection or communication claims.

## Build

Open in Android Studio with Android Gradle Plugin 8.7.3 and Android SDK 35 installed; run the `app` configuration on a physical Android device. The Android CI workflow builds a debug APK on pull requests and produces a version-tag release asset. Sensors/cameras vary; test on target devices.

## Known scope limits

Team support is an on-device roster and user-initiated case-bundle sharing, not cloud sync, invitations, access revocation, or real-time multi-device collaboration. Camera capture is delegated to the device's installed camera app; app-owned audio stops when the app backgrounds. Sensor capture is foreground-only and records explicit suspension/resume events, not a background-service guarantee. There is no external certified instrument integration, GPS capture, or production signing configuration. The published CI APK is an unsigned debug/development build. Treat the app as an investigation recorder, not certified scientific or safety equipment.
