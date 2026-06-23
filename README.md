<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amplop Nilai Kelulusan - SMP Negeri 1 Lingga</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css">
    <style>
        /* --- RESET & GLOBAL STYLES --- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: #f0f7ff;
            color: #1e293b;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            padding-bottom: 90px;
            position: relative;
            overflow-x: hidden;
        }

        /* --- MOBILE CONTAINER (MAX 440px) --- */
        .container-mobile {
            width: 100%;
            max-width: 440px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 16px;
            position: relative;
            z-index: 10;
        }

        /* --- UI GLASSMORPHISM COMPONENT (MATERIAL 3) --- */
        .m3-glass {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.9);
            border-radius: 24px;
            padding: 20px;
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.04);
        }

        /* --- HEADER BRANDING --- */
        .app-header {
            text-align: center;
            margin-bottom: 4px;
            padding-top: 10px;
        }
        .app-header h1 {
            font-size: 20px;
            font-weight: 800;
            color: #1d4ed8;
            letter-spacing: -0.5px;
        }
        .app-header p {
            font-size: 13px;
            color: #64748b;
            margin-top: 4px;
        }

        /* --- NAVIGASI LAMAN (TAB CONTROL) --- */
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        /* --- LAMAN 1: HOME (RATA-RATA TIAP MAPEL) --- */
        .subject-avg-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 8px;
        }
        .subject-avg-card {
            background: rgba(255, 255, 255, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.7);
            border-radius: 14px;
            padding: 12px 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .subject-avg-card span {
            font-size: 13px;
            font-weight: 600;
            color: #475569;
        }
        .subject-avg-card strong {
            font-size: 16px;
            font-weight: 700;
            color: #1d4ed8;
        }

        /* --- LAMAN 2: NILAIKU (PENCARIAN) --- */
        .search-box {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .search-box label {
            font-size: 14px;
            font-weight: 600;
            color: #334155;
        }
        .input-wrapper {
            position: relative;
        }
        .input-wrapper i {
            position: absolute;
            left: 16px;
            top: 50%;
            transform: translateY(-50%);
            color: #94a3b8;
        }
        .input-wrapper input {
            width: 100%;
            height: 48px;
            padding: 0 16px 0 44px;
            border-radius: 16px;
            border: 1px solid #cbd5e1;
            background: rgba(255, 255, 255, 0.9);
            font-size: 15px;
            outline: none;
            transition: all 0.2s;
        }
        .input-wrapper input:focus {
            border-color: #3b82f6;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.15);
        }
        .btn-search {
            width: 100%;
            height: 48px;
            background: #1d4ed8;
            color: white;
            border: none;
            border-radius: 16px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 12px rgba(29, 78, 216, 0.2);
        }

        /* --- LOADING SPINNER --- */
        .loading-container {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 30px 0;
            gap: 16px;
        }
        .spinner {
            width: 40px;
            height: 40px;
            border: 4px solid rgba(29, 78, 216, 0.1);
            border-top: 4px solid #1d4ed8;
            border-radius: 50%;
            animation: spin 0.8s linear infinite;
        }
        .pulse-text {
            font-size: 14px;
            color: #1d4ed8;
            font-weight: 600;
            animation: pulse 1.2s ease-in-out infinite;
        }

        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        @keyframes pulse { 0%, 100% { opacity: 0.6; } 50% { opacity: 1; } }

        /* --- KARTU HASIL INDIVIDU --- */
        #result-container {
            display: none;
        }
        .result-card {
            display: flex;
            flex-direction: column;
            gap: 16px;
            position: relative;
            overflow: hidden;
        }

        .card-rank-1 {
            background: linear-gradient(135deg, #d1fae5 0%, #a7f3d0 100%) !important;
            border: 2px solid #34d399 !important;
            box-shadow: 0 10px 25px rgba(52, 211, 153, 0.25) !important;
        }
        .card-rank-2 {
            background: linear-gradient(135deg, #dbaefe 0%, #bfdbfe 100%) !important;
            border: 1px solid #93c5fd !important;
        }
        .card-rank-3 {
            background: linear-gradient(135deg, #ffedd5 0%, #fdbb74 100%) !important;
            border: 1px solid #f97316 !important;
        }
        .card-rank-normal {
            background: rgba(255, 255, 255, 0.9);
        }

        .bounce-effect {
            animation: surpriseBounce 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) both;
        }
        @keyframes surpriseBounce {
            0% { transform: scale(0.3); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .student-profile {
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid rgba(0,0,0,0.06);
            padding-bottom: 12px;
        }
        .profile-info h2 {
            font-size: 16px;
            font-weight: 700;
            color: #0f172a;
        }
        .profile-info p {
            font-size: 12px;
            color: #64748b;
            margin-top: 4px;
        }
        .rank-badge {
            padding: 6px 12px;
            border-radius: 999px;
            font-size: 12px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .badge-1 { background: #10b981; color: white; }
        .badge-2 { background: #2563eb; color: white; }
        .badge-3 { background: #ea580c; color: white; }
        .badge-normal { background: #64748b; color: white; }

        /* TAMPILAN BANNER KELULUSAN RESMI & RATA-RATA */
        .congrats-banner {
            background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
            color: white;
            padding: 20px 16px;
            border-radius: 18px;
            text-align: center;
            box-shadow: inset 0 0 12px rgba(255,255,255,0.2);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }
        .congrats-text {
            font-size: 15px;
            font-weight: 700;
            letter-spacing: 0.5px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.15);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .congrats-text i {
            color: #f59e0b;
        }
        .score-display-large {
            font-size: 44px;
            font-weight: 900;
            letter-spacing: -1px;
            line-height: 1;
            background: linear-gradient(to bottom, #ffffff, #e2e8f0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            drop-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }
        .predikat-subtext {
            font-size: 11px;
            font-weight: 600;
            background: rgba(255, 255, 255, 0.2);
            padding: 4px 12px;
            border-radius: 6px;
            letter-spacing: 0.3px;
        }

        /* --- KOTAK INFO PENGAMBILAN SKL & SIMULASI --- */
        .skl-announcement {
            background: #fff7ed;
            border: 1px dashed #f97316;
            border-radius: 16px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        .skl-block {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .skl-title {
            font-size: 13px;
            font-weight: 700;
            color: #c2410c;
            display: flex;
            align-items: center;
            gap: 8px;
            border-bottom: 1px dashed rgba(249, 115, 22, 0.2);
            padding-bottom: 4px;
        }
        .skl-details {
            font-size: 12px;
            color: #ea580c;
            line-height: 1.5;
            list-style: none;
        }
        .skl-details li {
            margin-bottom: 4px;
            display: flex;
            align-items: flex-start;
            gap: 6px;
        }
        .skl-details i {
            margin-top: 3px;
            font-size: 10px;
            width: 12px;
            text-align: center;
        }

        /* --- FIXED BOTTOM NAVBAR --- */
        .bottom-navbar {
            position: fixed;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            max-width: 440px;
            height: 64px;
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-top: 1px solid rgba(255, 255, 255, 0.8);
            display: flex;
            justify-content: space-around;
            align-items: center;
            z-index: 999;
        }
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
            background: none;
            border: none;
            width: 70px;
            height: 100%;
            color: #94a3b8;
            cursor: pointer;
        }
        .nav-item i { font-size: 18px; }
        .nav-item span { font-size: 11px; font-weight: 600; }
        .nav-item.active { color: #1d4ed8; }

        /* --- EFEK VISUAL ANIMASI BINTANG KEJORA --- */
        .star-field-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 1;
            overflow: hidden;
            display: none;
        }
        .kejora-star {
            position: absolute;
            color: #f59e0b;
            filter: drop-shadow(0 0 6px rgba(245, 158, 11, 0.9));
            opacity: 0;
            animation: flashAndFly 2.5s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
        }
        @keyframes flashAndFly {
            0% { transform: scale(0.2) translate(0, 0) rotate(0deg); opacity: 0; }
            15% { opacity: 1; transform: scale(1.2) translate(10px, -15px) rotate(45deg); }
            85% { opacity: 0.9; }
            100% { transform: scale(0.3) translate(40px, -80px) rotate(180deg); opacity: 0; }
        }
    </style>
</head>
<body>

    <div class="star-field-overlay" id="kejora-overlay"></div>

    <div class="container-mobile">
        <div class="app-header">
            <h1>SMP NEGERI 1 LINGGA</h1>
            <p>Pengumuman Kelulusan Kelas IX TP. 2025/2026</p>
        </div>

        <div id="page-home" class="tab-content">
            <div class="m3-glass">
                <h3 style="font-size:15px; margin-bottom:12px; color:#0f172a;"><i class="fa-solid fa-calculator" style="color:#1d4ed8; margin-right:8px;"></i>Rata-Rata Nilai Tiap Mapel Sekolah</h3>
                <div class="subject-avg-grid" id="global-subject-averages">
                    </div>
            </div>
        </div>

        <div id="page-nilaiku" class="tab-content">
            <div class="m3-glass search-box">
                <label for="student-search-input">Masukkan Nama Lengkap Siswa</label>
                <div class="input-wrapper">
                    <i class="fa-solid fa-user"></i>
                    <input type="text" id="student-search-input" placeholder="Contoh: RAYYA ATHIYAH..." autocomplete="off">
                </div>
                <button class="btn-search" onclick="processSearch()"><i class="fa-solid fa-envelope-open-text"></i>Buka Amplop Nilai</button>
            </div>

            <div class="loading-container" id="loading-box">
                <div class="spinner"></div>
                <span class="pulse-text">Membuka Amplop Dokumen...</span>
            </div>

            <div id="result-container">
                </div>
        </div>
    </div>

    <nav class="bottom-navbar">
        <button class="nav-item" id="nav-home" onclick="switchTab('home')">
            <i class="fa-solid fa-chart-simple"></i>
            <span>Home</span>
        </button>
        <button class="nav-item" id="nav-nilaiku" onclick="switchTab('nilaiku')">
            <i class="fa-solid fa-address-card"></i>
            <span>Nilaiku</span>
        </button>
    </nav>

    <script>
        // DATASET LENGKAP: 10 Mata Pelajaran Lengkap Sesuai Transkrip Nilai Sekolah
        const rawStudentsData = [
            { name: "ADELIA DWI NURMANSYAH", agama: 90.20, pancasila: 82.80, ind: 89.00, mtk: 89.60, ipa: 83.00, ips: 83.60, ing: 82.00, pjok: 86.60, info: 85.80, seni: 86.80 },
            { name: "ANANDA IBNU FAHREZI", agama: 76.00, pancasila: 81.40, ind: 79.60, mtk: 78.20, ipa: 75.60, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.00, seni: 77.60 },
            { name: "DAFITRA ARIANSYAH", agama: 75.60, pancasila: 80.60, ind: 76.80, mtk: 76.60, ipa: 75.60, ips: 82.20, ing: 76.80, pjok: 77.20, info: 81.80, seni: 76.60 },
            { name: "DELVRY ANGGARA PANJAITAN", agama: 81.40, pancasila: 81.80, ind: 84.00, mtk: 83.20, ipa: 79.40, ips: 83.00, ing: 79.80, pjok: 78.60, info: 84.20, seni: 80.60 },
            { name: "DYRA ALTHA FUNISYA", agama: 94.60, pancasila: 88.00, ind: 92.20, mtk: 92.20, ipa: 86.00, ips: 88.40, ing: 91.00, pjok: 85.00, info: 91.00, seni: 87.80 },
            { name: "FAQIHA TAZKIATUN NUFUS", agama: 84.80, pancasila: 84.40, ind: 80.20, mtk: 81.80, ipa: 78.80, ips: 84.00, ing: 81.40, pjok: 81.80, info: 85.60, seni: 84.80 },
            { name: "GHASTAN GAUTAMA GINARDA", agama: 87.00, pancasila: 86.40, ind: 92.60, mtk: 85.00, ipa: 84.00, ips: 86.00, ing: 87.60, pjok: 86.80, info: 88.60, seni: 83.00 },
            { name: "JEANTRIKA SAPUTERA", agama: 76.20, pancasila: 80.20, ind: 78.00, mtk: 79.00, ipa: 75.40, ips: 81.60, ing: 76.60, pjok: 77.60, info: 81.80, seni: 78.60 },
            { name: "LIYANA ZAHIRA", agama: 81.20, pancasila: 82.20, ind: 80.80, mtk: 78.00, ipa: 76.00, ips: 82.40, ing: 77.20, pjok: 79.80, info: 83.00, seni: 80.60 },
            { name: "M.BAYU RIZKITULLAH", agama: 86.60, pancasila: 82.60, ind: 82.40, mtk: 84.60, ipa: 80.40, ips: 83.40, ing: 80.00, pjok: 80.60, info: 86.40, seni: 83.00 },
            { name: "MARWA DWI RAMADANI", agama: 83.20, pancasila: 83.20, ind: 86.80, mtk: 78.80, ipa: 78.20, ips: 84.80, ing: 82.00, pjok: 79.80, info: 84.60, seni: 85.20 },
            { name: "MUHAMMAD FADHIL ARDIANSYAH", agama: 82.80, pancasila: 82.80, ind: 81.80, mtk: 83.20, ipa: 79.20, ips: 84.40, ing: 81.20, pjok: 79.80, info: 85.40, seni: 81.20 },
            { name: "MUHAMMAD GIBRAN ASSYAFAR", agama: 79.60, pancasila: 81.40, ind: 82.00, mtk: 78.00, ipa: 75.80, ips: 81.80, ing: 76.60, pjok: 77.60, info: 82.00, seni: 77.60 },
            { name: "MUHAMMAD MUFLIH HIBATULLAH", agama: 77.00, pancasila: 80.40, ind: 76.20, mtk: 77.80, ipa: 75.80, ips: 81.40, ing: 76.60, pjok: 77.40, info: 82.20, seni: 76.60 },
            { name: "NATASYA ZULHAFIFAH", agama: 85.80, pancasila: 83.80, ind: 86.40, mtk: 82.20, ipa: 80.20, ips: 85.00, ing: 81.40, pjok: 82.80, info: 85.60, seni: 84.20 },
            { name: "RAFADIL ANANTA", agama: 75.00, pancasila: 80.00, ind: 75.60, mtk: 73.00, ipa: 74.80, ips: 80.80, ing: 75.40, pjok: 77.20, info: 81.20, seni: 76.60 },
            { name: "RAJA FATHUR ABDILLAH", agama: 83.80, pancasila: 82.40, ind: 82.00, mtk: 83.80, ipa: 79.20, ips: 83.60, ing: 80.40, pjok: 81.60, info: 85.40, seni: 81.00 },
            { name: "RATI JUNILA", agama: 83.20, pancasila: 81.80, ind: 82.40, mtk: 77.00, ipa: 76.20, ips: 81.60, ing: 78.40, pjok: 79.80, info: 82.80, seni: 81.20 },
            { name: "REFAN PINANDO", agama: 77.00, pancasila: 81.00, ind: 76.20, mtk: 77.60, ipa: 75.80, ips: 81.40, ing: 76.60, pjok: 77.40, info: 81.80, seni: 76.60 },
            { name: "RINA RIYANTI", agama: 85.80, pancasila: 85.20, ind: 85.60, mtk: 86.20, ipa: 81.20, ips: 85.00, ing: 82.20, pjok: 83.80, info: 86.20, seni: 84.60 },
            { name: "RISNA ULKA ARYANI", agama: 83.40, pancasila: 82.20, ind: 77.80, mtk: 81.40, ipa: 77.40, ips: 82.60, ing: 78.80, pjok: 80.60, info: 84.40, seni: 80.80 },
            { name: "RIZKA INDRI ADELIASA", agama: 81.20, pancasila: 81.80, ind: 77.40, mtk: 82.00, ipa: 77.40, ips: 82.80, ing: 78.40, pjok: 78.60, info: 83.40, seni: 79.80 },
            { name: "SHERIL GIANDA UTAMI", agama: 79.80, pancasila: 81.20, ind: 77.20, mtk: 78.00, ipa: 75.80, ips: 81.80, ing: 77.20, pjok: 77.40, info: 82.00, seni: 78.40 },
            { name: "SILA ADELIA", agama: 78.40, pancasila: 81.20, ind: 77.80, mtk: 77.60, ipa: 76.00, ips: 81.80, ing: 77.00, pjok: 77.60, info: 82.00, seni: 78.00 },
            { name: "SUKMASARI", agama: 84.80, pancasila: 83.60, ind: 83.60, mtk: 81.40, ipa: 79.00, ips: 84.00, ing: 81.00, pjok: 82.80, info: 85.40, seni: 83.80 },
            { name: "SYARIFAH NAFIA SAFIZ", agama: 85.60, pancasila: 83.40, ind: 90.00, mtk: 80.80, ipa: 81.20, ips: 85.00, ing: 82.40, pjok: 82.80, info: 85.20, seni: 83.60 },
            { name: "VIKY ADITYA SYAPUTRA", agama: 76.80, pancasila: 80.60, ind: 76.20, mtk: 77.80, ipa: 75.60, ips: 81.40, ing: 76.60, pjok: 77.40, info: 81.80, seni: 76.60 },
            { name: "ZALFA MUFIDAH INAYAH", agama: 85.80, pancasila: 84.40, ind: 83.40, mtk: 85.20, ipa: 80.60, ips: 84.80, ing: 81.40, pjok: 81.80, info: 86.40, seni: 83.60 },
            { name: "ΖΑΤΙΑ ΜAYSYA", agama: 90.20, pancasila: 86.60, ind: 87.20, mtk: 91.60, ipa: 84.60, ips: 87.00, ing: 87.20, pjok: 85.80, info: 88.60, seni: 85.00 },
            { name: "ADONIA NAJLA RAISSA", agama: 83.00, pancasila: 82.40, ind: 82.80, mtk: 81.40, ipa: 78.40, ips: 83.20, ing: 79.60, pjok: 80.60, info: 84.40, seni: 81.80 },
            { name: "AIRIN DWI RAMADHANI", agama: 85.60, pancasila: 84.40, ind: 87.40, mtk: 83.00, ipa: 81.00, ips: 85.00, ing: 82.60, pjok: 83.80, info: 85.80, seni: 84.60 },
            { name: "AISH GHAZIYA RAFIFA", agama: 83.60, pancasila: 82.20, ind: 81.60, mtk: 80.40, ipa: 77.80, ips: 82.80, ing: 79.20, pjok: 79.80, info: 84.20, seni: 81.60 },
            { name: "ARYA IMAM RISNANDA", agama: 78.60, pancasila: 81.40, ind: 78.60, mtk: 78.20, ipa: 76.00, ips: 81.80, ing: 77.00, pjok: 77.60, info: 82.00, seni: 77.80 },
            { name: "DEBY SEPTIANI", agama: 92.40, pancasila: 87.20, ind: 88.80, mtk: 90.20, ipa: 84.80, ips: 87.00, ing: 86.20, pjok: 84.80, info: 88.40, seni: 85.80 },
            { name: "DZIKRI HARITH HAZIQ", agama: 81.20, pancasila: 82.40, ind: 80.20, mtk: 79.60, ipa: 77.20, ips: 82.40, ing: 78.20, pjok: 79.80, info: 83.40, seni: 80.60 },
            { name: "GUNAWAN FAUZI", agama: 76.60, pancasila: 80.40, ind: 76.20, mtk: 76.80, ipa: 75.40, ips: 81.40, ing: 76.40, pjok: 77.40, info: 81.60, seni: 76.60 },
            { name: "IBNU SHALIM", agama: 79.80, pancasila: 81.40, ind: 76.80, mtk: 81.40, ipa: 77.40, ips: 82.60, ing: 78.60, pjok: 78.60, info: 83.60, seni: 79.80 },
            { name: "IMAM SYAHIBBULLAH", agama: 77.80, pancasila: 80.80, ind: 77.20, mtk: 76.20, ipa: 75.80, ips: 81.40, ing: 76.60, pjok: 77.40, info: 81.80, seni: 77.20 },
            { name: "IRVAN KURNIA", agama: 79.20, pancasila: 81.20, ind: 79.80, mtk: 77.80, ipa: 76.00, ips: 82.00, ing: 77.40, pjok: 77.60, info: 82.20, seni: 78.40 },
            { name: "ISNAINI", agama: 81.40, pancasila: 81.80, ind: 76.80, mtk: 80.60, ipa: 77.20, ips: 82.60, ing: 78.20, pjok: 78.60, info: 83.40, seni: 79.60 },
            { name: "KAFHA AZRI ILHAMSYAH", agama: 76.60, pancasila: 80.40, ind: 76.60, mtk: 76.00, ipa: 75.40, ips: 81.40, ing: 76.40, pjok: 77.40, info: 81.60, seni: 76.60 },
            { name: "KHASBI NOVALDI", agama: 75.40, pancasila: 80.20, ind: 76.80, mtk: 74.20, ipa: 74.80, ips: 81.20, ing: 76.00, pjok: 77.20, info: 81.20, seni: 76.60 },
            { name: "LIPIANA SUCI RAMARANI", agama: 89.20, pancasila: 85.00, ind: 87.80, mtk: 87.60, ipa: 82.40, ips: 85.80, ing: 84.40, pjok: 84.80, info: 87.20, seni: 85.00 },
            { name: "MECA ADELYA CAHYANI", agama: 88.40, pancasila: 85.40, ind: 93.00, mtk: 85.80, ipa: 84.00, ips: 86.40, ing: 87.60, pjok: 85.00, info: 88.80, seni: 84.00 },
            { name: "MEISYA AWALUN NURHASANAH", agama: 78.20, pancasila: 81.20, ind: 77.40, mtk: 77.40, ipa: 75.80, ips: 81.80, ing: 76.80, pjok: 77.40, info: 82.00, seni: 77.60 },
            { name: "MUHAMMAD ERWAN ZARKA", agama: 79.60, pancasila: 81.40, ind: 79.60, mtk: 78.00, ipa: 75.80, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.00, seni: 77.60 },
            { name: "NUR RAFNI YASMADI", agama: 78.40, pancasila: 81.20, ind: 77.80, mtk: 77.60, ipa: 76.00, ips: 81.80, ing: 77.00, pjok: 77.60, info: 82.00, seni: 78.00 },
            { name: "QIAN FERDINAND", agama: 81.20, pancasila: 81.80, ind: 77.40, mtk: 80.20, ipa: 77.20, ips: 82.60, ing: 78.20, pjok: 78.60, info: 83.20, seni: 79.60 },
            { name: "RAISA IDADI", agama: 84.40, pancasila: 83.00, ind: 85.20, mtk: 78.80, ipa: 78.00, ips: 83.60, ing: 80.40, pjok: 80.60, info: 84.40, seni: 83.20 },
            { name: "RISKA SARI", agama: 78.40, pancasila: 81.20, ind: 78.00, mtk: 78.00, ipa: 75.80, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.00, seni: 78.00 },
            { name: "SABRINA EMBUN PERTIWI", agama: 78.60, pancasila: 81.40, ind: 78.60, mtk: 77.60, ipa: 75.80, ips: 81.80, ing: 77.00, pjok: 77.60, info: 82.00, seni: 77.80 },
            { name: "SAPINAH", agama: 83.60, pancasila: 82.40, ind: 81.40, mtk: 78.80, ipa: 77.20, ips: 82.60, ing: 78.80, pjok: 79.80, info: 83.60, seni: 81.60 },
            { name: "SHAZIA ZARA ALISHA", agama: 83.20, pancasila: 82.80, ind: 83.00, mtk: 79.40, ipa: 77.80, ips: 83.40, ing: 79.60, pjok: 80.60, info: 84.00, seni: 82.20 },
            { name: "SUHARAYAH", agama: 82.40, pancasila: 82.20, ind: 79.60, mtk: 85.00, ipa: 78.80, ips: 83.60, ing: 80.60, pjok: 81.80, info: 85.60, seni: 81.40 },
            { name: "SYARIFAH NAJWA SAFIZ", agama: 84.80, pancasila: 83.00, ind: 86.20, mtk: 79.00, ipa: 78.20, ips: 84.20, ing: 81.20, pjok: 80.60, info: 84.40, seni: 83.80 },
            { name: "SYARIFAH ZILFA NATASYA", agama: 83.60, pancasila: 82.80, ind: 84.00, mtk: 80.40, ipa: 78.40, ips: 83.80, ing: 80.40, pjok: 80.60, info: 84.40, seni: 82.60 },
            { name: "SYIFA SYAQIRAH", agama: 81.40, pancasila: 82.00, ind: 81.20, mtk: 78.40, ipa: 76.60, ips: 82.40, ing: 77.80, pjok: 78.60, info: 83.00, seni: 80.60 },
            { name: "VANDERSAR MEICHAEL NAINGGOLAN", agama: 78.40, pancasila: 81.20, ind: 78.00, mtk: 77.80, ipa: 75.80, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.00, seni: 78.00 },
            { name: "ZAI ISRAKMIDIAH", agama: 81.20, pancasila: 81.80, ind: 80.00, mtk: 79.40, ipa: 76.80, ips: 82.40, ing: 77.80, pjok: 78.60, info: 83.00, seni: 80.20 },
            { name: "ACHAI ANDREAS", agama: 81.00, pancasila: 81.80, ind: 80.40, mtk: 77.80, ipa: 76.60, ips: 82.40, ing: 77.80, pjok: 78.60, info: 83.00, seni: 80.40 },
            { name: "ANGGARA PRATAMA", agama: 76.80, pancasila: 80.60, ind: 76.20, mtk: 77.40, ipa: 75.60, ips: 81.40, ing: 76.60, pjok: 77.40, info: 81.80, seni: 76.60 },
            { name: "ANUGRAH AGUSTI RAMADHANI", agama: 83.80, pancasila: 82.60, ind: 82.60, mtk: 83.20, ipa: 79.40, ips: 83.80, ing: 80.60, pjok: 81.60, info: 85.40, seni: 81.40 },
            { name: "ARFA", agama: 76.80, pancasila: 80.60, ind: 76.20, mtk: 76.40, ipa: 75.40, ips: 81.40, ing: 76.40, pjok: 77.40, info: 81.60, seni: 76.60 },
            { name: "DZAKIYYA NAILA SAKHI", agama: 89.20, pancasila: 85.40, ind: 88.80, mtk: 86.40, ipa: 82.40, ips: 86.20, ing: 84.80, pjok: 84.80, info: 87.20, seni: 85.60 },
            { name: "ERINA NAZIRA", agama: 81.20, pancasila: 81.80, ind: 78.60, mtk: 80.00, ipa: 77.20, ips: 82.60, ing: 78.20, pjok: 78.60, info: 83.40, seni: 79.80 },
            { name: "FAIZ FAYZUL HAQ", agama: 79.40, pancasila: 81.40, ind: 78.40, mtk: 78.00, ipa: 76.00, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.20, seni: 78.40 },
            { name: "HANY BAZLINDA", agama: 90.60, pancasila: 86.00, ind: 90.00, mtk: 88.40, ipa: 83.80, ips: 87.00, ing: 86.40, pjok: 85.80, info: 88.40, seni: 85.60 },
            { name: "HERISUSANTI", agama: 92.40, pancasila: 87.20, ind: 92.20, mtk: 88.80, ipa: 84.60, ips: 87.40, ing: 87.40, pjok: 85.80, info: 88.60, seni: 86.20 },
            { name: "HESTY YOLANDA SIRABANG", agama: 79.20, pancasila: 81.20, ind: 78.00, mtk: 73.40, ipa: 75.00, ips: 81.20, ing: 76.20, pjok: 77.20, info: 81.40, seni: 77.40 },
            { name: "MAHARANI DEWI", agama: 89.20, pancasila: 85.20, ind: 89.80, mtk: 86.60, ipa: 82.60, ips: 86.40, ing: 85.20, pjok: 84.80, info: 87.20, seni: 85.80 },
            { name: "MEGAWATI", agama: 81.20, pancasila: 81.80, ind: 78.60, mtk: 79.80, ipa: 77.20, ips: 82.60, ing: 78.20, pjok: 78.60, info: 83.40, seni: 79.80 },
            { name: "MULHUDA", agama: 79.60, pancasila: 81.40, ind: 78.60, mtk: 79.00, ipa: 76.40, ips: 82.00, ing: 77.60, pjok: 77.60, info: 82.20, seni: 78.40 },
            { name: "NAZILA MAHARANI", agama: 82.80, pancasila: 82.40, ind: 81.60, mtk: 78.60, ipa: 77.20, ips: 82.60, ing: 78.80, pjok: 79.80, info: 83.20, seni: 81.20 },
            { name: "NAZRIEL ALFARIZQY YUNIAR", agama: 92.40, pancasila: 86.80, ind: 93.20, mtk: 88.40, ipa: 84.60, ips: 87.20, ing: 87.40, pjok: 85.80, info: 88.60, seni: 86.00 },
            { name: "NI'A ROSA", agama: 79.80, pancasila: 81.40, ind: 78.80, mtk: 78.00, ipa: 75.80, ips: 81.80, ing: 77.20, pjok: 77.60, info: 82.00, seni: 78.00 },
            { name: "NOVITA ADHA RIAH", agama: 81.60, pancasila: 82.00, ind: 80.40, mtk: 79.80, ipa: 77.20, ips: 82.60, ing: 78.60, pjok: 79.80, info: 83.40, seni: 80.80 },
            { name: "NOVRIAN SAPUTRA", agama: 81.20, pancasila: 81.80, ind: 77.40, mtk: 80.20, ipa: 77.20, ips: 82.60, ing: 78.20, pjok: 78.60, info: 83.20, seni: 79.60 },
            { name: "RAHMANDA PRATAMA", agama: 76.80, pancasila: 80.60, ind: 76.20, mtk: 76.40, ipa: 75.40, ips: 81.40, ing: 76.40, pjok: 77.40, info: 81.60, seni: 76.60 },
            { name: "RISKY ARDIAN MISKA SACHPUTRA", agama: 76.40, pancasila: 80.40, ind: 76.80, mtk: 75.80, ipa: 75.20, ips: 81.40, ing: 76.40, pjok: 77.40, info: 81.60, seni: 76.60 },
            { name: "RIZKA ALFIA AZ ZAHRA", agama: 90.60, pancasila: 86.00, ind: 90.60, mtk: 86.00, ipa: 82.80, ips: 86.40, ing: 84.80, pjok: 84.80, info: 87.20, seni: 85.60 },
            { name: "SAHRINI RAMADANI", agama: 77.40, pancasila: 80.60, ind: 76.80, mtk: 76.80, ipa: 75.60, ips: 81.40, ing: 76.60, pjok: 77.40, info: 81.80, seni: 76.80 },
            { name: "SILVIA FRANSISKA NATALIA", agama: 79.40, pancasila: 81.20, ind: 77.40, mtk: 78.80, ipa: 76.20, ips: 82.00, ing: 77.40, pjok: 77.60, info: 82.20, seni: 78.20 },
            { name: "SUCI SAFIRA PUTRI", agama: 84.40, pancasila: 82.60, ind: 80.80, mtk: 87.00, ipa: 79.20, ips: 83.60, ing: 80.40, pjok: 81.60, info: 85.40, seni: 81.00 },
            { name: "SYARIFAH IZZATI AQILA", agama: 82.40, pancasila: 81.80, ind: 78.00, mtk: 86.40, ipa: 78.40, ips: 83.20, ing: 79.40, pjok: 80.60, info: 84.40, seni: 80.80 },
            { name: "USMAN", agama: 76.20, pancasila: 80.40, ind: 76.20, mtk: 75.60, ipa: 75.00, ips: 81.20, ing: 76.00, pjok: 77.20, info: 81.20, seni: 76.60 },
            { name: "WINDA AULIA", agama: 77.80, pancasila: 81.00, ind: 78.00, mtk: 77.20, ipa: 75.80, ips: 81.60, ing: 76.80, pjok: 77.40, info: 81.80, seni: 77.40 },
            { name: "ZIFARA OKTIA GISKA", agama: 83.80, pancasila: 82.40, ind: 80.40, mtk: 83.80, ipa: 79.20, ips: 83.60, ing: 80.40, pjok: 81.60, info: 85.40, seni: 81.00 },
            { name: "ZURRIATI FARHANA", agama: 82.40, pancasila: 82.20, ind: 81.00, mtk: 79.60, ipa: 77.20, ips: 82.60, ing: 78.60, pjok: 79.80, info: 83.40, seni: 81.00 }
        ];

        let processedStudents = [];
        let mapelGlobalAverages = {};

        function initData() {
            let keys = ["agama", "pancasila", "ind", "mtk", "ipa", "ips", "ing", "pjok", "info", "seni"];
            let totals = { agama: 0, pancasila: 0, ind: 0, mtk: 0, ipa: 0, ips: 0, ing: 0, pjok: 0, info: 0, seni: 0 };
            let totalSiswa = rawStudentsData.length;

            let calculated = rawStudentsData.map(s => {
                let sum = 0;
                keys.forEach(k => {
                    let val = s[k] || 75.00; 
                    sum += val;
                    totals[k] += val;
                });
                let finalAvg = sum / keys.length;

                return {
                    name: s.name.toUpperCase().trim(),
                    combinedAvg: finalAvg
                };
            });

            // Urutkan Rapor Berdasarkan Nilai Rata-rata Kombinasi
            calculated.sort((a, b) => b.combinedAvg - a.combinedAvg);
            processedStudents = calculated.map((item, idx) => {
                item.rank = idx + 1;
                return item;
            });

            // Hitung Rata-rata Mapel Global Sekolah
            keys.forEach(k => {
                mapelGlobalAverages[k] = (totals[k] / totalSiswa).toFixed(2);
            });

            renderHomeAverages();
        }

        function renderHomeAverages() {
            const container = document.getElementById('global-subject-averages');
            const mapelLabels = {
                agama: "Pendidikan Agama",
                pancasila: "Pendidikan Pancasila",
                ind: "Bahasa Indonesia",
                mtk: "Matematika",
                ipa: "Ilmu Pengetahuan Alam (IPA)",
                ips: "Ilmu Pengetahuan Sosial (IPS)",
                ing: "Bahasa Inggris",
                pjok: "PJOK",
                info: "Informatika",
                seni: "Seni Budaya & Prakarya"
            };

            container.innerHTML = Object.keys(mapelLabels).map(key => `
                <div class="subject-avg-card">
                    <span>${mapelLabels[key]}</span>
                    <strong>${mapelGlobalAverages[key]}</strong>
                </div>
            `).join('');
        }

        function getPredikatText(score) {
            if(score >= 85) return "BAIK";
            if(score >= 70) return "MEMADAI";
            return "KURANG";
        }

        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));

            if(tabName === 'home') {
                document.getElementById('page-home').classList.add('active');
                document.getElementById('nav-home').classList.add('active');
            } else {
                document.getElementById('page-nilaiku').classList.add('active');
                document.getElementById('nav-nilaiku').classList.add('active');
            }
        }

        function triggerKejoraEffect() {
            const overlay = document.getElementById('kejora-overlay');
            overlay.innerHTML = ""; 
            overlay.style.display = "block";

            for (let i = 0; i < 35; i++) {
                const star = document.createElement('i');
                star.className = "fa-solid fa-star kejora-star";
                star.style.left = `${Math.random() * 100}vw`;
                star.style.top = `${Math.random() * 100}vh`;
                star.style.fontSize = `${Math.random() * 14 + 8}px`;
                star.style.animationDelay = `${Math.random() * 0.8}s`;
                overlay.appendChild(star);
            }

            setTimeout(() => { overlay.style.display = "none"; }, 3500);
        }

        function processSearch() {
            const inputVal = document.getElementById('student-search-input').value.toUpperCase().trim();
            const resultContainer = document.getElementById('result-container');
            const loadingBox = document.getElementById('loading-box');

            if (inputVal === "") {
                alert("Harap masukkan nama lengkap siswa untuk melakukan pencarian.");
                return;
            }

            resultContainer.style.display = "none";
            loadingBox.style.display = "flex";

            setTimeout(() => {
                loadingBox.style.display = "none";
                const matchStudent = processedStudents.find(s => s.name === inputVal);

                if(!matchStudent) {
                    resultContainer.innerHTML = `
                        <div class="m3-glass bounce-effect" style="text-align:center; padding: 30px 20px;">
                            <i class="fa-solid fa-user-slash" style="font-size:32px; color:#f43f5e; margin-bottom:12px;"></i>
                            <h3 style="font-size:15px; color:#334155;">Nama Siswa Tidak Ditemukan</h3>
                            <p style="font-size:12px; color:#64748b; margin-top:4px;">Pastikan penulisan nama lengkap sudah benar sesuai data sekolah.</p>
                        </div>
                    `;
                } else {
                    triggerKejoraEffect();

                    let cardClass = 'card-rank-normal';
                    let badgeClass = 'badge-normal';
                    let badgeIcon = '<i class="fa-solid fa-hashtag"></i>';
                    let badgeText = `Rank ${matchStudent.rank}`;

                    if(matchStudent.rank === 1) { cardClass = 'card-rank-1'; badgeClass = 'badge-1'; badgeIcon = '<i class="fa-solid fa-trophy"></i>'; badgeText = 'Juara 1'; }
                    else if(matchStudent.rank === 2) { cardClass = 'card-rank-2'; badgeClass = 'badge-2'; badgeIcon = '<i class="fa-solid fa-medal"></i>'; badgeText = 'Juara 2'; }
                    else if(matchStudent.rank === 3) { cardClass = 'card-rank-3'; badgeClass = 'badge-3'; badgeIcon = '<i class="fa-solid fa-medal"></i>'; badgeText = 'Juara 3'; }

                    let formattedScore = matchStudent.combinedAvg.toFixed(2);
                    let predikatLabel = getPredikatText(matchStudent.combinedAvg);

                    resultContainer.innerHTML = `
                        <div class="m3-glass result-card ${cardClass} bounce-effect">
                            <div class="student-profile">
                                <div class="profile-info">
                                    <h2>${matchStudent.name}</h2>
                                    <p>Siswa SMP Negeri 1 Lingga</p>
                                </div>
                                <div class="rank-badge ${badgeClass}">
                                    ${badgeIcon}<span>${badgeText}</span>
                                </div>
                            </div>
                            
                            <div class="congrats-banner">
                                <div class="congrats-text">
                                    <i class="fa-solid fa-graduation-cap"></i>
                                    <span>selamat, lulus dengan rata rata nilai</span>
                                </div>
                                <div class="score-display-large">${formattedScore}</div>
                                <div class="predikat-subtext">PREDIKAT: ${predikatLabel}</div>
                            </div>

                            <div class="skl-announcement">
                                <div class="skl-block">
                                    <div class="skl-title">
                                        <i class="fa-solid fa-circle-info"></i>
                                        <span>INFORMASI PENGAMBILAN SKL & RAPOR</span>
                                    </div>
                                    <ul class="skl-details">
                                        <li><i class="fa-solid fa-calendar-day"></i><span><strong>Hari / Tanggal:</strong> Sabtu, 6 Juni 2026</span></li>
                                        <li><i class="fa-solid fa-clock"></i><span><strong>Waktu:</strong> Jam 09.00 WIB</span></li>
                                        <li><i class="fa-solid fa-location-dot"></i><span><strong>Tempat/Seragam:</strong> TU SMP Negeri 1 Lingga/Baju Seragam Putih Biru Menggunakan Sepatu Sekolah Hitam</span></li>
                                    </ul>
                                </div>

                                <div class="skl-block">
                                    <div class="skl-title" style="color: #1e3a8a; border-color: rgba(59, 130, 246, 0.2);">
                                        <i class="fa-solid fa-laptop-code" style="color: #2563eb;"></i>
                                        <span style="color: #1d4ed8;">SIMULASI PENDAFTARAN SPMB SMA/SMK</span>
                                    </div>
                                    <ul class="skl-details" style="color: #2563eb;">
                                        <li><i class="fa-solid fa-calendar-day"></i><span><strong>Tanggal:</strong> 2 s/d 3 Juni 2026</span></li>
                                        <li><i class="fa-solid fa-clock"></i><span><strong>Website SPMB:</strong> sispmb.kepriprov.go.id</span></li>
                                        <li><i class="fa-solid fa-globe"></i><span><strong>Metode:</strong> Daring (Online)</span></li>
                                        <li><i class="fa-brands fa-whatsapp" style="color: #25d366; font-size: 12px;"></i><span><em>Info selanjutnya silahkan hubungi Panitia SPMB SMA/SMK</em></span></li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    `;
                }
                resultContainer.style.display = "block";
            }, 1200);
        }

        window.onload = function() {
            initData();
            switchTab('nilaiku');
        };
    </script>
</body>
</html>
