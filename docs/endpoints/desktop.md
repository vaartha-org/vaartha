# Desktop Endpoint Specification (Windows/Linux)

## Technology Stack
*   **Language**: Python 3.10+.
*   **GUI Framework**: **PyQt6** (Modern, Cross-Platform, Scriptable styling).
*   **SIP Engine**: **Liblinphone Python Wrapper** (Wheel files available for Win/Lin).

## Features

### 1. Minimalist "Tray" Operation
*   The app minimizes to the System Tray.
*   **Toast Notifications**:
    *   **Windows**: Uses `win10toast` or native Python `WindowsQRCode`.
    *   **Linux**: Uses `libnotify`.

### 2. Host Mode (Registrar)
*   **Built-in Server**: The Desktop App includes a bundled version of `flexisip` (or a lightweight Python SIP signaling stack).
*   **Toggle**: "Enable Local Server" in Settings.
*   **Effect**:
    *   Starts the SIP Proxy on port 5060.
    *   Broadcasts `vaartha.local` via Avahi/Bonjour.
    *   Accepts connections from other Android/Desktop clients on the Local Network.

### 2. Screen Sharing
*   Leverages `Liblinphone`'s capability to grab the framebuffer.
*   **High FPS Mode**: For video playback sharing.
*   **Docs Mode**: Low bandwidth, high resolution for text.

### 3. Plugin Loader (The "Marketplace")
*   The Desktop app scans a `plugins/` folder at startup.
*   Each plugin is a Python module with a standard `entry_point`.
*   Plugins can inject tabs into the Main Window.

## Windows Specifics
*   **Installer**: MSIX package for easy IT deployment.
*   **Firewall**: Installer automatically adds specific rules for UDP 5060 and UDP 10000-20000 (RTP).

## Linux Specifics
*   **Packaging**: AppImage for universal distro support.
*   **Wayland Support**: Requires specific QT flags `QT_QPA_PLATFORM=xcb` if Wayland screen sharing is unstable.
