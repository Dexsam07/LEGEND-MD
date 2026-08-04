# WhatsApp Automation Tool - LEGEND SHYAM

[![Node.js](https://img.shields.io/badge/Node.js-16%2B-brightgreen)](https://nodejs.org/)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-Web--JS-blue)](https://wwebjs.dev/)
[![License](https://img.shields.io/badge/License-LEGEND%20SHYAM-orange)](https://whatsapp.com/channel/0029VbBgXTsKwqSKZKy38w2o)

A professional WhatsApp automation tool featuring an improved two-stage dashboard for seamless pairing and messaging. Designed for 🇮🇳 **LEGEND SHYAM** use only.

---

## 📌 Features

### 🔹 Stage 1: Mobile Pairing (Initial Screen)
- Clean, minimal dashboard showing only:
  - Mobile number input field
  - **GENERATE PAIR CODE** button
  - Live console for logs

### 🔹 Stage 2: Messaging (After Device Linking)
- Message type selector: **Single** or **Multiple** numbers
- **Single Number Mode**: Send to one number with custom speed
- **Multiple Numbers Mode**: Add multiple numbers and send bulk messages
- File upload for messages (`.txt` format)
- Live progress tracking with statistics
- Connection status display
- Logout option

---

## 🛠 Prerequisites

- **Node.js** 16+ 
- **npm** or **yarn**

---

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-repo/whatsapp-automation.git
   cd whatsapp-automation
```

2. Install dependencies
   ```bash
   npm install
   ```
3. Configure environment
   · Edit .env file if needed (default port is 22019)
4. Start the server
   ```bash
   npm start
   ```
   For development with auto-reload:
   ```bash
   npm run dev
   ```
5. Access the application
   · Open your browser and navigate to: http://localhost:22019

---

🚀 Usage

Step 1: Mobile Pairing (Stage 1)

1. Enter your WhatsApp mobile number (e.g., 9100000000)
2. Click GENERATE PAIR CODE
3. Copy the 8‑digit code displayed in the console
4. Open WhatsApp → Settings → Linked Devices → Link with phone number
5. Enter the pairing code to connect

✅ Once linked, the dashboard automatically switches to Stage 2.

Step 2: Messaging Dashboard (Stage 2)

After successful linking, you'll see:

· SELECT MESSAGE TYPE section with two options:
  · 📱 SINGLE NUMBER
  · 👥 MULTIPLE NUMBERS

📱 Single Number Mode

· Enter the recipient number
· Set speed (minimum 5 seconds between messages)
· Upload a .txt message file
· Click START NOW

👥 Multiple Numbers Mode

· Add numbers one by one using the + ADD button
· Set speed (minimum 5 seconds)
· Upload a .txt message file
· Click START NOW

Step 3: Monitor Progress

· Watch the live console for real‑time updates
· View statistics: Rounds, Sent, Failed
· Click STOP SENDING to halt the process

---

📄 File Format

Create a plain text file (.txt) with your message content:

```
Hello! This is an automated message.
Please reply if you receive this.
```

---

🔌 API Endpoints

Method Endpoint Description
POST /api/pair Request pairing code
POST /api/start-send Start sending messages
POST /api/stop-send Stop sending messages
POST /api/upload-numbers Upload a file with numbers
GET /api/status Get connection status
POST /api/logout Logout from WhatsApp

---

⚠️ Important Notes

· Two‑Stage Design: Stage 1 only shows pairing; Stage 2 appears after successful linking.
· Minimum delay: 5 seconds between messages (anti‑ban protection).
· Auto‑cleaning: Phone numbers are automatically formatted.
· Session credentials: Saved locally in auth_info/ directory.
· Continuous sending: Messages continue until stopped manually.
· File uploads: Temporary files are deleted after use.

---

🔧 Troubleshooting

Connection Issues

· Check console for detailed error messages.
· Re‑pair if connection drops.
· Ensure WhatsApp is properly linked.

Pairing Code Not Appearing

· Wait 5‑10 seconds after clicking GENERATE PAIR CODE.
· Check browser console for errors.
· Try with a different number.

Messages Not Sending

· Verify WhatsApp is properly linked.
· Confirm that numbers are valid.
· Ensure message file is in .txt format.
· Review console logs for specific errors.

---

☁️ Deployment Options

You can deploy this bot on any cloud platform that supports Node.js, such as:

· Render – render.com
· Railway – railway.app
· Bot‑Hosting.net – Legacy Bot Hosting

Tip: After deployment, you can connect your Telegram bot (username: @Shyammd_143_bot) by providing your number, and it will automatically link to the deployed instance.

---

📢 Branding

Powered by 🇮🇳 LEGEND SHYAM

Join WhatsApp Channel
Visit Website

---

📜 License

For 🇮🇳 LEGEND SHYAM use only.
Unauthorized distribution or commercial use is strictly prohibited.

---
