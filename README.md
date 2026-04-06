# Battery Level App

A Flutter application that demonstrates platform channel communication to fetch and display the current battery level on Android devices.

## 📱 Features

- Display current battery percentage
- Clean Material Design 3 UI
- Real-time battery level updates
- Error handling for devices without batteries (emulators)
- Platform channel integration with native Android (Kotlin)

## 🛠️ Tech Stack

- **Flutter** - UI framework
- **Kotlin** - Android platform-specific code
- **Platform Channels** - Flutter to native communication
- **Material Design 3** - UI components

<img width="374" height="616" alt="image" src="https://github.com/user-attachments/assets/8e154c2b-1124-46dc-a502-e48dd91928b2" />
<img width="325" height="622" alt="image" src="https://github.com/user-attachments/assets/0f056954-e6a6-476f-af46-6dab96a48bc5" />
<img width="293" height="626" alt="image" src="https://github.com/user-attachments/assets/410add11-8160-4a63-b391-0ae9aafe603d" />


## 📋 Prerequisites

Before running this project, make sure you have:

- [Flutter SDK](https://docs.flutter.dev/get-started/install) (3.0 or later)
- [Android Studio](https://developer.android.com/studio) with Flutter plugin
- [Android SDK](https://developer.android.com/studio#command-line-tools-only) (API 21 or later)
- Java Development Kit (JDK) 17 or later
- Android device (physical or emulator) with API 21+

## 🚀 Getting Started

### 1. Clone the project

```bash
git clone <your-repo-url>
cd batterylevel
2. Install dependencies
bash
flutter pub get
3. Run the app
On Android emulator:

bash
# List available emulators
flutter emulators

# Launch an emulator
flutter emulators --launch <emulator-name>

# Run the app
flutter run
On physical Android device:

bash
# Enable USB debugging on your device
# Connect via USB
flutter run
On Chrome (for quick testing):

bash
flutter run -d chrome
📁 Project Structure
text
batterylevel/
├── android/                    # Android platform-specific code
│   └── app/
│       └── src/
│           └── main/
│               └── kotlin/
│                   └── MainActivity.kt  # Kotlin implementation
├── lib/
│   └── main.dart              # Flutter UI code
├── README.md                   # This file
└── pubspec.yaml               # Project dependencies
🔧 How It Works
Flutter Side (Dart)
dart
// Create a MethodChannel
static const platform = MethodChannel('samples.flutter.dev/battery');

// Call platform method
final int result = await platform.invokeMethod('getBatteryLevel');
Android Side (Kotlin)
kotlin
// Create MethodChannel and handle method calls
MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL)
    .setMethodCallHandler { call, result ->
        if (call.method == "getBatteryLevel") {
            val batteryLevel = getBatteryLevel()
            result.success(batteryLevel)
        }
    }

// Get battery level using Android BatteryManager API
private fun getBatteryLevel(): Int {
    val batteryManager = getSystemService(Context.BATTERY_SERVICE) as BatteryManager
    return batteryManager.getIntProperty(BatteryManager.BATTERY_PROPERTY_CAPACITY)
}
📱 Platform Support
Platform	Support	Status
Android	✅ Full support	Working
iOS	✅ Supported	Requires Swift implementation
Windows	✅ Supported	Requires C++ implementation
macOS	✅ Supported	Requires Swift implementation
Linux	✅ Supported	Requires C implementation
Web	⚠️ Partial	UI works, battery API not available
🎯 Usage
Launch the app on your Android device

Tap the "Get Battery Level" button

View your current battery percentage

The app will show an error message if running on an emulator (emulators don't have batteries)

🐛 Troubleshooting
Common Issues and Solutions
Issue: "NDK not found" error

bash
# Solution: Install NDK via Android Studio SDK Manager
# Tools → SDK Manager → SDK Tools → Check "NDK (Side by side)"
Issue: Emulator not showing battery level

text
Solution: This is normal - emulators don't have real batteries
The app will show "Battery level not available"
Issue: Build fails with Gradle errors

bash
# Clean and rebuild
flutter clean
flutter pub get
flutter run
Issue: "Unable to find bundled Java version"

text
Solution: In Android Studio:
File → Project Structure → SDK Location
Set JDK path to: C:\Program Files\Java\jdk-21
Issue: Resource shrinking error

bash
# Fix by disabling shrinkResources in build.gradle.kts
buildTypes {
    release {
        isShrinkResources = false
        isMinifyEnabled = false
    }
}
📊 Data Flow Diagram
text
┌─────────────┐         ┌──────────────┐         ┌─────────────────┐
│   Flutter   │         │   Platform   │         │    Android      │
│     UI      │ ◄─────► │   Channel    │ ◄─────► │   Battery API   │
│  (Dart)     │         │              │         │   (Kotlin)      │
└─────────────┘         └──────────────┘         └─────────────────┘
      │                         │                           │
      │ 1. User clicks button   │                           │
      ├────────────────────────►│                           │
      │                         │ 2. invokeMethod()         │
      │                         ├──────────────────────────►│
      │                         │                           │ 3. Get battery
      │                         │                           │    level
      │                         │ 4. Return result          │
      │                         │◄──────────────────────────┤
      │ 5. Display battery %    │                           │
      │◄────────────────────────┤                           │
🔄 Future Improvements
Add battery charging status indicator

Implement battery health information

Add temperature monitoring

Create battery usage graph

Add notification for low battery

Support for iOS platform

Add widget for home screen

Implement battery saver mode detection
