# WhatsApp Automation Tool - LEGEND SHYAM  

🚀 **Professional WhatsApp Automation Tool** with a two‑stage dashboard and full Telegram bot integration.  
Built for 🇮🇳 **LEGEND SHYAM** – automate your WhatsApp messaging with ease.

![Version](https://img.shields.io/badge/version-2.0-blue) ![Node](https://img.shields.io/badge/node-16%2B-green) ![License](https://img.shields.io/badge/license-LEGEND%20SHYAM-red)

---

## 📌 Table of Contents
- [Features](#-features)
- [Two‑Stage Dashboard](#-two-stage-dashboard)
- [Telegram Bot Integration](#-telegram-bot-integration)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage Guide](#-usage-guide)
- [API Endpoints](#-api-endpoints)
- [File Formats](#-file-formats)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)
- [Branding & Support](#-branding--support)
- [License](#-license)

---

## ✨ Features

- **Two‑Stage Dashboard** – minimal pairing screen first, full messaging dashboard after linking.
- **Mobile Pairing** – generate an 8‑digit code and link your WhatsApp via the official app.
- **Flexible Messaging**:
  - **Single Number** – send to one recipient with custom delay.
  - **Multiple Numbers** – add numbers one by one or upload a list.
- **File Upload** – send your message from a `.txt` file.
- **Live Progress** – real‑time logs, sent/failed counts, and stop control.
- **Automatic Number Cleaning** – phone numbers are formatted automatically.
- **Session Persistence** – credentials saved locally; no need to re‑pair on restart.
- **Telegram Bot** – control everything from Telegram with inline buttons.
- **Anti‑Ban Protection** – minimum 5‑second delay between messages.
- **Cross‑Platform** – runs on any Node.js environment.

---

## 🖥️ Two‑Stage Dashboard

### Stage 1: Mobile Pairing (Initial Screen)
- Clean dashboard with **only**:
  - Mobile number input field
  - **GENERATE PAIR CODE** button
  - Live console/log area
- After generating the code, you see an 8‑digit pairing code in the console.
- Use it in WhatsApp → Settings → Linked Devices → Link with phone number.

### Stage 2: Messaging Dashboard (After Linking)
Once the device is linked, the dashboard auto‑switches to:
- **Message Type Selector** – SINGLE NUMBER or MULTIPLE NUMBERS.
- **Single Mode** – enter one number, set speed (≥5s), upload message, and start.
- **Multiple Mode** – add numbers using the **+ ADD** button, set speed, upload message, and start.
- **Live Statistics** – Rounds, Sent, Failed.
- **Stop Button** – halt sending at any time.
- **Logout** – disconnect WhatsApp session.

---

## 🤖 Telegram Bot Integration

The tool is fully controllable via the **[@Shyammd_143_bot](https://t.me/Shyammd_143_bot)** Telegram bot.

### How It Works
1. **Start the Bot** – send `/start` or click the **Start** button.
2. **Inline Keyboard** – the bot presents a **“Connect WhatsApp”** button.
3. **Click the Button** – the bot asks for your WhatsApp mobile number.
4. **Enter Number** – send your number (with or without country code).
5. **Pairing Code** – the bot returns an 8‑digit pairing code.
6. **Link Device** – open WhatsApp → Settings → Linked Devices → Link with phone number, and enter the code.
7. **Success** – the bot confirms connection and you can now send messages via Telegram commands.

### Telegram Commands
| Command | Description |
|---------|-------------|
| `/start` | Show welcome message and the **Connect WhatsApp** button. |
| `/status` | Check current connection status. |
| `/send` | (After linking) Start sending a message (prompts for number(s) and message). |
| `/stop` | Stop an ongoing sending process. |
| `/logout` | Disconnect the WhatsApp session. |

All Telegram interactions mirror the web dashboard functionalities, making remote control seamless.

---

## 📋 Prerequisites

- **Node.js** 16.x or higher
- **npm** or **yarn** package manager
- A **WhatsApp** account (active mobile number)
- **Telegram** account (to use the bot)

---

## ⚙️ Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Dexsam07/LEGEND-MD.git
   cd LEGEND-MD
```

2. Install dependencies
   ```bash
   npm install
   ```
3. Configure environment
   · Copy .env.example to .env (if provided) or create a new .env file.
   · Set the desired PORT (default: 22019).
   ```env
   PORT=22019
   TELEGRAM_BOT_TOKEN=your_bot_token_here   # optional, if you host the bot separately
   ```
4. Start the server
   ```bash
   npm start
   ```
   For development with auto‑reload:
   ```bash
   npm run dev
   ```
5. Access the web dashboard
   · Open your browser and go to http://localhost:22019

---

🔧 Configuration

· Session Storage – session credentials are saved in the auth_info/ folder. Keep this folder safe; deleting it will require re‑pairing.
· Environment Variables – all settings are in .env.
· Telegram Bot – the bot token can be set in .env if you run the bot as part of this project. Alternatively, the bot can be hosted separately (the recommended approach is to use the already active @Shyammd_143_bot).

---

📖 Usage Guide

Web Dashboard Usage

1. Pair Your Device
   · Enter your mobile number (e.g., 9100000000 – without + or spaces).
   · Click GENERATE PAIR CODE.
   · Copy the 8‑digit code from the live console.
   · In WhatsApp → Settings → Linked Devices → Link with phone number → enter the code.
   · The dashboard will automatically switch to Stage 2.
2. Choose Message Type
   · SINGLE NUMBER – for one recipient.
   · MULTIPLE NUMBERS – for multiple recipients.
3. Single Number Mode
   · Enter the victim's number.
   · Set speed (minimum 5 seconds).
   · Upload a .txt file with your message.
   · Click START NOW.
4. Multiple Numbers Mode
   · Add numbers using the + ADD button (you can also upload a list via API).
   · Set speed.
   · Upload message file.
   · Click START NOW.
5. Monitor & Control
   · Watch the console for real‑time logs.
   · See statistics update.
   · Click STOP SENDING to pause the process.

Telegram Bot Usage

· Start: /start – shows main menu.
· Connect: Click the Connect WhatsApp button, then send your number.
· Send: After linking, use /send and follow the prompts (number(s) and message).
· Stop: /stop during an active send.
· Logout: /logout to disconnect.

---

📡 API Endpoints

The tool exposes a RESTful API for integration:

Method Endpoint Description
POST /api/pair Generate pairing code (requires number in body).
POST /api/start-send Start sending messages (requires type, numbers, speed, message).
POST /api/stop-send Stop the current sending process.
POST /api/upload-numbers Upload a file with numbers (for bulk).
GET /api/status Get connection status.
POST /api/logout Logout from WhatsApp.

---

📄 File Formats

Message File (.txt)

Create a plain text file with your message content.
Example:

```
Hello! This is an automated message from LEGEND SHYAM.
Please reply if you receive this.
```

Numbers File (.txt or .csv)

For bulk upload, list one number per line:

```
9100000000
9199999999
9188888888
```

---

🚀 Deployment

You can deploy this tool on various platforms:

· Render – use the Node.js environment.
· Railway – simple one‑click deploy.
· bot‑hosting.net – (legacy) use with your own server.
· VPS / Any Cloud – standard Node.js deployment.

Note: The Telegram bot @Shyammd_143_bot is already hosted and can be used directly with your deployed WhatsApp automation instance. Ensure your instance's API is accessible (or use the local web dashboard).

---

🛠️ Troubleshooting

Issue Solution
Pairing code not appearing Wait 5‑10 seconds after clicking GENERATE PAIR CODE. Check console logs. Try with a different number.
Connection drops Re‑pair using the dashboard or Telegram bot. Ensure stable internet.
Messages not sending Verify WhatsApp is linked. Check that numbers are valid (with country code). Ensure message file is a .txt. Review console logs for errors.
Telegram bot doesn't respond Make sure you're using the correct bot @Shyammd_143_bot. Check your internet.
“Invalid number” error Ensure the number includes the country code without + (e.g., 9100000000 for India).
Session expired Delete the auth_info/ folder and re‑pair.

---

🏷️ Branding & Support

Powered by LEGEND SHYAM
👑 Join WhatsApp Channel
📱 Telegram Bot
🐙 GitHub Repository

---

📜 License

This project is licensed under the LEGEND SHYAM proprietary license.
For 🇮🇳 LEGEND SHYAM use only. Unauthorized distribution or commercial use is prohibited.

---

🙏 Acknowledgments

· WhatsApp Web – for the underlying protocol.
· Baileys – the WhatsApp library powering the automation.
· Telegram Bot API – for enabling remote control.
· The LEGEND SHYAM Community – for continuous support and feedback.

---

Happy Automating!
LEGEND SHYAM – Making Automation Legendary.

