# Development environment inventory

Observed 2026-10-04 using read-only checks. No installation, build, emulator, server, device connection, or license acceptance occurred. `adb` and Gradle were not executed.

## Repository

The repository contains discovery documents and ADRs, with no Android application source, Gradle build files, wrapper, or manifest. Git reports untracked `.scratch/`, `CONTEXT.md`, and `docs/adr/`; no tracked modifications appeared. Existing work was preserved. Root `AGENTS.md` requires direct feedback, local Markdown issues, and domain terminology/decisions in `CONTEXT.md` and `docs/adr/`.

## Available tools

- Host architecture: `arm64`.
- `/usr/bin/java` and `/usr/bin/javac` resolve to OpenJDK **18.0.2**, confirmed with version commands. `java_home -V` identifies its home under `$HOME/Library/Java/JavaVirtualMachines/openjdk-18.0.2/Contents/Home`.
- Java's registry also includes ARM64 JDK **17.0.1** at `/Library/Java/JavaVirtualMachines/jdk-17.0.1.jdk/Contents/Home`, plus older installations.
- Homebrew OpenJDK **25** is present at `/opt/homebrew/opt/openjdk/libexec/openjdk.jdk/Contents/Home`, confirmed from its release metadata; it is not the active command-line Java.
- `/opt/homebrew/bin/gradle` points to `/opt/homebrew/Cellar/gradle/9.1.0/bin/gradle`; its executable and versioned launcher JAR exist. This establishes installed files, not working Android-build compatibility.

## Not found in checked locations

`sdkmanager`, `adb`, `emulator`, and `avdmanager` were not on PATH. `ANDROID_HOME` and `ANDROID_SDK_ROOT` were unset. No SDK was found at `~/Library/Android/sdk`, `/Library/Android/sdk`, or conventional Homebrew Android SDK/command-line-tools locations. Android Studio was absent from `/Applications`, `~/Applications`, and its Homebrew cask path. `~/.android/avd` exists but is empty. These are bounded checks, not proof that no custom installation exists elsewhere.

## Before compilation and testing

Establish an Android SDK/tooling installation and required SDK packages/licenses; select a compatible JDK/Android Gradle Plugin/Gradle/dependency combination and create a pinned project wrapper. Emulator testing would additionally need an emulator and TV system image. Physical testing needs the user's Google TV model/OS and an agreed installation/debugging connection. None was selected or exercised here.
