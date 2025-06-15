# Muhiyudheen Juma Masjid (Prayer Notifier)

A simple app for mosques to notify users of Adhan and Iqamah prayer times.

## Overview

* **Admin Interface**: Mosque representatives log in with an admin password (stored in a local `Config` file, excluded from Git) to upload weekly prayer and Iqamah schedules to Firebase Firestore.
* **End User**: Automatically retrieves the schedule for the week and sets up notifications:

  * **iOS**: Schedules all notifications at once, for a week, using zoned schedules.
  * **Android**: Caches the week’s entries locally and uses AlarmManager (`alarmClock: true`) to schedule only the next upcoming prayer. On each alarm trigger, the next one is scheduled in a background isolate.

## Features

* **Firebase Backend**: Secure upload of prayer times by mosque admin.
* **Exact Alarms on Android**: Uses `SCHEDULE_EXACT_ALARM` + `alarmClock` to ensure timely notifications.
* **Battery Optimization Exemption**: Requests to ignore optimizations on aggressive OEM ROMs.
* **Timezone Aware on iOS**: Uses `flutter_local_notifications` zoned schedules.
* **Lightweight**: No analytics or personal data collection.

## Getting Started

1. **Clone the repo**

   ```bash
   git clone https://github.com/YourOrg/mosque_prayer_notifier.git](https://github.com/cilyde/Muhiyudheen_Juma_Masjid.git
   cd muhiyudheen_juma_masjid
   ```
2. **Add Config**
   Create `lib/config.dart` (ignored by Git) containing easily configurable properties.:
 ```dart
    class Config {
  static String logoMain = "assets/images/logoMain.PNG";
  static String logoCompact = "assets/images/logoCompact.PNG";

  static String masjidName = "Muhiyudheen Juma Masjid";
  static String masjidLocation = "Antartica";
  static String masjidAddress = "Near Antartica";

  static Color accentColor = Colors.green;

  static bool darkTheme = true;

  static String adminPassword = "123";

  static bool showExportLogsButton=false;
}
   ```

3. **Install dependencies**

   ```bash
   flutter pub get
   ```
   
4. **Run the app**

   ```bash
   flutter run
   ```

## Permissions

* `INTERNET`, `ACCESS_NETWORK_STATE` — fetch/prune schedules.
* `SCHEDULE_EXACT_ALARM` — schedule exact alarms on Android.
* `WAKE_LOCK` — keep CPU awake for alarms.
* `RECEIVE_BOOT_COMPLETED` — re-schedule alarms on reboot.
* `REQUEST_IGNORE_BATTERY_OPTIMIZATIONS` — request exemption on aggressive OEM ROMs.
* `POST_NOTIFICATIONS` — show notifications on Android 13+.

## Folder Structure

```
lib/
├── Models/ # Data classes and model definitions (e.g. NotificationEntry)
├── Services/ # Handles Firebase and alarm logic (e.g. FirestoreService, Alarm scheduling)
├── ViewModels/ # Manages state and business logic (MVVM pattern)
├── Views/ # UI code including Home screen and Admin upload
├── Config.dart # App-wide configuration (e.g. admin password, theme)
├── firebase_options.dart# Firebase initialization settings
└── main.dart # Entry point of the app
```

## Admin Usage

* Launch app and open the side menu.
* Tap **Admin Login**, enter the admin password.
* Use **Upload Schedule** to push a week of prayer times to Firebase.

## Deployment to Play Store

1. Configure release keystore in `android/app/build.gradle`.
2. Build AAB:

   ```bash
   flutter build appbundle --release
   ```
3. Upload to Play Console production track.
4. Add store listing, screenshots, feature graphic, privacy policy URL.
5. Declare sensitive permissions (exact alarms, battery exemption) and justify in the console.

## Privacy Policy

See [PRIVACY\_POLICY.md](PRIVACY_POLICY.md) for full details.


## 6. Contact Us

Questions? Email ** cilydestudios@gmail.com **.
