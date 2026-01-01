# Plugin Ecosystem Architecture

The Plugin System allows **VAARTHA** to evolve from a Chat App to a Workspace OS.

## Core Concepts

### 1. The "Sandbox" & Licensing
 Plugins run in a semi-isolated environment. This allows us to mix **Open Source (GPL)** Core with **Proprietary (Closed)** Plugins.
*   **Dynamic Loading**: Plugins are loaded at runtime, not statically linked. This (generally) respects the LGPL/GPL boundary if the API is clean.
*   **Signature Lock**: Production builds only load plugins signed by "Vaartha Corp" to prevent tampering, unless "Dev Mode" is active.

### 2. Plugin Manifest (`plugin.json`)
Every plugin must define:
```json
{
  "id": "com.vaartha.whiteboard",
  "name": "Collaborative Board",
  "version": "1.0.0",
  "permissions": ["DRAW_OVERLAY", "NETWORK_DATA_CHANNEL"],
  "entry_point": "main.py"
}
```

## Standard Plugins

### A. The Whiteboard
*   **Tech**: HTML5 Canvas (Fabric.js) rendered in a WebView.
*   **Sync**:
    *   Uses SIP **MESSAGE** method (Content-Type: `application/json`) to send vector updates (Line drawn from X,Y to A,B).
    *   No central server needed; state is shared P2P.

### B. AI Recording & Insights (Local)
*   **Privacy Rule**: Audio never leaves the device.
*   **Pipeline**:
    1.  **Capture**: Hook into the RTP Stream (Audio Receive).
    2.  **Transcribe**: Feed 30s chunks to **Whisper.cpp** (running locally).
    3.  **Analyze**: Text is fed to a quantized LLM (e.g., Llama-3-8B-4bit).
    4.  **Output**: "Meeting Minutes" generated as a text file in the chat.
*   **Hardware**: Checks for GPU (NVIDIA/AMD) or NPU availability. Falls back to lightweight models if CPU-only.

## User Custom Plugins
Users can write Python scripts (Desktop) or JS Widgets (Mobile) to add features like:
*   **Polls / Voting**
*   **Attendance Tracker** (for classrooms)
*   **File Drop** (Auto-accept files from specific users)
