# GrabDuct User Guide

## What is GrabDuct?

GrabDuct is a tool that captures video from Chrome browser tabs and sends it as GPU textures to VJ software (Resolume, VDMX, OBS, etc.). It achieves low-latency, high-quality video routing through zero-copy GPU texture sharing using Spout on Windows and Syphon on macOS.

## Version

| Component | Version |
|-----------|---------|
| Chrome Extension | 0.2.2 |
| Receiver App | 0.2.1 |

## System Requirements

| Item | Windows | macOS |
|------|---------|-------|
| OS | Windows 10/11 | macOS 13 (Ventura) or later |
| Browser | Chrome / Chromium 116+ | Chrome / Chromium 116+ |
| GPU | Direct3D 11 compatible | Metal compatible |
| Texture Output | Spout | Syphon |
| Runtime | GStreamer (bundled with installer) | GStreamer (bundled with .app) |

## Architecture

GrabDuct consists of two components:

1. **Chrome Extension** — Captures video from browser tabs and assigns them to players.
2. **Receiver Application** — A native app that runs in the system tray / menu bar, receives video via WebRTC, and outputs it as Spout/Syphon textures.

Both components must be running simultaneously for video capture to work.

---

## Setup

### 1. Installing the Receiver Application

#### Windows

Run the GrabDuct installer (`GrabDuctReceiverSetup.exe`). After installation, the receiver will reside in the system tray (notification area).

#### macOS

Open the DMG file (`GrabDuctReceiver.dmg`) and drag `GrabDuct Receiver.app` to the Applications folder.

**Handling Gatekeeper Warnings (for unsigned builds):**

On macOS, attempting to open an unsigned app may trigger a warning saying "cannot be opened because the developer cannot be verified." Use one of the following methods to resolve this:

**Method 1: Open via Right-Click**

1. Right-click (or Control-click) `GrabDuct Receiver.app` in Finder
2. Select **Open** from the context menu
3. Click **Open** in the confirmation dialog

This is only required the first time. After that, you can launch the app normally by double-clicking.

**Method 2: Remove quarantine attribute with xattr**

Run the following command in Terminal:

```bash
xattr -cr /Applications/GrabDuct\ Receiver.app
```

`xattr -cr` recursively removes the quarantine attribute (`com.apple.quarantine`) that macOS assigns to downloaded files, which bypasses the Gatekeeper block.

> `-c` removes all extended attributes; `-r` processes directories recursively.

### 2. Installing the Chrome Extension

**Installing from a ZIP package:**

1. Extract the distributed `grabduct-extension-vX.Y.Z.zip` to a folder of your choice
2. Navigate to `chrome://extensions/` in Chrome
3. Enable **Developer mode** in the top-right corner
4. Click **Load unpacked** and select the extracted folder
5. The GrabDuct icon will appear in the toolbar

**Loading directly from source:**

In step 4 above, select the `extension/` folder.

### 3. Starting the Receiver

Launch the GrabDuct Receiver application.

- **Windows**: An icon appears in the system tray. Right-click to open the menu.
- **macOS**: An icon appears in the menu bar. Click to open the menu. No icon is shown in the Dock.

Menu items:

- **Settings** — Open the settings panel
- **Quit** — Exit the application

### 4. Discord Authentication

Using GrabDuct requires joining and authenticating with the KonaLab Discord server.

1. Select **Settings** from the menu
2. Click **Log in with Discord** on the login screen
3. The Discord authorization page opens in your browser
4. Authorize the application
5. Once authenticated, the main screen becomes available

---

## Basic Usage

### Assigning a Tab to a Player

1. Open a page with video content in Chrome
2. Click the GrabDuct extension icon in the toolbar
3. The popup displays the current tab name and up to 4 player slots
4. Click a player slot showing "Idle" to assign the current tab

The status indicator turns green once capture begins.

### Player Slot States

| Indicator | Status | Meaning |
|-----------|--------|---------|
| Gray dot | Idle | No tab assigned |
| Green dot | Capturing | Video is being captured and sent |
| Red dot | Error | Capture failed (see Troubleshooting) |
| Lock icon | Supporter only | Requires Supporter plan |

### Unassigning a Tab

Click a player slot showing "This tab" to unassign the current tab.

### Reassigning a Player

Clicking a player already assigned to a different tab will display a confirmation dialog. Confirming will reassign the player to the current tab.

### Receiver Connection Status

The connection status is displayed at the top of the popup.

- **Green** ("Receiver connected") — The receiver app is running and reachable
- **Red** ("Receiver not connected") — The receiver app is not running or not responding

The extension checks the connection status every 5 seconds.

---

## Receiver Settings

Open the settings panel from the menu. There are three tabs.

### Status Tab

Displays the following information:

- Current plan (Free or Supporter) with player count and resolution limits
- Per-player status cards (connection state and resolution)
- Spout/Syphon output names for active players (e.g., `GrabDuct Player 1`)
- Error information

### Settings Tab

#### Discord Authentication

- Displays your Discord username and membership expiration date
- **Re-verify Role** — Manually re-verify Discord server membership and Supporter role
- **Log Out** — Sign out of Discord (returns to login screen)

#### Output Resolution

You can set the output resolution per player. Presets are organized by aspect ratio.

