# Kiebord (DrutoPost Edition)
<p align="center">
<img width="128" height="128" alt="Kiebord" src="https://github.com/user-attachments/assets/346d3099-7f42-462a-931c-959a216ebccc" />
</p>

<table>
  <tr>
<td><img width="512" alt="borno-phonetic" src="https://github.com/user-attachments/assets/35c84108-40bb-4f04-99e7-04c9f9d58019" /></td>
<td><img width="512" alt="national" src="https://github.com/user-attachments/assets/ce2f1910-4eb1-4d67-8f2b-b00b0153ae72" /></td>
  </tr>
</table>

[![CI Build](https://github.com/JayedAhsan/Kiebord/actions/workflows/publish.yml/badge.svg?branch=main)](https://github.com/JayedAhsan/Kiebord/actions/workflows/publish.yml)
[![Latest Release](https://img.shields.io/github/v/release/JayedAhsan/Kiebord?include_prereleases&label=Latest%20Release)](https://github.com/JayedAhsan/Kiebord/releases)
[![Android](https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2024%2B)-blue)](https://developer.android.com)
[![Rust](https://img.shields.io/badge/Engine-Rust%20NDK-orange)](https://www.rust-lang.org)
[![Kotlin](https://img.shields.io/badge/UI-Jetpack%20Compose-purple)](https://developer.android.com/jetpack/compose)
[![License](https://img.shields.io/badge/License-GPL%203.0-green.svg)](https://www.gnu.org/licenses/gpl-3.0)

A high-performance, open-source input method editor (IME) for Android built with Jetpack Compose and a native Rust engine, maintained and remastered by **DrutoPost**.

---

## Highlights & Enhancements

* **Language-Specific Typefaces**:
  * **Bangla Mode**: Typeset using the bespoke **Bornomala** font for clear glyph rendering and authentic script ergonomics.
  * **Arabic Mode**: Typeset using the elegant **Scheherazade** font with dedicated Harakat and diacritics support.
  * **English / Symbols**: Crisp typography powered by the standard keyboard font family.
* **Streamlined Bottom Row**: Removed the globe key beside the spacebar across all layout configurations to grant an expanded, spacious spacebar for maximum typing comfort and ergonomic thumb gestures.
* **Minimalist & Distraction-Free Settings**: Streamlined preference experience focusing purely on typing customization, keyboard layouts, gestures, and theme aesthetics.
* **Production-Ready Release Workflow**: Automated release pipeline with pre-configured signing support and demo keystore credentials for seamless APK generation.

---

## Features

### Supported Layouts

| Language | Layouts |
|---|---|
| Bangla | Borno Phonetic, Avro Phonetic, Borno Easy, National (BSTI), Probhat, Khipro |
| English | QWERTY, Borno Math |
| Arabic | Arabic (with dedicated Harakat / diacritics row) |

*Custom layouts can also be added by placing JSON layout files in `assets/layouts/`.*

### Input & Editing
* **Gesture Typing**: Glide-to-type capability across supported layouts.
* **Smart Predictions**: On-device candidate completions and next-word suggestions.
* **Spacebar Trackpad & Delete Gestures**: Slide across the full-width spacebar to navigate the cursor; slide left from the backspace key to swiftly erase words.
* **Sandboxed Clipboard**: In-memory clip manager with pin/unpin support and auto-expiration options.
* **Text Editing Panel**: Dedicated directional arrows, text selection handles, copy, cut, paste, undo, and redo.
* **Emoji Picker**: Integrated emoji panel with search and category navigation.
* **Voice Typing**: Direct speech-to-text input via the system voice recognizer.
* **One-Handed Mode & Resizing**: Toggleable left/right one-handed modes and adjustable keyboard height.
* **Haptic Feedback**: Keypress vibration support.
* **Dynamic Themes**: Beautiful light, dark, and blurred gradient themes with complete Theme Designer support.

---

## Project Structure

```
kiebord/
├── app/                  # Application entry point, onboarding, and settings UI
├── core/
│   ├── common/           # Shared models (KeyDef, KeyType, etc.)
│   ├── data/             # Preferences datastore and layout repositories
│   └── theme/            # Theme models, theme parser, and custom fonts (Bornomala, Scheherazade)
├── feature/
│   ├── ime/              # InputMethodService implementation, Compose canvas, and JNI bindings
│   └── themedesigner/    # Theme studio and interactive color customizer
├── native/
│   └── kiebord-engine/   # Rust native library (spatial model, trie dictionaries, BornoTSF)
└── docs/                 # Layout and theme development specifications
```

---

## Building from Source

### Prerequisites
* JDK 17 or 21
* Android SDK Platform 35 or 36
* Android NDK `26.2.11394342`
* Rust 1.75+ with `cargo-ndk` (for compiling native Rust libraries)

### Build Commands

Clone the repository:
```bash
git clone https://github.com/drutopost/kiebord.git
cd kiebord
```

Build the debug APK:
```bash
./gradlew assembleDebug
```

Build the signed release APK:
```bash
./gradlew assembleRelease
```

Build the release Android App Bundle (for Google Play):
```bash
./gradlew bundleRelease
```

Native Rust sources (`kiebord-engine`) can be compiled manually to generate `libborno_engine.so`:
```bash
cd native/kiebord-engine
cargo ndk -t arm64-v8a -t armeabi-v7a -t x86_64 -o ../../feature/ime/src/main/jniLibs build --release
```

---

## Keystore & Signing Configuration

For local development and automated CI workflows, a demo keystore based on company **DrutoPost** is included:
* **Keystore Location**: `app/drutopost-demo.jks`
* **Keystore Password**: `drutopost123`
* **Key Alias**: `drutopost`
* **Key Password**: `drutopost123`

To build release APKs using custom production keys, specify the following environment variables:
* `KEYSTORE_FILE`: Absolute path to your `.jks` or `.keystore` file
* `KEYSTORE_PASSWORD`: Keystore password
* `KEY_ALIAS`: Key alias
* `KEY_PASSWORD`: Key password

---

## Organization & Credits

* **Remastered By**: [DrutoPost](https://drutopost.com)
* **Original Project**: [Kiebord](https://github.com/JayedAhsan/Kiebord) by Jayed Ahsan Saad ([Codepotro](https://codepotro.com))

---

## License

This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**. See the `LICENSE` file for the full license text.
