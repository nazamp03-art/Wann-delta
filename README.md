<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Delta & Plato Relay Key Tool</title>
    <style>
        @keyframes rgbBorder {
            0% { border-color: #ff0000; box-shadow: 0 0 15px #ff0000; }
            33% { border-color: #00ff00; box-shadow: 0 0 15px #00ff00; }
            66% { border-color: #0000ff; box-shadow: 0 0 15px #0000ff; }
            100% { border-color: #ff0000; box-shadow: 0 0 15px #ff0000; }
        }

        @keyframes rgbBackground {
            0% { background-color: #1a0000; }
            33% { background-color: #001a00; }
            66% { background-color: #00001a; }
            100% { background-color: #1a0000; }
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            font-family: sans-serif;
            animation: rgbBackground 10s infinite;
            color: #f8fafc;
            display: flex;
            flex-direction: column;
        }

        /* Layar Login Key */
        #auth-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(15, 23, 42, 0.95);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 100;
        }
        .auth-card {
            background: #1e293b;
            padding: 24px;
            border-radius: 8px;
            width: 90%;
            max-width: 350px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            border: 2px solid #ff0000;
            animation: rgbBorder 6s infinite;
            box-sizing: border-box;
        }
        .auth-card input {
            width: 100%;
            padding: 10px;
            border-radius: 6px;
            border: 1px solid #475569;
            background: #0f172a;
            color: #fff;
            box-sizing: border-box;
            outline: none;
        }
        .auth-card button {
            padding: 10px;
            background: #10b981;
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
        }
        .auth-card button:hover {
            background: #059669;
        }
        #authError {
            color: #ef4444;
            font-size: 13px;
            text-align: center;
            display: none;
        }

        /* Aplikasi Utama */
        #app-container {
            display: none;
            flex-direction: column;
            width: 100%;
            height: 100%;
        }
        #menu-container {
            padding: 16px;
            background: #1e293b;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            display: flex;
            flex-direction: column;
            gap: 10px;
            z-index: 10;
            border-bottom: 3px solid #ff0000;
            animation: rgbBorder 6s infinite;
        }
        .header-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .watermark {
            font-size: 12px;
            color: #38bdf8;
            font-weight: bold;
            background: #0f172a;
            padding: 4px 8px;
            border-radius: 4px;
            border: 1px solid #38bdf8;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            border-radius: 6px;
            border: 2px solid #ff0000;
            background: #0f172a;
            color: #fff;
            box-sizing: border-box;
            outline: none;
            animation: rgbBorder 6s infinite;
        }
        .btn-group {
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
        }
        button {
            padding: 10px 16px;
            background: #3b82f6;
            color: white;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            flex: 1;
            min-width: 120px;
        }
        button:hover {
            background: #2563eb;
        }
        #copyBtn {
            background: #10b981;
        }
        #copyBtn:hover {
            background: #059669;
        }
        #quickBtn {
            background: #8b5cf6;
        }
        #quickBtn:hover {
            background: #7c3aed;
        }
        #status {
            font-size: 14px;
            color: #94a3b8;
        }
        #tokenDisplay {
            background: #020617;
            padding: 8px;
            border-radius: 4px;
            font-family: monospace;
            color: #38bdf8;
            word-break: break-all;
            display: none;
        }
        #viewer-container {
            flex: 1;
            width: 100%;
            position: relative;
            background: #000;
            border: 4px solid #ff0000;
            animation: rgbBorder 6s infinite;
            box-sizing: border-box;
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
        .hidden {
            display: none !important;
        }
    </style>
