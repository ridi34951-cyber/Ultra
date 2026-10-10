# Kamera GyroLock V8 — Gyro-only stabilization

Android project for GitHub Actions APK builds. This version deliberately uses **only gyro-based stabilization**. If the gyro filter fails, the app reports the FFmpeg diagnostic and preserves the original recording; it does not silently switch to `deshake` or another fallback.

## Changes in V8
- Reduced FFmpeg's interpolated gyro trajectory points from 180 to 32 to reduce per-frame expression evaluation cost.
- Uses the `libx264` ultrafast preset at CRF 21 for faster encoding, with 30 FPS constant-frame-rate output.
- Computes the trajectory smoothing window in linear time instead of repeatedly scanning the same samples.
- Shows the actual FFmpeg error if gyro processing fails and keeps the original video untouched.

## Build APK
1. Upload the **contents** of this folder to a GitHub repository (not the ZIP itself).
2. Open **Actions** and run `Build Kamera GyroLock V8 APK`, or push to `main`/`master`.
3. Download `Kamera-GyroLock-V8-debug-apk` from the completed workflow's Artifacts section.

## Important
Gyroscope-based electronic stabilization depends on the phone's gyro sensor, camera orientation/timing alignment, and FFmpeg codec support. The app does not use image-based fallback. If the gyro command is unsupported on a device, it will report the reason instead of running a slow alternate filter. Test on short clips first; no APK build or on-device test can be claimed until GitHub Actions and a device test complete successfully.
