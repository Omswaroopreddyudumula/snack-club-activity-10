# Executed checks

Execution date: October 27, 2026 (America/New_York).

Environment: Flutter 3.47.2 stable, Dart 3.13.2, macOS arm64. Flutter doctor selected Android Studio's JDK 25.0.3. Android emulator tested: emulator-5554, sdk gphone16k arm64, Android 17 / API 37.

| Command | Observed result |
| --- | --- |
| `flutter --version` | Flutter 3.47.2 / Dart 3.13.2 |
| `flutter doctor -v` | Android licenses partly unaccepted; Xcode CocoaPods absent. Neither blocked this Android build/test. |
| `flutter devices` | Two Android emulators, macOS, Chrome detected. |
| `flutter emulators` | Activity09Fresh, Pixel_8, and iOS simulator listed. |
| `flutter create --platforms=android --org edu.example --project-name snack_club outputs/snack_club` | Succeeded, generated Android host including Gradle wrapper JAR/scripts. |
| `flutter pub get` | Succeeded. Newer incompatible dependency versions reported, lockfile retained. |
| `dart format lib test integration_test` | Succeeded. |
| `flutter analyze` (initial) | Two informational missing-braces findings. |
| `dart fix --apply` | Fixed those two findings. |
| `dart format lib test integration_test` (after fixes) | Succeeded. |
| `flutter analyze` (final) | No issues found. |
| `dart format --output=none --set-exit-if-changed lib test integration_test` | Passed; three files, zero changes. |
| `flutter test` (initial and final) | All five widget tests passed in both runs. |
| `flutter test integration_test/app_test.dart -d emulator-5554` | Built, installed, and passed one Android integration smoke test. |
| `flutter build apk --debug` (initial and final) | Succeeded. Final delivery is the normal app build after the integration run. |
| `adb -s emulator-5554 shell getprop sys.boot_completed` | Returned 1. |
| `adb -s emulator-5554 shell pidof edu.example.snack_club` | Returned a running process ID during emulator testing. |

Gradle printed Java native-access warnings but completed successfully. No release/store build, physical-device test, manual visual QA, real account service, or repository publishing was performed. The keyboard layout check uses a simulated inset in a widget test; the Android smoke test covers valid signup and the first local tip. Do not read it as exhaustive device testing.

A first attempt to redirect `flutter pub get` output used a path relative to the workspace instead of the project. The shell rejected that redirection before Flutter ran; the command was then executed successfully from the project folder. Raw logs are included in `verification/`, including the initial analyzer findings and final clean results.

## Submission limitations

The retrieved assignment ends at “Clearly i”; the remaining rubric could not be recovered. The known core and Task A requirements are implemented. The README identifies the project owner and repository and describes the implementation.

The source archive excludes machine-specific local.properties, caches, build directories, IDE metadata, and signing keys. Flutter regenerates local configuration with `flutter pub get` / build on another machine. The APK uses debug signing and is intended for classroom demonstration.

Local workspace paths in archived verification logs are normalized to `<project>/` for portability. The current source changes only the local-tip label and a comment; the previous Android build and emulator results apply to the earlier label.
