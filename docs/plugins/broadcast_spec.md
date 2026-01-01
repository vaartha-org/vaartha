# Broadcast & Notification Plugin Spec

**Purpose**: Allows organizations (Schools/Offices) to send one-to-many alerts that are persistent and rich-media capable.

## 1. Feature Overview
*   **Push Announcements**: "Emergency Fire Drill at 2 PM", "Exam Schedule Released".
*   **Targeting**: Send to `All`, `@Staff`, `@Students`, or `Grade-12`.
*   **Rich Content**: Support for Images, PDFs, and HTML formatting.
*   **Persistence**: Notices live in a "Notice Board" tab, not just a fleeting popup.

## 2. Technical Implementation
*   **Protocol**: SIP `MESSAGE` or a proprietary HTTPS side-channel (fetched from MinIO).
*   **Payload**:
    ```json
    {
      "type": "broadcast",
      "priority": "high",
      "title": "School Closure",
      "body": "Due to heavy rain, school is closed tomorrow.",
      "attachment_url": "http://minio.local/files/notice.pdf",
      "expiry": "2026-01-02T18:00:00Z"
    }
    ```
*   **Client Behavior**:
    1.  Receives payload.
    2.  Check `priority`: If `high`, vibrated device even in silent mode (configurable).
    3.  Stores in local SQLite `notices.db`.
    4.  Updates "Notice Board" UI badge count.

## 3. Monetization
*   This is a **Premium Plugin**.
*   Free Tier: Text-only broadcasts.
*   Paid Tier: Rich Media, Attachments, and Analytics (Who saw it?).
