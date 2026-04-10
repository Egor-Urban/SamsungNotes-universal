# Samsung Notes Patch for Non-Samsung Devices

This repository contains a patched version of **Samsung Notes** specifically modified to work on non-Samsung tablets and smartphones. Tested and confirmed working on **Redmi Pad Pro 12.1 (2024)**.

## 📱 Tested Device
* **Model:** Redmi Pad 2 Pro (POCO Pad equivalent)
* **System:** HyperOS (Android 16)

## 🛠 The Fix (Technical Details)
The original app expects the presence of Samsung's proprietary `SemFloatingFeature` class to identify the device brand when handling assets (like custom templates). On non-Samsung devices, this causes a `java.lang.NoClassDefFoundError`.

I have patched the `clinit` (static constructor) in `com.samsung.android.support.senl.nt.model.assist.common.C2paHandler` using Smali editing:
* Disabled the call to `Lcom/samsung/android/feature/SemFloatingFeature;->getInstance()`.
* Hardcoded the `CLAIM_GENERATOR` string to "Samsung" to satisfy the app logic.
* Prevented the crash during `downloadTemplateImage` and `onActivityResult` flows.

## 🚀 How to Install
1.  Download the APK from the [Releases](https://github.com/Egor-Urban/SamsungNotes-universal/releases/tag/4.4.37.35m) section.
2.  Uninstall any previous versions of Samsung Notes.
3.  Install the patched APK.
4.  (Optional) If you want to sync with Samsung Cloud, you may need a separate "Samsung Checkout" or "Samsung Account" stub/app depending on your ROM.

## ⚠️ Known Limitations
* **Sync:** Samsung Cloud sync might require additional Samsung services installed as system apps.
* **S-Pen Features:** Air Actions and specific S-Pen pressure sensitivity features are hardware-dependent and may not work on Xiaomi/Redmi styluses.

## ⚖️ Disclaimer
This is a modified version of a proprietary application. All rights belong to Samsung Electronics Co., Ltd. Use this patch at your own risk. I am not responsible for any data loss or issues caused by using this mod.

---
*If this patch helped you, feel free to give this repo a ⭐!*
