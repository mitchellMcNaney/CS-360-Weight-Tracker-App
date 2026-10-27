# Android Weight Tracker

A native Android application for recording daily weight measurements, setting personal goals, and reviewing progress over time. Built in **Java** with **SQLite**, this project began as a mobile development course assignment and was subsequently enhanced with a more modular architecture, progress analytics, and stronger password storage.

## Features

- **Accounts:** Create an account, sign in, and update account information.
- **Weight tracking:** Add, update, and delete weight entries stored locally in SQLite.
- **Goals:** Set a target weight and compare it with recorded progress.
- **Progress analytics:** Calculate moving averages, recent weight trends, daily logging streaks, weight changes, an estimated time to a goal, and potential plateaus.
- **SMS notifications:** Optional goal-related text messaging, subject to Android permissions and device support.

## Tech stack

- Java and Android SDK
- Android Studio and Gradle
- SQLite for on-device persistence
- Argon2id for new password hashes, with verification and upgrade support for legacy PBKDF2 credentials
- XML layouts for the Android user interface

## Project structure

```text
app/src/main/
├── java/com/example/mcnaneyprojectone/
│   ├── LoginActivity.java
│   ├── Home.java
│   ├── Progress.java
│   ├── Account.java
│   ├── SmsPermissionsActivity.java
│   ├── database/DatabaseHelper.java
│   ├── model/                # User, WeightEntry, Goal
│   ├── security/PasswordUtils.java
│   ├── service/              # User, Weight, Goal, Analytics, Notification
│   └── util/DateFormats.java
├── res/                      # Layouts, themes, and other resources
└── AndroidManifest.xml
```

The app separates screen logic from reusable services and data models. `DatabaseHelper` manages SQLite storage, while `AnalyticsService` performs calculations independently of the UI and database layers.

## Notable enhancements

### Architecture

Refactored the original application to separate account management, weight entries, goals, notifications, and analytics into dedicated services and models. This makes the code easier to navigate and extend.

### Algorithms and analytics

Added calculations for moving averages, trend classification, logging streaks, goal estimates, and plateau detection. The analytics layer operates on weight-entry data without requiring Android UI components.

### Data and password security

Introduced salted Argon2id password hashing for new credentials. The application also supports verification of older PBKDF2 hashes and migration after successful authentication. SQLite schema upgrades preserve existing data where supported.

## Getting started

1. Clone or download this repository.
2. Open the project root in **Android Studio**.
3. Allow Gradle to sync and download dependencies.
4. Run the `app` configuration on an Android emulator or device with **Android 14 (API 34) or newer**.
5. Create a test account and begin logging sample weights.

The project targets Android API 36 and uses Java 11 source compatibility. SMS functionality requires appropriate permission and a compatible device; it may not work in a typical emulator.

## Current scope and limitations

This is a **portfolio and educational project**, not a production health application.

- Data is stored locally on the device; the project does not implement a cloud account or synchronization service.
- Goal-time estimates extrapolate historical weight changes and are not medical predictions.
- SMS functionality depends on device capabilities and user-granted permissions.
- The app retains compatibility paths for older password formats as part of its migration design.
- The included automated tests are starter examples rather than comprehensive coverage.
- Backup and session handling have not been hardened for a production release.

## Background

Originally developed for a mobile application development course, this app was revisited as a computer science capstone project. The enhancements focused on three areas: **software architecture**, **algorithms and data structures**, and **database/security practices**.

The repository demonstrates iterative improvement of an existing application rather than a complete rewrite.
