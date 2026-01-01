# Open Core Business Model

**Strategy**: The "Core" engine is Free & Open Source (FOSS). Advanced "Enterprise/Premium" features are Closed Source Plugins linked dynamically.

## 1. The Separation of Concerns

We follow the **Android Model** (AOSP vs. Google Play Services) or **Mattermost Model**.

### The "Core" (FOSS)
### The "Core" (FOSS)
*   **License**: **AGPLv3** (Affero General Public License).
    *   *Why?* The "Affero" clause protects you from Cloud Providers (like AWS) taking your code and hosting it as a service without contributing back. This is the industry standard for Open Core (e.g., MongoDB, Grafana).
*   **Repo**: `github.com/vaartha-org/vaartha` (Monorepo)
*   **Features (The "Comms" Layer)**:
    *   SIP Registration & Routing.
    *   1-on-1 Audio/Video Calling.
    *   Basic Text Chat.
    *   Local file transfer.
    *   Ad-Hoc Mobile Mesh (Level 0).

### The "Premium" (Proprietary)
*   **License**: Commercial EULA.
*   **Repo**: `gitlab.com/vaartha-corp/premium-plugins` (Private).
*   **Features (The "Intelligence" Layer)**:
    *   **Whiteboard**: Complex collaboration tools.
    *   **AI Insights**: The Whisper/LLM pipeline.
    *   **LDAP/AD Sync**: Integration with Corporate Active Directory.
    *   **Audit Logs**: Compliance reporting tools.

## 2. Technical Implementation: Dynamic Linking

We do **not** maintain two separate apps. We maintain **one** app that can load signed plugins.

### The "Plugin Loader" Logic
1.  **Startup**: The App checks `plugins/` directory.
2.  **Signature Verification**: It verifies the digital signature of `whiteboard.vpl` (Vaartha Plugin) using a public key embedded in the Core.
3.  **Loading**:
    *   *Signed by Vaartha Corp?* -> LOAD.
    *   *Unsigned/Invalid?* -> IGNORE (or explicit user override for dev mode).

### Deployment
*   **Community Edition (Free)**: Download includes only the Core.
*   **Enterprise Edition (Paid)**: Customer receives a ZIP file containing the Core + Premium Plugins pre-installed.

## 3. Why this works?
*   **No Code Forking**: You don't have to merge changes from "Community" to "Enterprise" manually. Enterprise is just a *superset*.
*   **Community Trust**: The Core is truly open. No "crippleware". It functions perfectly as a phone.
*   **Monetization**: Companies pay for the "Productivity" features (Whiteboard, AI), not the "Connectivity".
