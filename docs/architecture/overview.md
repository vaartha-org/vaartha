# Architecture Overview

**VAARTHA** is designed as a **Privacy-First, Offline-First** communication ecosystem.

## Core Topology: The Triangle

The system avoids the traditional "Star" topology of cloud apps where all data passes through a central vendor server. Instead, it uses a SIP-based Federated model for signaling and Peer-to-Peer (P2P) for media.

### 1. The Registrar (Signaling Server)
*   **Protocol**: SIP (Session Initiation Protocol) over UDP/TCP/TLS.
*   **Function**: Acts as a dynamic directory.
*   **Data**: Stores *only* metadata (Who is online, IP address). Does *not* store messages or media.
*   **Software**: Flexisip (preferred) or Kamailio.

### 2. The Endpoints (Peers)
*   **Protocol**: RTP/SRTP (Real-time Transport Protocol).
*   **Function**: Direct device-to-device communication.
*   **Data**: Audio/Video flows directly between users.
*   **Encryption**: ZRTP or SDES-SRTP for End-to-End Encryption (E2EE).

### 2. Network Optimizations

#### A. NAT Traversal (Solving "One-Way Audio")
Since we cannot rely on public STUN servers (like Google's), we implement a multi-layered approach:
1.  **ICE (Interactive Connectivity Establishment)**: The client tries *every* possible IP (Local LAN, Valid Public, VPN IP).
2.  **Local STUN**: The Vaartha Registrar (Server) runs a built-in STUN server on UDP 3478.
    *   *Mechanism*: Clients ping the server to discover their "Public" IP relative to the NAT.
3.  **Symmetric NAT Handling**: For strict corporate firewalls, we enable "Media Relay" (TURN-like behavior) on the Registrar itself, forcing media to bridge through the server if P2P fails.

#### B. Audio Latency & Quality
Achieving "WhatsApp-like" quality requires tuning:
1.  **Codec**: Use **Opus** (48kHz) exclusively. It handles packet loss better than legacy G.711.
2.  **Jitter Buffer**: Set to `adaptive` (60ms - 200ms).
    *   *Logic*: If Wi-Fi is shaky, increase buffer size (slight delay, but smooth audio) -> If Wi-Fi is good, shrink buffer (instant audio).
3.  **Process Priority**: The RTP thread is set to `THREAD_PRIORITY_URGENT_AUDIO` (-19 strictness) in the Linux kernel on endpoints.

### 3. Network Requirements

### Local Area Network (LAN)
*   **Multicast DNS (mDNS)**: Users can discover the server locally via `vaartha.local` without configuring DNS servers.
*   **No Internet Required**: The entire stack functions on an isolated switch.

### Data Sovereignty
*   **Storage**: All chat history is stored locally on the user's device (SQLite).
*   **Ephemeral Metadata**: The server logs can be configured to rotate/delete instantly.
