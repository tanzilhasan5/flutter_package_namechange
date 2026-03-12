
Option 1: Using rename package (Easiest)
bashdart pub global activate rename
dart pub global run rename --bundleId com.yourcompany.appname
This handles Android + iOS in one command.

Option 2: Manual
Android
android/app/build.gradle
gradledefaultConfig {
    applicationId "com.yourcompany.newname"  // change this
    ...
}
android/app/src/main/AndroidManifest.xml
xml<manifest package="com.yourcompany.newname">
```

Then rename the folder structure inside:
```
android/app/src/main/kotlin/com/yourcompany/newname/MainActivity.kt
Update MainActivity.kt package declaration too:
kotlinpackage com.yourcompany.newname

iOS
Open ios/Runner.xcodeproj in Xcode →

Select Runner target → General tab
Change Bundle Identifier to com.yourcompany.newname

Or edit ios/Runner/Info.plist:
xml<key>CFBundleIdentifier</key>
<string>com.yourcompany.newname</string>

After changing, clean the build:
bashflutter clean
flutter pub get
flutter run

Recommendation: Use the rename package — it avoids missing any file manually. If your project uses flavors or multiple build variants, manual is safer so you have full control.

Identified API syntax change in package version
Identified API syntax change in package version
The new rename v3 uses subcommands. Use this instead:

bash
dart pub global run rename setBundleId --value com.yourcompany.walkthroughpro
To also change the app name:

bash
dart pub global run rename setAppName --value "Walkthrough Pro"
To target a specific platform only:

bash
dart pub global run rename setBundleId --value com.yourcompany.walkthroughpro --targets android
dart pub global run rename setBundleId --value com.yourcompany.walkthroughpro --targets ios
Then clean:

bash
flutter clean
flutter pub get
