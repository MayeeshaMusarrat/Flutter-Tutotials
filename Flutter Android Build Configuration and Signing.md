
# Android Build Configuration, App Signing, and ProGuard (My app name was FlutterFly)

For the last few days, I have been studying about build configuration, product flavors, app signing, and ProGuard. These elements help manage different app versions (e.g., development vs. production), ensure secure signing for Play Store distribution, and optimize the app’s size.

Here are some interesting things I learned:

* Before publishing on the Play Store, Android requires your app to be digitally signed with a unique keystore. This prevents others from modifying your app and ensures authenticity.
* ProGuard removes unused code and obfuscates sensitive code, making it:

  1. Smaller
  2. Harder to reverse-engineer

---

## How I Signed My App

* Generated keystore using `keytool` command in the terminal (under `android/app/`)

  * **Command:**

    ```bash
    keytool -genkeypair -v -keystore flutterfly_keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias flutterfly
    ```
* Entered required information in the terminal
* `flutterfly_keystore.jks` file is generated
* Created a `key.properties` file inside the `android/` folder and stored the keystore details
* These credentials are then used under `signingConfigs` in `android/app/build.gradle` directory

  * The `signingConfigs` block reads the key information from `key.properties`. If the file exists, it applies the key automatically when building a release version
* Set `minifyEnabled` and `shrinkResources` to *true* under the `buildTypes` block in the same directory
* Created a `proguard-rules.pro` file under `android/app/`
* Since I have three flavors (**dev**, **prod**, and **staging**), and I wanted to create an app bundle file for **prod** only, I ran the following commands:

  ```bash
  flutter clean
  flutter build appbundle --flavor prod
  ```
* Verified my app signing by running:

  ```bash
  jarsigner -verify -verbose -certs build/app/outputs/bundle/prodRelease/app-prod-release.aab
  ```

  * It said `"jar verified."` for correct setup.
  * You can set minifyEnabled and shrinkResources to false, and check the before and after app sizes in .aab files. My .aab path is `build/app/outputs/bundle/prodRelease/app-prod-release.aab`

> ⚠️ **Warning:** Don't try to store secrets in `gradle.properties`. GitGuardian flagged my code 😦

You can check out my repo as a reference! 

https://github.com/Learnathon-By-Geeky-Solutions/flutterfly/tree/main

And here are the blogs I looked up:

[1] https://dev.to/teerasej/step-by-step-to-publish-your-flutter-project-as-andriod-app-bundle-1bpe

[2] https://medium.com/@ChanakaDev/simplifying-android-proguard-rules-in-flutter-apps-2bfa6a1d5e68 


---
