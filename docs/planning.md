# VAARTHA Master Plan & Roadmap

This document outlines the strategic roadmap for bringing **VAARTHA** to life, from initial prototype to enterprise deployment.

## Phase 1: The Foundation (Weeks 1-2)
**Goal:** Prove the "Triangle" Topology (Registrar + P2P Media) works in an offline environment.

### 1. Infrastructure Setup
*   **Server**: Deploy `flexisip-proxy` using Docker Compose on a Raspberry Pi or Laptop.
*   **Network**: Verify `mdns` (vaartha.local) resolution on a closed Wi-Fi router (No WAN).
*   **Testing**: Use `sipvicious` or `nmap` ensuring only port 5060 (SIP) and 5004 (RTP) are open.

### 2. The "Ping" POC
*   **Script**: Create `vaartha_ping.py` to register a dummy user and send an OPTIONS packet.
*   **Manual Test**: Connect two stock Linphone Android clients to the server.
*   **Success Matrix**:
    *   [ ] Register A and B.
    *   [ ] Call A to B (Audio).
    *   [ ] Call A to B (Video).
    *   [ ] Verify Wireshark trace: Media flows directly (Peer-to-Peer), not through server.

## Phase 2: The Desktop Client (MVP) (Weeks 3-6)
**Goal:** A usable Desktop App for Windows/Linux.

### 1. UI Implementation (PyQt6)
*   **Login Screen**: Fields for "Username" and "Server Secret" (No password, uses TLS Cert).
*   **Buddy List**: Poll server for `presence` status.

### 2. SIP Integration
*   **Liblinphone**: Bind the Python wrapper to the UI buttons.
*   **Event Handling**: Correctly handle `IncomingCall`, `CallConnected`, `CallTerminated` signals.

### 3. Testing
*   **Memory Leak Test**: Run the app for 24h.
*   **Crash Test**: Disconnect/Reconnect Wi-Fi during a call.

## Phase 3: The Mobile Experience (Weeks 7-10)
**Goal:** A simplified, branded Android App.

### 1. Fork & clean
*   Fork `linphone-android`.
*   **Remove**: "Assistant" (Wizard), "In-App Purchase", "Cloud Backup".
*   **Add**: Hardcoded "Local Discovery" logic.

### 2. The "Local Push" Service
*   Implement a Foreground Service with a Persistent TCP Socket.
*   **Battery Optimization**: Use `AlarmManager` for 15-min keep-alives.

### 3. Ad-Hoc Host Mode (The "Supernode")
*   **Goal**: Allow one phone to be the Server.
*   **Task**: Port `flexisip` (C++) to Android via NDK OR implement a minimal Python/Kotlin SIP Registrar.
*   **UI**: Add "Host Network" toggle in Settings.

## Phase 4: Plugin & Ecosystem (Weeks 11-14)
**Goal:** Extend functionality without bloating the core.

### 1. Whiteboard Plugin
*   Implement the `Canvas` class.
*   Test P2P `SIP MESSAGE` latency for drawing vectors.

### 2. AI Insights (The Local Brain)
*   **Integration**: Hook `Whisper.cpp` into the audio stream.
*   **Privacy Verify**: Ensure ZERO bytes are sent to `api.openai.com` or similar.

## Phase 5: Testing & Deployment (Week 15+)

### 1. Public Network Pilot
*   Deploy to a Public Cloud instance (AWS/DigitalOcean) for the "CityChat" scenario.
*   Enable `fail2ban` and robust TLS protections.

### 2. "College" Simulation
*   Set up two routers with different subnets (Simulation of two campuses).
*   Config Federation between two Servers.
*   Verify cross-subnet calling.

### 3. One-Click Distribution
*   **Windows**: Build `VaarthaSetup.exe` (NSIS).
*   **Linux**: Build `Vaartha.AppImage`.
*   **Android**: Generate `.apk` signed with release key.
