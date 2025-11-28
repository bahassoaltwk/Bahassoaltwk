<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tryout CPNS Online</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --light-color: #ecf0f1;
            --success-color: #27ae60;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f8f9fa;
            color: #333;
        }
        
        .navbar-brand {
            font-weight: bold;
            color: var(--primary-color) !important;
        }
        
        .btn-primary {
            background-color: var(--secondary-color);
            border-color: var(--secondary-color);
        }
        
        .btn-primary:hover {
            background-color: #2980b9;
            border-color: #2980b9;
        }
        
        .card {
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            border: none;
            margin-bottom: 20px;
        }
        
        .card-header {
            background-color: var(--primary-color);
            color: white;
            border-radius: 10px 10px 0 0 !important;
            font-weight: bold;
        }
        
        .login-container {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
        }
        
        .login-card {
            width: 100%;
            max-width: 400px;
            padding: 30px;
            border-radius: 15px;
        }
        
        .timer {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent-color);
        }
        
        .question-number {
            display: inline-block;
            width: 35px;
            height: 35px;
            line-height: 35px;
            text-align: center;
            border-radius: 50%;
            background-color: var(--light-color);
            margin: 5px;
            cursor: pointer;
        }
        
        .question-number.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .question-number.answered {
            background-color: var(--success-color);
            color: white;
        }
        
        .question-number.flagged {
            background-color: var(--accent-color);
            color: white;
        }
        
        .result-card {
            text-align: center;
            padding: 30px;
        }
        
        .score-display {
            font-size: 3rem;
            font-weight: bold;
            color: var(--secondary-color);
        }
        
        .progress-bar-custom {
            height: 10px;
            border-radius: 5px;
        }
        
        .section-title {
            border-left: 5px solid var(--secondary-color);
            padding-left: 15px;
            margin: 20px 0;
        }
        
        footer {
            background-color: var(--primary-color);
            color: white;
            padding: 20px 0;
            margin-top: 30px;
        }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <!-- Halaman Login -->
    <div id="login-page" class="login-container">
        <div class="card login-card">
            <div class="card-body">
                <h2 class="text-center mb-4">Login Tryout CPNS</h2>
                <form id="login-form">
                    <div class="mb-3">
                        <label for="email" class="form-label">Email</label>
                        <input type="email" class="form-control" id="email" placeholder="Masukkan email" required>
                    </div>
                    <div class="mb-3">
                        <label for="password" class="form-label">Password</label>
                        <input type="password" class="form-control" id="password" placeholder="Masukkan password" required>
                    </div>
                    <div class="mb-3 form-check">
                        <input type="checkbox" class="form-check-input" id="remember">
                        <label class="form-check-label" for="remember">Ingat saya</label>
                    </div>
                    <button type="submit" class="btn btn-primary w-100">Login</button>
                </form>
                <div class="text-center mt-3">
                    <a href="#" class="text-decoration-none">Lupa password?</a>
                </div>
                <div class="text-center mt-3">
                    <p>Belum punya akun? <a href="#" class="text-decoration-none">Daftar di sini</a></p>
                </div>
            </div>
        </div>
    </div>

    <!-- Halaman Dashboard (Setelah Login) -->
    <div id="dashboard-page" class="hidden">
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container">
                <a class="navbar-brand" href="#"><i class="fas fa-graduation-cap me-2"></i>TRYOUT CPNS</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNav">
                    <ul class="navbar-nav ms-auto">
                        <li class="nav-item">
                            <a class="nav-link active" href="#"><i class="fas fa-home me-1"></i> Dashboard</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#"><i class="fas fa-history me-1"></i> Riwayat Tryout</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#"><i class="fas fa-user me-1"></i> Profil</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link" href="#" id="logout-btn"><i class="fas fa-sign-out-alt me-1"></i> Logout</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>

        <div class="container mt-4">
            <div class="row">
                <div class="col-md-8">
                    <div class="card">
                        <div class="card-header">
                            <h4 class="mb-0">Tryout Tersedia</h4>
                        </div>
                        <div class="card-body">
                            <div class="row">
                                <div class="col-md-6 mb-3">
                                    <div class="card h-100">
                                        <div class="card-body">
                                            <h5 class="card-title">Tryout SKD Paket 1</h5>
                                            <p class="card-text">Tes Kompetensi Dasar dengan 110 soal dalam waktu 120 menit.</p>
                                            <p><i class="fas fa-clock me-2"></i>120 menit</p>
                                            <p><i class="fas fa-question-circle me-2"></i>110 soal</p>
                                            <button class="btn btn-primary mt-2 start-exam" data-exam="1">Mulai Tryout</button>
                                        </div>
                                    </div>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <div class="card h-100">
                                        <div class="card-body">
                                            <h5 class="card-title">Tryout SKD Paket 2</h5>
                                            <p class="card-text">Tes Kompetensi Dasar dengan 110 soal dalam waktu 120 menit.</p>
                                            <p><i class="fas fa-clock me-2"></i>120 menit</p>
                                            <p><i class="fas fa-question-circle me-2"></i>110 soal</p>
                                            <button class="btn btn-primary mt-2 start-exam" data-exam="2">Mulai Tryout</button>
                                        </div>
                                    </div>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <div class="card h-100">
                                        <div class="card-body">
                                            <h5 class="card-title">Tryout TKB Hukum</h5>
                                            <p class="card-text">Tes Kompetensi Bidang untuk formasi Hukum.</p>
                                            <p><i class="fas fa-clock me-2"></i>90 menit</p>
                                            <p><i class="fas fa-question-circle me-2"></i>70 soal</p>
                                            <button class="btn btn-primary mt-2 start-exam" data-exam="3">Mulai Tryout</button>
                                        </div>
                                    </div>
                                </div>
                                <div class="col-md-6 mb-3">
                                    <div class="card h-100">
                                        <div class="card-body">
                                            <h5 class="card-title">Tryout TKB Ekonomi</h5>
                                            <p class="card-text">Tes Kompetensi Bidang untuk formasi Ekonomi.</p>
                                            <p><i class="fas fa-clock me-2"></i>90 menit</p>
                                            <p><i class="fas fa-question-circle me-2"></i>70 soal</p>
                                            <button class="btn btn-primary mt-2 start-exam" data-exam="4">Mulai Tryout</button>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="col-md-4">
                    <div class="card">
                        <div class="card-header">
                            <h4 class="mb-0">Profil Pengguna</h4>
                        </div>
                        <div class="card-body text-center">
                            <img src="https://via.placeholder.com/100" class="rounded-circle mb-3" alt="Profil">
                            <h5>Nama Pengguna</h5>
                            <p class="text-muted">user@example.com</p>
                            <div class="d-grid gap-2">
                                <button class="btn btn-outline-primary">Edit Profil</button>
                            </div>
                        </div>
                    </div>
                    
                    <div class="card mt-4">
                        <div class="card-header">
                            <h4 class="mb-0">Statistik Tryout</h4>
                        </div>
                        <div class="card-body">
                            <div class="mb-3">
                                <p>Tryout Diselesaikan <span class="float-end">5</span></p>
                                <div class="progress progress-bar-custom">
                                    <div class="progress-bar bg-success" style="width: 50%"></div>
                                </div>
                            </div>
                            <div class="mb-3">
                                <p>Rata-rata Nilai <span class="float-end">75.5</span></p>
                                <div class="progress progress-bar-custom">
                                    <div class="progress-bar bg-info" style="width: 75.5%"></div>
                                </div>
                            </div>
                            <div class="mb-3">
                                <p>Peringkat <span class="float-end">42</span></p>
                                <div class="progress progress-bar-custom">
                                    <div class="progress-bar bg-warning" style="width: 42%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Halaman Ujian -->
    <div id="exam-page" class="hidden">
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container">
                <a class="navbar-brand" href="#"><i class="fas fa-graduation-cap me-2"></i>TRYOUT CPNS</a>
                <div class="navbar-text ms-auto timer" id="exam-timer">120:00</div>
            </div>
        </nav>

        <div class="container mt-4">
            <div class="row">
                <div class="col-md-9">
                    <div class="card">
                        <div class="card-header d-flex justify-content-between align-items-center">
                            <h4 class="mb-0" id="exam-title">Tryout SKD Paket 1</h4>
                            <div>
                                <button class="btn btn-sm btn-outline-light" id="flag-question">
                                    <i class="far fa-flag"></i> Tandai
                                </button>
                            </div>
                        </div>
                        <div class="card-body">
                            <div class="mb-4">
                                <h5 class="section-title">TWK - Tes Wawasan Kebangsaan</h5>
                                <div id="question-numbers-twk" class="mb-3">
                                    <!-- Nomor soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                            
                            <div class="mb-4">
                                <h5 class="section-title">TIU - Tes Intelegensi Umum</h5>
                                <div id="question-numbers-tiu" class="mb-3">
                                    <!-- Nomor soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                            
                            <div class="mb-4">
                                <h5 class="section-title">TKP - Tes Karakteristik Pribadi</h5>
                                <div id="question-numbers-tkp" class="mb-3">
                                    <!-- Nomor soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="card mt-4">
                        <div class="card-header">
                            <h4 class="mb-0">Soal <span id="current-question-number">1</span></h4>
                        </div>
                        <div class="card-body">
                            <div id="question-text">
                                <p>Berikut ini yang bukan merupakan nilai-nilai yang terkandung dalam Pancasila adalah...</p>
                            </div>
                            
                            <div id="question-options" class="mt-4">
                                <div class="form-check mb-2">
                                    <input class="form-check-input" type="radio" name="answer" id="option1" value="A">
                                    <label class="form-check-label" for="option1">
                                        Ketuhanan Yang Maha Esa
                                    </label>
                                </div>
                                <div class="form-check mb-2">
                                    <input class="form-check-input" type="radio" name="answer" id="option2" value="B">
                                    <label class="form-check-label" for="option2">
                                        Kemanusiaan yang adil dan beradab
                                    </label>
                                </div>
                                <div class="form-check mb-2">
                                    <input class="form-check-input" type="radio" name="answer" id="option3" value="C">
                                    <label class="form-check-label" for="option3">
                                        Individualisme yang kompetitif
                                    </label>
                                </div>
                                <div class="form-check mb-2">
                                    <input class="form-check-input" type="radio" name="answer" id="option4" value="D">
                                    <label class="form-check-label" for="option4">
                                        Persatuan Indonesia
                                    </label>
                                </div>
                                <div class="form-check mb-2">
                                    <input class="form-check-input" type="radio" name="answer" id="option5" value="E">
                                    <label class="form-check-label" for="option5">
                                        Keadilan sosial bagi seluruh rakyat Indonesia
                                    </label>
                                </div>
                            </div>
                            
                            <div class="d-flex justify-content-between mt-4">
                                <button class="btn btn-secondary" id="prev-question">
                                    <i class="fas fa-arrow-left me-1"></i> Soal Sebelumnya
                                </button>
                                <button class="btn btn-primary" id="next-question">
                                    Soal Berikutnya <i class="fas fa-arrow-right ms-1"></i>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="col-md-3">
                    <div class="card">
                        <div class="card-header">
                            <h4 class="mb-0">Navigasi Soal</h4>
                        </div>
                        <div class="card-body">
                            <div class="mb-3">
                                <small class="text-muted">TWK (30 soal)</small>
                                <div id="navigation-twk" class="d-flex flex-wrap mt-1">
                                    <!-- Navigasi soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                            
                            <div class="mb-3">
                                <small class="text-muted">TIU (35 soal)</small>
                                <div id="navigation-tiu" class="d-flex flex-wrap mt-1">
                                    <!-- Navigasi soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                            
                            <div class="mb-3">
                                <small class="text-muted">TKP (45 soal)</small>
                                <div id="navigation-tkp" class="d-flex flex-wrap mt-1">
                                    <!-- Navigasi soal akan diisi oleh JavaScript -->
                                </div>
                            </div>
                            
                            <div class="d-grid gap-2 mt-4">
                                <button class="btn btn-success" id="finish-exam">Selesaikan Tryout</button>
                            </div>
                        </div>
                    </div>
                    
                    <div class="card mt-4">
                        <div class="card-header">
                            <h4 class="mb-0">Status Soal</h4>
                        </div>
                        <div class="card-body">
                            <div class="d-flex align-items-center mb-2">
                                <div class="question-number me-2" style="background-color: #e9ecef;"></div>
                                <small>Belum dijawab</small>
                            </div>
                            <div class="d-flex align-items-center mb-2">
                                <div class="question-number me-2 answered"></div>
                                <small>Sudah dijawab</small>
                            </div>
                            <div class="d-flex align-items-center mb-2">
                                <div class="question-number me-2 flagged"></div>
                                <small>Ditandai</small>
                            </div>
                            <div class="d-flex align-items-center">
                                <div class="question-number me-2 active"></div>
                                <small>Sedang dikerjakan</small>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Halaman Hasil -->
    <div id="result-page" class="hidden">
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
            <div class="container">
                <a class="navbar-brand" href="#"><i class="fas fa-graduation-cap me-2"></i>TRYOUT CPNS</a>
                <div class="navbar-nav ms-auto">
                    <a class="nav-link" href="#" id="back-to-dashboard"><i class="fas fa-arrow-left me-1"></i> Kembali ke Dashboard</a>
                </div>
            </div>
        </nav>

        <div class="container mt-4">
            <div class="card result-card">
                <div class="card-body">
                    <h2 class="card-title">Hasil Tryout SKD Paket 1</h2>
                    <div class="score-display my-4">425</div>
                    <p class="lead">Selamat! Nilai Anda memenuhi passing grade CPNS.</p>
                    
                    <div class="row mt-5">
                        <div class="col-md-4 mb-4">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">TWK</h5>
                                    <div class="score-display" style="font-size: 2rem;">145</div>
                                    <p>Nilai Minimum: 65</p>
                                    <div class="progress progress-bar-custom mb-2">
                                        <div class="progress-bar bg-success" style="width: 90%"></div>
                                    </div>
                                    <p>25/30 soal benar</p>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-4 mb-4">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">TIU</h5>
                                    <div class="score-display" style="font-size: 2rem;">150</div>
                                    <p>Nilai Minimum: 80</p>
                                    <div class="progress progress-bar-custom mb-2">
                                        <div class="progress-bar bg-info" style="width: 85%"></div>
                                    </div>
                                    <p>28/35 soal benar</p>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-4 mb-4">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">TKP</h5>
                                    <div class="score-display" style="font-size: 2rem;">130</div>
                                    <p>Nilai Minimum: 126</p>
                                    <div class="progress progress-bar-custom mb-2">
                                        <div class="progress-bar bg-warning" style="width: 95%"></div>
                                    </div>
                                    <p>40/45 soal benar</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="row mt-4">
                        <div class="col-md-6">
                            <div class="card">
                                <div class="card-header">
                                    <h5 class="mb-0">Statistik Tryout</h5>
                                </div>
                                <div class="card-body">
                                    <p>Waktu Pengerjaan: <strong>110 menit 25 detik</strong></p>
                                    <p>Soal Dijawab: <strong>93 dari 110 soal</strong></p>
                                    <p>Soal Ditandai: <strong>7 soal</strong></p>
                                    <p>Rata-rata Waktu Per Soal: <strong>1 menit 11 detik</strong></p>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="card">
                                <div class="card-header">
                                    <h5 class="mb-0">Rekomendasi</h5>
                                </div>
                                <div class="card-body">
                                    <p>Anda memiliki performa yang baik pada semua bagian tes. Fokuskan latihan pada:</p>
                                    <ul>
                                        <li>TIU - Penalaran Analitis</li>
                                        <li>TKP - Pelayanan Publik</li>
                                    </ul>
                                    <button class="btn btn-primary mt-2">Lihat Pembahasan Soal</button>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-4">
                        <button class="btn btn-success me-2">Coba Tryout Lain</button>
                        <button class="btn btn-outline-primary">Unduh Sertifikat</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <footer class="text-center">
        <div class="container">
            <p>&copy; 2023 Tryout CPNS Online. All rights reserved.</p>
            <p>Disclaimer: Website ini hanya simulasi untuk keperluan demonstrasi.</p>
        </div>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Data simulasi untuk tryout
        const examData = {
            title: "Tryout SKD Paket 1",
            duration: 120, // dalam menit
            questions: {
                twk: 30,
                tiu: 35,
                tkp: 45
            }
        };

        // Inisialisasi state aplikasi
        let currentPage = 'login';
        let currentQuestion = 1;
        let userAnswers = {};
        let flaggedQuestions = new Set();
        let examTimer;
        let timeRemaining = examData.duration * 60; // dalam detik

        // Fungsi untuk berpindah halaman
        function showPage(pageId) {
            document.getElementById('login-page').classList.add('hidden');
            document.getElementById('dashboard-page').classList.add('hidden');
            document.getElementById('exam-page').classList.add('hidden');
            document.getElementById('result-page').classList.add('hidden');
            
            document.getElementById(pageId).classList.remove('hidden');
            currentPage = pageId;
            
            if (pageId === 'exam-page') {
                initializeExam();
                startTimer();
            }
        }

        // Fungsi untuk inisialisasi ujian
        function initializeExam() {
            // Reset state
            currentQuestion = 1;
            userAnswers = {};
            flaggedQuestions = new Set();
            timeRemaining = examData.duration * 60;
            
            // Set judul ujian
            document.getElementById('exam-title').textContent = examData.title;
            
            // Buat nomor soal untuk setiap bagian
            createQuestionNumbers('twk', examData.questions.twk);
            createQuestionNumbers('tiu', examData.questions.tiu);
            createQuestionNumbers('tkp', examData.questions.tkp);
            
            // Buat navigasi soal
            createQuestionNavigation('twk', examData.questions.twk, 1);
            createQuestionNavigation('tiu', examData.questions.tiu, examData.questions.twk + 1);
            createQuestionNavigation('tkp', examData.questions.tkp, examData.questions.twk + examData.questions.tiu + 1);
            
            // Tampilkan soal pertama
            showQuestion(1);
        }

        // Fungsi untuk membuat nomor soal
        function createQuestionNumbers(section, count) {
            const container = document.getElementById(`question-numbers-${section}`);
            container.innerHTML = '';
            
            for (let i = 1; i <= count; i++) {
                const numberElement = document.createElement('span');
                numberElement.className = 'question-number';
                numberElement.textContent = i;
                numberElement.dataset.question = i;
                numberElement.addEventListener('click', () => showQuestion(getGlobalQuestionNumber(section, i)));
                container.appendChild(numberElement);
            }
        }

        // Fungsi untuk membuat navigasi soal
        function createQuestionNavigation(section, count, startNumber) {
            const container = document.getElementById(`navigation-${section}`);
            container.innerHTML = '';
            
            for (let i = 1; i <= count; i++) {
                const globalNumber = startNumber + i - 1;
                const numberElement = document.createElement('span');
                numberElement.className = 'question-number';
                numberElement.textContent = globalNumber;
                numberElement.dataset.question = globalNumber;
                numberElement.addEventListener('click', () => showQuestion(globalNumber));
                container.appendChild(numberElement);
            }
        }

        // Fungsi untuk mendapatkan nomor soal global
        function getGlobalQuestionNumber(section, localNumber) {
            if (section === 'twk') return localNumber;
            if (section === 'tiu') return examData.questions.twk + localNumber;
            if (section === 'tkp') return examData.questions.twk + examData.questions.tiu + localNumber;
            return localNumber;
        }

        // Fungsi untuk menampilkan soal
        function showQuestion(questionNumber) {
            currentQuestion = questionNumber;
            document.getElementById('current-question-number').textContent = questionNumber;
            
            // Update status aktif di navigasi
            document.querySelectorAll('.question-number').forEach(el => {
                el.classList.remove('active');
            });
            
            document.querySelectorAll(`.question-number[data-question="${questionNumber}"]`).forEach(el => {
                el.classList.add('active');
            });
            
            // Tampilkan jawaban yang sudah dipilih (jika ada)
            const selectedAnswer = userAnswers[questionNumber];
            if (selectedAnswer) {
                document.querySelector(`input[name="answer"][value="${selectedAnswer}"]`).checked = true;
            } else {
                document.querySelectorAll('input[name="answer"]').forEach(input => {
                    input.checked = false;
                });
            }
            
            // Update status flag
            const flagButton = document.getElementById('flag-question');
            if (flaggedQuestions.has(questionNumber)) {
                flagButton.innerHTML = '<i class="fas fa-flag"></i> Hapus Tanda';
                flagButton.classList.add('btn-warning');
            } else {
                flagButton.innerHTML = '<i class="far fa-flag"></i> Tandai';
                flagButton.classList.remove('btn-warning');
            }
            
            // Update status navigasi berdasarkan jawaban
            updateQuestionStatus(questionNumber);
        }

        // Fungsi untuk memperbarui status soal di navigasi
        function updateQuestionStatus(questionNumber) {
            const numberElement = document.querySelector(`.question-number[data-question="${questionNumber}"]`);
            
            // Hapus semua status
            numberElement.classList.remove('answered', 'flagged');
            
            // Tambah status berdasarkan kondisi
            if (userAnswers[questionNumber]) {
                numberElement.classList.add('answered');
            }
            
            if (flaggedQuestions.has(questionNumber)) {
                numberElement.classList.add('flagged');
            }
        }

        // Fungsi untuk memulai timer
        function startTimer() {
            clearInterval(examTimer);
            
            examTimer = setInterval(() => {
                timeRemaining--;
                
                if (timeRemaining <= 0) {
                    clearInterval(examTimer);
                    finishExam();
                    return;
                }
                
                const minutes = Math.floor(timeRemaining / 60);
                const seconds = timeRemaining % 60;
                document.getElementById('exam-timer').textContent = 
                    `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            }, 1000);
        }

        // Fungsi untuk menyelesaikan ujian
        function finishExam() {
            clearInterval(examTimer);
            showPage('result-page');
        }

        // Event Listeners
        document.getElementById('login-form').addEventListener('submit', function(e) {
            e.preventDefault();
            showPage('dashboard-page');
        });

        document.getElementById('logout-btn').addEventListener('click', function(e) {
            e.preventDefault();
            showPage('login-page');
        });

        document.querySelectorAll('.start-exam').forEach(button => {
            button.addEventListener('click', function() {
                showPage('exam-page');
            });
        });

        document.getElementById('prev-question').addEventListener('click', function() {
            if (currentQuestion > 1) {
                showQuestion(currentQuestion - 1);
            }
        });

        document.getElementById('next-question').addEventListener('click', function() {
            const totalQuestions = examData.questions.twk + examData.questions.tiu + examData.questions.tkp;
            if (currentQuestion < totalQuestions) {
                showQuestion(currentQuestion + 1);
            }
        });

        document.getElementById('flag-question').addEventListener('click', function() {
            if (flaggedQuestions.has(currentQuestion)) {
                flaggedQuestions.delete(currentQuestion);
                this.innerHTML = '<i class="far fa-flag"></i> Tandai';
                this.classList.remove('btn-warning');
            } else {
                flaggedQuestions.add(currentQuestion);
                this.innerHTML = '<i class="fas fa-flag"></i> Hapus Tanda';
                this.classList.add('btn-warning');
            }
            updateQuestionStatus(currentQuestion);
        });

        document.getElementById('finish-exam').addEventListener('click', function() {
            if (confirm('Apakah Anda yakin ingin menyelesaikan tryout? Anda tidak dapat kembali setelah mengirim jawaban.')) {
                finishExam();
            }
        });

        document.getElementById('back-to-dashboard').addEventListener('click', function(e) {
            e.preventDefault();
            showPage('dashboard-page');
        });

        // Simpan jawaban ketika user memilih opsi
        document.querySelectorAll('input[name="answer"]').forEach(input => {
            input.addEventListener('change', function() {
                userAnswers[currentQuestion] = this.value;
                updateQuestionStatus(currentQuestion);
            });
        });

        // Inisialisasi halaman login sebagai halaman pertama
        showPage('login-page');
    </script>
</body>
</html>
