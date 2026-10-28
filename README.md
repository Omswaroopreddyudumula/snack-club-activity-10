# Snack Club — MAD 4360 Activity 10

Undergraduate track: core signup form and Task A only.

## Project information

- Prepared for: Om Swaroop Reddy Udumula
- Repository URL: https://github.com/Omswaroopreddyudumula/snack-club-activity-10
- Project scope: Undergraduate core signup form and Task A local signup tip simulation.
- Project components: Flutter signup form, field validation, local signup tips, Android project files, automated tests, and documentation.
- Screenshots or recording: No course screenshots or recording are included. Whether these are required could not be confirmed because the complete rubric was unavailable.

## Reflection on the implementation

This project demonstrates how a Flutter Form and a GlobalKey keep validation in one place. Checking trimmed input prevents spaces from satisfying required fields, while a basic email pattern catches common formatting mistakes. Validation alone does not create an account or verify an email address.

The local tip simulation shows how a small amount of state can control asynchronous UI behavior. Disabling the button during the delay prevents overlapping requests, the counter produces a repeatable sequence, and the mounted check protects against updating a page that has been closed. Disposing the text controllers is also part of managing the page's lifecycle.

The tests cover validation failures, successful signup, tip order and loading, disposal, and a simulated keyboard inset. The Android emulator smoke test adds evidence that the app runs on Android, although it does not replace a full manual review across devices.

The available assignment text ends at “Clearly i”; requirements beyond that fragment were unavailable. The UI explicitly identifies Task A as a local simulation. Confirm the missing rubric text before submitting.

## Run

Requires Flutter with Dart, Android SDK, a supported JDK, and accepted Android SDK licenses.

```sh
flutter pub get
dart format --output=none --set-exit-if-changed lib test integration_test
flutter analyze
flutter test
flutter run -d emulator-5554
flutter test integration_test/app_test.dart -d emulator-5554
flutter build apk --debug
```

The commands above use the Android emulator ID tested for this project; use `flutter devices` to find the appropriate ID on another machine.

The debug APK is produced at `build/app/outputs/flutter-apk/app-debug.apk`. A copy is included in the delivery if the build succeeded. It uses Flutter's normal debug signing and is a classroom demo, not a store release. The application ID `edu.example.snack_club` is an explicit example placeholder.

## Design decisions

`lib/main.dart` contains the app and a stateful signup page so the form is easy to follow. MaterialApp and ThemeData provide the orange Material theme. Scaffold resizes for the keyboard; SafeArea, SingleChildScrollView, and a width constraint keep the form readable on small and wide screens. All three controllers are disposed when the page leaves the widget tree.

The form key runs every validator. Names must contain a non-whitespace character. Email validation trims surrounding spaces and uses a basic pattern requiring one @ and a dot after it; this checks syntax, not mailbox ownership. Passwords must contain a non-whitespace character and be at least six characters in their entered form. Passwords are obscured, with suggestions and autocorrect disabled. A green success SnackBar appears only when validation passes. There is no account creation, database, analytics, credential logging, or persistence. Text exists in controller memory while the screen is active.

Task A uses the fixed `password_help` category and exactly three local strings. A counter wraps back to zero after the third tip, so the order is predictable. A 600 ms delay makes loading visible, and the button plus a method guard prevent duplicate requests. A mounted check prevents updating a disposed page. Results are ordinary Text widgets; all fixed tips are below 240 characters. No API key or network service is used.

## Files and tests

- `lib/main.dart`: complete UI, validation, and local simulation.
- `test/widget_test.dart`: required/whitespace fields, malformed email, short password, valid signup and green SnackBar, password configuration, tip order/loading/length, disposal, and small screen with simulated keyboard inset.
- `integration_test/app_test.dart`: Android smoke test for valid signup and the first tip.
- `android/`: generated Android host project, Gradle scripts, wrapper scripts, wrapper JAR and properties.
- `CHECKS.md`: actual execution results and environment limitations.

The generated Android launcher icon is Flutter's default; the requested cookie icon appears prominently inside the app. Only Android host files are included because this delivery targets an APK. No Task B or graduate extension is implemented.
