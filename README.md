<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <title>Admin - Generator Voucher</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Segoe+UI:wght@400;600;700;900&display=swap" rel="stylesheet">

    <style>
        :root {
            --primary: #2c3e50;
            --danger: #c0392b;
            --badge-7days: #3498db;
            --badge-30days: #9b59b6;
            --badge-90days: #e67e22;
            --badge-365days: #27ae60;
            --badge-silver: #95a5a6; 
            --badge-gold: #f1c40f;   
            --badge-diamond: #00e5ff; 
        }

        body { font-family: 'Segoe UI', sans-serif; background: #f4f7f6; padding: 15px; display: flex; flex-direction: column; align-items: center; margin: 0; transition: zoom 0.2s ease; }
        
        .admin-box { 
            background: white; 
            padding: 20px; 
            border-radius: 15px; 
            box-shadow: 0 5px 25px rgba(0,0,0,0.1); 
            width: 100%; 
            max-width: 800px; 
            box-sizing: border-box; 
            position: relative; 
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

        /* WARNA OPTION DROPDOWN */
        .opt-7days { color: var(--badge-7days) !important; font-weight: bold; }
        .opt-30days { color: var(--badge-30days) !important; font-weight: bold; }
        .opt-90days { color: var(--badge-90days) !important; font-weight: bold; }
        .opt-365days { color: var(--badge-365days) !important; font-weight: bold; }
        
        .opt-silver { color: #7f8c8d !important; font-weight: bold; }
        .opt-gold { color: #f39c12 !important; font-weight: bold; }
        .opt-diamond { color: #00a8ff !important; font-weight: bold; }
        
        button#generate-btn { width: 100%; padding: 15px; background: var(--primary); color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 1rem; transition: 0.2s; }
        button#generate-btn:disabled { background: #ccc; cursor: not-allowed; }

        h3 { margin-top: 30px; margin-bottom: 15px; color: #555; font-size: 1.1rem; border-left: 5px solid #3498db; padding-left: 10px; }
        .head-history { margin-top: 80px !important; border-left-color: #e74c3c !important; }
        .list-box { background: #f8f9fa; padding: 10px; height: 450px; overflow-y: auto; border: 1px solid #eee; border-radius: 10px; }

        .item-row { display: flex; justify-content: space-between; align-items: center; background: white; padding: 12px; margin-bottom: 10px; border-radius: 8px; border-left: 5px solid #ccc; box-shadow: 0 2px 4px rgba(0,0,0,0.05); animation: fadeIn 0.4s; }
        .history-row { flex-direction: column; align-items: flex-start; border-left: 5px solid #555; margin-bottom: 30px; padding: 18px; box-shadow: 0 4px 8px rgba(0,0,0,0.08); }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

        .badge { padding: 4px 10px; border-radius: 4px; font-size: 0.75rem; font-weight: 800; color: #fff; margin-left: 5px; text-transform: uppercase; display: inline-block; vertical-align: middle; }
        .bg-7days { background: var(--badge-7days); }
        .bg-30days { background: var(--badge-30days); }
        .bg-90days { background: var(--badge-90days); }
        .bg-365days { background: var(--badge-365days); }
        .bg-silver { background: var(--badge-silver); color: #fff; }
        .bg-gold { background: var(--badge-gold); color: #fff; }
        .bg-diamond { background: var(--badge-diamond); color: #fff; }

        .code-text { font-family: 'Courier New', monospace; font-weight: 800; font-size: 1.05rem; color: #333; letter-spacing: 3px; }
        .user-info { display: block; font-size: 0.85rem; color: #444; margin-top: 8px; line-height: 1.4; }
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
<body style="zoom: 0.9;">

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
                    <option value="0.6">Level 2 (60%)</option>
                    <option value="0.7">Level 3 (70%)</option>
                    <option value="0.8">Level 4 (80%)</option>
                    <option value="0.9" selected>Level 5 (90%)</option>
                    <option value="1.0">Level 6 (Normal)</option>
                    <option value="1.1">Level 7 (110%)</option>
                    <option value="1.2">Level 8 (120%)</option>
                    <option value="1.3">Level 9 (130%)</option>
                    <option value="1.4">Level 10 (140%)</option>
                </select>
            </div>
        </div>
        
        <div class="header-container">
            <h1>🛠️ Admin Generator</h1>
            <button id="login-btn">🔑 LOGIN ADMIN (Google)</button>
        </div>
        
        <div class="form-group">
            <select id="plan-select">
                <optgroup label="PAKET WAKTU (Akses Penuh)">
                    <option value="7_days" class="opt-7days">🗓️ Paket 7 Hari</option>
                    <option value="30_days" class="opt-30days">📅 Paket 1 Bulan</option>
                    <option value="90_days" class="opt-90days">📊 Paket 3 Bulan</option>
                    <option value="365_days" class="opt-365days">🏆 Paket 1 Tahun</option>
                </optgroup>

                <optgroup label="PAKET KUNCI SILVER">
                    <option value="promo_silver_1" class="opt-silver">🥈 1 Kunci Silver</option>
                    <option value="promo_silver_5" class="opt-silver">🥈 5 Kunci Silver</option>
                    <option value="silver" class="opt-silver">🥈 10 Kunci Silver</option>
                    <option value="promo_silver_20" class="opt-silver">🥈 20 Kunci Silver</option>
                    <option value="promo_silver_50" class="opt-silver">🥈 50 Kunci Silver</option>
                    <option value="promo_silver_100" class="opt-silver">🥈 100 Kunci Silver</option>
                </optgroup>

                <optgroup label="PAKET KUNCI GOLD">
                    <option value="promo_gold_1" class="opt-gold">👑 1 Kunci Gold</option>
                    <option value="promo_gold_5" class="opt-gold">👑 5 Kunci Gold</option>
                    <option value="gold" class="opt-gold">👑 10 Kunci Gold</option>
                    <option value="promo_gold_20" class="opt-gold">👑 20 Kunci Gold</option>
                    <option value="promo_gold_50" class="opt-gold">👑 50 Kunci Gold</option>
                    <option value="promo_gold_70" class="opt-gold">👑 70 Kunci Gold</option>
                </optgroup>

                <optgroup label="PAKET KUNCI DIAMOND">
                    <option value="promo_diamond_1" class="opt-diamond">💎 1 Kunci Diamond</option>
                    <option value="promo_diamond_5" class="opt-diamond">💎 5 Kunci Diamond</option>
                    <option value="diamond" class="opt-diamond">💎 10 Kunci Diamond</option>
                    <option value="promo_diamond_15" class="opt-diamond">💎 15 Kunci Diamond</option>
                    <option value="promo_diamond_25" class="opt-diamond">💎 25 Kunci Diamond</option>
                    <option value="promo_diamond_30" class="opt-diamond">💎 30 Kunci Diamond</option>
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

        <h3>🎫 Voucher Aktif</h3>
        <div id="active-list" class="list-box">Silakan Login...</div>

        <div id="history-container" style="display: none;">
            <h3 class="head-history">📜 Riwayat Voucher</h3>
            <div id="history-list" class="list-box" style="background:#fffafa;">Memuat riwayat...</div>
        </div>

    </div>

    <script>
        function setZoom(val) { document.body.style.zoom = val; }
        function toggleZoomMenu() {
            const menu = document.getElementById('zoom-menu-box');
            menu.classList.toggle('show-menu');
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, update, onValue, remove, off } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";
        import { getAuth, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBublDvXwqKWK3lACZ_plD3ORMS1h2MvTM",
            authDomain: "kuis-belajar-fc843.firebaseapp.com",
            databaseURL: "https://kuis-belajar-fc843-default-rtdb.asia-southeast1.firebasedatabase.app",
            projectId: "kuis-belajar-fc843",
            storageBucket: "kuis-belajar-fc843.firebasestorage.app",
            messagingSenderId: "851984555383",
            appId: "1:851984555383:web:e47824f590620b73849572"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        const auth = getAuth(app);

        // --- KONFIGURASI ADMIN ---
        const ADMIN_UID = "G6N2sLEF6vX0e3X9ndbmft1oHVg2"; 
        // -------------------------

        const loginBtn = document.getElementById('login-btn');
        const genBtn = document.getElementById('generate-btn');
        const activeListDiv = document.getElementById('active-list');
        const historyContainer = document.getElementById('history-container'); 
        const historyListDiv = document.getElementById('history-list');

        let activeListener = null;
        let historyListener = null;

        // --- SISTEM LOGIN & DETEKSI USER ---
        onAuthStateChanged(auth, (user) => {
            if (user) {
                if (user.uid === ADMIN_UID) {
                    // ADMIN LOGIN
                    loginBtn.innerHTML = `✅ Admin: <b>${user.email.split('@')[0]}</b> (Logout)`;
                    loginBtn.style.background = "#27ae60";
                    loginBtn.onclick = () => signOut(auth);

                    genBtn.disabled = false;
                    genBtn.innerText = "⚡ GENERATE VOUCHER (12 DIGIT)";
                    genBtn.style.background = "#2c3e50";

                    historyContainer.style.display = "block";
                    activeListDiv.innerHTML = "Memuat data...";
                    historyListDiv.innerHTML = "Memuat riwayat..."; // Text Awal

                    startListeningData();
                } else {
                    // BUKAN ADMIN
                    loginBtn.innerHTML = `⚠️ AKSES DITOLAK: ${user.email}`;
                    loginBtn.style.background = "#e74c3c";
                    loginBtn.onclick = () => signOut(auth);
                    genBtn.disabled = true;
                    genBtn.innerText = "⛔ ANDA BUKAN ADMIN";
                    genBtn.style.background = "#95a5a6";
                    historyContainer.style.display = "none";
                    activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#c0392b; font-weight:bold;">⛔ AKSES DITOLAK<br>Anda Tidak Terdaftar Sebagai Admin, KELUAR!.</div>';
                    stopListeningData();
                }
            } else {
                // BELUM LOGIN
                loginBtn.innerHTML = `🔑 Login Admin (Google)`;
                loginBtn.style.background = "#4285F4";
                loginBtn.onclick = loginGoogle;
                genBtn.disabled = true;
                genBtn.innerText = "🔒 Login Terlebih Dahulu";
                genBtn.style.background = "#ccc";
                historyContainer.style.display = "none";
                activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">🔒 Silakan Login Terlebih Dulu.</div>';
                stopListeningData();
            }
        });

        function loginGoogle() {
            const provider = new GoogleAuthProvider();
            signInWithPopup(auth, provider).catch(error => myAlert("Gagal Login: " + error.message));
        }

        function startListeningData() {
            // 1. Ambil Voucher Aktif
            activeListener = onValue(ref(db, 'vouchers'), (snapshot) => {
                if (snapshot.exists()) {
                    const data = snapshot.val();
                    const entries = Object.entries(data);
                    
                    entries.sort((a, b) => {
                        const typeA = a[1];
                        const typeB = b[1];
                        const getPriority = (t) => {
                            if (t.includes('days')) return 1;
                            if (t.includes('silver')) return 2;
                            if (t.includes('gold')) return 3;
                            if (t.includes('diamond')) return 4;
                            return 99;
                        };
                        const diffGroup = getPriority(typeA) - getPriority(typeB);
                        if(diffGroup !== 0) return diffGroup;
                        const getQty = (t) => {
                            if(t === 'silver' || t === 'gold' || t === 'diamond') return 10; 
                            const match = t.match(/(\d+)/);
                            return match ? parseInt(match[0]) : 0;
                        };
                        return getQty(typeA) - getQty(typeB);
                    });

                    let html = "";
                    entries.forEach(([code, type]) => {
                        const badge = getBadgeInfo(type);
                        html += `
                            <div class="item-row" style="border-left-color: ${badge.colorCode || '#ccc'}">
                                <div style="flex:1;">
                                    <span class="code-text">${code}</span>
                                    <span class="badge ${badge.css}">${badge.text}</span>
                                </div>
                                <div>
                                    <button class="btn-mini btn-copy" onclick="copyV('${code}', '${type}')">Salin</button>
                                    <button class="btn-mini btn-del" onclick="delV('${code}')">Hapus</button>
                                </div>
                            </div>`;
                    });
                    activeListDiv.innerHTML = html;
                } else {
                    activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Tidak ada voucher aktif.</div>';
                }
            }, (error) => {
                activeListDiv.innerHTML = '<div style="color:red; text-align:center;">⛔ Gagal memuat data (Permission Denied).</div>';
            });

            // 2. Ambil Riwayat (DENGAN ANTI-STUCK FORCE)
            // Kita set timer 3 detik. Jika Firebase belum respon, kita paksa tulisan berubah.
            const loadingTimeout = setTimeout(() => {
                if (historyListDiv.innerHTML === "Memuat riwayat...") {
                    historyListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Belum ada riwayat / Data Kosong.</div>';
                }
            }, 3000);

            historyListener = onValue(ref(db, 'voucher_history'), (snapshot) => {
                clearTimeout(loadingTimeout); // Hapus timer jika data masuk
                
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
    <div class="item-row history-row" style="border-left-color: ${badge.colorCode || '#555'}">
        <span class="date-info">🕒 ${hari} | ${jam} | ${tgl}</span>
        <div style="width: 100%;">
            <span class="code-text">${item.code}</span>
            <span class="badge ${badge.css}">${badge.text}</span> 
            <span class="user-info">
                👤 Dipakai: <b>${item.user || 'Unknown'}</b><br>
                ${item.email ? `@${item.email}` : ''}<br>
                <span style="font-size: 0.7rem; color: #999; font-family: monospace;">UID: ${item.uid || '-'}</span>
            </span>
        </div>
    </div>`;
                    });
                    historyListDiv.innerHTML = html;
                } else {
                    historyListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Belum ada riwayat penggunaan.</div>';
                }
            }, (error) => {
                clearTimeout(loadingTimeout);
                historyListDiv.innerHTML = '<div style="color:red; text-align:center; padding:20px;">⛔ Gagal memuat riwayat (Permission Denied).</div>';
            });
        }

        function stopListeningData() {
            if (activeListener) off(ref(db, 'vouchers'));
            if (historyListener) off(ref(db, 'voucher_history'));
        }

        function getBadgeInfo(type) {
            // PAKET WAKTU
            if(type === '7_days') return { text: '7 HARI', css: 'bg-7days', label: '7 Hari', colorCode: '#3498db' };
            if(type === '30_days') return { text: '1 BULAN', css: 'bg-30days', label: '1 Bulan', colorCode: '#9b59b6' };
            if(type === '90_days') return { text: '3 BULAN', css: 'bg-90days', label: '3 Bulan', colorCode: '#e67e22' };
            if(type === '365_days') return { text: '1 TAHUN', css: 'bg-365days', label: '1 Tahun', colorCode: '#27ae60' };

            // STANDARD 10 KEYS (Legacy)
            if(type === 'silver') return { text: '10 Kunci SILVER', css: 'bg-silver', label: '10 Kunci Silver', colorCode: '#95a5a6' };
            if(type === 'gold') return { text: '10 Kunci GOLD', css: 'bg-gold', label: '10 Kunci Gold', colorCode: '#f1c40f' };
            if(type === 'diamond') return { text: '10 Kunci DIAMOND', css: 'bg-diamond', label: '10 Kunci Diamond', colorCode: '#00e5ff' };

            // PROMO SILVER
            if(type.includes('silver')) {
                const qty = type.replace('promo_silver_', '');
                return { text: `${qty} Kunci SILVER`, css: 'bg-silver', label: `${qty} Kunci Silver`, colorCode: '#95a5a6' };
            }

            // PROMO GOLD
            if(type.includes('gold')) {
                const qty = type.replace('promo_gold_', '');
                return { text: `${qty} Kunci GOLD`, css: 'bg-gold', label: `${qty} Kunci Gold`, colorCode: '#f1c40f' };
            }

            // PROMO DIAMOND
            if(type.includes('diamond')) {
                const qty = type.replace('promo_diamond_', '');
                return { text: `${qty} Kunci DIAMOND`, css: 'bg-diamond', label: `${qty} Kunci Diamond`, colorCode: '#00e5ff' };
            }

            return { text: type ? type.toUpperCase() : 'UNKNOWN', css: 'bg-7days', label: type, colorCode: '#333' };
        }

        function makeCode(length) {
            const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
            let result = '';
            for (let i = 0; i < length; i++) result += chars.charAt(Math.floor(Math.random() * chars.length));
            return result;
        }

        window.copyV = (code, type) => {
            const info = getBadgeInfo(type);
            const textToCopy = `${code} = ${info.label}`; 
            
            navigator.clipboard.writeText(textToCopy);
            myAlert("Disalin: " + textToCopy);
        };

        window.delV = (code) => {
            if (!auth.currentUser) return;
            if (auth.currentUser.uid !== ADMIN_UID) return myAlert("⛔ Anda bukan Admin!");
            myConfirm("Hapus voucher ini?", () => remove(ref(db, `vouchers/${code}`)));
        };

        document.getElementById('generate-btn').onclick = () => {
            if (!auth.currentUser) return myAlert("Login dulu!");
            if (auth.currentUser.uid !== ADMIN_UID) return myAlert("⛔ Anda bukan Admin!");

            const type = document.getElementById('plan-select').value;
            const qty = parseInt(document.getElementById('voucher-qty').value);
            const updates = {};
            for (let i = 0; i < qty; i++) updates[makeCode(12)] = type;
            update(ref(db, 'vouchers'), updates)
                .then(() => myAlert(`✅ Sukses buat ${qty} voucher!`))
                .catch(e => myAlert("Gagal: " + e.message));
        };

        window.myAlert = (msg) => {
            const toast = document.getElementById('custom-toast');
            toast.innerText = msg; toast.style.display = 'block';
            setTimeout(() => toast.style.display = 'none', 3000);
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
