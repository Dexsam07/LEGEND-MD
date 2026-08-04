# WhatsApp Automation Tool - LEGEND SHYAM  

🚀 **Professional WhatsApp Automation Tool** with a two‑stage dashboard and seamless Telegram bot integration.  
Built for 🇮🇳 **LEGEND SHYAM** – automate your WhatsApp messaging with ease.

![Version](https://img.shields.io/badge/version-2.0-blue) ![Node](https://img.shields.io/badge/node-16%2B-green) ![License](https://img.shields.io/badge/license-LEGEND%20SHYAM-red)

---

## 📌 Table of Contents
- [Overview](#-overview)
- [Quick Deploy (One‑Click)](#-quick-deploy-oneclick)
- [Two‑Stage Dashboard](#-two-stage-dashboard)
- [Telegram Bot Integration (No Setup Required!)](#-telegram-bot-integration-no-setup-required)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Deployment Options](#-deployment-options)
- [Usage Guide](#-usage-guide)
  - [Connecting via Telegram Bot](#connecting-via-telegram-bot)
  - [Using the Web Dashboard (After Linking)](#using-the-web-dashboard-after-linking)
- [API Endpoints](#-api-endpoints)
- [File Formats](#-file-formats)
- [Troubleshooting](#-troubleshooting)
- [Branding & Support](#-branding--support)
- [License](#-license)

---

## ✨ Overview

This tool automates WhatsApp messaging through a clean web interface and a Telegram bot. It features:

- **Two‑Stage Dashboard** – minimal pairing screen first, full messaging dashboard after linking.
- **Flexible Messaging** – send to a single number or bulk to multiple numbers.
- **File Upload** – send your message from a `.txt` file.
- **Live Progress** – real‑time logs, sent/failed counts, and stop control.
- **Anti‑Ban Protection** – minimum 5‑second delay between messages.
- **Session Persistence** – credentials saved locally; no need to re‑pair on restart.
- **Telegram Bot Integration** – control everything from Telegram with inline buttons.

---

## 🚀 Quick Deploy (One‑Click)

Deploy your own instance of this tool on your preferred platform with just one click:

| Platform | Button |
|----------|--------|
| **Render** | [![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com) |
| **Railway** | [![Deploy on Railway](https://railway.app/button.svg)](https://railway.app) |
| **Heroku** | [![Deploy to Heroku](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com) |
| **Katabump** | [![Deploy to Katabump](https://katabump.com/deploy-button.svg)](https://katabump.com/) |
| **Bot‑Hosting.net** | [![Deploy to Bot-Hosting](https://legacy.bot-hosting.net/assets/deploy-button.svg)](https://legacy.bot-hosting.net/?aff=1340584978613932053) |

> **Note:** The Telegram bot **@Shyammd_143_bot** is already configured and maintained by LEGEND SHYAM. You do **not** need to provide any bot token – everything is pre‑set in the code. Just deploy and the bot will work with your instance automatically.

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

## 🤖 Telegram Bot Integration (No Setup Required!)

We have already deployed and maintained the Telegram bot **[@Shyammd_143_bot](https://t.me/Shyammd_143_bot)** for you.  
**You do not need to configure any bot token or environment variables** – the bot is fully ready to use and is already linked to the code.

Simply open Telegram, search for **@Shyammd_143_bot**, and start the bot.  
It will guide you through the entire pairing process.

### How the Bot Works
1. **Start** – send `/start` or click the **Start** button.
2. **Connect** – click the **“Connect WhatsApp”** inline button.
3. **Enter Number** – send your WhatsApp mobile number (with or without country code, e.g., `9100000000`).
4. **Get Pairing Code** – the bot replies with an 8‑digit pairing code.
5. **Link Device** – open WhatsApp → Settings → Linked Devices → Link with phone number, and enter the code.
6. **Success** – the bot confirms that your device is linked. You can now send messages via the web dashboard or Telegram commands.

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
3. Configure environment (optional)
   · Copy .env.example to .env (if provided) or create a new .env file.
   · Set the desired PORT (default: 22019).
          Note: The Telegram bot token is already embedded in index.js – you do not need to add it.
   ```env
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
5. Access the web dashboard
   · Open your browser and go to http://localhost:22019

---

🚀 Deployment Options

You can deploy this tool on various platforms. The Telegram bot will work with any deployed instance as long as the instance is running.

· Render – use the Node.js environment.
    https://render.com/images/deploy-to-render-button.svg
· Railway – simple one‑click deploy.
    https://railway.app/button.svg
· Heroku – deploy with a single click.
    https://www.herokucdn.com/deploy/button.svg
· Katabump – another hosting option.
    https://katabump.com/deploy-button.svg
· Legacy Bot Hosting – use with your own server.
    https://legacy.bot-hosting.net/assets/deploy-button.svg
· VPS / Any Cloud – standard Node.js deployment.

Important: The Telegram bot @Shyammd_143_bot is already hosted and maintained by LEGEND SHYAM. It will work with your deployed instance automatically, as long as your instance is reachable. No extra configuration is needed.

---

📖 Usage Guide

Connecting via Telegram Bot

1. Open Telegram and search for @Shyammd_143_bot.
2. Send /start and click the “Connect WhatsApp” button.
3. Send your WhatsApp number (e.g., 9100000000 – without + or spaces).
4. Copy the 8‑digit pairing code provided by the bot.
5. In WhatsApp → Settings → Linked Devices → Link with phone number → enter the code.
6. Once linked, the bot will confirm. You can now use the web dashboard or Telegram commands to send messages.

Using the Web Dashboard (After Linking)

1. Pair Your Device (if not already paired via the bot):
   · Open the web dashboard at http://localhost:22019
   · Enter your mobile number and click GENERATE PAIR CODE.
   · Copy the code from the console and link as described above.
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
