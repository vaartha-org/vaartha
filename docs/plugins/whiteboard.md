# Whiteboard Plugin Specification

**Role**: A shared, infinite canvas for collaboration during calls.

## Technical Implementation

### 1. Canvas Engine
*   **Library**: **Fabric.js** (Standard) or **Excalidraw** (for "hand-drawn" feel).
*   **Rendering**:
     *   **Desktop**: `QWebEngineView` loading a local HTML/JS bundle.
     *   **Android**: `WebView` loading local assets.

### 2. Synchronization Protocol (Peer-to-Peer)
We do not use a central WebSocket server. Data travels over the **SIP MESSAGE** or **SIP INFO** channel, or a dedicated **DTLS-SRTP Data Channel**.

#### The Protocol
*   **Action-Based Sync**: Instead of sending the whole image, we send command deltas.
    ```json
    {
      "type": "DRAW",
      "obj": "PATH",
      "points": [[10,10], [12,14], ...],
      "color": "#FF0000",
      "thickness": 2,
      "uuid": "a1b2-c3d4"
    }
    ```
*   **Conflict Resolution**: Last-Write-Wins (LWW) based on NTP timestamp, or CRDT (Yjs) if complexity allows.

### 3. Features
*   **Pen / Marker / Eraser**: Standard tools.
*   **Image Drop**: Drag & Drop images onto the canvas. They are base64 encoded and sent to peers (limit 5MB).
*   **Save & Export**: Users can save the board as PNG/PDF locally.

## UI Integration
*   **Desktop**: Opens as a new Tab `[Call 10:23] [Whiteboard]`.
*   **Mobile**: A toggle button "Open Board" overlays the video feed.