</head>
<body>

    <!-- Layar Verifikasi Key -->
    <div id="auth-screen">
        <div class="auth-card">
            <h3 style="margin: 0; text-align: center;">Masukan Key Akses</h3>
            <p style="font-size: 12px; color: #94a3b8; text-align: center; margin: 0;">Made by Wann</p>
            <input type="password" id="keyInput" placeholder="Masukkan Key di sini...">
            <div id="authError">Key salah! Silakan coba lagi.</div>
            <button id="loginBtn">Masuk Aplikasi</button>
        </div>
    </div>

    <!-- Halaman Utama Aplikasi -->
    <div id="app-container">
        <div id="menu-container">
            <div class="header-title">
                <h3 style="margin: 0;">Delta & Plato Relay Key Tool</h3>
                <span class="watermark">Made by Wann</span>
            </div>
            <input type="text" id="urlInput" placeholder="Tempel link delta bypass / plato di sini...">
            <div class="btn-group">
                <button id="startBtn">Muat Halaman</button>
                <button id="quickBtn">Buka ixcore.xyz</button>
                <button id="copyBtn" class="hidden">Salin Token</button>
            </div>
            <div id="status">Status: Masukkan tautan untuk memulai...</div>
            <div id="tokenDisplay"></div>
        </div>

        <div id="viewer-container" class="hidden">
            <iframe id="targetFrame" sandbox="allow-scripts allow-same-origin allow-forms allow-popups"></iframe>
        </div>
    </div>

    <script>
        const CORRECT_KEY = "WannDeltaKey-01";

        const authScreen = document.getElementById('auth-screen');
        const appContainer = document.getElementById('app-container');
        const keyInput = document.getElementById('keyInput');
        const loginBtn = document.getElementById('loginBtn');
        const authError = document.getElementById('authError');

        const startBtn = document.getElementById('startBtn');
        const quickBtn = document.getElementById('quickBtn');
        const copyBtn = document.getElementById('copyBtn');
        const urlInput = document.getElementById('urlInput');
        const statusDiv = document.getElementById('status');
        const viewerContainer = document.getElementById('viewer-container');
        const targetFrame = document.getElementById('targetFrame');
        const tokenDisplay = document.getElementById('tokenDisplay');

        let extractedToken = '';

        // Sistem Verifikasi Key
        loginBtn.addEventListener('click', function() {
            if (keyInput.value.trim() === CORRECT_KEY) {
                authScreen.style.display = 'none';
                appContainer.style.display = 'flex';
            } else {
                authError.style.display = 'block';
            }
        });

        startBtn.addEventListener('click', function() {
            const rawUrl = urlInput.value.trim();

            if (!rawUrl) {
                alert('Silakan masukkan tautan terlebih dahulu!');
                return;
            }

            statusDiv.innerText = 'Status: Memuat halaman verifikasi...';
            viewerContainer.classList.remove('hidden');
            targetFrame.src = rawUrl;
        });

        quickBtn.addEventListener('click', function() {
            const presetUrl = 'https://www.ixcore.xyz/';
            urlInput.value = presetUrl;
            statusDiv.innerText = 'Status: Memuat ixcore.xyz...';
            viewerContainer.classList.remove('hidden');
            targetFrame.src = presetUrl;
        });

        setInterval(function() {
            try {
                if (targetFrame.contentWindow) {
                    const frameDoc = targetFrame.contentDocument || targetFrame.contentWindow.document;
                    if (frameDoc) {
                        const bodyText = frameDoc.body.innerText;
                        const match = bodyText.match(/(FREE_[a-zA-Z0-9]+)/);
                        
                        if (match && match[1] && match[1] !== extractedToken) {
                            extractedToken = match[1];
                            tokenDisplay.innerText = extractedToken;
                            tokenDisplay.style.display = 'block';
                            copyBtn.classList.remove('hidden');
                            statusDiv.innerText = 'Status: Token berhasil ditemukan!';
                        }
                    }
                }
            } catch (e) {}
        }, 1000);

        copyBtn.addEventListener('click', function() {
            if (extractedToken) {
                navigator.clipboard.writeText(extractedToken).then(function() {
                    statusDiv.innerText = 'Status: Token berhasil disalin ke clipboard!';
                }).catch(function() {
                    const textArea = document.createElement("textarea");
                    textArea.value = extractedToken;
                    document.body.appendChild(textArea);
                    textArea.select();
                    document.execCommand('copy');
                    document.body.removeChild(textArea);
                    statusDiv.innerText = 'Status: Token berhasil disalin!';
                });
            }
        });
    </script>

</body>
</html>
