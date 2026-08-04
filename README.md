<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>WhatsApp Automation — LEGEND SHYAM</title>

    <!-- Font Awesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
    <!-- Socket.io client -->
    <script src="https://cdn.socket.io/4.5.0/socket.io.min.js">
    </script>

    <style>
        /* ===== RESET & BASE ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-primary: #0b0e14;
            --bg-card: #141a24;
            --bg-card-hover: #1c2535;
            --border-color: #2a3344;
            --text-primary: #f0f4ff;
            --text-secondary: #9aa8c7;
            --text-muted: #6a7a9a;
            --accent: #00d98b;
            --accent-dark: #00b873;
            --accent-glow: rgba(0, 217, 139, 0.25);
            --danger: #ff4757;
            --warning: #ffa502;
            --radius: 16px;
            --radius-sm: 10px;
            --shadow: 0 12px 48px rgba(0, 0, 0, 0.5);
            --transition: 0.25s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg-primary);
            color: var(--text-primary);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            background-image: radial-gradient(ellipse at 30% 20%, rgba(0, 217, 139, 0.04) 0%, transparent 60%),
                radial-gradient(ellipse at 70% 80%, rgba(0, 217, 139, 0.02) 0%, transparent 50%);
        }

        /* ===== APP CONTAINER ===== */
        .app-container {
            width: 100%;
            max-width: 820px;
            margin: 0 auto;
        }

        /* ===== CARD ===== */
        .card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            padding: 32px 36px;
            box-shadow: var(--shadow);
            backdrop-filter: blur(4px);
            transition: var(--transition);
        }

        .card:hover {
            border-color: rgba(0, 217, 139, 0.2);
        }

        /* ===== HEADER ===== */
        .app-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 28px;
            flex-wrap: wrap;
            gap: 12px;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .brand-icon {
            width: 44px;
            height: 44px;
            border-radius: 12px;
            background: linear-gradient(135deg, var(--accent), var(--accent-dark));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            color: #0b0e14;
            font-weight: 800;
            box-shadow: 0 0 24px var(--accent-glow);
        }

        .brand h1 {
            font-size: 20px;
            font-weight: 800;
            letter-spacing: -0.3px;
            background: linear-gradient(135deg, #fff 60%, var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .brand span {
            font-weight: 400;
            color: var(--text-secondary);
            font-size: 13px;
            -webkit-text-fill-color: var(--text-secondary);
        }

        .status-badge {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 13px;
            font-weight: 600;
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid var(--border-color);
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            display: inline-block;
            transition: var(--transition);
        }

        .status-dot.disconnected {
            background: var(--danger);
            box-shadow: 0 0 12px rgba(255, 71, 87, 0.4);
        }

        .status-dot.connecting {
            background: var(--warning);
            box-shadow: 0 0 12px rgba(255, 165, 2, 0.4);
            animation: pulse 1.2s ease-in-out infinite;
        }

        .status-dot.connected {
            background: var(--accent);
            box-shadow: 0 0 16px var(--accent-glow);
        }

        @keyframes pulse {
            0%,
            100% {
                opacity: 1;
                transform: scale(1);
            }
            50% {
                opacity: 0.4;
                transform: scale(0.85);
            }
        }

        /* ===== STAGE 1 — PAIRING ===== */
        #stage1 {
            display: block;
        }

        #stage1.hidden {
            display: none;
        }

        .pairing-title {
            font-size: 15px;
            font-weight: 500;
            color: var(--text-secondary);
            margin-bottom: 6px;
        }

        .pairing-sub {
            font-size: 13px;
            color: var(--text-muted);
            margin-bottom: 20px;
        }

        .input-group {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            align-items: center;
        }

        .input-group .field {
            flex: 1;
            min-width: 200px;
            position: relative;
        }

        .input-group .field i {
            position: absolute;
            left: 14px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
            font-size: 15px;
        }

        .input-group input {
            width: 100%;
            padding: 14px 14px 14px 44px;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border-color);
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-primary);
            font-size: 15px;
            font-family: inherit;
            transition: var(--transition);
            outline: none;
        }

        .input-group input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
            background: rgba(255, 255, 255, 0.06);
        }

        .input-group input::placeholder {
            color: var(--text-muted);
        }

        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            padding: 14px 28px;
            border: none;
            border-radius: var(--radius-sm);
            font-size: 14px;
            font-weight: 600;
            font-family: inherit;
            cursor: pointer;
            transition: var(--transition);
            background: var(--border-color);
            color: var(--text-secondary);
            white-space: nowrap;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--accent), var(--accent-dark));
            color: #0b0e14;
            box-shadow: 0 4px 20px var(--accent-glow);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 32px var(--accent-glow);
        }

        .btn-primary:active {
            transform: scale(0.97);
        }

        .btn-primary:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .btn-danger {
            background: rgba(255, 71, 87, 0.15);
            color: var(--danger);
            border: 1px solid rgba(255, 71, 87, 0.3);
        }

        .btn-danger:hover {
            background: rgba(255, 71, 87, 0.25);
        }

        .btn-outline {
            background: transparent;
            border: 1px solid var(--border-color);
            color: var(--text-secondary);
        }

        .btn-outline:hover {
            border-color: var(--text-secondary);
            color: var(--text-primary);
        }

        .btn-sm {
            padding: 8px 16px;
            font-size: 12px;
        }

        .btn-block {
            width: 100%;
            justify-content: center;
        }

        .pair-code-box {
            margin-top: 18px;
            padding: 16px 20px;
            background: rgba(0, 217, 139, 0.06);
            border: 1px dashed rgba(0, 217, 139, 0.25);
            border-radius: var(--radius-sm);
            display: none;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 12px;
        }

        .pair-code-box.show {
            display: flex;
        }

        .pair-code-box .code {
            font-size: 28px;
            font-weight: 800;
            letter-spacing: 4px;
            color: var(--accent);
            font-family: 'Courier New', monospace;
        }

        .pair-code-box .label {
            font-size: 13px;
            color: var(--text-secondary);
        }

        /* ===== STAGE 2 — DASHBOARD ===== */
        #stage2 {
            display: none;
        }

        #stage2.show {
            display: block;
        }

        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 18px;
            margin: 20px 0 18px;
        }

        @media (max-width: 640px) {
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
        }

        .mode-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-sm);
            padding: 18px 20px 20px;
            cursor: pointer;
            transition: var(--transition);
            position: relative;
        }

        .mode-card:hover {
            border-color: rgba(0, 217, 139, 0.3);
            background: rgba(255, 255, 255, 0.04);
        }

        .mode-card.active {
            border-color: var(--accent);
            background: rgba(0, 217, 139, 0.06);
            box-shadow: 0 0 20px var(--accent-glow);
        }

        .mode-card .icon {
            font-size: 22px;
            margin-bottom: 4px;
            display: block;
        }

        .mode-card .title {
            font-weight: 700;
            font-size: 15px;
        }

        .mode-card .desc {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .mode-card .check {
            position: absolute;
            top: 12px;
            right: 14px;
            color: var(--accent);
            font-size: 18px;
            opacity: 0;
            transition: var(--transition);
        }

        .mode-card.active .check {
            opacity: 1;
        }

        /* ===== CONTROLS ===== */
        .controls-area {
            margin: 16px 0 14px;
        }

        .controls-area .row {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
            align-items: center;
            margin-bottom: 12px;
        }

        .controls-area .row label {
            font-size: 13px;
            font-weight: 500;
            color: var(--text-secondary);
            min-width: 80px;
        }

        .controls-area .row input,
        .controls-area .row select {
            flex: 1;
            min-width: 140px;
            padding: 10px 14px;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border-color);
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-primary);
            font-size: 14px;
            font-family: inherit;
            outline: none;
            transition: var(--transition);
        }

        .controls-area .row input:focus,
        .controls-area .row select:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }

        .controls-area .row input[type="file"] {
            padding: 8px;
            background: transparent;
            border: none;
            color: var(--text-secondary);
        }

        .controls-area .row input[type="file"]::file-selector-button {
            padding: 6px 16px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            background: rgba(255, 255, 255, 0.04);
            color: var(--text-primary);
            font-family: inherit;
            cursor: pointer;
            transition: var(--transition);
        }

        .controls-area .row input[type="file"]::file-selector-button:hover {
            background: rgba(255, 255, 255, 0.08);
        }

        .number-list {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin: 6px 0 10px;
        }

        .number-tag {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 4px 12px 4px 14px;
            background: rgba(0, 217, 139, 0.08);
            border: 1px solid rgba(0, 217, 139, 0.15);
            border-radius: 40px;
            font-size: 13px;
            color: var(--text-primary);
        }

        .number-tag .remove {
            cursor: pointer;
            color: var(--text-muted);
            font-size: 12px;
            transition: var(--transition);
        }

        .number-tag .remove:hover {
            color: var(--danger);
        }

        /* ===== CONSOLE ===== */
        .console {
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-sm);
            padding: 14px 18px;
            height: 140px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 13px;
            color: var(--text-secondary);
            line-height: 1.6;
            margin-top: 14px;
            scroll-behavior: smooth;
        }

        .console .log-entry {
            opacity: 0.9;
        }

        .console .log-entry.success {
            color: var(--accent);
        }

        .console .log-entry.error {
            color: var(--danger);
        }

        .console .log-entry.info {
            color: #70b8ff;
        }

        .console .log-entry.warn {
            color: var(--warning);
        }

        .console::-webkit-scrollbar {
            width: 4px;
        }

        .console::-webkit-scrollbar-track {
            background: transparent;
        }

        .console::-webkit-scrollbar-thumb {
            background: var(--border-color);
            border-radius: 8px;
        }

        /* ===== STATS BAR ===== */
        .stats {
            display: flex;
            gap: 24px;
            margin: 12px 0 10px;
            flex-wrap: wrap;
        }

        .stats .stat {
            display: flex;
            align-items: baseline;
            gap: 6px;
            font-size: 13px;
            color: var(--text-secondary);
        }

        .stats .stat .num {
            font-weight: 700;
            font-size: 18px;
            color: var(--text-primary);
        }

        .stats .stat .num.green {
            color: var(--accent);
        }

        .stats .stat .num.red {
            color: var(--danger);
        }

        /* ===== TELEGRAM BADGE ===== */
        .telegram-badge {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: 18px;
            padding: 12px 18px;
            border-radius: var(--radius-sm);
            background: rgba(0, 136, 204, 0.08);
            border: 1px solid rgba(0, 136, 204, 0.15);
            font-size: 13px;
            color: var(--text-secondary);
            flex-wrap: wrap;
        }

        .telegram-badge a {
            color: #0088cc;
            font-weight: 600;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            transition: var(--transition);
        }

        .telegram-badge a:hover {
            color: #00a2e8;
            text-decoration: underline;
        }

        .telegram-badge .btn-telegram {
            background: #0088cc;
            color: #fff;
            padding: 6px 18px;
            border-radius: 40px;
            font-weight: 600;
            font-size: 13px;
            border: none;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .telegram-badge .btn-telegram:hover {
            background: #00a2e8;
            transform: scale(1.02);
        }

        /* ===== RESPONSIVE ===== */
        @media (max-width: 640px) {
            .card {
                padding: 20px 16px;
            }
            .input-group {
                flex-direction: column;
            }
            .input-group .field {
                min-width: 100%;
            }
            .btn {
                width: 100%;
                justify-content: center;
            }
            .brand h1 {
                font-size: 17px;
            }
            .stats {
                gap: 12px;
            }
            .pair-code-box .code {
                font-size: 22px;
            }
            .controls-area .row {
                flex-direction: column;
                align-items: stretch;
            }
            .controls-area .row label {
                min-width: auto;
            }
        }

        /* ===== UTILITY ===== */
        .mt-8 {
            margin-top: 8px;
        }
        .mt-12 {
            margin-top: 12px;
        }
        .mb-8 {
            margin-bottom: 8px;
        }
        .flex {
            display: flex;
        }
        .flex-center {
            align-items: center;
            justify-content: center;
        }
        .gap-8 {
            gap: 8px;
        }
        .gap-12 {
            gap: 12px;
        }
        .text-center {
            text-align: center;
        }
        .hidden {
            display: none !important;
        }
        .w-full {
            width: 100%;
        }
        .text-muted {
            color: var(--text-muted);
        }
        .text-secondary {
            color: var(--text-secondary);
        }
        .fade-in {
            animation: fadeIn 0.4s ease;
        }

        @keyframes fadeIn {
            0% {
                opacity: 0;
                transform: translateY(8px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* loader spinner */
        .spinner {
            display: inline-block;
            width: 18px;
            height: 18px;
            border: 2px solid rgba(0, 217, 139, 0.2);
            border-top: 2px solid var(--accent);
            border-radius: 50%;
            animation: spin 0.7s linear infinite;
        }

        @keyframes spin {
            0% {
                transform: rotate(0deg);
            }
            100% {
                transform: rotate(360deg);
            }
        }
    </style>
</head>

<body>

    <div class="app-container">
        <div class="card" id="app">

            <!-- ===== HEADER ===== -->
            <div class="app-header">
                <div class="brand">
                    <div class="brand-icon">
                        <i class="fab fa-whatsapp"></i>
                    </div>
                    <div>
                        <h1>LEGEND SHYAM <span>· WA</span></h1>
                    </div>
                </div>
                <div class="status-badge">
                    <span class="status-dot disconnected" id="statusDot"></span>
                    <span id="statusText">Disconnected</span>
                </div>
            </div>

            <!-- ===== STAGE 1 : PAIRING ===== -->
            <div id="stage1">
                <div class="pairing-title">
                    <i class="fas fa-phone-alt" style="margin-right: 8px; color: var(--accent);"></i> Mobile Pairing
                </div>
                <div class="pairing-sub">
                    Enter your WhatsApp number to generate an 8‑digit pairing code.
                </div>

                <div class="input-group">
                    <div class="field">
                        <i class="fas fa-phone"></i>
                        <input type="text" id="phoneInput" placeholder="e.g. 9100000000" value="9100000000" />
                    </div>
                    <button class="btn btn-primary" id="pairBtn">
                        <i class="fas fa-qrcode"></i> GENERATE PAIR CODE
                    </button>
                </div>

                <div class="pair-code-box" id="pairCodeBox">
                    <div>
                        <div class="label"><i class="fas fa-key"></i> Your 8‑digit code</div>
                        <div class="code" id="pairCodeDisplay">—— —— —— ——</div>
                    </div>
                    <button class="btn btn-outline btn-sm" id="copyCodeBtn">
                        <i class="fas fa-copy"></i> Copy
                    </button>
                </div>

                <div class="telegram-badge" style="margin-top:18px;">
                    <i class="fab fa-telegram-plane" style="color:#0088cc; font-size:18px;"></i>
                    <span>Control via Telegram too —</span>
                    <a href="https://t.me/Shyammd_143_bot" target="_blank">
                        <i class="fab fa-telegram"></i> @Shyammd_143_bot
                    </a>
                    <span style="color:var(--text-muted); font-size:12px;">(start → send number → get 8‑digit code)</span>
                </div>
            </div>

            <!-- ===== STAGE 2 : DASHBOARD ===== -->
            <div id="stage2">
                <!-- Mode selector -->
                <div style="font-size:14px; font-weight:500; color:var(--text-secondary); margin-bottom:4px;">
                    <i class="fas fa-bolt" style="color:var(--accent);"></i> Select Message Type
                </div>
                <div class="dashboard-grid">
                    <div class="mode-card active" data-mode="single" id="modeSingle">
                        <div class="check"><i class="fas fa-check-circle"></i></div>
                        <span class="icon">📱</span>
                        <div class="title">SINGLE NUMBER</div>
                        <div class="desc">Send to one recipient</div>
                    </div>
                    <div class="mode-card" data-mode="multiple" id="modeMultiple">
                        <div class="check"><i class="fas fa-check-circle"></i></div>
                        <span class="icon">👥</span>
                        <div class="title">MULTIPLE NUMBERS</div>
                        <div class="desc">Bulk send to many</div>
                    </div>
                </div>

                <!-- Controls -->
                <div class="controls-area">
                    <!-- Single number input -->
                    <div id="singleControls">
                        <div class="row">
                            <label><i class="fas fa-user"></i> Number</label>
                            <input type="text" id="singleNumber" placeholder="e.g. 919876543210" />
                        </div>
                    </div>

                    <!-- Multiple numbers input -->
                    <div id="multipleControls" class="hidden">
                        <div class="row">
                            <label><i class="fas fa-list"></i> Numbers</label>
                            <div style="flex:1; display:flex; gap:8px; flex-wrap:wrap;">
                                <input type="text" id="multiNumberInput" placeholder="e.g. 919876543210" style="flex:1; min-width:120px;" />
                                <button class="btn btn-outline btn-sm" id="addNumberBtn">
                                    <i class="fas fa-plus"></i> ADD
                                </button>
                            </div>
                        </div>
                        <div class="number-list" id="numberList"></div>
                    </div>

                    <!-- Speed & file -->
                    <div class="row">
                        <label><i class="fas fa-clock"></i> Speed</label>
                        <input type="number" id="speedInput" value="5" min="5" step="1" style="max-width:100px;" />
                        <span style="font-size:13px; color:var(--text-muted);">sec (min 5)</span>
                    </div>

                    <div class="row">
                        <label><i class="fas fa-file-alt"></i> Message</label>
                        <input type="file" id="messageFile" accept=".txt" />
                        <span style="font-size:12px; color:var(--text-muted);">.txt file</span>
                    </div>

                    <div class="row" style="gap:12px; flex-wrap:wrap;">
                        <button class="btn btn-primary" id="startSendBtn">
                            <i class="fas fa-play"></i> START NOW
                        </button>
                        <button class="btn btn-danger" id="stopSendBtn">
                            <i class="fas fa-stop"></i> STOP SENDING
                        </button>
                        <button class="btn btn-outline btn-sm" id="logoutBtn" style="margin-left:auto;">
                            <i class="fas fa-sign-out-alt"></i> Logout
                        </button>
                    </div>
                </div>

                <!-- Stats -->
                <div class="stats">
                    <div class="stat"><span class="num" id="statRounds">0</span> Rounds</div>
                    <div class="stat"><span class="num green" id="statSent">0</span> Sent</div>
                    <div class="stat"><span class="num red" id="statFailed">0</span> Failed</div>
                    <div class="stat" id="statProgress" style="flex:1; text-align:right; color:var(--text-muted);">● Idle</div>
                </div>

                <!-- Console -->
                <div class="console" id="console"></div>

                <!-- Telegram badge (repeated) -->
                <div class="telegram-badge" style="margin-top:14px;">
                    <i class="fab fa-telegram-plane" style="color:#0088cc; font-size:16px;"></i>
                    <span>Bot:</span>
                    <a href="https://t.me/Shyammd_143_bot" target="_blank">
                        <i class="fab fa-telegram"></i> @Shyammd_143_bot
                    </a>
                    <span style="color:var(--text-muted); font-size:12px;">— start → send number → get code</span>
                </div>
            </div>

        </div><!-- /.card -->
    </div><!-- /.app-container -->

    <script>
        // ============================================================
        //  FRONTEND LOGIC — Socket.io + DOM
        // ============================================================

        // ----- DOM refs -----
        const $ = id => document.getElementById(id);
        const stage1 = $('stage1');
        const stage2 = $('stage2');
        const phoneInput = $('phoneInput');
        const pairBtn = $('pairBtn');
        const pairCodeBox = $('pairCodeBox');
        const pairCodeDisplay = $('pairCodeDisplay');
        const copyCodeBtn = $('copyCodeBtn');
        const statusDot = $('statusDot');
        const statusText = $('statusText');
        const consoleEl = $('console');

        const modeSingle = $('modeSingle');
        const modeMultiple = $('modeMultiple');
        const singleControls = $('singleControls');
        const multipleControls = $('multipleControls');
        const singleNumber = $('singleNumber');
        const multiNumberInput = $('multiNumberInput');
        const addNumberBtn = $('addNumberBtn');
        const numberList = $('numberList');
        const speedInput = $('speedInput');
        const messageFile = $('messageFile');
        const startSendBtn = $('startSendBtn');
        const stopSendBtn = $('stopSendBtn');
        const logoutBtn = $('logoutBtn');

        const statRounds = $('statRounds');
        const statSent = $('statSent');
        const statFailed = $('statFailed');
        const statProgress = $('statProgress');

        // ----- State -----
        let socket = null;
        let isConnected = false;
        let isSending = false;
        let selectedMode = 'single';
        let numbers = [];
        let pairCode = '';

        // ----- Helpers -----
        function log(msg, type = 'info') {
            const entry = document.createElement('div');
            entry.className = `log-entry ${type}`;
            const time = new Date().toLocaleTimeString();
            entry.textContent = `[${time}] ${msg}`;
            consoleEl.appendChild(entry);
            consoleEl.scrollTop = consoleEl.scrollHeight;
        }

        function setStatus(state, text) {
            statusDot.className = 'status-dot ' + state;
            statusText.textContent = text;
        }

        function updateStats(rounds, sent, failed) {
            statRounds.textContent = rounds || 0;
            statSent.textContent = sent || 0;
            statFailed.textContent = failed || 0;
        }

        function renderNumberTags() {
            numberList.innerHTML = '';
            numbers.forEach((n, i) => {
                const tag = document.createElement('span');
                tag.className = 'number-tag';
                tag.innerHTML = `${n} <span class="remove" data-index="${i}"><i class="fas fa-times-circle"></i></span>`;
                tag.querySelector('.remove').addEventListener('click', () => {
                    numbers.splice(i, 1);
                    renderNumberTags();
                });
                numberList.appendChild(tag);
            });
        }

        // ----- Socket.io -----
        function initSocket() {
            socket = io();

            socket.on('connect', () => {
                log('🔌 WebSocket connected.', 'info');
            });

            socket.on('disconnect', () => {
                log('🔌 WebSocket disconnected.', 'warn');
                if (!isConnected) setStatus('disconnected', 'Disconnected');
            });

            socket.on('status', (data) => {
                const { state, message } = data;
                if (state === 'connected') {
                    isConnected = true;
                    setStatus('connected', 'Connected');
                    stage1.classList.add('hidden');
                    stage2.classList.add('show');
                    log('✅ WhatsApp linked successfully!', 'success');
                    log('📋 Ready to send messages.', 'info');
                    updateStats(0, 0, 0);
                } else if (state === 'disconnected') {
                    isConnected = false;
                    setStatus('disconnected', 'Disconnected');
                    stage1.classList.remove('hidden');
                    stage2.classList.remove('show');
                    log('❌ Disconnected. Re-pair to continue.', 'error');
                } else if (state === 'connecting') {
                    setStatus('connecting', 'Connecting…');
                } else {
                    if (message) log(`📡 ${message}`, 'info');
                }
            });

            socket.on('pair-code', (data) => {
                pairCode = data.code;
                pairCodeDisplay.textContent = pairCode.split('').join(' ');
                pairCodeBox.classList.add('show');
                log(`🔑 Pairing code: ${pairCode}`, 'success');
                setStatus('connecting', 'Waiting for link…');
                pairBtn.disabled = false;
                pairBtn.innerHTML = '<i class="fas fa-qrcode"></i> GENERATE PAIR CODE';
            });

            socket.on('pair-error', (msg) => {
                log(`❌ ${msg}`, 'error');
                pairBtn.disabled = false;
                pairBtn.innerHTML = '<i class="fas fa-qrcode"></i> GENERATE PAIR CODE';
            });

            socket.on('progress', (data) => {
                const { rounds, sent, failed, current, total, status } = data;
                updateStats(rounds, sent, failed);
                if (status === 'sending') {
                    statProgress.textContent = `● Sending ${current}/${total}`;
                } else if (status === 'idle') {
                    statProgress.textContent = '● Idle';
                } else if (status === 'stopped') {
                    statProgress.textContent = '⏹ Stopped';
                } else if (status === 'done') {
                    statProgress.textContent = '✅ Completed';
                }
            });

            socket.on('log', (data) => {
                log(data.msg, data.type || 'info');
            });

            socket.on('send-done', () => {
                isSending = false;
                startSendBtn.disabled = false;
                startSendBtn.innerHTML = '<i class="fas fa-play"></i> START NOW';
                statProgress.textContent = '✅ Completed';
                log('🏁 Sending completed.', 'success');
            });

            socket.on('send-stopped', () => {
                isSending = false;
                startSendBtn.disabled = false;
                startSendBtn.innerHTML = '<i class="fas fa-play"></i> START NOW';
                statProgress.textContent = '⏹ Stopped';
                log('⏹ Sending stopped by user.', 'warn');
            });

            socket.on('error', (msg) => {
                log(`❌ ${msg}`, 'error');
                isSending = false;
                startSendBtn.disabled = false;
                startSendBtn.innerHTML = '<i class="fas fa-play"></i> START NOW';
            });
        }

        // ----- Pairing -----
        async function generatePair() {
            const phone = phoneInput.value.trim().replace(/\D/g, '');
            if (!phone || phone.length < 8) {
                log('⚠️ Please enter a valid mobile number.', 'warn');
                return;
            }

            pairBtn.disabled = true;
            pairBtn.innerHTML = '<span class="spinner"></span> Generating…';
            pairCodeBox.classList.remove('show');

            try {
                const res = await fetch('/api/pair', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ phone })
                });
                const data = await res.json();
                if (!res.ok) {
                    log(`❌ ${data.error || 'Pairing failed'}`, 'error');
                    pairBtn.disabled = false;
                    pairBtn.innerHTML = '<i class="fas fa-qrcode"></i> GENERATE PAIR CODE';
                    return;
                }
                // socket will handle the pair-code event
                log('📡 Pairing request sent. Waiting for code…', 'info');
            } catch (e) {
                log(`❌ Network error: ${e.message}`, 'error');
                pairBtn.disabled = false;
                pairBtn.innerHTML = '<i class="fas fa-qrcode"></i> GENERATE PAIR CODE';
            }
        }

        // ----- Copy code -----
        copyCodeBtn.addEventListener('click', () => {
            if (pairCode) {
                navigator.clipboard.writeText(pairCode).then(() => {
                    log('📋 Code copied to clipboard!', 'success');
                }).catch(() => {
                    // fallback
                    const ta = document.createElement('textarea');
                    ta.value = pairCode;
                    document.body.appendChild(ta);
                    ta.select();
                    document.execCommand('copy');
                    ta.remove();
                    log('📋 Code copied!', 'success');
                });
            }
        });

        // ----- Start send -----
        async function startSend() {
            if (isSending) return;

            // Validate
            if (!isConnected) {
                log('⚠️ Not connected. Please pair first.', 'warn');
                return;
            }

            const speed = parseInt(speedInput.value) || 5;
            if (speed < 5) {
                log('⚠️ Speed must be at least 5 seconds.', 'warn');
                return;
            }

            const file = messageFile.files[0];
            if (!file) {
                log('⚠️ Please select a .txt message file.', 'warn');
                return;
            }
            if (!file.name.endsWith('.txt')) {
                log('⚠️ Message file must be .txt format.', 'warn');
                return;
            }

            let targets = [];
            if (selectedMode === 'single') {
                const num = singleNumber.value.trim().replace(/\D/g, '');
                if (!num || num.length < 8) {
                    log('⚠️ Enter a valid single number.', 'warn');
                    return;
                }
                targets = [num];
            } else {
                if (numbers.length === 0) {
                    log('⚠️ Add at least one number for bulk send.', 'warn');
                    return;
                }
                targets = [...numbers];
            }

            // Read file
            const reader = new FileReader();
            reader.onload = async function(e) {
                const messageText = e.target.result;
                if (!messageText.trim()) {
                    log('⚠️ Message file is empty.', 'warn');
                    return;
                }

                const payload = {
                    mode: selectedMode,
                    numbers: targets,
                    speed,
                    message: messageText
                };

                isSending = true;
                startSendBtn.disabled = true;
                startSendBtn.innerHTML = '<span class="spinner"></span> Sending…';
                log(`🚀 Starting send to ${targets.length} number(s)…`, 'info');

                try {
                    const res = await fetch('/api/start-send', {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    const data = await res.json();
                    if (!res.ok) {
                        log(`❌ ${data.error || 'Failed to start'}`, 'error');
                        isSending = false;
                        startSendBtn.disabled = false;
                        startSendBtn.innerHTML = '<i class="fas fa-play"></i> START NOW';
                    }
                } catch (err) {
                    log(`❌ Network error: ${err.message}`, 'error');
                    isSending = false;
                    startSendBtn.disabled = false;
                    startSendBtn.innerHTML = '<i class="fas fa-play"></i> START NOW';
                }
            };
            reader.readAsText(file);
        }

        // ----- Stop send -----
        async function stopSend() {
            if (!isSending) return;
            try {
                await fetch('/api/stop-send', { method: 'POST' });
                log('⏹ Stop request sent.', 'warn');
            } catch (e) {
                log(`❌ ${e.message}`, 'error');
            }
        }

        // ----- Logout -----
        async function logout() {
            if (!confirm('Logout from WhatsApp?')) return;
            try {
                const res = await fetch('/api/logout', { method: 'POST' });
                const data = await res.json();
                log(data.message || 'Logged out.', 'info');
                isConnected = false;
                setStatus('disconnected', 'Disconnected');
                stage1.classList.remove('hidden');
                stage2.classList.remove('show');
                updateStats(0, 0, 0);
                statProgress.textContent = '● Idle';
            } catch (e) {
                log(`❌ ${e.message}`, 'error');
            }
        }

        // ----- Mode toggle -----
        function setMode(mode) {
            selectedMode = mode;
            modeSingle.classList.toggle('active', mode === 'single');
            modeMultiple.classList.toggle('active', mode === 'multiple');
            singleControls.classList.toggle('hidden', mode !== 'single');
            multipleControls.classList.toggle('hidden', mode !== 'multiple');
        }

        // ----- Event listeners -----
        pairBtn.addEventListener('click', generatePair);
        phoneInput.addEventListener('keydown', (e) => { if (e.key === 'Enter') generatePair(); });

        modeSingle.addEventListener('click', () => setMode('single'));
        modeMultiple.addEventListener('click', () => setMode('multiple'));

        addNumberBtn.addEventListener('click', () => {
            const raw = multiNumberInput.value.trim().replace(/\D/g, '');
            if (!raw || raw.length < 8) {
                log('⚠️ Enter a valid number (min 8 digits).', 'warn');
                return;
            }
            if (numbers.includes(raw)) {
                log('⚠️ Number already added.', 'warn');
                return;
            }
            numbers.push(raw);
            renderNumberTags();
            multiNumberInput.value = '';
            log(`➕ Added ${raw}`, 'info');
        });

        multiNumberInput.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') addNumberBtn.click();
        });

        startSendBtn.addEventListener('click', startSend);
        stopSendBtn.addEventListener('click', stopSend);
        logoutBtn.addEventListener('click', logout);

        // ----- Init -----
        setMode('single');
        setStatus('disconnected', 'Disconnected');
        initSocket();

        log('🟢 Welcome to LEGEND SHYAM WhatsApp Automation', 'success');
        log('📱 Enter your number and generate a pair code to begin.', 'info');

        // Auto-fill demo number
        if (!phoneInput.value) phoneInput.value = '9100000000';

        console.log('🚀 LEGEND SHYAM — WhatsApp Automation Tool');
        console.log('📌 Telegram: @Shyammd_143_bot');
    </script>

</body>
</html>
