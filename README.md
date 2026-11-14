# Ghost Hunter Pro

Native Android field recorder built around the evidence-first product requirements in [`PRODUCT_SPEC.md`](PRODUCT_SPEC.md).

## Current app

A lightweight Java/Android starter app that discovers device magnetometer, accelerometer, gyroscope, ambient-light, and barometer sensors at runtime; displays live readings; records sensor samples with timestamps to an in-memory session; adds timestamped markers; and exports a CSV through Android's document picker. It is local-only and works without network access. Missing sensors are disclosed instead of simulated.

The app deliberately does not claim paranormal detection or communication. Sensor outputs describe physical measurements and can be affected by device and environmental conditions. It is not safety equipment.

## Build

Open this project in Android Studio with Android Gradle Plugin 8.7.3 and Android SDK 35 installed, then sync and run the `app` configuration on a physical Android device. Sensors differ by device; emulator readings are not representative. A Gradle wrapper is not included yet.

## Current limitations

This is the first implementation slice, not the complete product specified in `PRODUCT_SPEC.md`. Sessions currently live in memory and are lost if the process exits; there is no persistent case library, audio/video capture, PDF report, team sync, calibration workflow, or background recording service. Keep the app foregrounded during a session. These limitations should be addressed before presenting it as production-ready.
