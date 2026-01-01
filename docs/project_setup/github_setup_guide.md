# GitHub Setup Guide for Vaartha

This guide will walk you through setting up the repository structure for your future company.

## Phase 1: Create the Organization
**Goal**: Establish a professional identity separate from your personal account.

1.  Log in to your personal GitHub (`mrsutharsuresh`).
2.  Go to **[New Organization](https://github.com/organizations/plan)**.
3.  **Plan**: Select "Free" (Public repositories are unlimited).
4.  **Name**: `vaartha-org` (or `vaartha-open-source` if taken).
5.  **Email**: Use your professional email.

## Phase 2: Create the "Monorepo"
**Goal**: Create the single public repository that will hold the Community Edition.

1.  Go to your new Organization page.
2.  Click **New Repository**.
3.  **Name**: `vaartha`.
4.  **Public/Private**: Select **Public**.
5.  **Initialize**: Check "Add a README file".
6.  **Add .gitignore**: Select "Python" (we will customize it later).
7.  **Add License**: Select **GNU Affero General Public License v3.0**.
8.  Click **Create Repository**.

## Phase 3: Push Your Local Code
**Goal**: Move your local work (`d:\Code\VAARTHA`) to this new repo.

1.  Open your terminal in `d:\Code\VAARTHA`.
2.  Initialize Git (if not already done):
    ```powershell
    git init
    ```
3.  Rename the default branch:
    ```powershell
    git branch -M main
    ```
4.  Add the new remote:
    ```powershell
    git remote add origin https://github.com/vaartha-org/vaartha.git
    ```
5.  Pull the license/readme created on GitHub (rebase strategy):
    ```powershell
    git pull origin main --rebase
    ```
6.  Add all your documentation and code:
    ```powershell
    git add .
    git commit -m "Initial commit: Documentation and Planning"
    ```
7.  Push:
    ```powershell
    git push -u origin main
    ```

## Phase 4: Create the Private Premium Repo (Future Step)
*Do this only when you are ready to write the proprietary plugins.*

1.  In the Organization, create **New Repository**.
2.  Name: `vaartha-premium`.
3.  **Public/Private**: Select **Private**.
4.  This will act as your "Secret Vault" for IP like the AI Engine logic.

## Phase 5: Branding (Optional but Recommended)
1.  Go to Organization Settings -> **Profile**.
2.  Upload the Vaartha Logo.
3.  Verified Badge: If you buy a domain (`vaartha.in`), verify it in GitHub settings to get the "Verified" badge.
