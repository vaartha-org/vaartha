# AI Recording & Insights Specification

**Goal**: Provide "Meeting Intelligence" (Transcripts, Summaries, Action Items) *without* sending a single byte of audio to the cloud.

## The constraints
1.  **Offline only**: No OpenAI API, no Google Cloud Speech.
2.  **Privacy**: Audio must stay in RAM or encrypted local disk.
3.  **Hardware**: Variable end-user hardware (Weak laptops vs. Gaming PCs).

## The Pipeline

### 1. Audio Capture
*   **Desktop**: `PyAudio` or `SoundCard` library to tap into the "Speaker Output" loopback (what the user hears) and "Microphone Input" (what the user says).
*   **Format**: Downsample to 16kHz Mono (optimal for Whisper).

### 2. Transcription (Speech-To-Text)
*   **Engine**: **Whisper.cpp** or **Faster-Whisper**.
*   **Model Selection (Auto-Detect)**:
    *   *High-End PC (RTX GPU)*: Load `medium` model.
    *   *Standard Laptop*: Load `base.en` (quantized int8).
    *   *Mobile*: Load `tiny` model.
*   **Diarization**: Identify "Speaker A" vs "Speaker B" based on stereo channel separation (Left=Remote, Right=Local) if possible.

### 3. Intelligence (The LLM)
*   **Engine**: **Llama.cpp** (Python bindings).
*   **Model**: **Phi-3-Mini** (3.8GB) or **Mistral-7B-Quantized**.
*   **Trigger**:
    *   *Real-time*: Too heavy for most.
    *   *Post-Call*: automatically starts processing when the red "Hang Up" button is pressed.
*   **Prompt**:
    > "You are a professional secretary. Summarize the following meeting transcript into 3 bullet points and list any assigned tasks."

### 4. Storage & Display
*   **Format**: Transcripts stored in `chat.db` (SQLite) linked to the Call History ID.
*   **UI**: A "Smart Summary" button appears next to the Call Log item once processing is done.
