# Repository Strategy & GitHub Structure

To implement the **Open Core** model effectively, we will organize repositories to separate FOSS (Free and Open Source) from Proprietary IP while maintaining ease of build.

## 1. Organization Structure

We will create a GitHub Organization: `github.com/vaartha-org` (Public).
*   **Why an Org?** Even as a solo dev, it looks professional and allows you to move repos later without breaking links.

## 2. Repository List

### The "Monorepo" Strategy (Recommended for Solo Founders)
Instead of managing 5 different repos (which is a nightmare for a single person), we will use **One Main Repo**.

| Repo Name | Visibility | License | Description |
| :--- | :--- | :--- | :--- |
| **`vaartha`** | **Public** | **AGPLv3** | The Monorepo. Contains `android/`, `desktop/`, and `server/` folders. |
| `vaartha-premium` | **Private** | **Commercial** | Contains the proprietary plugins (`whiteboard`, `ai-insights`). |

### Why not separate repos?
*   **Atomic Commits**: You can update the Server and Android Client in a single commit ("Added feature X").
*   **Unified Issues**: All bugs live in one Issue Tracker.
*   **Easier CI/CD**: One pipeline to build everything.

## 3. Development Workflow

### Feature Branches & Submodules
1.  **Developers** check out `vaartha-desktop`.
2.  **Proprietary Code** is pulled as a **Git Submodule** into `vaartha-desktop/plugins/private`.
    *   *Note*: The public `.gitignore` MUST exclude `plugins/private` so accidental pushes don't leak code.
    *   The `vaartha-desktop` repo contains a definition for the submodule, but public users (who don't have auth) will get an empty folder or skip it.

### Release Pipeline (CI/CD)
*   **Pipeline A (Community)**:
    1.  Checkout `vaartha-desktop`.
    2.  Build.
    3.  Artifact: `Vaartha_Community_v1.0.exe`.
*   **Pipeline B (Enterprise)**:
    1.  Checkout `vaartha-desktop`.
    2.  Checkout `vaartha-plugins-ent` into `plugins/`.
    3.  Sign Plugins with Private Key.
    4.  Build.
    5.  Artifact: `Vaartha_Enterprise_v1.0.exe`.

## 4. Naming Conventions
*   **Branches**: `feature/xyz`, `bugfix/abc`, `release/v1.x`.
*   **Tags**: `v1.0.0-ce` (Community), `v1.0.0-ee` (Enterprise).
