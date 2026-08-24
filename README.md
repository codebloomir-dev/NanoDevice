
# 📱 NanoDevice

**A lightweight, zero-dependency Android library for retrieving complete device information with zero crashes.**

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![API](https://img.shields.io/badge/API-21%2B-brightgreen.svg)](https://android-arsenal.com/api?level=21)
[![Size](https://img.shields.io/badge/Size-35KB-blue)]()

---

## 📖 Introduction

**NanoDevice** is a powerful, lightweight, and **zero-dependency** Android library that provides complete device information with just a few lines of code. From hardware details to battery status, network info, sensors, and system properties – everything is covered.

### Why NanoDevice?

- 🚀 **Zero Dependencies** – Works only with Android SDK, no conflicts with other libraries.
- 🛡️ **Crash-Proof** – Every method is wrapped with `try-catch` to prevent crashes.
- 📦 **Lightweight** – Less than 50KB in size.
- 🔄 **Real-time Data** – Always fetches fresh data from the system.
- 🧩 **Easy to Use** – Just `init()` and start getting information.

---

## ✨ Features

| Category | Details |
|----------|---------|
| **Device** | Model, Brand, Manufacturer, Android Version, API Level, Serial, Hardware, Bootloader, Radio, Root Status, Emulator Detection |
| **Screen** | Width, Height, Density, DPI, Orientation, Size (inches), Cutout, Brightness, Timeout |
| **Memory** | Total/Used/Available RAM, RAM Percentage, Internal Storage (Total/Used/Available), External Storage Status |
| **Network** | Connection Status, Network Type (WiFi/4G/3G/2G), Operator, Country, Airplane Mode |
| **Battery** | Level, Charging Status, Health, Plug Type, Voltage, Temperature, Technology |
| **Processor** | Name, Cores, Max/Min Frequency, Architecture, 64-bit Support, Supported ABIs |
| **Sensors** | Accelerometer, Gyroscope, Magnetometer, Proximity, Light, Fingerprint, Step Counter |
| **Display** | Refresh Rate, HDR Support, Wide Color Gamut, Round Screen, Supported Modes |
| **System** | Security Patch, Build Time, Time Zone, Developer Mode, Bluetooth/WiFi Status, OS Version, Java Version |

---

## 📥 Installation

### 1. Download the AAR File

Download the `nanodevice-1.0.0.aar` file from this repository.

### 2. Add to Your Project

Place the AAR file in your `app/libs` folder.

### 3. Update `build.gradle` (Module: app)

```gradle
dependencies {
    implementation files('libs/nanodevice-1.0.0.aar')
}
```

4. Click Sync Now

---

🚀 Quick Start

1. Initialize the Library

In your MainActivity or Application class:

```java
import com.codebloom.nanodevice.NanoDevice;

public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        // Initialize NanoDevice
        NanoDevice.init(this);
    }
}
```

2. Get Device Information

```java
// Device Info
String model = NanoDevice.getModel();
String androidVersion = NanoDevice.getAndroidVersion();
boolean isRooted = NanoDevice.isRooted();

// Screen Info
int width = NanoDevice.getScreenWidth();
int height = NanoDevice.getScreenHeight();
double size = NanoDevice.getScreenSizeInches();

// Memory Info
long totalRAM = NanoDevice.getTotalRAM();
long availableRAM = NanoDevice.getAvailableRAM();
long totalStorage = NanoDevice.getTotalStorage();

// Network Info
boolean isConnected = NanoDevice.isConnected();
String networkType = NanoDevice.getNetworkType();

// Battery Info
int batteryLevel = NanoDevice.getBatteryLevel();
boolean isCharging = NanoDevice.isCharging();

// Processor Info
String processorName = NanoDevice.getProcessorName();
int cores = NanoDevice.getProcessorCores();

// Sensors
boolean hasAccelerometer = NanoDevice.hasAccelerometer();
boolean hasFingerprint = NanoDevice.hasFingerprintSensor();
```

3. Display All Information at Once

```java
String allInfo = getDeviceInfo();
textView.setText(allInfo);

private String getDeviceInfo() {
    StringBuilder info = new StringBuilder();
    
    info.append("📱 DEVICE\n");
    info.append("Model: ").append(NanoDevice.getModel()).append("\n");
    info.append("Brand: ").append(NanoDevice.getBrand()).append("\n");
    info.append("Android: ").append(NanoDevice.getAndroidVersion()).append("\n\n");
    
    info.append("🖥️ SCREEN\n");
    info.append("Size: ").append(NanoDevice.getScreenWidth()).append("x")
        .append(NanoDevice.getScreenHeight()).append("px\n");
    info.append("Density: ").append(NanoDevice.getScreenDensity()).append("\n\n");
    
    info.append("💾 MEMORY\n");
    info.append("RAM: ").append(formatSize(NanoDevice.getTotalRAM())).append("\n");
    info.append("Storage: ").append(formatSize(NanoDevice.getTotalStorage())).append("\n\n");
    
    info.append("🔋 BATTERY\n");
    info.append("Level: ").append(NanoDevice.getBatteryLevel()).append("%\n");
    info.append("Charging: ").append(NanoDevice.isCharging()).append("\n\n");
    
    info.append("📡 NETWORK\n");
    info.append("Connected: ").append(NanoDevice.isConnected()).append("\n");
    info.append("Type: ").append(NanoDevice.getNetworkType()).append("\n");
    
    return info.toString();
}

private String formatSize(long size) {
    if (size <= 0) return "0 B";
    final String[] units = {"B", "KB", "MB", "GB", "TB"};
    int digitGroups = (int) (Math.log10(size) / Math.log10(1024));
    return String.format("%.1f %s", size / Math.pow(1024, digitGroups), units[digitGroups]);
}
```

---

📖 Complete Usage Guide

Device Information

Method Return Type Description
getModel() String Device model (e.g., SM-X115)
getBrand() String Device brand (e.g., Samsung)
getManufacturer() String Device manufacturer
getAndroidVersion() String Android version (e.g., 16)
getApiLevel() int API level (e.g., 36)
isEmulator() boolean Check if running on emulator
isRooted() boolean Check if device is rooted
getSerial() String Device serial (Android 10+ returns "Access Denied")
getHardware() String Hardware platform
getBootloader() String Bootloader version
getRadio() String Radio version
isTvDevice() boolean Check if TV device
isWatchDevice() boolean Check if smartwatch

Screen Information

Method Return Type Description
getScreenWidth() int Screen width in pixels
getScreenHeight() int Screen height in pixels
getScreenDensity() float Screen density (e.g., 1.33)
getScreenDpi() int Screen DPI (e.g., 213)
getScreenOrientation() String "Portrait" or "Landscape"
getScreenSizeInches() double Screen size in inches
hasScreenCutout() boolean Check for notch/cutout (requires Activity)
getScreenBrightness() int Current screen brightness
getScreenTimeout() int Screen timeout in milliseconds

Memory Information

Method Return Type Description
getTotalRAM() long Total RAM in bytes
getAvailableRAM() long Available RAM in bytes
getUsedRAM() long Used RAM in bytes
getRAMPercentage() int RAM usage percentage
isLowRamDevice() boolean Check if low RAM device
getTotalStorage() long Total internal storage in bytes
getAvailableStorage() long Available internal storage in bytes
getUsedStorage() long Used internal storage in bytes
getStoragePercentage() int Storage usage percentage

Network Information

Method Return Type Description
isConnected() boolean Check network connectivity
getNetworkType() String "WiFi", "4G", "3G", "2G", "No Connection"
isWifiConnected() boolean Check WiFi connection
isMobileConnected() boolean Check mobile data connection
getNetworkOperator() String Network operator name
getNetworkCountryIso() String Network country code
isAirplaneModeOn() boolean Check airplane mode

Battery Information

Method Return Type Description
getBatteryLevel() int Battery percentage (0-100)
isCharging() boolean Check if charging
getBatteryStatus() int Battery status constant
getBatteryHealth() int Battery health constant
getBatteryPlugType() int Plug type (AC/USB/Wireless)
getBatteryVoltage() int Battery voltage in mV
getBatteryTemperature() int Battery temperature in °C
getBatteryTechnology() String Battery technology (e.g., Li-ion)

Processor Information

Method Return Type Description
getProcessorName() String Processor name/hardware
getProcessorCores() int Number of CPU cores
getMaxFreq() int Maximum CPU frequency in MHz
getMinFreq() int Minimum CPU frequency in MHz
getProcessorArchitecture() String CPU architecture (e.g., arm64-v8a)
is64Bit() boolean Check if 64-bit device
getSupportedABIs() String[] Supported ABIs

Sensor Information

Method Return Type Description
hasAccelerometer() boolean Check accelerometer
hasGyroscope() boolean Check gyroscope
hasMagnetometer() boolean Check magnetometer
hasProximitySensor() boolean Check proximity sensor
hasLightSensor() boolean Check light sensor
hasFingerprintSensor() boolean Check fingerprint sensor
hasStepCounter() boolean Check step counter
getAvailableSensors() List<String> List of all available sensors

Display Information (Advanced)

Method Return Type Description
DisplayInfo.getDisplayName(Context) String Display name
DisplayInfo.getRefreshRate(Context) float Refresh rate in Hz
DisplayInfo.isHDR(Context) boolean Check HDR support
DisplayInfo.isWideColorGamut(Context) boolean Check wide color gamut
DisplayInfo.isScreenRound(Context) boolean Check round screen
DisplayInfo.getSupportedRefreshRates(Context) int Number of supported refresh rates

System Information (Advanced)

Method Return Type Description
SystemInfo.getSystemSecurityPatch() String Security patch date
SystemInfo.getSystemBuildTime() String Build time
SystemInfo.getSystemTimeZone() String Current time zone
SystemInfo.isDeveloperModeOn(Context) boolean Check developer mode
SystemInfo.isLocationEnabled(Context) boolean Check location enabled
SystemInfo.isBluetoothOn(Context) boolean Check Bluetooth status
SystemInfo.isWifiOn(Context) boolean Check WiFi status
SystemInfo.getOsVersion() String OS version
SystemInfo.getJavaVersion() String Java version

---

❌ Common Mistakes & Solutions

1. Not Initializing the Library

```java
// ❌ Wrong
String model = NanoDevice.getModel();

// ✅ Correct
NanoDevice.init(this);
String model = NanoDevice.getModel();
```

2. Not Adding Required Permissions

For network information, add this to AndroidManifest.xml:

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

3. Using hasScreenCutout() Without Activity

```java
// ❌ Wrong (causes crash)
boolean cutout = NanoDevice.hasScreenCutout();

// ✅ Correct (pass Activity)
boolean cutout = NanoDevice.hasScreenCutout(MainActivity.this);
```

---

📄 License

This library is released under the MIT License. You are free to use, modify, and distribute it, even in commercial projects.

---

🤝 Contributing

If you have ideas, suggestions, or find any issues, feel free to open an Issue. Pull requests are also welcome!

---

📞 Contact

· GitHub: codebloomir-dev

· Email: codebloomir.dev@gmail.com

---

⭐ Support

If you like this library, please give it a Star ⭐ on GitHub to help others discover it!

---

Built with ❤️ by codebloom

Thank you for using NanoDevice! ☕

