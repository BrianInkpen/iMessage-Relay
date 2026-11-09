# iMessage Relay (iMess Relay)

A robust, lightweight Android client and macOS Python relay server that bridges **iMessage** and **SMS** to your Android device (fully optimized for older Android versions like Android 7.1 Nougat up to modern Android versions).

---

## Features

- **Blue & Green Bubbles:** Authentic Apple styling where iMessages appear in blue and SMS text messages appear in green (with right-aligned sent messages and left-aligned received messages).
- **Contact Integration:** Automatically resolves phone numbers and email handles to contact names from your device's address book. Long-press any conversation to instantly save new contacts.
- **Rich Media & Attachments:**
  - View picture messages (including automatic HEIC-to-JPEG conversion for iPhone photos).
  - Send pictures directly from your phone gallery using the `+` button.
  - Tap video attachments to open and stream them directly in **VLC for Android**.
- **Read & Delivery Receipts:** Real-time status indicators (`Sent`, `Delivered`, `Read` with timestamps).
- **Read Syncing:** Opening a chat automatically marks messages as read on your iMac.
- **Persistent Deletion:** Delete conversations or messages in the app, and they are permanently hidden locally and deleted on your iMac via AppleScript.
- **Tailscale VPN Support:** Connect securely over Tailscale so your messaging works seamlessly both at home on Wi-Fi and away from home on cellular data.
- **AMOLED Dark Mode:** Battery-saving dark theme with a toggle in the menu.

---

## Project Structure

- **Android App (`/app`)**: Built in Java with Material design styling, background polling service (`PollService`), and contact lookup.
- **macOS Relay Server (`imessage_relay.py`)**: A lightweight Python HTTP server that reads macOS `chat.db` and controls Apple Messages via AppleScript.

---

## Setup Instructions

### 1. macOS Relay Server Setup
1. Place `imessage_relay.py` in your home directory (`~/imessage_relay.py`).
2. **Grant Full Disk Access:** Open **System Settings > Privacy & Security > Full Disk Access** and ensure your **Terminal** app is enabled (required to read macOS `chat.db`).
3. Run the server:
   ```bash
   caffeinate -i python3 ~/imessage_relay.py
   ```
4. Note the generated **URL** and **Token**.

*(Optional)* To auto-start the server on iMac reboot, create a `LaunchAgent` plist in `~/Library/LaunchAgents/com.imessrelay.server.plist`.

### 2. Android App Setup
1. Install the APK (`app-debug.apk`) on your Android device.
2. Open the app, enter your Mac's **Tailscale URL** (e.g. `YOUR-IP-ADDRESS:8765`) and authentication **Token**, then tap **Save & connect**.

---

## Building from Source

```bash
./gradlew assembleDebug
```
The compiled APK will be located at:
`app/build/outputs/apk/debug/app-debug.apk`

---

## Author / Creator

Created and developed by **Brian Inkpen**.

---

## Issues & Support

If you encounter any issues or have questions, please let me know by emailing me at [djinkpen@inkpenmedia.org](mailto:djinkpen@inkpenmedia.org).

---

## Disclaimer & Privacy Notice

- **Personal Use Only:** This software is provided for personal, private use and educational purposes only. It is designed to allow you to bridge your own personal messages from your own macOS hardware to your own Android device.
- **Not Affiliated with Apple:** This project is an independent open-source utility and is not endorsed by, affiliated with, or supported by Apple Inc. iMessage is a registered trademark of Apple Inc.
