# Expo SDK 53 + AGP 8.5.1 + Gradle 8.7 Repro

This repository demonstrates a build failure when using **Expo SDK 53** with **Android Gradle Plugin 8.5.1** and **Gradle 8.7**.

## Steps to Reproduce
1. `npx create-expo-app expo-agp85-gradle87-repro`
2. `cd expo-agp85-gradle87-repro`
3. `npm install expo@~53.0.7`
4. `npx expo prebuild --platform android`
5. Update `android/build.gradle` to use AGP 8.5.1:
   ```gradle
   dependencies {
       classpath("com.android.tools.build:gradle:8.5.1")
   } ```
6. Update android/gradle/wrapper/gradle-wrapper.properties to use Gradle 8.7:
```
distributionUrl=https\://services.gradle.org/distributions/gradle-8.7-all.zip
```
8. Run:
```
cd android
./gradlew clean
```

### Actual

Kotlin compile fails inside expo-modules-autolinking:
```
> Task :expo-gradle-plugin:expo-autolinking-settings-plugin:compileKotlin FAILED
e: .../expo-modules-autolinking/.../SettingsManager.kt:24:28 Unresolved reference: extensions
e: .../expo-modules-autolinking/.../SettingsManager.kt:112:15 Unresolved reference: extra
```

## Environment
- Expo SDK: 53.0.7
- React Native: 0.79.x
- Android Gradle Plugin: 8.5.1
- Gradle: 8.7
- JDK: 21
- Node: 20.19.x
