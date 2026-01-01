# Project Charter: VAARTHA (वार्ता)

**Tagline:** *The Private Thread.*
**Mission:** To provide a secure, serverless-style communication tool for private networks that functions without the internet, ensuring total data sovereignty.

---

## 1. Documentation & Planning

We have transitioned from a single Readme to a comprehensive documentation suite. Please verify the following documents for detailed execution.

### **[Master Plan & Roadmap](docs/planning.md)**
Click above for the **Detailed Step-by-Step Execution Plan** (Phases 1-5), including Development, Testing, and Deployment strategies.

### **Project Setup & Strategy**
*   **[GitHub Setup Guide](docs/project_setup/github_setup_guide.md)**: Step-by-step instructions to create the Org and Repos.
*   **[Repository Structure](docs/project_setup/repository_structure.md)**: Monorepo strategy details.
*   **[Open Core Business Model](docs/business_model.md)**: Strategy for monetizing Premium Plugins.

### **Detailed Specifications**
*   **[Server Installation](docs/server/installation.md)**: Guide for setting up a dedicated Raspberry Pi/Linux server.
*   **[Architecture Overview](docs/architecture/overview.md)**: The "Triangle" Topology & Privacy Model.
*   **[Scalability & Modularity](docs/architecture/scalability.md)**: From Home Wi-Fi to City-Wide Networks (Matrix).
*   **[Distributed Scenarios](docs/architecture/distributed.md)**: Multi-Campus & Public Network Architectures.
*   **[Android Client](docs/endpoints/android.md)**: Mobile App specs (Local Push).
*   **[Desktop Client](docs/endpoints/desktop.md)**: Windows/Linux App specs.
*   **[Plugin Ecosystem](docs/plugins/ecosystem.md)**: How to extend the platform.
*   **[Whiteboard](docs/plugins/whiteboard.md)**: Collaborative P2P Canvas.
*   **[AI Insights](docs/plugins/ai_insights.md)**: Offline-First Meeting Intelligence.

---

## 2. The Core Concept

**VAARTHA** is an open-source communication platform designed specifically for **Private Networks (LAN/VPN)**.

### **Key Differentiators**

| Feature | Traditional Tools (Zoom/WhatsApp) | **VAARTHA** |
| --- | --- | --- |
| **Connectivity** | Requires Internet | **Works Offline (LAN/WiFi)** |
| **Data Path** | Cloud Servers | **Peer-to-Peer (Device-to-Device)** |
| **Privacy** | Data stored by Vendor | **Data never leaves the premises** |
| **Bandwidth** | High Internet Bandwidth | **Local LAN Bandwidth Only** |

---

## 3. Immediate Action
You are ready to begin **Phase 1**. Refer to the **[Master Plan](docs/planning.md)** for the first set of tasks regarding Server Infrastructure and the "Ping" Prototype.