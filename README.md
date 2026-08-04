# 📱 WhatsApp Automation Tool — LEGEND SHYAM

[![Version](https://img.shields.io/badge/version-2.0-blue)](https://github.com/Dexsam07/LEGEND-MD)
[![License](https://img.shields.io/badge/license-LEGEND%20SHYAM-red)](https://github.com/Dexsam07/LEGEND-MD)
[![Node](https://img.shields.io/badge/node-%3E%3D16.0-brightgreen)](https://nodejs.org/)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-API-25D366)](https://whatsapp.com/)

> **Professional Two‑Stage WhatsApp Automation Dashboard**  
> Built with ❤️ by **LEGEND SHYAM** — for 🇮🇳 LEGEND SHYAM use only.

---

## 🚀 Overview

This tool provides a clean, secure, and efficient way to send bulk WhatsApp messages through a web interface.  
It features a **two‑stage dashboard**:

- **Stage 1 — Mobile Pairing:** Minimal screen to link your WhatsApp device using a pairing code.  
- **Stage 2 — Messaging Dashboard:** After successful linking, you get full control to send messages to single or multiple recipients with adjustable speed and live progress.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔐 **Two‑Stage UI** | Clean separation of pairing and messaging; automatically switches after device linking. |
| 📱 **Single Number Mode** | Send messages to one recipient with custom delay (minimum 5 seconds). |
| 👥 **Multiple Numbers Mode** | Add a list of numbers, send bulk messages with controlled speed. |
| 📂 **Message File Upload** | Upload a `.txt` file containing your message content. |
| 📊 **Live Progress** | Real‑time console logs, round counters, and success/failure stats. |
| ⏱ **Anti‑Ban Protection** | Configurable delay (min 5 seconds) between messages to avoid detection. |
| 🔁 **Continuous Sending** | Messages are sent in a loop until you manually stop the process. |
| 🧹 **Auto‑Formatting** | Phone numbers are cleaned automatically (removes extra characters). |
| 🔄 **Session Persistence** | Credentials saved locally; no need to re‑pair on every restart. |
| 🚪 **Logout Option** | Securely disconnect your WhatsApp session from the dashboard. |

---

## 📋 Prerequisites

- **Node.js** (version 16 or higher)  
- **npm** or **yarn**  
- A WhatsApp account with an active mobile number.

---

## ⚙️ Installation & Setup

### 1. Clone the repository
```bash
git clone https://github.com/Dexsam07/LEGEND-MD.git
cd LEGEND-MD
```

2. Install dependencies

```bash
npm install
```

3. Environment configuration

Copy the example environment file and adjust if necessary:

```bash
cp .env.example .env
```

Edit .env to set your preferred port (default: 22019):

```
PORT=22019
```

4. Start the server

```bash
npm start
```

For development with auto‑reload:

```bash
npm run dev
```

5. Access the dashboard

Open your browser and go to:

```
http://localhost:22019
```

---

🧭 Usage Guide

Stage 1 — Mobile Pairing

1. On the initial screen, you see only a mobile number input and a “GENERATE PAIR CODE” button.
2. Enter your WhatsApp mobile number (e.g., 9100000000 – country code without +).
3. Click the button – an 8‑digit pairing code will appear in the live console.
4. Open WhatsApp on your phone → Settings → Linked Devices → Link with phone number.
5. Enter the 8‑digit code to link the device.
6. Once linked, the dashboard automatically switches to Stage 2.

Stage 2 — Messaging Dashboard

After successful linking, you see two message type options:

📱 Single Number Mode

· Enter the recipient’s phone number.
· Set the delay between messages (minimum 5 seconds).
· Upload a .txt file containing your message.
· Click “START NOW” – messages will be sent repeatedly until you stop.

👥 Multiple Numbers Mode

· Add numbers one by one using the “+ ADD” button.
· Set the delay speed (minimum 5 seconds).
· Upload your message file.
· Click “START NOW” – the tool will cycle through the number list and send the message to each.

Live Monitoring & Control

· The console panel shows real‑time logs, including sent/failed status and current round.
· The “STOP SENDING” button immediately halts the sending process.
· The “LOGOUT” button disconnects the WhatsApp session.

---

📁 File Format

Message File (.txt)

Create a plain text file with your message content. Example:

```
Hello! This is an automated message.
Please reply if you receive this.
```

The tool reads the entire file content as the message to be sent.

---

🌐 API Endpoints

Endpoint Method Description
/api/pair POST Request a pairing code for the given mobile number.
/api/start-send POST Start sending messages (requires session active).
/api/stop-send POST Stop the current sending process.
/api/upload-numbers POST Upload a list of numbers (for multiple mode).
/api/status GET Get current connection status.
/api/logout POST Logout and clear the WhatsApp session.

---

🛠 Deployment

Render / Railway / Heroku

1. Push your code to a Git repository.
2. Create a new web service on your chosen platform.
3. Set the environment variable PORT (if needed) and start command npm start.
4. Deploy – the dashboard will be accessible via the provided URL.

Bot‑Hosting (e.g., legacy.bot-hosting.net)

Follow the platform’s instructions to deploy your Node.js application.
After deployment, provide your WhatsApp number to the bot to establish connection.

---

🔧 Troubleshooting

Issue Solution
Pairing code not shown Wait 5‑10 seconds; check browser console for errors; try with a different number.
Connection fails Ensure your WhatsApp number is correctly entered (without +). Re‑pair if needed.
Messages not sending Verify that the device is linked; check that numbers are valid; ensure the message file is .txt.
Logs not updating Refresh the page; make sure WebSocket or long‑polling is active.
Port already in use Change the PORT in .env and restart the server.

---

📌 Important Notes

· Minimum delay is 5 seconds between messages to respect WhatsApp’s anti‑spam policies and protect your account.
· The tool does not store messages or numbers permanently; all data is held in memory and cleared on stop/logout.
· Session credentials are stored locally in auth_info/ – do not share this folder.
· For continuous sending, the process loops indefinitely until you press STOP.

---

🤝 Contributing

This project is maintained by LEGEND SHYAM.
If you have suggestions or improvements, feel free to open an issue or pull request on the GitHub repository.

---

📢 Connect

· 📱 WhatsApp Channel: Join here
· 🤖 Telegram Bot: @Shyammd_143_bot
· 🐙 GitHub: Dexsam07/LEGEND-MD

---

📄 License

For 🇮🇳 LEGEND SHYAM use only.
Unauthorized distribution or commercial use is strictly prohibited.

---

Made with ❤️ by LEGEND SHYAM — automating WhatsApp, one message at a time.
