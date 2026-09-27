# LxHost

**Easy Web Development Kit for Android**

LxHost turns your Android device into a lightweight local web server. Host HTML, CSS, JavaScript, images, static files, and PHP projects directly from your phone or tablet.

No cloud account or separate PHP installation is required for local hosting.

## Features

- Host websites directly from Android
- Serve static HTML, CSS, JavaScript, images, fonts, JSON, and other web files
- Host a folder selected through Android’s file picker
- Import and serve a ZIP website project
- Optional bundled PHP runtime for PHP projects
- Configurable HTTP port and bind address
- Same-network/LAN access
- Optional public forwarding support
- Optional HTTP Basic Authentication
- Connection-attempt limits and temporary blocking
- Live server and request logs
- Open the hosted website directly in your browser
- Auto-start server when the app launches
- Keep the server running while the app is in the background
- Verbose logging for troubleshooting
- Dark user interface

## Requirements

- Android 5.0/API 21 or later
- ARM64-compatible Android device for the current release build
- A website folder or ZIP archive to host
- Wi-Fi or another network connection when accessing the site from another device

## Installation

1. Download the latest LxHost APK from the project’s Releases page.
2. Install the APK on your Android device.
3. If Android asks for permission to install from an unknown source, allow it for the application used to open the APK.
4. Open **LxHost**.

## Quick start

### 1. Select your website

1. Open LxHost.
2. Tap **Pick Source**.
3. Select a website folder using the Android file picker, or choose a ZIP archive.
4. Confirm the selected source.

A basic static website may look like this:

```text
my-site/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── app.js
├── images/
└── assets/
```

For a normal static website, LxHost uses `index.html` as the main page. PHP projects may use `index.php`.

### 2. Start the server

1. Return to the main screen.
2. Tap **Run**.
3. Wait until the server status changes to running.
4. Read the URL displayed in the live log.

Example:

```text
http://192.168.1.42:8080
```

The IP address will be different on each network and may change when the device reconnects to Wi-Fi.

### 3. Open your website

- Tap **Forward** to open the site in the browser on the Android device.
- To open it from another device, connect both devices to the same Wi-Fi network and enter the displayed URL in that device’s browser.

Example:

```text
http://192.168.*.*:8080
```

### 4. Stop the server

Tap **Stop** when you have finished sharing or testing the website.

## Hosting a folder

Folder hosting is recommended for active development.

When you edit files inside the selected folder, refresh the browser to load the latest version. All files and subfolders inside the selected directory can be served by the HTTP server.

## Hosting a ZIP file

1. Tap **Pick Source**.
2. Select a ZIP archive.
3. LxHost extracts the archive into app-private storage.
4. Start the server with **Run**.

Make sure the website entry file is located at the expected root level of the archive. If the ZIP contains an extra top-level folder, the website may not load until the project structure is corrected.

## PHP projects

LxHost includes a bundled PHP runtime. PHP does not need to be installed separately on the Android device.

Example project structure:

```text
php-project/
├── index.php
├── config.php
├── css/
└── includes/
```

The bundled runtime provides common PHP functionality, including support for capabilities such as cURL, SQLite3, OpenSSL, XML, ZIP, and image-related libraries. Actual behavior may depend on the PHP script, device, Android version, and runtime configuration.

> Only run PHP code that you trust. Review scripts before making a PHP project reachable by other devices.

## Settings

Open the navigation drawer and select **Settings**.

### Work Directory

The work directory is the folder used for hosted files. The default path shown by the app is:

```text
/storage/emulated/0/LxHost
```

Use **Browse** to choose another directory when required.

### Forward Rule

| Option | Description |
|---|---|
| **Same Network** | Allows devices connected to the same Wi-Fi or LAN. Recommended for local testing. |
| **Random Public** | Uses a randomized public URL/port when public forwarding is available. |
| **All** | Allows any reachable client that can connect to the server. |

Use **Same Network** unless public access is specifically required.

### Connection Attempts

These settings help limit repeated failed connection or authentication attempts:

- **Max Attempts** — maximum number of failed attempts.
- **Time Interval** — time window, in seconds, used to count attempts.
- **Block Duration** — number of minutes a blocked client is denied.

### Connection Lock

Enable **Enable Lock** to require a username and password.

1. Enable **Enable Lock**.
2. Enter a username.
3. Enter a strong password.
4. Confirm the password.
5. Select which connection methods require authentication.
6. Tap **Save**.

LxHost uses HTTP Basic Authentication. Basic Authentication is Base64-encoded and is not encryption by itself. Use it only on a trusted network, and never reuse an important personal password.

### Network

- **Port** — HTTP port used by the server. The default shown by the app is `8080`.
- **Bind Address** — network address where the server listens. The default example is `0.0.0.0`.
- **Auto Start Server on Launch** — starts the server automatically when LxHost opens.
- **Keep Alive in Background** — attempts to keep the server running while the app is minimized.
- **Verbose Logging** — shows more detailed server activity.

Tap **Save** to apply changes, **Reset** to restore defaults, or **Cancel** to discard unsaved changes.

## Main screen controls

| Control | Description |
|---|---|
| **Pick Source** | Select a folder or ZIP archive to host. |
| **Run** | Start the local web server. |
| **Stop** | Stop the local web server. |
| **Forward** | Open the hosted site and start the configured forwarding flow. |
| **Server Status** | Shows the current server state. |
| **Path to Host** | Displays the selected hosting source. |
| **Main File** | Shows the default entry file, usually `index.html`. |
| **Live Log** | Shows startup messages and incoming HTTP requests. |

