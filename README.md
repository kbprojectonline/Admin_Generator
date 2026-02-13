<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <title>Admin - Master Generator (Final Layout Fix)</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Segoe+UI:wght@400;600;700;900&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary: #2c3e50;
            --danger: #c0392b; /* MERAH */
            --warning: #f39c12; 
            --return: #3498db; 
            --badge-7days: #3498db;
            --badge-30days: #9b59b6;
            --badge-90days: #e67e22;
            --badge-365days: #27ae60;
            --badge-silver: #bdc3c7;
            --badge-gold: #ffd700;
            --badge-diamond: #00e5ff;
        }

        /* ZOOM LEVEL 2 (60%) */
        body { font-family: 'Segoe UI', sans-serif; background: #f4f7f6; padding: 15px; display: flex; flex-direction: column; align-items: center; margin: 0; transition: zoom 0.2s ease; zoom: 0.6; }
        
        .admin-box { 
            background: white; 
            padding: 20px; 
            border-radius: 15px; 
            box-shadow: 0 5px 25px rgba(0,0,0,0.1); 
            width: 100%; 
            max-width: 800px; 
            box-sizing: border-box; 
            position: relative; 
            overflow: hidden; 
        }
        
        .header-container {
            display: flex; justify-content: center; align-items: center;
            border-bottom: 2px solid #eee; padding-bottom: 10px; margin-bottom: 20px;
            margin-top: 10px; flex-direction: column; gap: 10px;
        }

        h1 { color: var(--primary); margin: 0; font-size: 1.3rem; text-align: center; width: 100%; }

        #login-btn {
            background: #4285F4; color: white; border: none; padding: 10px 20px;
            border-radius: 20px; font-weight: bold; font-size: 0.9rem; cursor: pointer;
            display: flex; align-items: center; gap: 8px; transition: 0.3s;
            box-shadow: 0 3px 10px rgba(66, 133, 244, 0.3);
        }
        #login-btn:hover { background: #357ae8; transform: translateY(-2px); }

        .menu-wrapper { position: absolute; top: 15px; right: 15px; z-index: 100; }
        .hamburger-btn {
            background: transparent; color: #555; border: none; padding: 5px;
            font-size: 30px; cursor: pointer; transition: 0.2s; outline: none; line-height: 1;
        }
        .hamburger-btn:hover, .hamburger-btn:active { color: var(--primary); }

        .zoom-dropdown {
            display: none; position: absolute; top: 40px; right: 0;
            background: white; border: 1px solid #ddd; border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.15); padding: 10px; z-index: 100;
            width: 160px; text-align: left;
        }
        .show-menu { display: block !important; }
        .zoom-dropdown label { display: block; margin-bottom: 5px; font-weight: bold; color: #555; }
        .zoom-dropdown select { width: 100%; padding: 8px; border-radius: 5px; border: 1px solid #ccc; font-size: 14px; }
        
        .form-group { display: flex; gap: 10px; margin-bottom: 20px; flex-wrap: wrap; }
        .form-group select { 
            padding: 12px; border-radius: 8px; border: 1px solid #ccc; font-size: 16px; 
            background: white; color: #333; outline: none; appearance: none; -webkit-appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%2212%22%20height%3D%2212%22%20viewBox%3D%220%200%2012%2012%22%3E%3Cpath%20fill%3D%22%23333%22%20d%3D%22M10.293%203.293L6%207.586%201.707%203.293A1%201%200%2000.293%204.707l5%205a1%201%200%20001.414%200l5-5a1%201%200%2010-1.414-1.414z%22%2F%3E%3C%2Fsvg%3E");
            background-repeat: no-repeat; background-position: right 12px center; padding-right: 35px;
        }
        .form-group select:first-child { flex: 2; min-width: 150px; }
        #voucher-qty { flex: 1; min-width: 80px; }

        .opt-7days { color: var(--badge-7days) !important; font-weight: bold; }
        .opt-30days { color: var(--badge-30days) !important; font-weight: bold; }
        .opt-90days { color: var(--badge-90days) !important; font-weight: bold; }
        .opt-365days { color: var(--badge-365days) !important; font-weight: bold; }
        
        .opt-silver { color: #7f8c8d !important; font-weight: bold; }
        .opt-gold { color: #b8860b !important; font-weight: bold; }
        .opt-diamond { color: #008b8b !important; font-weight: bold; }
        
        button#generate-btn { width: 100%; padding: 15px; background: var(--primary); color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 1rem; transition: 0.2s; }
        button#generate-btn:disabled { background: #ccc; cursor: not-allowed; }

        /* HEADER SPACING */
        h3 {
            margin-bottom: 15px; 
            color: #555; 
            font-size: 1.1rem; 
            padding-left: 10px;
            border-left: 5px solid;
        }

        .head-active { margin-top: 90px !important; border-left-color: #3498db; }
        
        /* HEADER DIBERIKAN: MERAH (Sama kayak History) */
        .head-given { margin-top: 80px !important; border-left-color: var(--danger); }

        /* HEADER RIWAYAT: MERAH */
        .head-history { margin-top: 80px !important; border-left-color: var(--danger); }

        .list-box { background: #f8f9fa; padding: 10px; height: 350px; overflow-y: auto; border: 1px solid #eee; border-radius: 10px; }

        /* SWIPE STYLES */
        .swipe-wrapper { position: relative; margin-bottom: 10px; overflow: hidden; border-radius: 8px; }
        .swipe-bg {
            position: absolute; top: 0; bottom: 0; right: 0; width: 100%; color: white;
            display: flex; align-items: center; justify-content: flex-end; padding-right: 20px;
            font-weight: bold; font-size: 0.9rem; box-sizing: border-box; z-index: 1; border-radius: 8px;
        }
        .bg-send { background: var(--warning); }
        .bg-return { background: var(--return); }

        .item-row { 
            position: relative; z-index: 2; display: flex; justify-content: space-between; align-items: center; 
            background: white; padding: 12px; border-radius: 8px; 
            box-shadow: 0 2px 4px rgba(0,0,0,0.05); transition: transform 0.2s ease-out; 
        }
        
        /* STYLE KHUSUS RIWAYAT */
        .history-row { 
            flex-direction: column; 
            align-items: flex-start; 
            border-left: 5px solid #555; /* Tetap abu-abu gelap untuk item riwayat */
            margin-bottom: 30px; 
            padding: 18px; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.08); 
        }

        .badge { padding: 4px 10px; border-radius: 4px; font-size: 0.75rem; font-weight: 800; color: #fff; margin-left: 5px; text-transform: uppercase; display: inline-block; vertical-align: middle; }
        .bg-7days { background: var(--badge-7days); }
        .bg-30days { background: var(--badge-30days); }
        .bg-90days { background: var(--badge-90days); }
        .bg-365days { background: var(--badge-365days); }
        .bg-silver { background: var(--badge-silver); color: #444; }
        .bg-gold { background: var(--badge-gold); }
        .bg-diamond { background: var(--badge-diamond); }

        .code-text { font-family: 'Courier New', monospace; font-weight: 800; font-size: 1.05rem; color: #333; letter-spacing: 3px; }
        
        .user-info { display: block; font-size: 0.85rem; color: #444; margin-top: 8px; }
        
        .date-info { font-size: 0.85rem; color: #d35400; font-weight: bold; margin-bottom: 12px; display: block; width: 100%; border-bottom: 1px dashed #ddd; padding-bottom: 8px; letter-spacing: 1.5px; }

        .btn-mini { padding: 8px 12px; border: none; border-radius: 6px; cursor: pointer; font-size: 0.8rem; color: white; font-weight: 600; margin-left: 4px; }
        .btn-copy { background: #7f8c8d; }
        .btn-del { background: var(--danger); }

        #custom-toast { position: fixed; top: 20px; right: 20px; left: 20px; background: #333; color: white; padding: 15px; border-radius: 10px; text-align: center; z-index: 9999; display: none; box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
        #custom-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.6); display: none; justify-content: center; align-items: center; z-index: 10000; padding: 20px; }
        .modal-content { background: white; padding: 20px; border-radius: 15px; width: 100%; max-width: 350px; text-align: center; }
        .modal-btns { display: flex; gap: 10px; margin-top: 20px; }
        .modal-btns button { flex: 1; padding: 12px; border-radius: 8px; border: none; font-weight: 900; cursor: pointer; }
    </style>
</head>
<body style="zoom: 0.6;">

    <div id="custom-toast"></div>
    <div id="custom-overlay">
        <div class="modal-content">
            <p id="modal-msg" style="color: #333; font-weight: 600;"></p>
            <div class="modal-btns">
                <button onclick="closeModal()" style="background: #eee;">Batal</button>
                <button id="modal-confirm-btn" style="background: var(--danger); color: white;">Hapus</button>
            </div>
        </div>
    </div>

    <div class="admin-box">
        
        <div class="menu-wrapper">
            <button class="hamburger-btn" onclick="toggleZoomMenu()">☰</button>
            <div id="zoom-menu-box" class="zoom-dropdown">
                <label>Ukuran Layar:</label>
                <select id="zoom-level" onchange="setZoom(this.value)">
                    <option value="0.5">Level 1 (50%)</option>
                    <option value="0.6" selected>Level 2 (60%)</option>
                    <option value="0.7">Level 3 (70%)</option>
                    <option value="0.8">Level 4 (80%)</option>
                    <option value="0.9">Level 5 (90%)</option>
                    <option value="1.0">Level 6 (Normal)</option>
                </select>
            </div>
        </div>
        
        <div class="header-container">
            <h1>🛠️ Admin Generator</h1>
            <button id="login-btn">🔑 LOGIN ADMIN (Google)</button>
        </div>
        
        <div class="form-group">
            <select id="plan-select">
                <optgroup label="PAKET WAKTU">
                    <option value="7_days" class="opt-7days">🗓️ Paket 7 Hari</option>
                    <option value="30_days" class="opt-30days">📅 Paket 1 Bulan</option>
                    <option value="90_days" class="opt-90days">📊 Paket 3 Bulan</option>
                    <option value="365_days" class="opt-365days">🏆 Paket 1 Tahun</option>
                </optgroup>
                <optgroup label="PAKET SILVER">
                    <option value="silver_1" class="opt-silver">🥈 1 Kunci Silver</option>
                    <option value="silver_5" class="opt-silver">🥈 5 Kunci Silver</option>
                    <option value="silver" class="opt-silver">🥈 10 Kunci Silver</option> <option value="silver_20" class="opt-silver">🥈 20 Kunci Silver</option>
                    <option value="silver_50" class="opt-silver">🥈 50 Kunci Silver</option>
                    <option value="silver_100" class="opt-silver">🥈 100 Kunci Silver</option>
                </optgroup>
                <optgroup label="PAKET GOLD">
                    <option value="gold_1" class="opt-gold">👑 1 Kunci Gold</option>
                    <option value="gold_5" class="opt-gold">👑 5 Kunci Gold</option>
                    <option value="gold" class="opt-gold">👑 10 Kunci Gold</option> <option value="gold_20" class="opt-gold">👑 20 Kunci Gold</option>
                    <option value="gold_50" class="opt-gold">👑 50 Kunci Gold</option>
                    <option value="gold_70" class="opt-gold">👑 70 Kunci Gold</option>
                </optgroup>
                <optgroup label="PAKET DIAMOND">
                    <option value="diamond_1" class="opt-diamond">💎 1 Kunci Diamond</option>
                    <option value="diamond_5" class="opt-diamond">💎 5 Kunci Diamond</option>
                    <option value="diamond" class="opt-diamond">💎 10 Kunci Diamond</option> <option value="diamond_15" class="opt-diamond">💎 15 Kunci Diamond</option>
                    <option value="diamond_30" class="opt-diamond">💎 30 Kunci Diamond</option>
                </optgroup>
            </select>
            
            <button onclick="window.location.reload()" style="padding: 12px; border-radius: 8px; border: 1px solid #ccc; background: white; cursor: pointer; font-size: 16px;">🔄</button>
            
            <select id="voucher-qty">
                <option value="1">1</option><option value="2">2</option><option value="3">3</option>
                <option value="4">4</option><option value="5" selected>5</option><option value="6">6</option>
                <option value="7">7</option><option value="8">8</option><option value="9">9</option>
                <option value="10">10</option>
            </select>
        </div>
        
        <button id="generate-btn" disabled>🔒 LOGIN DULU UNTUK GENERATE</button>

        <h3 class="head-active">🎫 Voucher Aktif (Geser Kiri = Kirim)</h3>
        <div id="active-list" class="list-box">Silakan Login...</div>

        <h3 class="head-given">📤 Voucher Telah Diberikan (Geser Kiri = Kembalikan)</h3>
        <div id="given-list" class="list-box" style="background: #fffafa;">Menunggu Login...</div>

        <div id="history-container" style="display: none;">
            <h3 class="head-history">📜 Riwayat Voucher</h3>
            <div id="history-list" class="list-box" style="background:#fffafa;">Memuat riwayat...</div>
        </div>

    </div>

    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>

    <script>
        function setZoom(val) { document.body.style.zoom = val; }
        function toggleZoomMenu() {
            const menu = document.getElementById('zoom-menu-box');
            menu.classList.toggle('show-menu');
        }

        const firebaseConfig = {
            apiKey: "AIzaSyBublDvXwqKWK3lACZ_plD3ORMS1h2MvTM",
            authDomain: "kuis-belajar-fc843.firebaseapp.com",
            databaseURL: "https://kuis-belajar-fc843-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "kuis-belajar-fc843",
            storageBucket: "kuis-belajar-fc843.firebasestorage.app",
            messagingSenderId: "851984555383",
            appId: "1:851984555383:web:e47824f590620b73849572"
        };

        firebase.initializeApp(firebaseConfig);
        const db = firebase.database();
        const auth = firebase.auth();

        const ADMIN_UID = "G6N2sLEF6vX0e3X9ndbmft1oHVg2"; 

        const loginBtn = document.getElementById('login-btn');
        const genBtn = document.getElementById('generate-btn');
        const activeListDiv = document.getElementById('active-list');
        const givenListDiv = document.getElementById('given-list'); 
        const historyContainer = document.getElementById('history-container'); 
        const historyListDiv = document.getElementById('history-list');

        let globalVouchers = {};
        let globalGiven = {};
        let isMasterLoaded = false; 

        // AUTH STATE
        auth.onAuthStateChanged((user) => {
            if (user) {
                if (user.uid === ADMIN_UID) {
                    loginBtn.innerHTML = `✅ Admin: <b>${user.email.split('@')[0]}</b> (Logout)`;
                    loginBtn.style.background = "#27ae60";
                    loginBtn.onclick = () => auth.signOut();

                    genBtn.disabled = false;
                    genBtn.innerText = "⚡ GENERATE VOUCHER (12 DIGIT)";
                    genBtn.style.background = "#2c3e50";

                    historyContainer.style.display = "block";
                    activeListDiv.innerHTML = "Memuat data...";
                    givenListDiv.innerHTML = "Memuat data terkirim...";
                    historyListDiv.innerHTML = "Memuat riwayat...";

                    startListeningData();
                } else {
                    loginBtn.innerHTML = `⚠️ AKSES DITOLAK: ${user.email}`;
                    loginBtn.style.background = "#e74c3c";
                    loginBtn.onclick = () => auth.signOut();
                    genBtn.disabled = true;
                    genBtn.innerText = "⛔ ANDA BUKAN ADMIN";
                    historyContainer.style.display = "none";
                    activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#c0392b;">⛔ AKSES DITOLAK</div>';
                    givenListDiv.innerHTML = '';
                }
            } else {
                loginBtn.innerHTML = `🔑 Login Admin (Google)`;
                loginBtn.style.background = "#4285F4";
                loginBtn.onclick = loginGoogle;
                genBtn.disabled = true;
                genBtn.innerText = "🔒 Login Terlebih Dahulu";
                genBtn.style.background = "#ccc";
                historyContainer.style.display = "none";
                activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">🔒 Silakan Login.</div>';
                givenListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">🔒 Silakan Login.</div>';
            }
        });

        function loginGoogle() {
            const provider = new firebase.auth.GoogleAuthProvider();
            auth.signInWithPopup(provider).catch(error => myAlert("Gagal Login: " + error.message));
        }

        function startListeningData() {
            // 1. Ambil Data Master & Aktifkan Flag Loading Selesai
            db.ref('vouchers').on('value', (snapshot) => {
                globalVouchers = snapshot.exists() ? snapshot.val() : {};
                isMasterLoaded = true; // DATA UTAMA SUDAH MASUK
                renderAllLists();
            });

            // 2. Ambil Data Given Tracker
            db.ref('vouchers_given').on('value', (snapshot) => {
                globalGiven = snapshot.exists() ? snapshot.val() : {};
                renderAllLists();
            });

            // 3. Ambil Riwayat
            db.ref('voucher_history').on('value', (snapshot) => {
                if (snapshot.exists()) {
                    const data = Object.values(snapshot.val()).sort((a, b) => b.date - a.date);
                    let html = "";
                    data.forEach(item => {
                        const badge = getBadgeInfo(item.type);
                        const dateObj = new Date(item.date);
                        const hari = dateObj.toLocaleDateString('id-ID', { weekday: 'long' });
                        const jam = dateObj.toLocaleTimeString('id-ID').replace(/\./g, ':');
                        const tgl = dateObj.toLocaleDateString('id-ID').split('/').join('.');
                        
                        html += `
                        <div class="item-row history-row">
                            <span class="date-info">🕒 ${hari} | ${jam} | ${tgl}</span>
                            <div style="width: 100%;">
                                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 5px;">
                                    <span class="code-text" style="font-size: 0.95rem;">${item.code}</span>
                                    <span class="badge ${badge.css}" style="font-size: 0.65rem;">${badge.text}</span> 
                                </div>
                                <span class="user-info">
                                    <div style="margin-bottom: 6px;">👤 Dipakai: <b>${item.user || 'Unknown'}</b></div>
                                    <div style="margin-bottom: 6px;">${item.email ? `@${item.email}` : ''}</div>
                                    <div style="margin-bottom: 6px; font-size: 0.8rem; color: #555; font-family: monospace; font-weight: bold;">UID: ${item.uid || '-'}</div>
                                </span>
                            </div>
                        </div>`;
                    });
                    historyListDiv.innerHTML = html;
                } else {
                    historyListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Belum ada riwayat penggunaan.</div>';
                }
            });
        }

        function renderAllLists() {
            // A. RENDER ACTIVE LIST
            const activeEntries = Object.entries(globalVouchers).filter(([code, type]) => !globalGiven[code]);
            
            const getSortIndex = (type) => {
                let clean = type.toLowerCase().replace('promo_', '');
                const map = { '7_days': 1, '30_days': 2, '90_days': 3, '365_days': 4 };
                if (clean.includes('silver')) return 10;
                if (clean.includes('gold')) return 20;
                if (clean.includes('diamond')) return 30;
                return map[clean] || 99;
            };
            activeEntries.sort((a, b) => getSortIndex(a[1]) - getSortIndex(b[1]));

            if (activeEntries.length > 0) {
                let html = "";
                activeEntries.forEach(([code, type]) => {
                    const badge = getBadgeInfo(type);
                    
                    // WARNA GARIS DIHILANGKAN (JADI CLEAN)
                    html += `
                        <div class="swipe-wrapper">
                            <div class="swipe-bg bg-send">KIRIM >></div>
                            <div class="item-row" id="act-${code}">
                                <div style="flex:1;">
                                    <span class="code-text">${code}</span>
                                    <span class="badge ${badge.css}">${badge.text}</span>
                                </div>
                                <div>
                                    <button class="btn-mini btn-copy" onclick="copyV('${code}', '${type}')">Salin</button>
                                    <button class="btn-mini btn-del" onclick="delV('${code}')">Hapus</button>
                                </div>
                            </div>
                        </div>`;
                });
                activeListDiv.innerHTML = html;
                
                activeEntries.forEach(([code, type]) => {
                    const row = document.getElementById(`act-${code}`);
                    if(row) addSwipeLogic(row, () => moveVoucherToGiven(code, type));
                });

            } else {
                activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Tidak ada voucher aktif.</div>';
            }

            // B. RENDER GIVEN LIST (DENGAN LOGIKA AUTO-HANGUS)
            const givenEntries = Object.entries(globalGiven);
            
            if (givenEntries.length > 0) {
                let html = "";
                givenEntries.forEach(([code, type]) => {
                    
                    if (isMasterLoaded) {
                        if (!globalVouchers[code]) {
                            db.ref(`vouchers_given/${code}`).remove(); 
                            return; 
                        }
                    }

                    const badge = getBadgeInfo(type);
                    // BORDER DIUBAH JADI MERAH (#c0392b)
                    html += `
                        <div class="swipe-wrapper">
                            <div class="swipe-bg bg-return">KEMBALIKAN >></div>
                            <div class="item-row" id="giv-${code}" style="border-left: 5px solid #c0392b; background: #fff;">
                                <div style="display: flex; flex-direction: column; width: 100%;">
                                    <div style="display: flex; justify-content: space-between; align-items: center; width: 100%;">
                                        <span class="code-text" style="color: #333;">${code}</span>
                                        <span class="badge ${badge.css}">${badge.text}</span>
                                    </div>
                                    <div style="font-size: 0.75rem; color: #d35400; font-weight:bold; margin-top: 5px;">📤 SUDAH DIKIRIM</div>
                                </div>
                            </div>
                        </div>`;
                });
                givenListDiv.innerHTML = html;

                givenEntries.forEach(([code, type]) => {
                    if (globalVouchers[code]) { 
                        const row = document.getElementById(`giv-${code}`);
                        if(row) addSwipeLogic(row, () => returnToActive(code));
                    }
                });
            } else {
                // TEXT DIHILANGKAN TOTAL (BLANK)
                givenListDiv.innerHTML = '';
            }
        }

        // --- SWIPE LOGIC ---
        function addSwipeLogic(element, actionCallback) {
            let startX = 0;
            let currentTranslate = 0;
            let isDragging = false;

            element.addEventListener('touchstart', (e) => {
                startX = e.touches[0].clientX;
                isDragging = true;
                element.style.transition = 'none'; 
            });

            element.addEventListener('touchmove', (e) => {
                if (!isDragging) return;
                const currentX = e.touches[0].clientX;
                const diff = currentX - startX;
                if (diff < 0) { 
                    currentTranslate = diff;
                    if (currentTranslate < -150) currentTranslate = -150;
                    element.style.transform = `translateX(${currentTranslate}px)`;
                }
            });

            element.addEventListener('touchend', () => {
                isDragging = false;
                element.style.transition = 'transform 0.3s ease-out';
                if (currentTranslate < -80) { 
                    element.style.transform = `translateX(-100%)`; 
                    setTimeout(() => actionCallback(), 200);
                } else {
                    element.style.transform = `translateX(0)`;
                }
            });
        }

        function getBadgeInfo(type) {
            if (!type) return { text: 'UNKNOWN', css: 'bg-7days', label: 'Unknown' };
            let raw = type.toLowerCase();
            if (raw === '7_days') return { text: '7 HARI', css: 'bg-7days', label: '7 Hari' };
            if (raw === '30_days') return { text: '1 BULAN', css: 'bg-30days', label: '1 Bulan' };
            if (raw === '90_days') return { text: '3 BULAN', css: 'bg-90days', label: '3 Bulan' };
            if (raw === '365_days') return { text: '1 TAHUN', css: 'bg-365days', label: '1 Tahun' };
            if (raw.includes('silver') || raw.includes('gold') || raw.includes('diamond')) {
                let tier = '', cssClass = '';
                if (raw.includes('silver')) { tier = 'Silver'; cssClass = 'bg-silver'; }
                else if (raw.includes('gold')) { tier = 'Gold'; cssClass = 'bg-gold'; }
                else if (raw.includes('diamond')) { tier = 'Diamond'; cssClass = 'bg-diamond'; }
                let parts = raw.split('_');
                let qty = 10; 
                for (let part of parts) { if (!isNaN(part) && part !== '') qty = part; }
                return { text: `${qty} KUNCI ${tier.toUpperCase()}`, css: cssClass, label: `${qty} Kunci ${tier}` };
            }
            return { text: type.toUpperCase(), css: 'bg-7days', label: type };
        }

        function makeCode(length) {
            const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
            let result = '';
            for (let i = 0; i < length; i++) result += chars.charAt(Math.floor(Math.random() * chars.length));
            return result;
        }

        // --- FUNGSI AKSI (ALERT YANG DIPERBAIKI) ---
        
        window.moveVoucherToGiven = (code, rawType) => {
            const info = getBadgeInfo(rawType);
            const textToCopy = `${code} = ${info.label}`;
            navigator.clipboard.writeText(textToCopy);
            myAlert(textToCopy); 
            
            if (!auth.currentUser) return;
            db.ref(`vouchers_given/${code}`).set(rawType);
        };

        window.returnToActive = (code) => {
            myAlert("Dikembalikan ke Stok Aktif!");
            db.ref(`vouchers_given/${code}`).remove();
        };

        window.copyV = (code, rawType) => {
             const info = getBadgeInfo(rawType); 
             const textToCopy = `${code} = ${info.label}`;
             navigator.clipboard.writeText(textToCopy);
             myAlert(textToCopy); 
        };

        window.delV = (code) => {
            myConfirm("Hapus permanen?", () => {
                db.ref(`vouchers/${code}`).remove();
                db.ref(`vouchers_given/${code}`).remove();
            });
        };

        document.getElementById('generate-btn').onclick = () => {
            const type = document.getElementById('plan-select').value;
            const qty = parseInt(document.getElementById('voucher-qty').value);
            const updates = {};
            for (let i = 0; i < qty; i++) updates[makeCode(12)] = type;
            
            db.ref('vouchers').update(updates)
                .then(() => myAlert(`✅ Sukses buat ${qty} voucher!`))
                .catch(e => myAlert("Gagal: " + e.message));
        };

        window.myAlert = (msg) => {
            const toast = document.getElementById('custom-toast');
            toast.innerText = msg; toast.style.display = 'block';
            setTimeout(() => toast.style.display = 'none', 5000);
        };
        
        window.myConfirm = (msg, action) => {
            document.getElementById('modal-msg').innerText = msg;
            document.getElementById('custom-overlay').style.display = 'flex';
            document.getElementById('modal-confirm-btn').onclick = () => { action(); closeModal(); };
        };
        window.closeModal = () => document.getElementById('custom-overlay').style.display = 'none';

    </script>
</body>
</html>
