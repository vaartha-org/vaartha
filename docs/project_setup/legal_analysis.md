# Legal Rights, Obligations, and Business Potential

## 1. Your Rights (The "God Mode" of Copyright)

As the **Original Creator**, you hold the Copyright to the code.
*   **The AGPLv3 license binds *others*, not you.**
*   **Dual Licensing Power**: Because you own the copyright, you can sell the *exact same code* to big corporations under a "Commercial License" (so they don't have to open-source their modifications).
    *   *Example*: MongoDB, Qt, and MySQL do this.
*   **Repo Control**: You decide what features go into "Core" (Free) and what goes into "Premium" (Paid).

### Critical Recommendation: The CLA
To maintain this power when others start contributing, you must require a **Contributor License Agreement (CLA)**.
*   **What it does**: "I give my code to Suresh. Suresh can do whatever he wants with it, including re-licensing it."
*   **Without a CLA**: If "Bob" contributes a huge feature, *he* owns the copyright to that chunk. You cannot sell a "Commercial License" of the whole app without Bob's permission.

## 2. Business Potential (How to make money)

### A. The "Open Core" Upsell (High Margin)
*   **Product**: Sell the "Private Plugins" (Whiteboard, AI, Audit Logs).
*   **Customer**: Enterprises, Colleges, Government offices.
*   **Pitch**: "Use the Free version for testing. Buy the Enterprise version for your 5,000 employees to get LDAP sync and Whiteboards."

### B. "Vaartha Cloud" (SaaS)
*   **Product**: Hosting the server so they don't have to.
*   **Customer**: Small businesses who can't manage a Linux server.
*   **Protection**: The AGPLv3 license prevents Amazon/Google from simply taking your code and competing with you easily. They would have to release their full source code if they did.

### C. "Rugged Hardware" (Niche)
*   **Product**: Sell cheap-ish Android tablets pre-loaded with Vaartha in "Kiosk Mode".
*   **Customer**: Construction sites, Disaster Relief NGOs, Event Organizers.
*   **Value**: "It works out of the box, no internet needed."

## 3. Your Obligations & Risks

### A. Stewardship
*   You cannot just "abandon" the Open Source version. If you make it useless to force people to pay, the community will "Fork" it and make a better free version.
*   **Balance**: The Core must be genuinely useful.

### B. Security
*   As the primary maintainer, people look to you for CVE patches.

### C. Legal Enforcement
*   If a company violates the AGPL (uses your code without sharing theirs), you have to decide whether to ignore it or sue them. (Usually, a "Cease and Desist" email is enough).

## Summary Table

| Role | Rights | Obligations |
| :--- | :--- | :--- |
| **You (Owner)** | Unlimited. Can sell/close/open code. | Maintain trust. |
| **Free User** | Can use/modify/share (under AGPL). | Must share source if they modify & host it. |
| **Paid Customer** | Can use without sharing source. | Pay annual license fee. |
