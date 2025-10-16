# Intercom Bug Reproduction (Expo + React Native)

This repository is a minimal Expo project created to reproduce a **bug with `@intercom/intercom-react-native`** versions 9.*.* when used with the **old React Native architecture**.

It was reported in this Intercom Community question: https://community.intercom.com/mobile-sdks-24/intercom-react-native-does-not-compile-for-expo-during-build-when-combined-with-other-packages-12960

This is NOT present when using version 8.8.0 of the React Native Intercom module, and thus introduced with the upgrade to the new package.
## 🧱 Stack

- **Expo SDK 52**
- **React Native (old architecture)**
- **@intercom/intercom-react-native**
- **@usercentrics/react-native-sdk**
- **config-plugin-react-native-intercom**
- **expo-build-properties**

## ⚙️ Setup

1. Install dependencies:
   ```bash
   yarn install
   ```
   Ensure Node version ≥ 20.19.4 (required by Metro):

```
nvm install 20.19.4 && nvm use 20.19.4

```

Prebuild native projects:

```
npx expo prebuild --clean

```

run:

```
yarn ios

```
assert that you can not build due to below issue.

## Bug description:

I’ve encountered a reproducible build issue on iOS when combining Intercom React Native v9.2.0 with @usercentrics/react-native-sdk.

✅ Works fine

- Intercom v9.2.0 alone → builds and runs on iOS.
- Usercentrics alone → builds and runs on iOS.

❌ Breaks when combined
When both dependencies are installed, the iOS build fails during compilation with errors like:

```
13 |
  14 | #ifndef __cplusplus
> 15 | #error This file must be compiled as Obj-C++. If you are importing it, you must change your file extension to .mm.
     |  ^ This file must be compiled as Obj-C++. If you are importing it, you must change your file extension to .mm.
  16 | #endif
  17 |
  18 | // Avoid multiple includes of IntercomReactNativeSpec symbols
```

```
'optional' file not found
'tuple' file not found
'utility' file not found
```
