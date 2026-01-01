# Distributed & Public Architecture

**VAARTHA** supports scaling beyond a single LAN to cover distributed campuses and public-facing scenarios.

## 1. Distributed Campus (The "College" Scenario)

**Scenario**: A university has 3 campuses (Engineering, Medical, Arts) in different physical locations, but wants a unified communication network.

### Architecture: Mesh Federation
Instead of one central server which creates a single point of failure and latency, we deploy a **Federated Mesh**.

*   **Campus A Server**: `sip.eng.college.edu`
*   **Campus B Server**: `sip.med.college.edu`

#### Mechanics
1.  **Local Traffic**: User A calling User B *within* Campus A stays 100% local. Media never leaves the campus LAN.
2.  **Inter-Campus Call**:
    *   User A dials User C (at Campus B).
    *   Server A does a DNS SRV lookup for `sip.med.college.edu`.
    *   Server A authenticates with Server B via TLS Mutual Authentication.
    *   Signaling is bridged.
    *   **Media Path**:
        *   *Option 1 (VPN)*: Site-to-Site VPN allows direct RTP flow.
        *   *Option 2 (ICE/TURN)*: A TURN server at each campus edge relays media over the public internet securely (SRTP).

## 2. Public Network Mode

For organizations wanting to offer a standardized communication app to the public (e.g., "CityChat").

### Custom Branding (White-Labeling)
The ecosystem supports full re-branding for public deployment.

*   **Manifest-Based Configuration**: The Client App downloads a `config.json` upon first login:
    *   **Assets**: App Icon, Splash Screen, Color Palette (Hex codes).
    *   **Terminology**: "Call" -> "Connect", "Chat" -> "Ping".
    *   **Features**: Enable/Disable Crypto Wallet, Whiteboard, etc.

### Public Endpoints
*   **Mobile (Android/iOS)**: Published to App Stores under the Organization's Name.
*   **Web Portal**: a WebRTC-based client (using SIP.js) for browser access without install.

### Security for Public Ops
*   **Public Registrar**: Hardened Linux server with Fail2Ban and Rate Limiting.
*   **TLS Everywhere**: SIP-over-TLS is mandatory.
*   **Push Notifications**: Requires integration with APNS (Apple) and FCM (Google), OR a persistent background socket service (battery intensive but private).
