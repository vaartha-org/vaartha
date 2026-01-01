# System Scalability & Modularity Matrix

This document answers the critical questions: "Will it work for my family?" and "How exactly does it grow to a city-wide network?"

## 1. Small Scale: The "Home" Deployment
**Scenario**: A 3-4 person family wanting private communication within the house or small office.

### Feasibility Analysis
*   **Yes, it works effectively.**
*   **Hardware**: A Raspberry Pi 4 OR an old laptop running the Server (Docker container).
*   **Configuration**: Zero-Config via **mDNS**.
    *   The server broadcasts `vaartha.local` on the Wi-Fi.
    *   Android/Desktop clients auto-detect this. No IP typing needed.
*   **Experience**:
    *   Works exactly like WhatsApp.
    *   **Bonus**: Works even when your ISP (Internet Provider) is down.
    *   **Latency**: Extremely low (<5ms) because traffic never leaves the router.

### The "Host Mode" (Zero Hardware Cost)
**Q**: Do I need to buy a Raspberry Pi?
**A**: No. One of your endpoints can act as the Registrar.
*   **Desktop Host**: A Windows/Linux PC can run the Server (in the background) *while* also running the Client App.
*   **Mobile Host**: High-end Android phones can also act as the Registrar for a small group (see Level 0 below).

## 2. The Scalability Curve

The system is designed to grow from 1 user to 1 million users by adding modules, not rewriting core code.

| Level | Scale | Infrastructure | Discovery Method | Registrar Role |
| :--- | :--- | :--- | :--- | :--- |
| **Level 0** | **Ad-Hoc / Mobile Mesh** (1-10 users) | One Mobile Phone (The "Supernode") | Existing Wi-Fi OR Hotspot | **Embedded**: One phone runs a micro-SIP server service. |
| **Level 1** | **Home / Small Office** (1-50 users) | Single Device (Pi/Laptop) | mDNS (`vaartha.local`) | **All-in-One**: Handles Auth, Registry, and Presence. |
| **Level 2** | **Enterprise / SME** (50-2,000 users) | Dedicated VM / Server | Internal DNS (`sip.corp.com`) | **Active-Standby**: Two nodes (Primary/Backup) sharing a Redis database for session handling. |
| **Level 3** | **Distributed Campus** (Multiple Sites) | Federated Mesh | DNS SRV Records | **Federated**: Each site has its own Master Registrar. They talk to each other only for inter-site calls. |
| **Level 4** | **Public / City** (1M+ users) | Cloud Cluster | Public DNS + Load Balancer | **Sharded**: Architecture splits into Edge Proxies (Load Balancers) -> Core Registrars -> Database Cluster. |

## 3. Registrar Switching & Migration Strategy

How do users move from "Home" to "Office" or migrate servers?

### Scenario A: Roaming (The "Road Warrior")
*   **Requirement**: A user has a "Home" server and an "Office" server.
*   **Solution**: Multi-Account Support.
    *   The Client App supports multiple profiles.
    *   It auto-connects to `vaartha.local` when at home.
    *   It auto-connects to `sip.company.com` when at work.
    *   *Note: These are distinct identities (Dad@Home vs. Employee@Work).*

### Scenario B: Server Upgrade (Moving from IP X to IP Y)
*   **Requirement**: You upgrade the server hardware and the IP changes.
*   **Solution**: **DNS-Based Indirection**.
    *   *Never* hardcode IPs in the client. Always use a Hostname (`sip.vaartha.internal`).
    *   When the server moves, you only update the DNS Record (or mDNS broadcast).
    *   Clients auto-reconnect to the new IP within seconds (DNS TTL).

### Scenario C: High Availability Failover
*   **Requirement**: The Primary Server crashes.
*   **Mechanism**:
    1.  Client has two records: `sip.primary.com` (Priority 10) and `sip.backup.com` (Priority 20).
    2.  If Primary fails TCP handshake, Client auto-switches to Backup.
    3.  Redis Backend ensures the Backup knows the user's last status.

## 4. Modularity
The ecosystem is modular by keeping "Signaling" separate from "Features".
*   **Core**: Flexisip (Only moves packets).
*   **Feature A**: Push Notification Service (Separate microservice).
*   **Feature B**: User Portal / Admin Panel (Separate web app).
*   **Feature C**: AI Analysis (Separate Python process on the client).
*   *You can upgrade the AI module without touching the Server.*
