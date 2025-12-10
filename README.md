<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Candra Tools - Media Downloader & IQC Generator</title>
    <style>
        /* --- 1. CSS Dasar & Latar Belakang (Tema Gelap ala Game) --- */
        :root {
            --dark-blue: #0d1b32;
            --main-blue: #1f50a8;
            --accent-gold: #ffc107;
            --text-light: #f0f0f0;
            --text-soft: #aaaaaa;
            --card-bg: rgba(25, 45, 80, 0.6);
            --chat-bubble: #0b93f6; /* Warna chat iOS */
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: var(--dark-blue);
            color: var(--text-light);
            margin: 0;
            padding: 0;
            /* Simulasi pola latar belakang vertikal seperti di game */
            background-image: repeating-linear-gradient(90deg, var(--dark-blue), var(--dark-blue) 40px, rgba(31, 80, 168, 0.1) 41px, rgba(31, 80, 168, 0.1) 80px);
            background-size: cover;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .container {
            width: 90%;
            max-width: 1200px;
            margin: 20px auto;
            padding: 20px;
        }

        /* --- 2. Header dan Developer Name --- */
        header {
            background-color: rgba(0, 0, 0, 0.3);
            padding: 15px 0;
            text-align: center;
            border-bottom: 2px solid var(--main-blue);
        }

        header h1 {
            color: var(--accent-gold);
            margin: 0;
            font-size: 2.5em;
            text-shadow: 0 0 10px rgba(255, 193, 7, 0.5);
        }

        .developer-info {
            font-size: 0.9em;
            color: var(--text-soft);
            margin-top: 5px;
        }

        /* --- 3. Gaya Kartu & Fitur Utama --- */
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin-top: 30px;
        }

        .card {
            background-color: var(--card-bg);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            border-left: 5px solid var(--main-blue);
            transition: transform 0.3s, border-left-color 0.3s;
        }

        .card:hover {
            transform: translateY(-5px);
            border-left-color: var(--accent-gold);
        }

        .card h3 {
            margin-top: 0;
            color: var(--accent-gold);
            border-bottom: 1px solid rgba(255, 193, 7, 0.3);
            padding-bottom: 10px;
        }

        input[type="url"], button {
            width: 100%;
            padding: 12px;
            margin-bottom: 10px;
            border-radius: 8px;
            border: 1px solid var(--main-blue);
            box-sizing: border-box;
        }

        input[type="url"] {
            background-color: var(--dark-blue);
            color: var(--text-light);
        }

        button {
            background-color: var(--main-blue);
            color: white;
            cursor: pointer;
            transition: background-color 0.2s;
            text-transform: uppercase;
            font-weight: bold;
        }

        button:hover {
            background-color: #163a77;
        }

        /* --- 4. IQC Generator (Chat Bubble) --- */
        .chat-generator {
            grid-column: 1 / -1; /* Ambil seluruh lebar */
            background-color: var(--card-bg);
            padding: 30px;
            border-radius: 12px;
            margin-top: 30px;
            border: 1px solid var(--main-blue);
        }

        .chat-area {
            display: flex;
            justify-content: flex-end;
            margin-top: 20px;
        }

        .chat-bubble {
            max-width: 60%;
            background-color: var(--chat-bubble);
            color: white;
            padding: 10px 15px;
            border-radius: 20px;
            position: relative;
            animation: pressEffect 0.2s ease-out; /* Animasi Press/Touch */
            cursor: default;
        }

        /* Efek Tanda Ditekan (Seperti di iPhone) */
        .chat-bubble.pressed {
            opacity: 0.7;
            transform: scale(0.98);
        }

        .chat-bubble:after {
            content: '';
            position: absolute;
            bottom: 0;
            right: -7px;
            width: 15px;
            height: 15px;
            background-color: var(--chat-bubble);
            clip-path: polygon(0 0, 100% 0, 100% 100%);
            transform: rotate(45deg);
        }

        #chatOutput {
            font-size: 1.1em;
            white-space: pre-wrap;
        }

        /* --- 5. Footer --- */
        footer {
            margin-top: auto; /* Dorong ke bawah */
            padding: 15px 0;
            text-align: center;
            font-size: 0.8em;
            color: var(--text-soft);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
    </style>
</head>
<body>

    <header>
        <h1>Candra Tools</h1>
        <p class="developer-info">Developed by: Candra</p>
    </header>

    <div class="container">
        
        <div class="card-grid">
            
            <div class="card">
                <h3>📥 TikTok Video Downloader</h3>
                <input type="url" placeholder="Masukkan URL Video TikTok..." id="tiktokUrl">
                <button onclick="downloadFeature('TikTok')">Download Video (Tanpa Watermark)</button>
                <small style="color: var(--text-soft);">*Fitur ini hanya simulasi front-end.</small>
            </div>

            <div class="card">
                <h3>🎵 YouTube to MP3 Converter</h3>
                <input type="url" placeholder="Masukkan URL YouTube..." id="ytUrl">
                <button onclick="downloadFeature('YouTube MP3')">Convert & Download MP3</button>
                <small style="color: var(--text-soft);">*Fitur ini hanya simulasi front-end.</small>
            </div>

            <div class="card">
                <h3>📸 Instagram Media Downloader</h3>
                <input type="url" placeholder="Masukkan URL Postingan Instagram..." id="igUrl">
                <button onclick="downloadFeature('Instagram')">Download Gambar/Video</button>
                <small style="color: var(--text-soft);">*Fitur ini hanya simulasi front-end.</small>
            </div>
            
        </div>

        <div class="chat-generator">
            <h3>💬 IQC (iOS Quote/Chat) Generator</h3>
            <p style="color: var(--text-soft);">Buat teks chat bergaya bubble iOS yang sedang 'ditekan'.</p>

            <textarea id="chatInput" rows="3" placeholder="Tulis teks yang Anda inginkan di sini..." style="width: 100%; padding: 10px; border-radius: 8px; border: 1px solid var(--main-blue); background-color: var(--dark-blue); color: var(--text-light); box-sizing: border-box;"></textarea>
            
            <button onclick="generateChatBubble()">Tampilkan Bubble Chat</button>

            <div class="chat-area">
                <div class="chat-bubble" id="chatBubbleContainer">
                    <p id="chatOutput">Ketikkan teks Anda di atas untuk melihat hasilnya!</p>
                </div>
            </div>
        </div>
        
    </div>

    <footer>
        &copy; 2025 Candra Tools. All rights reserved. | <a href="#" style="color: var(--accent-gold); text-decoration: none;">Privacy</a>
    </footer>

    <script>
        // --- 6. JavaScript untuk Fungsionalitas ---

        function downloadFeature(featureName) {
            alert(`Fitur ${featureName} berhasil diaktifkan! (Catatan: Ini adalah simulasi antarmuka. Fungsionalitas download memerlukan backend server.)`);
        }

        function generateChatBubble() {
            const inputElement = document.getElementById('chatInput');
            const outputElement = document.getElementById('chatOutput');
            const bubbleContainer = document.getElementById('chatBubbleContainer');
            
            const inputText = inputElement.value.trim();

            if (inputText === "") {
                outputElement.textContent = "Teks tidak boleh kosong!";
                return;
            }

            // Update teks di bubble
            outputElement.textContent = inputText;

            // Tambahkan dan hapus kelas 'pressed' untuk simulasi efek ditekan
            bubbleContainer.classList.add('pressed');
            
            // Hapus kelas 'pressed' setelah 300ms
            setTimeout(() => {
                bubbleContainer.classList.remove('pressed');
            }, 300);
        }
    </script>
</body>
</html>
