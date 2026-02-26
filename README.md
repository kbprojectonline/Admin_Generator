<html lang="id">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
        <title>Admin - Master Generator (Final Style Fix)</title>
        <link href="https://fonts.googleapis.com/css2?family=Segoe+UI:wght@400;600;700;900&display=swap" rel="stylesheet">
        <style>
            :root {
                --primary: #2c3e50;
                --danger: #c0392b;
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
            .head-active { margin-top: 70px !important; border-left-color: #3498db; }
            .head-given { margin-top: 80px !important; border-left-color: var(--warning); }
            .head-history { margin-top: 80px !important; border-left-color: #e74c3c; }
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
            .history-row { flex-direction: column; align-items: flex-start; border-left: 5px solid #555; margin-bottom: 30px; padding: 18px; box-shadow: 0 4px 8px rgba(0,0,0,0.08); }
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

            /* // INI TAMBAHNYA: Style Box Hapus Masal */
            .mass-delete-area {
                background: #fff5f5; padding: 15px; border: 2px dashed #fab1a0; border-radius: 12px;
                margin-top: 15px; display: none; 
            }
            .mass-delete-flex { display: flex; gap: 8px; align-items: center; flex-wrap: wrap; }
            .mass-delete-flex select { padding: 10px; border-radius: 8px; border: 1px solid #ccc; flex: 1; font-weight: bold; }
            .btn-mass-del { background: var(--danger); color: white; border: none; padding: 10px 15px; border-radius: 8px; font-weight: 900; cursor: pointer; }
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
                <h1></h1>
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

            <h3 class="head-active">🎫 Voucher Aktif</h3>
            <div id="active-list" class="list-box" style="background: #fffafa;">Silakan Login...</div>
            <h3 class="head-given">📤 Voucher Telah Diberikan</h3>
            <div id="given-list" class="list-box" style="background: #f8f9fa;">Menunggu Login...</div>

<div id="mass-delete-container" style="display: none; width: 100%; margin-top: 100px;">
    <h3 style="color: #555; font-size: 20px; padding-left: 10px; border-left: 5px solid #e74c3c; margin-bottom: 15px;">🗑️ Menghapus Voucher Aktif</h3>
    
    <div style="background: #fffafb; border: 1px solid #eee; padding: 20px; border-radius: 12px;">
        <div class="mass-delete-flex" style="display: flex; flex-direction: column; gap: 12px;">
            
            <select id="mass-del-type" style="width: 100%; height: 80px; padding: 10px; border-radius: 12px; font-size: 16px; border: 1px solid #ccc; text-align: center; text-align-last: center; font-weight: bold; appearance: none; -webkit-appearance: none; background-color: white;">
                <optgroup label="PAKET WAKTU">
                    <option value="7_days">🗓️ Paket 7 Hari</option>
                    <option value="30_days">📅 Paket 1 Bulan</option>
                    <option value="90_days">📊 Paket 3 Bulan</option>
                    <option value="365_days">🏆 Paket 1 Tahun</option>
                </optgroup>
                <optgroup label="PAKET SILVER">
                    <option value="silver_1">🥈 1 Kunci Silver</option>
                    <option value="silver_5">🥈 5 Kunci Silver</option>
                    <option value="silver">🥈 10 Kunci Silver</option>
                    <option value="silver_20">🥈 20 Kunci Silver</option>
                    <option value="silver_50">🥈 50 Kunci Silver</option>
                    <option value="silver_100">🥈 100 Kunci Silver</option>
                </optgroup>
                <optgroup label="PAKET GOLD">
                    <option value="gold_1">👑 1 Kunci Gold</option>
                    <option value="gold_5">👑 5 Kunci Gold</option>
                    <option value="gold">👑 10 Kunci Gold</option>
                    <option value="gold_20">👑 20 Kunci Gold</option>
                    <option value="gold_50">👑 50 Kunci Gold</option>
                    <option value="gold_70">👑 70 Kunci Gold</option>
                </optgroup>
                <optgroup label="PAKET DIAMOND">
                    <option value="diamond_1">💎 1 Kunci Diamond</option>
                    <option value="diamond_5">💎 5 Kunci Diamond</option>
                    <option value="diamond">💎 10 Kunci Diamond</option>
                    <option value="diamond_15">💎 15 Kunci Diamond</option>
                    <option value="diamond_30">💎 30 Kunci Diamond</option>
                </optgroup>
            </select>

            <select id="mass-del-qty" style="width: 100%; height: 80px; border-radius: 12px; font-size: 16px; border: 1px solid #ccc; text-align: center; text-align-last: center; font-weight: bold; appearance: none; -webkit-appearance: none; background-color: white; cursor: pointer;">
                <option value="5">5 Pcs</option>
                <option value="10">10 Pcs</option>
                <option value="20">20 Pcs</option>
                <option value="30">30 Pcs</option>
                <option value="40">40 Pcs</option>
                <option value="50">50 Pcs</option>
                <option value="100">100 Pcs</option>
                <option value="1000">Hapus All</option>
            </select>

            <button onclick="runMassDelete()" style="width: 100%; background: #e74c3c; color: white; border: none; padding: 14px; border-radius: 12px; cursor: pointer; font-weight: bold; font-size: 15px;">
                HAPUS PERMANENT
            </button>
        </div>
        
        <p style="font-size: 11px; color: #888; margin-top: 12px; margin-bottom: 0; text-align: left;">*Menghapus Stok yang Voucher Aktif Saja.</p>
    </div>
</div>

            <div id="history-container" style="display: none;">
                <h3 class="head-history">📜 Riwayat Pembelian Kunci</h3>
                <div id="history-list" class="list-box" style="background:#fffafa;">Memuat riwayat...</div>
            </div>
            


<div id="history-delete-container" style="display: none; width: 100%; margin-top: 80px;">
    <h3 style="color: #555; font-size: 18px; padding-left: 10px; border-left: 5px solid #2c3e50; margin-bottom: 15px;">🗑️ Menghapus Riwayat Kunci</h3>
    <div style="background: #fffafb; border: 1px solid #eee; padding: 20px; border-radius: 12px;">
        
        <div style="display: flex; flex-direction: column; gap: 12px;">
            
            <select id="hist-del-qty" style="width: 100%; height: 80px; border-radius: 12px; font-size: 16px; border: 1px solid #ccc; text-align: center; text-align-last: center; font-weight: bold; appearance: none; -webkit-appearance: none; background-color: white; cursor: pointer;">
                <option value="1">Hapus 1 Riwayat</option>
                <option value="2">Hapus 2 Riwayat</option>
                <option value="3">Hapus 3 Riwayat</option>
                <option value="4">Hapus 4 Riwayat</option>
                <option value="5">Hapus 5 Riwayat</option>
                <option value="10">Hapus 10 Riwayat</option>
            </select>
            
            <button onclick="runHistoryDelete()" style="width: 100%; background: #e74c3c; color: white; border: none; padding: 14px; border-radius: 12px; cursor: pointer; font-weight: bold; font-size: 15px;">
                HAPUS PERMANENT
            </button>
            
        </div>
        
        <p style="font-size: 11px; color: #888; margin-top: 12px; margin-bottom: 0; text-align: left;">*Menghapus Riwayat Kunci dari yang Terlama.</p>
    </div>
</div>
<div id="premium-history-container" style="display: none; width: 100%; margin-top: 80px;">
    <h3 style="color: #555; font-size: 18px; padding-left: 10px; border-left: 5px solid #27ae60; margin-bottom: 15px;">⏳ Riwayat Pembelian Waktu</h3>
    <div id="premium-history-list" class="list-box" style="background:#f0fdf4;">Memuat riwayat paket waktu...</div>
</div>
<div id="premium-history-delete-container" style="display: none; width: 100%; margin-top: 80px;">
    <h3 style="color: #555; font-size: 18px; padding-left: 10px; border-left: 5px solid #27ae60; margin-bottom: 15px;">🗑️ Menghapus Riwayat Waktu</h3>
    <div style="background: #fffafb; border: 1px solid #eee; padding: 20px; border-radius: 12px;">
        
        <div style="display: flex; flex-direction: column; gap: 12px;">
            <select id="premium-hist-del-qty" style="width: 100%; height: 80px; border-radius: 12px; font-size: 16px; border: 1px solid #ccc; text-align: center; text-align-last: center; font-weight: bold; appearance: none; -webkit-appearance: none; background-color: white; cursor: pointer;">
                <option value="1">Hapus 1 Riwayat</option>
                <option value="2">Hapus 2 Riwayat</option>
                <option value="3">Hapus 3 Riwayat</option>
                <option value="4">Hapus 4 Riwayat</option>
                <option value="5">Hapus 5 Riwayat</option>
                <option value="10">Hapus 10 Riwayat</option>
            </select>
            
            <button onclick="runPremiumHistoryDelete()" style="width: 100%; background: #e74c3c; color: white; border: none; padding: 14px; border-radius: 12px; cursor: pointer; font-weight: bold; font-size: 15px;">
                HAPUS PERMANENT
            </button>
        </div>
        
        <p style="font-size: 11px; color: #888; margin-top: 12px; margin-bottom: 0; text-align: left;">*Menghapus Riwayat Waktu dari yang Terlama.</p>
    </div>
</div>
<div id="users-management-container" style="display: none; width: 100%; margin-top: 80px;">
    <h3 style="color: #555; font-size: 20px; padding-left: 10px; border-left: 5px solid #800000; margin-bottom: 15px;">👥 Manajemen Pengguna</h3>
    <div id="users-list" class="list-box" style="background: #fdf2f2; height: 480px; padding: 15px;">Memuat data users...</div>
</div>
        </div> <script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
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
            let recentlyDeleted = JSON.parse(localStorage.getItem('memDeleted') || '{}');
            let currentUsersData = {};
            let currentBannedData = {};
// AUTH STATE
            auth.onAuthStateChanged((user) => {
                if (user) {
                    const userRef = db.ref('users/' + user.uid);
                    const statusRef = db.ref('users/' + user.uid + '/isOnline');

                    db.ref('.info/connected').on('value', (snapshot) => {
                        if (snapshot.val() === true) {
                            statusRef.onDisconnect().set(firebase.database.ServerValue.TIMESTAMP);
                            statusRef.set(true);
                            userRef.update({
                                email: user.email,
                                profilename: "Admin Master"
                            });
                        }
                    });

                    if (user.uid === ADMIN_UID) {
                        loginBtn.innerHTML = `✅ Admin: <b>${user.email.split('@')[0]}</b> (Logout)`;
                        loginBtn.style.background = "#27ae60";
                        loginBtn.onclick = () => auth.signOut();
                        genBtn.disabled = false;
                        genBtn.innerText = "⚡ GENERATE VOUCHER (12 DIGIT)";
                        genBtn.style.background = "#2c3e50";
                        
                        // INI YANG BIKIN SEMUA KOTAKNYA MUNCUL (BLOCK)
                        document.getElementById('mass-delete-container').style.display = "block"; 
                        document.getElementById('premium-history-container').style.display = "block";
                        document.getElementById('premium-history-delete-container').style.display = "block"; // <--- INI KUNCINYA
                        document.getElementById('history-delete-container').style.display = "block";
                        historyContainer.style.display = "block";
                        document.getElementById('users-management-container').style.display = "block";
                        
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
                        
                        // INI UNTUK MENYEMBUNYIKAN KALAU BUKAN ADMIN (NONE)
                        historyContainer.style.display = "none";
                        document.getElementById('mass-delete-container').style.display = "none"; 
                        document.getElementById('premium-history-container').style.display = "none";
                        document.getElementById('premium-history-delete-container').style.display = "none"; // <--- TAMBAH DI SINI JUGA
                        document.getElementById('history-delete-container').style.display = "none";
                        document.getElementById('users-management-container').style.display = "none";
                        
                        activeListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#c0392b;">⛔ AKSES DITOLAK</div>';
                        givenListDiv.innerHTML = '';
                    }
                } else {
                    loginBtn.innerHTML = `🔑 Login Sebagai Admin (Google)`;
                    loginBtn.style.background = "#4285F4";
                    loginBtn.onclick = loginGoogle;
                    genBtn.disabled = true;
                    genBtn.innerText = "🔒 Login Terlebih Dahulu";
                    genBtn.style.background = "#ccc";
                    
                    // INI UNTUK MENYEMBUNYIKAN KALAU BELUM LOGIN (NONE)
                    historyContainer.style.display = "none";
                    document.getElementById('mass-delete-container').style.display = "none"; 
                    document.getElementById('premium-history-container').style.display = "none";
                    document.getElementById('premium-history-delete-container').style.display = "none"; // <--- DAN TAMBAH DI SINI
                    document.getElementById('history-delete-container').style.display = "none";
                    document.getElementById('users-management-container').style.display = "none";
                    
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
db.ref('users').on('value', (snapshot) => {
    currentUsersData = snapshot.val() || {}; // Simpan salinan ke memori
    
    renderUsersList(currentUsersData);
}, (error) => {
    document.getElementById('users-list').innerHTML = `<div style="text-align:center; padding:20px; color:#c0392b; font-weight:bold;">❌ Gagal: ${error.message}</div>`;
});

// 3. Ambil Riwayat (Diperbarui dengan Realtime Name)
db.ref('voucher_history').on('value', (snapshot) => {
    if (snapshot.exists()) {
        const data = Object.values(snapshot.val()).sort((a, b) => b.date - a.date);
let html = "";
let htmlPremium = ""; // TAMBAHAN: Variabel untuk menampung 4 paket waktu
let uniqueUids = []; 

data.forEach(item => {
    const badge = getBadgeInfo(item.type);
    const dateObj = new Date(item.date);
    const hari = dateObj.toLocaleDateString('id-ID', { weekday: 'long' });
    const jam = dateObj.toLocaleTimeString('id-ID').replace(/\./g, ':');
    const tgl = dateObj.toLocaleDateString('id-ID').split('/').join('.');
    
    if (item.uid && !uniqueUids.includes(item.uid)) {
        uniqueUids.push(item.uid);
    }

    let baseUser = item.user || 'Unknown';
    let safeBaseUser = baseUser.length > 8 ? baseUser.substring(0, 8) : baseUser;

    // TAMBAHAN: Bungkus desain kotak riwayat ke dalam variabel barisRiwayat
    let barisRiwayat = `
    <div class="item-row history-row">
        <span class="date-info">🕒 ${hari} | ${jam} | ${tgl}</span>
        <div style="width: 100%;">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 5px;">
                <span class="code-text" style="font-size: 0.95rem;">${item.code}</span>
                <span class="badge ${badge.css}" style="font-size: 0.65rem;">${badge.text}</span>
            </div>
            <span class="user-info">
                <div style="margin-bottom: 6px;">👤 Dipakai: <b class="realtime-name" data-uid="${item.uid}">${safeBaseUser}</b></div>
                <div style="margin-bottom: 6px;">${item.email ? `@${item.email}` : ''}</div>
                <div style="margin-bottom: 6px; font-size: 0.8rem; color: #555; font-family: monospace; font-weight: bold;">UID: ${item.uid || '-'}</div>
            </span>
        </div>
    </div>`;

// PISAHKAN LOGIKANYA DENGAN IF - ELSE
    if (['7_days', '30_days', '90_days', '365_days'].includes(item.type)) {
        // Jika ini paket waktu, masukkan HANYA ke kotak Premium
        htmlPremium += barisRiwayat; 
    } else {
        // Jika BUKAN paket waktu (misal: kunci silver, gold, diamond), masukkan ke kotak Biasa
        html += barisRiwayat; 
    }
});

historyListDiv.innerHTML = html;
// TAMBAHAN: Tampilkan data yang sudah difilter ke kotak window baru
document.getElementById('premium-history-list').innerHTML = htmlPremium || '<div style="text-align:center; padding:20px; color:#999;">Belum ada riwayat paket waktu.</div>';
        
        uniqueUids.forEach(uid => {
            db.ref('users/' + uid).once('value').then(userSnap => {
                if(userSnap.exists()) {
                    const userData = userSnap.val();
                    
                    // AMBIL DATA & POTONG PAKSA REALTIME (Maksimal 8 Karakter)
                    let rawDynName = userData.profilename || userData.profileName || userData.displayName || (userData.email ? userData.email.split('@')[0] : "User");
                    let dynamicName = rawDynName.length > 8 ? rawDynName.substring(0, 8) : rawDynName;
                    
                    if (dynamicName) {
                        document.querySelectorAll(`.realtime-name[data-uid="${uid}"]`).forEach(el => {
                            el.innerText = dynamicName;
                        });
                    }
                }
            }).catch(err => {
                console.error("Gagal menarik data untuk UID: " + uid, err);
            });
        });

    } else {
        historyListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999;">Belum ada riwayat penggunaan.</div>';
    }
});
db.ref('banned_temporary').on('value', (snapshot) => {
                currentBannedData = snapshot.val() || {};
                renderUsersList(currentUsersData); 
            });
            
            }
            function renderAllLists() {
                // A. RENDER ACTIVE LIST
                const activeEntries = Object.entries(globalVouchers).filter(([code, type]) => !globalGiven[code]);
// GANTI BAGIAN INI (LENGKAP DARI TAHUNAN SAMPAI DIAMOND)
const getSortIndex = (type) => {
    let clean = type.toLowerCase().replace('promo_', '').trim();
    const priority = {
        '7_days': 1,
        '30_days': 2,
        '90_days': 3,
        '365_days': 4,
        'silver_1': 5,
        'silver_5': 6,
        'silver': 7,
        'silver_20': 8,
        'silver_50': 9,
        'silver_100': 10,
        'gold_1': 11,
        'gold_5': 12,
        'gold': 13,
        'gold_20': 14,
        'gold_50': 15,
        'gold_70': 16,
        'diamond_1': 17,
        'diamond_5': 18,
        'diamond': 19,
        'diamond_15': 20,
        'diamond_30': 21
    };
    return priority[clean] || 99;
};
                activeEntries.sort((a, b) => getSortIndex(a[1]) - getSortIndex(b[1]));
                if (activeEntries.length > 0) {
                    let html = "";
                    activeEntries.forEach(([code, type]) => {
                        const badge = getBadgeInfo(type);
                        html += `
                        <div class="swipe-wrapper">
                            <div class="swipe-bg bg-send">KIRIM >></div>
                            <div class="item-row" id="act-${code}">
                                <div style="flex:1; display: flex; flex-direction: column; gap: 10px;">
                                    <span class="code-text">${code}</span>
                                    <span class="badge ${badge.css}" style="width: fit-content;">${badge.text}</span>
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
                // B. RENDER GIVEN LIST (TANPA KLIK SALIN, SIZE & STYLE FIXED)
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
                        html += `
                        <div class="swipe-wrapper">
                            <div class="swipe-bg bg-return">KEMBALIKAN >></div>
                            <div class="item-row" id="giv-${code}" style="border-left: 5px solid #95a5a6; background: #fff; cursor: default;">
                                <div style="display: flex; flex-direction: column; width: 100%;">
                                    <div style="display: flex; justify-content: space-between; align-items: center; width: 100%;">
                                        <span class="code-text" style="color: #333; font-size: 0.95rem;">${code}</span>
                                        <span class="badge ${badge.css}" style="font-size: 0.7rem;">${badge.text}</span>
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
                    givenListDiv.innerHTML = '';
                }
            }
            // --- SWIPE LOGIC ---
function addSwipeLogic(element, actionCallback) {
            let startX = 0;
            let startY = 0; // Tambahan: Deteksi posisi atas-bawah
            let currentTranslate = 0;
            let isDragging = false;

            element.addEventListener('touchstart', (e) => {
                if (e.touches.length > 1) return; 

                startX = e.touches[0].clientX;
                startY = e.touches[0].clientY; // Simpan posisi awal Y
                isDragging = true;
                element.style.transition = 'none'; 
            });

            element.addEventListener('touchmove', (e) => {
                if (e.touches.length > 1) return; 
                if (!isDragging) return;

                const currentX = e.touches[0].clientX;
                const currentY = e.touches[0].clientY;
                
                const diffX = currentX - startX;
                const diffY = currentY - startY;

                // LOGIKA PENTING:
                // Jika gerakan menyamping (X) lebih besar daripada gerakan atas-bawah (Y)
                // Maka matikan scroll (preventDefault) agar fokus swipe voucher
                if (Math.abs(diffX) > Math.abs(diffY)) {
                    if (e.cancelable) e.preventDefault(); 
                } else {
                    return; // Jika geraknya vertikal, biarkan scrolling halaman, jangan geser voucher
                }

                // Hanya geser voucher jika arahnya ke kiri (negatif)
                if (diffX < 0) {
                    currentTranslate = diffX;
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
            // --- FUNGSI AKSI ---
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
    myConfirm("Hapus Permanent?", () => {
        const updates = {};
        updates['vouchers/' + code] = null;
        updates['vouchers_given/' + code] = null;

        db.ref().update(updates)
            .then(() => {
                myAlert("✅ Voucher Berhasil Dihapus Permanent!");
            })
            .catch((error) => {
                myAlert("❌ Gagal: " + error.message);
            });
    });
};
document.getElementById('generate-btn').onclick = () => {
    const type = document.getElementById('plan-select').value;
    const qty = parseInt(document.getElementById('voucher-qty').value);
    
    // 1. LANGSUNG TRIGER POP-UP (Biar kerasa pas diklik)
    myAlert(`⚡ Proses membuat ${qty} voucher...`);

    const updates = {};
    for (let i = 0; i < qty; i++) updates[makeCode(12)] = type;
    
    db.ref('vouchers').update(updates)
    .then(() => {
        // 2. TIMPA DENGAN POP-UP SUKSES
        myAlert(`✅ Sukses buat ${qty} voucher!`);
    })
    .catch(e => myAlert("Gagal: " + e.message));
};
window.myAlert = (msg) => {
    const toast = document.getElementById('custom-toast');
    
    // PAKSA RESET: Hilangkan class/display dan hentikan timer sebelumnya
    toast.style.display = 'none';
    if (window.toastTimer) clearTimeout(window.toastTimer);

    // Kasih jeda 10ms biar browser sempat ngerender "hilang" sebelum muncul lagi
    setTimeout(() => {
        toast.innerText = msg;
        toast.style.display = 'block';
        
        // Timer buat ngilangin otomatis
        window.toastTimer = setTimeout(() => {
            toast.style.display = 'none';
        }, 5000);
    }, 10); 
};
window.myConfirm = (msg, action, btnText = "Hapus", btnColor = "") => {
                document.getElementById('modal-msg').innerText = msg;
                
                const confirmBtn = document.getElementById('modal-confirm-btn');
                confirmBtn.innerText = btnText;
                
                // RESET STYLE AGRESIF
                confirmBtn.removeAttribute('style'); // Hapus semua gaya lama
                
                // Terapkan gaya baru dengan prioritas tertinggi
                if (btnColor) {
                    confirmBtn.setAttribute('style', `background: ${btnColor} !important; color: white !important; flex: 1; padding: 12px; border-radius: 8px; border: none; font-weight: 900; cursor: pointer;`);
                } else {
                    // Jika tidak ada warna khusus (misal untuk tombol Delete), kembalikan ke merah bawaan
                    confirmBtn.setAttribute('style', `background: var(--danger) !important; color: white !important; flex: 1; padding: 12px; border-radius: 8px; border: none; font-weight: 900; cursor: pointer;`);
                }
                
                document.getElementById('custom-overlay').style.display = 'flex';
                confirmBtn.onclick = () => { action(); closeModal(); };
            };
            window.closeModal = () => document.getElementById('custom-overlay').style.display = 'none';
window.runMassDelete = () => {
    const typeSelect = document.getElementById('mass-del-type');
    const targetType = typeSelect.value;
    const targetQty = parseInt(document.getElementById('mass-del-qty').value);

    // Ambil teks label (misal: "7 Hari"), bersihkan emoji agar pop-up rapi
    let namaPaket = typeSelect.options[typeSelect.selectedIndex].text;
    namaPaket = namaPaket.replace(/[^\x00-\x7F]/g, "").replace("Paket", "").trim();

    // 1. Filter stok yang ada di memori (globalVouchers)
    const matches = Object.entries(globalVouchers)
        .filter(([code, type]) => {
            const isMatch = (type === targetType);
            const isNotGiven = !globalGiven[code]; // Belum dikasih ke user
            return isMatch && isNotGiven;
        })
        .slice(0, targetQty);

    // 2. Jika benar-benar kosong
    if (matches.length === 0) {
        myAlert("❌ Stok " + namaPaket + " sudah habis!");
        return;
    }

    // 3. Panggil Pop-up INTERNAL kamu (myConfirm)
    // Angka yang muncul adalah matches.length (angka asli di stok)
    myConfirm(`Hapus Permanent ${matches.length} Stok, ${namaPaket}?`, () => {
        const updates = {};
        matches.forEach(([code]) => {
            updates[`vouchers/${code}`] = null;
        });

        // 4. Proses Hapus ke Database
        db.ref().update(updates)
            .then(() => myAlert(`✅ Berhasil menghapus ${matches.length} stok ${namaPaket}!`))
            .catch(err => myAlert("Gagal: " + err.message));
    });
};
window.runHistoryDelete = () => {
    const qty = parseInt(document.getElementById('hist-del-qty').value);
    
    db.ref('voucher_history').once('value', (snapshot) => {
        if (!snapshot.exists()) {
            myAlert("❌ Tidak ada riwayat untuk dihapus!");
            return;
        }

const historyData = [];
        snapshot.forEach((child) => {
            const item = child.val();
            // FILTER: JANGAN MASUKKAN PAKET WAKTU KE PENGHAPUSAN BIASA
            if (!['7_days', '30_days', '90_days', '365_days'].includes(item.type)) {
                historyData.push({ key: child.key, date: item.date });
            }
        });

        // Urutkan dari yang paling lama (angka date terkecil)
        historyData.sort((a, b) => a.date - b.date);

        const targets = historyData.slice(0, qty);

        myConfirm(`Yakin, Hapus ${targets.length} Riwayat, Dari yang Paling Lama?`, () => {
            const updates = {};
            targets.forEach(item => {
                updates[`voucher_history/${item.key}`] = null;
            });

            db.ref().update(updates)
                .then(() => myAlert(`✅ Berhasil menghapus ${targets.length} riwayat lama!`))
                .catch(err => myAlert("Gagal: " + err.message));
        });
    });
};

window.runPremiumHistoryDelete = () => {
    const qty = parseInt(document.getElementById('premium-hist-del-qty').value);
    
    db.ref('voucher_history').once('value', (snapshot) => {
        if (!snapshot.exists()) {
            myAlert("❌ Tidak ada riwayat untuk dihapus!");
            return;
        }

        const historyData = [];
        snapshot.forEach((child) => {
            const item = child.val();
            // FILTER: HANYA AMBIL PAKET WAKTU UNTUK DIHAPUS DI SINI
            if (['7_days', '30_days', '90_days', '365_days'].includes(item.type)) {
                historyData.push({ key: child.key, date: item.date });
            }
        });

        if (historyData.length === 0) {
            myAlert("❌ Tidak ada Riwayat Waktu untuk dihapus!");
            return;
        }

        // Urutkan dari yang paling lama (angka date terkecil)
        historyData.sort((a, b) => a.date - b.date);
        const targets = historyData.slice(0, qty);

        myConfirm(`Yakin, Hapus ${targets.length} Riwayat Waktu, Dari yang Paling Lama?`, () => {
            const updates = {};
            targets.forEach(item => {
                updates[`voucher_history/${item.key}`] = null;
            });

            db.ref().update(updates)
                .then(() => myAlert(`✅ Berhasil menghapus ${targets.length} riwayat waktu lama!`))
                .catch(err => myAlert("Gagal: " + err.message));
        });
    });
};

let lastActiveCache = {}; 

function renderUsersList(usersData) {
    const usersListDiv = document.getElementById('users-list');
    
    // 1. BERSIHKAN MEMORI DENGAN AMAN
    let memChanged = false;
    Object.keys(recentlyDeleted).forEach(id => {
        const dbUser = usersData && usersData[id];
        const isBanned = currentBannedData[id] && Date.now() < currentBannedData[id];
        
        // Hapus memori HANYA JIKA waktu banned habis dan user sudah benar-benar login membawa email
        if (!isBanned && dbUser && dbUser.email) {
            delete recentlyDeleted[id];
            memChanged = true;
        }
    });
    if(memChanged) localStorage.setItem('memDeleted', JSON.stringify(recentlyDeleted));
    
    // 2. GABUNGKAN SEMUA UID
    const allUids = new Set([...Object.keys(usersData || {}), ...Object.keys(recentlyDeleted), ...Object.keys(currentBannedData)]);
    
    // 3. MERGE DATA MEMORI & DATABASE BIAR NAMA ASLI AMAN
    let userArray = Array.from(allUids).map(uid => {
        const memData = recentlyDeleted[uid] || {};
        const dbData = (usersData && usersData[uid]) || {};
        
        let finalUser = { ...dbData };
        // KEMBALIKAN SEMUA VARIABEL NAMA LO (Jangan ada yang dihapus)
        if (!finalUser.email) finalUser.email = memData.email;
        if (!finalUser.profilename) finalUser.profilename = memData.profilename || memData.profileName || memData.displayName || memData.name;
        if (!finalUser.diamond) finalUser.diamond = memData.diamond;
        if (!finalUser.gold) finalUser.gold = memData.gold;
        if (!finalUser.silver) finalUser.silver = memData.silver;
        
        return [uid, finalUser];
    }).filter(([uid]) => uid !== ADMIN_UID);

    if (userArray.length === 0) {
        usersListDiv.innerHTML = '<div style="text-align:center; padding:20px; color:#999; font-weight: bold;">Tidak ada data user terdaftar.</div>';
        return;
    }

// 4. LOGIKA UI LOCK 60 DETIK
    const getStatusInfo = (uid, userOnlineStatus, userEmail) => {
        if (!userEmail) {
            return { text: "🔒 MENUNGGU LOGIN", active: false, isGhost: true };
        }

        // JIKA USER KLIK LOGOUT -> BUNUH STATUS HIJAU DETIK INI JUGA!
        if (userOnlineStatus === "LOGOUT") {
            delete lastActiveCache[uid]; // Hapus memori penahan 60 detik
            return { text: "⚫ OFFLINE", active: false };
        }

        const sekarang = Date.now();
        if (userOnlineStatus === true) {
            lastActiveCache[uid] = sekarang;
            return { text: "🟢 ACTIVE NOW", active: true };
        }
        
        const waktuTerakhir = lastActiveCache[uid] || (typeof userOnlineStatus === 'number' ? userOnlineStatus : 0);
        const selisih = Math.floor((sekarang - waktuTerakhir) / 1000);

        if (selisih <= 60) return { text: "🟢 ACTIVE NOW", active: true }; 
        const mins = Math.floor(selisih / 60);
        if (mins < 60) return { text: `⚫ Online ${mins} menit lalu`, active: false };
        const hours = Math.floor(mins / 60);
        if (hours < 24) return { text: `⚫ Online ${hours} jam lalu`, active: false };
        return { text: "⚫ OFFLINE", active: false };
    };

    // 5. SORTING KASTA
    userArray.sort((a, b) => {
        const getRank = (uid, userObj) => {
            const isBanned = currentBannedData[uid] && Date.now() < currentBannedData[uid];
            const dbData = usersData && usersData[uid];
            const isGhost = !dbData || !dbData.email; 
            
            if (isBanned) return 4;
            if (isGhost) return 3;
            
            // Pass the email to getStatusInfo
            const info = getStatusInfo(uid, (dbData && dbData.isOnline), userObj.email);
            if (info.active) return 1;
            return 2;
        };

        const rankA = getRank(a[0], a[1]);
        const rankB = getRank(b[0], b[1]);

        if (rankA !== rankB) return rankA - rankB; 

        // KEMBALIKAN SORTING NAMA ASLI
        let nameA = (a[1].profilename || a[1].profileName || a[1].displayName || a[1].name || a[1].email || "").toLowerCase();
        let nameB = (b[1].profilename || b[1].profileName || b[1].displayName || b[1].name || b[1].email || "").toLowerCase();
        return nameA.localeCompare(nameB); 
    });

    // 6. RENDER LAYOUT
    let html = "";
    try {
        userArray.forEach(([uid, user]) => {
            const isBanned = currentBannedData[uid] && Date.now() < currentBannedData[uid];
            
            // Cek hantu dari DATABASE ASLI
            const dbData = usersData && usersData[uid];
            const isGhost = !dbData || !dbData.email; 

            let statusText = "";
            let statusColor = "";
            let isReallyActive = false;

            if (isBanned) {
                const sisaMenit = Math.ceil((currentBannedData[uid] - Date.now()) / 60000);
                statusText = `⏳ COOLDOWN (${sisaMenit} Menit)`;
                statusColor = "#e67e22";
            } else if (isGhost) {
                statusText = "⏳ COOLDOWN SELESAI";
                statusColor = "#7f8c8d";
            } else if (user.disabled) {
                statusText = "⛔ DISABLED";
                statusColor = "#c0392b";
            } else {
                // Pass the email to getStatusInfo
                const status = getStatusInfo(uid, user.isOnline, user.email);
                statusText = status.text;
                statusColor = status.active ? "#27ae60" : "#7f8c8d";
                isReallyActive = status.active;
            }

            const cardBorder = isBanned ? "3px solid #e67e22" : (isGhost ? "3px solid #7f8c8d" : (isReallyActive ? "3px solid #27ae60" : "1px solid #ddd"));

            // LOGIKA 8 KARAKTER SUDAH DIKEMBALIKAN 100%
            let rawName = user.profilename || user.profileName || user.displayName || user.name || (user.email ? user.email.split('@')[0] : "User Baru");
            const userName = rawName.length > 8 ? rawName.substring(0, 8) : rawName;
            
            const dKunci = user.diamond || (user.keys && user.keys.diamond) || 0;
            const gKunci = user.gold || (user.keys && user.keys.gold) || 0;
            const sKunci = user.silver || (user.keys && user.keys.silver) || 0;

            html += `
            <div style="display: flex; flex-direction: column; background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.05); margin-bottom: 15px; border: ${cardBorder}; transition: border 0.3s ease;">
                <div style="margin-bottom: 12px;">
                    <div style="font-weight: 900; color: #333; font-size: 1.1rem; margin-bottom: 4px;">${userName}</div>
                    <div style="font-size: 0.85rem; color: #555; margin-bottom: 4px;"><b>@</b> ${user.email || 'No Email'}</div>
                    
                    <div style="font-size: 0.75rem; color: #aaa; font-family: monospace; margin-bottom: 6px;">UID: ${uid}</div>
                    
                    <div style="display: flex; justify-content: space-around; background: #f9f9f9; padding: 10px; border-radius: 10px; margin: 15px 0; border: 1px solid #eee;">
                        <div>💎 <b>${dKunci}</b></div><div>👑 <b>${gKunci}</b></div><div>🥈 <b>${sKunci}</b></div>
                    </div>
                    <div style="color: ${statusColor}; font-weight: 900; font-size: 0.95rem; text-transform: uppercase; margin-top: 5px;">
                        ${statusText}
                    </div>
                </div>
                <div style="display: flex; gap: 10px; border-top: 1px solid #eee; padding-top: 12px;">
                    ${isBanned ? `<div style="flex:1; text-align:center; font-size:0.8rem; color:#7f8c8d; font-weight:bold;">⚠️ Akun Ini Telah Di Delete</div>` : 
                    (isGhost ? `<div style="flex:1; text-align:center; font-size:0.8rem; color:#7f8c8d; font-weight:bold;">⚠️ Menunggu Akun Login</div>` : 
                    `<button style="flex: 1; padding: 10px; background: ${user.disabled ? '#27ae60':'#f39c12'}; color: white; border: none; border-radius: 8px; font-weight: bold; font-size: 0.8rem;" onclick="toggleDisableUser('${uid}', ${!user.disabled})">${user.disabled ? 'Enable':'Disable'}</button>
                     <button style="flex: 1; padding: 10px; background: #c0392b; color: white; border: none; border-radius: 8px; font-weight: bold; font-size: 0.8rem;" onclick="deleteUser('${uid}')">Delete</button>`)}
                </div>
                ${(!isGhost && !isBanned) ? `<button style="width: 100%; padding: 10px; background: #3498db; color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 0.85rem; margin-top: 10px;" onclick="sendPromoMessage('${uid}')">💬 Kirim Pesan</button>` : ''}
            </div>`;
        });
        usersListDiv.innerHTML = html;
    } catch (e) {
        usersListDiv.innerHTML = `<div style="text-align:center; padding:20px; color:#c0392b; font-weight:bold;">❌ Error Tampilan: ${e.message}</div>`;
    }
}

// === 2. FUNGSI DISABLE / ENABLE ===
window.toggleDisableUser = (uid, disable) => {
    // Ubah kata aksi menjadi Disable / Enable agar sesuai dengan pop-up
    const actionText = disable ? "Disable" : "Enable";
    
    // Teks dan Warna (Disable = Oranye, Enable = Hijau)
    const btnText = disable ? "Disable" : "Enable";
    const btnColor = disable ? "#f39c12" : "#27ae60"; // <--- Pakai kode Hex warna Oranye di sini!

    myConfirm(`Yakin ingin, ${actionText} Akun Ini?`, () => {
        db.ref(`users/${uid}/disabled`).set(disable)
            .then(() => myAlert(`✅ Akun berhasil di-${disable ? 'disable' : 'enable'}!`))
            .catch(err => myAlert("❌ Gagal: " + err.message));
    }, btnText, btnColor);
};

window.deleteUser = (uid) => {
    const userData = currentUsersData[uid];
    if (!userData) {
        myAlert("❌ Data tidak ditemukan!");
        return;
    }

myConfirm(`Yakin Ingin, Hapus Permanet Akun Ini?`, () => {
            recentlyDeleted[uid] = { ...userData };
            localStorage.setItem('memDeleted', JSON.stringify(recentlyDeleted)); // SIMPAN KE BROWSER

        // --- TAMBAHAN LOGIKA BANNED 5 MENIT ---
        const bannedUntil = Date.now() + (5 * 60 * 1000); 
        
        const updates = {};
        updates[`users/${uid}`] = null; 
        updates[`banned_temporary/${uid}`] = bannedUntil; 

        db.ref().update(updates)
            .then(() => {
                myAlert("✅ User dihapus & dilarang login 5 menit!");
                renderUsersList(currentUsersData);
            })
            .catch(err => {
                delete recentlyDeleted[uid];
                myAlert("❌ Gagal: " + err.message);
            });
    }, "Delete"); 
};

// === 3. FUNGSI KIRIM PESAN PROMO ===
window.sendPromoMessage = (uid) => {
    // Langsung tembak ke database tanpa konfirmasi
db.ref(`users/${uid}/promoMessage`).set(true)
        .then(() => myAlert("✅ Pesan berhasil dikirim!"))
        .catch(err => myAlert("❌ Gagal: " + err.message));
};

setInterval(() => {
    if (currentUsersData) {
        renderUsersList(currentUsersData);
    }
}, 1000);
// ==========================================
// FITUR SILENT REFRESH (ANTI FREEZE TANPA KEDIP)
// ==========================================
setInterval(() => {
    // 1. Putus koneksi "kabel gaib" Firebase sesaat
    firebase.database().goOffline();
    
    // 2. Sambungin lagi 1 detik kemudian (Data langsung seger tanpa loading browser!)
    setTimeout(() => {
        firebase.database().goOnline();
    }, 1000);
}, 20000); // Refresh otomatis setiap 20 detik
        </script>
    </body>
</html>