Long-press entries in the live log to select and copy them.

## Network access

### Same-device access

Use the **Forward** button to open the website in the Android device’s browser.

### Same Wi-Fi access

1. Connect the Android device and visitor device to the same Wi-Fi network.
2. Start the LxHost server.
3. Copy the URL from the live log.
4. Open the URL in the visitor device’s browser.

Some guest Wi-Fi networks prevent devices from communicating with each other. If the URL does not open, try a trusted home, office, or hotspot network.

### Public access

Public forwarding should be used only when intentionally required. Before enabling it:

- Remove private files from the hosted folder.
- Enable the connection lock.
- Use a strong, unique password.
- Do not host secrets, API keys, backups, or personal documents.
- Stop the server when public access is no longer needed.

## Security recommendations

LxHost makes files from the selected source available to connected clients. You are responsible for choosing the correct files and network scope.

- Prefer **Same Network** for development and testing.
- Do not serve `.env` files, private keys, database files, passwords, or backups.
- Use a strong password when enabling the connection lock.
- Do not reuse your email, banking, or primary account password.
- Do not use LxHost to distribute malware, phishing pages, illegal content, or attack tools.
- Review PHP code before running it.
- Stop the server when it is no longer needed.
- Avoid public forwarding on an untrusted network.
- LxHost is intended for local development and sharing, not hardened production hosting.

## Troubleshooting

### The server remains on “Server starting” or “Forwarding”

Leave the LxHost app and reopen it. The in-app guide recommends reopening the app without repeatedly changing settings or tapping multiple controls.

### Another device cannot connect

1. Confirm the server is running.
2. Confirm both devices are on the same Wi-Fi/LAN.
3. Use the exact IP address and port shown in the live log.
4. Check whether guest-network isolation is enabled.
5. Try port `8080` or another unused port above `1024`.
6. Check the selected Forward Rule.
7. Check whether the connection lock credentials are correct.

### Port already in use

Open **Settings**, choose another unused port, save the changes, and start the server again.

### The home page does not load

Confirm that the selected source contains the correct entry file:

- Static website: `index.html`
- PHP website: `index.php`

Also check that the filename capitalization and folder structure are correct.

### CSS, JavaScript, or images are missing

Check that:

- The files are included in the selected folder or ZIP.
- Relative paths are correct.
- Filename capitalization matches the references in your HTML.
- Required subfolders were included in the hosted root.

### PHP files download instead of executing

Confirm that PHP is enabled in Settings, the file uses the `.php` extension, and the server was restarted after changing PHP settings.

### The server stops in the background

Enable **Keep Alive in Background**, allow notification permission if requested, and review Android battery-optimization settings for LxHost. Some device manufacturers may stop background services automatically.

### The URL changes

The device’s local IP address can change after reconnecting to Wi-Fi or changing networks. Always use the current URL shown in the live log.

## Permissions

LxHost requests the following permissions:

| Permission | Purpose |
|---|---|
| `INTERNET` | Runs the HTTP server and supports network functions. |
| `ACCESS_NETWORK_STATE` | Checks network availability and connection state. |
| `ACCESS_WIFI_STATE` | Reads Wi-Fi information needed for local hosting. |
| `FOREGROUND_SERVICE` | Supports server operation while the app is not visible. |
| `FOREGROUND_SERVICE_SPECIAL_USE` | Declares the background server service category on supported Android versions. |
| `POST_NOTIFICATIONS` | Displays server/background-service notifications where required by Android. |
| `WAKE_LOCK` | Helps maintain server responsiveness while background operation is enabled. |

The Android file picker is used to let users select the folders and ZIP files they want to host.

## Privacy

LxHost is designed for local hosting and does not require a cloud account. According to the in-app Terms of Service, the app does not use analytics or telemetry and stores its configuration locally.

The files you choose to host may be accessed by clients that can reach the server. Do not select private or sensitive folders unless you understand the network exposure.

Review the project’s official privacy policy before publishing the app, especially if future versions add analytics, crash reporting, advertisements, third-party forwarding, or other external services.

## Technical information

| Item | Value |
|---|---|
| App name | LxHost |
| Package ID | `com.bounce.lxhost.pro` |
| Minimum Android version | Android 5.0/API 21 |
| Target Android version | API 34 / Android 14 |
| Current version | 1.0 / build 1 |
| Architecture in current APK | ARM64 (`arm64-v8a`) |
| Main purpose | Local HTTP hosting for static and PHP web projects |

## Support

The project information shown inside the app lists the following support channels:

- Telegram: [@The_Bounce_MM](https://t.me/The_Bounce_MM)
- GitHub: [The-Bounce-LLC](https://github.com/The-Bounce-LLC)
- Discord: [LxHost community](https://discord.gg/J9QkWe9wB2)

## Responsible use

LxHost is intended for lawful web development, testing, demonstrations, offline applications, and controlled file sharing. Do not use it to host malware, phishing pages, illegal material, or content that violates another person’s rights.

You are responsible for the files you serve, the network configuration you choose, and all traffic generated from your device.

## License

MIT License

Copyright (c) 2026 The Bounce LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


If the project includes bundled PHP or third-party libraries, include their required license notices in the repository as well.

---

**LxHost — Host your web projects directly from Android.**
