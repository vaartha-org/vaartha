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

## Network Requirements

### Local Area Network (LAN)
*   **Multicast DNS (mDNS)**: Users can discover the server locally via `vaartha.local` without configuring DNS servers.
*   **No Internet Required**: The entire stack functions on an isolated switch.

### Data Sovereignty
*   **Storage**: All chat history is stored locally on the user's device (SQLite).
*   **Ephemeral Metadata**: The server logs can be configured to rotate/delete instantly.
