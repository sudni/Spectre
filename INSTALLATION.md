# Spectre Installation Guide

## System Requirements
- **Android Version:** Android 12 (API 31) or higher
- **Processor:** ARM64 recommended (ARM32 also supported)
- **RAM:** Minimum 2GB (4GB recommended)
- **Storage:** ~50MB free space

## Installation Methods

### Method 1: Via ADB (Android Debug Bridge) - Recommended for Developers

#### Prerequisites:
- USB cable
- Android device with USB debugging enabled
- ADB installed on your computer

#### Steps:
1. **Enable USB Debugging on your phone:**
   - Go to Settings > About Phone
   - Tap "Build Number" 7 times to enable Developer Options
   - Go back and open Developer Options
   - Enable "USB Debugging"

2. **Connect your phone and install:**
   ```bash
   adb install -r spectre-debug.apk
   ```
   - The `-r` flag allows reinstalling if already installed

3. **Launch the app:**
   ```bash
   adb shell am start -n dev.thomasbuilds.spectre.debug/.MainActivity
   ```

### Method 2: Direct Installation (Easiest)

#### Steps:
1. **Download the APK** from the releases page or workflow artifacts
2. **Transfer to your phone** (via email, cloud storage, or USB)
3. **Open file manager** and navigate to the download
4. **Tap the APK file** to start installation
5. **If prompted:** Grant installation from unknown sources
   - Settings > Apps & notifications > Special app access > Install unknown apps > Your File Manager > Allow
6. **Tap "Install"** and wait for completion
7. **Launch the app** from your home screen

### Method 3: Android Studio (For Development)

1. Clone this repository
2. Open the project in Android Studio
3. Click **Run > Run 'app'** or press **Shift+F10**
4. Select your connected device or emulator
5. Android Studio will build, sign, and install automatically

## Permissions

The app requires the following permissions - grant them when prompted:

- **Location** - For GPS-based RF scanning
- **Phone State** - To detect cellular signals
- **Wi-Fi** - To scan for Wi-Fi networks
- **Bluetooth** - To detect Bluetooth signals
- **Notifications** - For real-time alerts
- **Network** - For data connectivity

## Troubleshooting

### APK Won't Install
- **"Installation blocked":** Check Settings > Security > Install from unknown sources
- **"Parse error":** The APK file may be corrupted. Try downloading again
- **"Insufficient storage":** Free up space on your device
- **"app not installed":** Try: `adb install -r -g spectre-debug.apk` (grants permissions)

### App Crashes on Launch
- Ensure Android 12+ is installed: Settings > About > Android version
- Try clearing app data: Settings > Apps > Spectre > Storage > Clear Data
- Reinstall the app
- Check logcat for errors: `adb logcat -s Spectre`

### No Permissions Granted
- Manually grant permissions: Settings > Apps > Spectre > Permissions
- Toggle the permissions you need

### USB Debugging Connection Issues
- Restart ADB: 
  ```bash
  adb kill-server
  adb devices
  ```
- Reconnect USB cable
- Accept the RSA fingerprint prompt on your phone
- Ensure USB connection is set to "File Transfer" mode (not charging only)

### Can't Find APK After Download
- Check your Downloads folder
- Use a file manager app
- Try re-downloading from a different source

## Uninstallation

### Via ADB:
```bash
adb uninstall dev.thomasbuilds.spectre.debug
```

### Via Phone:
1. Go to Settings > Apps
2. Find and select Spectre
3. Tap "Uninstall"

## Building from Source

To build your own APK:

```bash
# Clone the repository
git clone https://github.com/sudni/Spectre.git
cd Spectre

# Build debug APK (fastest)
./gradlew assembleDebug

# Build release APK (optimized)
./gradlew assembleRelease
```

APK files will be located in:
- **Debug:** `app/build/outputs/apk/debug/app-debug.apk`
- **Release:** `app/build/outputs/apk/release/app-release.apk`

Then install using Method 1 or 2 above.

## Getting Help

- Check [GitHub Issues](https://github.com/sudni/Spectre/issues) for known problems
- Review the [README.md](README.md) for usage instructions
- For ADB issues, refer to [Android Developer documentation](https://developer.android.com/studio/command-line/adb)
- For Android permission issues, see [Android Permissions Guide](https://developer.android.com/guide/topics/permissions/overview)

## Security Note

The provided APK is signed with a debug certificate for testing purposes. For production or distribution use, obtain and sign with a proper release certificate.