**16:9**
- 1280×720 (720p) — Free
- 1920×1080 (1080p) — Supporter only
- 2560×1440 (1440p) — Supporter only
- 3840×2160 (4K) — Supporter only

**4:3**
- 640×480 (VGA) — Free
- 960×720 — Free
- 1024×768 (XGA) — Free
- 1440×1080 — Supporter only
- 1920×1440 — Supporter only
- 2880×2160 — Supporter only

**1:1**
- 480×480 — Free
- 720×720 — Free
- 1080×1080 — Supporter only
- 1440×1440 — Supporter only
- 2160×2160 — Supporter only

Selecting **Custom** allows you to specify any width and height (capped at your plan's maximum resolution).

> Resolution changes take effect after reconnecting the player.

### About Tab

View application version information and open-source software license notices. Each license is displayed in a collapsible section.

Licenses shown:

- **GStreamer** — LGPL-2.1-or-later
- **Spout2 SDK** (Windows) — BSD 2-Clause License
- **Syphon Framework** (macOS) — BSD 3-Clause License
- **Rust Crates** (tokio, serde, egui, etc.) — MIT / Apache-2.0
- **Noto Sans JP** — SIL Open Font License 1.1

---

## Plan Comparison

| Feature | Free | Supporter |
|---------|------|-----------|
| Simultaneous Players | 2 | 4 |
| Max Resolution | 720p (1280×720) | 4K (3840×2160) |
| Resolution Presets | Standard only | All presets |

Supporter status is determined by your role on the KonaLab Discord server. It is valid for 30 days and is automatically re-verified when fewer than 7 days remain.

---

## Using with VJ Software

While a player is capturing, the video is available as a Spout (Windows) or Syphon (macOS) source. Source names are:

- `GrabDuct Player 1`
- `GrabDuct Player 2`
- `GrabDuct Player 3`
- `GrabDuct Player 4`

### Resolume Arena / Avenue

1. Open the **Sources** tab
2. Select **Spout** (Windows) or **Syphon** (macOS)
3. Choose the `GrabDuct Player N` source
4. Drag it to a layer/clip slot

### OBS Studio

1. Add a new **Source**
2. Select **Spout2 Capture** (Windows) or **Syphon Client** (macOS)
3. Choose `GrabDuct Player N` from the dropdown

### Other VJ Software (VDMX, MadMapper, etc.)

Any software that supports Spout (Windows) or Syphon (macOS) input will show GrabDuct players as available sources.

---

## Auto Recapture

GrabDuct automatically recaptures video in the following situations:

- SPA navigation (moving between videos without a full page reload)
- Changes to video elements within the page (DOM mutations)
- Navigation within single-page applications

Recapture is controlled with a 500ms debounce to prevent frequent retriggering. Player assignments are maintained during recapture.

---

## Troubleshooting

### Popup shows "Receiver not connected"

- Verify the GrabDuct Receiver application is running (check the system tray / menu bar)
- The receiver listens on `localhost:9876`. Ensure your firewall is not blocking local connections
- Restart the receiver application

### App won't open on macOS

If you see "cannot be opened because the developer cannot be verified," or nothing happens when you double-click:

1. Right-click the app in Finder → select **Open**, or
2. Run the following in Terminal:

```bash
xattr -cr /Applications/GrabDuct\ Receiver.app
```

See "Setup > macOS > Handling Gatekeeper Warnings" for details.

### Video not showing in VJ software

- Confirm the player status is green ("Receiving") in the settings panel
- Ensure the VJ software is scanning for Spout/Syphon sources
- Verify the correct player name (e.g., `GrabDuct Player 1`) is selected
- DRM-protected content may not be capturable via `captureStream()`

### "No video elements found on this page"

- Confirm a `<video>` element exists on the page and playback has started
- Navigate to the page with video and wait for it to fully load before assigning a player

### Player enters "Error" state

- Check Chrome DevTools console (F12) for `[GrabDuct]` log messages
- Common causes: video track ended, WebRTC ICE connection failure, page navigation
- Unassign the player and try reassigning

### Membership expiration warning

- A warning appears in the settings panel when your Discord membership expiration is approaching (fewer than 7 days remaining)
- Click **Re-verify Role** to refresh membership verification
- If you are no longer a server member, rejoin the Discord server and log in again

---

## Configuration File

The receiver's configuration file is stored at:

- **Windows**: `%APPDATA%\GrabDuct\config.json`
- **macOS**: `~/Library/Application Support/GrabDuct/config.json`

This file contains the Discord authentication token (obfuscated), Supporter expiration date, and per-player resolution settings. It is created automatically on first launch.

---

## Technical Details

- Video is transmitted from Chrome to the receiver via WebRTC over localhost (no external network communication)
- The WebSocket signaling server runs on `127.0.0.1:9876` (local only)
- H.264 High Profile is preferred for hardware acceleration
- Bitrate is set to a maximum of 50 Mbps to maximize quality over local connections
- GPU texture sharing uses Direct3D 11 shared textures (Windows) or IOSurface (macOS) for zero-copy transfer
- The macOS build is a Universal Binary (arm64 + x86_64)
- The receiver runs as a menu bar app and does not appear in the Dock (macOS)
- Audio capture and transmission are not supported
