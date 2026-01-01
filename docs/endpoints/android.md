# Android Endpoint Specification

## Technology Stack
*   **Language**: Kotlin (for UI/Logic), C++ (via JNI for SIP stack).
*   **Core Library**: **Linphone SDK (Mobile)**.
*   **Min SDK**: Android 8.0 (Oreo).

## Key Features

### 1. Offline Push Notifications
Standard Android Apps rely on Firebase (FCM) for wake-ups. VAARTHA cannot rely on Google.
*   **Solution**: **Foreground Service** with a persistent TCP connection to the SIP Log.
*   **Battery Opts**: Use Android's `AlarmManager` for "Keep-Alive" heartbeats every 10 minutes.

### 2. Local Discovery
*   **NSD (Network Service Discovery)**: The app listens for `_sip._udp` mDNS broadcasts to auto-find the server. No manual IP entry required.

### 3. UI/UX (Material 3)
*   **The "Lobby"**: A dashboard showing "Online Users" in the building.
*   **The "Secure Room"**: Visual indicator (Lock Icon) when ZRTP encryption is verified (SAS code match).

## Mobile Host Capability (Ad-Hoc Mode)
Every Vaartha Android installation includes a lightweight **SIP Proxy Module** (disabled by default).
*   **Activation**: User goes to Settings -> Advanced -> "Enable Host Mode".
*   **Function**:
    *   The phone starts a `Flexisip` micro-instance (or specialized Kotlin SIP Proxy).
    *   It broadcasts `vaartha.local` via mDNS.
    *   **Networking**:
        *   *Scenario A (Shared Wi-Fi)*: If all phones are on the same Home Router, they just auto-connect.
        *   *Scenario B (No Wi-Fi)*: The Host Phone creates a **Wi-Fi Hotspot**, and others connect to it.
*   **Use Case**: Camping trips, Disaster relief, rapid field deployment where no server exists.

## Branding Hooks
The codebase is structured with a distinct `theme` module.
*   `colors.xml`: Primary, Secondary, Background.
*   `strings.xml`: All text resources.
*   `drawables/`: Vectors for logos.
To rebrand for a "College Edition", we only swap this module.
