<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Pendaftaran Siswa Baru - SMK Negeri 1 Purbalingga</title>
    
    <!-- Bootstrap 5 CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Bootstrap Icons -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
    <!-- DataTables CSS -->
    <link rel="stylesheet" href="https://cdn.datatables.net/1.13.7/css/dataTables.bootstrap5.min.css">
    
    <style>
        :root {
            --primary-color: #1e3a8a;
            --secondary-color: #3b82f6;
            --accent-color: #f59e0b;
            --success-color: #10b981;
            --danger-color: #ef4444;
            --dark-color: #1f2937;
            --light-bg: #f3f4f6;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--light-bg);
        }

        .navbar {
            background-color: var(--primary-color) !important;
            box-shadow: 0 2px 4px rgba(0,0,0,.1);
        }

        .navbar-brand {
            font-weight: 600;
            font-size: 1.3rem;
        }

        .card {
            border: none;
            border-radius: 12px;
            box-shadow: 0 2px 8px rgba(0,0,0,.08);
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 16px rgba(0,0,0,.12);
        }

        .btn-primary {
            background-color: var(--secondary-color);
            border-color: var(--secondary-color);
            border-radius: 8px;
            padding: 10px 24px;
            font-weight: 500;
            transition: all 0.3s;
        }

        .btn-primary:hover {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
            transform: translateY(-1px);
        }

        .form-control, .form-select {
            border-radius: 8px;
            border: 1px solid #d1d5db;
            padding: 12px 16px;
            transition: all 0.3s;
        }

        .form-control:focus, .form-select:focus {
            border-color: var(--secondary-color);
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }

        .form-label {
            font-weight: 500;
            color: var(--dark-color);
            margin-bottom: 6px;
        }

        .stats-card {
            background: linear-gradient(135deg, var(--secondary-color), var(--primary-color));
            color: white;
            border-radius: 12px;
            padding: 24px;
            margin-bottom: 20px;
        }

        .stats-card .icon {
            font-size: 2.5rem;
            opacity: 0.8;
        }

        .stats-card h3 {
            font-size: 2rem;
            font-weight: 700;
            margin: 8px 0;
        }

        .table-responsive {
            border-radius: 12px;
            overflow: hidden;
        }

        .table {
            margin-bottom: 0;
        }

        .table thead th {
            background-color: var(--primary-color);
            color: white;
            font-weight: 600;
            border: none;
            padding: 16px;
        }

        .table tbody tr {
            transition: background-color 0.2s;
        }

        .table tbody tr:hover {
            background-color: rgba(59, 130, 246, 0.05);
        }

        .badge {
            padding: 6px 12px;
            border-radius: 6px;
            font-weight: 500;
        }

        .sidebar {
            background-color: white;
            min-height: calc(100vh - 76px);
            box-shadow: 2px 0 8px rgba(0,0,0,.05);
            padding: 24px 0;
        }

        .nav-pills .nav-link {
            border-radius: 8px;
            margin: 4px 16px;
            color: var(--dark-color);
            padding: 12px 20px;
            transition: all 0.3s;
        }

        .nav-pills .nav-link:hover {
            background-color: var(--light-bg);
            color: var(--secondary-color);
        }

        .nav-pills .nav-link.active {
            background-color: var(--secondary-color);
            color: white;
        }

        .photo-preview {
            width: 150px;
            height: 150px;
            border-radius: 8px;
            object-fit: cover;
            border: 3px solid #e5e7eb;
        }

        .alert {
            border: none;
            border-radius: 8px;
            padding: 16px 20px;
        }

        .progress {
            height: 8px;
            border-radius: 4px;
        }

        .modal-content {
            border-radius: 12px;
            border: none;
        }

        .modal-header {
            background-color: var(--primary-color);
            color: white;
            border-radius: 12px 12px 0 0;
        }

        .step-indicator {
            display: flex;
            justify-content: space-between;
            margin-bottom: 40px;
        }

        .step {
            flex: 1;
            text-align: center;
            position: relative;
        }

        .step::after {
            content: '';
            position: absolute;
            top: 20px;
            left: 50%;
            width: 100%;
            height: 2px;
            background-color: #e5e7eb;
            z-index: -1;
        }

        .step:last-child::after {
            display: none;
        }

        .step-circle {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #e5e7eb;
            color: #6b7280;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            margin-bottom: 8px;
            transition: all 0.3s;
        }

        .step.active .step-circle {
            background-color: var(--secondary-color);
            color: white;
        }

        .step.completed .step-circle {
            background-color: var(--success-color);
            color: white;
        }

        .loading-spinner {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 9999;
        }

        @media (max-width: 768px) {
            .sidebar {
                min-height: auto;
                margin-bottom: 20px;
            }
            
            .stats-card {
                margin-bottom: 16px;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Spinner -->
    <div class="loading-spinner">
        <div class="spinner-border text-primary" style="width: 3rem; height: 3rem;" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>

    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
                <i class="bi bi-building"></i> SMK Negeri 1 Purbalingga
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="#"><i class="bi bi-house-door"></i> Beranda</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#"><i class="bi bi-info-circle"></i> Tentang</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#"><i class="bi bi-telephone"></i> Kontak</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="container-fluid">
        <div class="row">
            <!-- Sidebar -->
            <div class="col-md-3 col-lg-2 sidebar">
                <div class="nav flex-column nav-pills">
                    <a class="nav-link active" href="#" data-page="dashboard">
                        <i class="bi bi-speedometer2"></i> Dashboard
                    </a>
                    <a class="nav-link" href="#" data-page="form">
                        <i class="bi bi-person-plus"></i> Tambah Siswa
                    </a>
                    <a class="nav-link" href="#" data-page="list">
                        <i class="bi bi-list-ul"></i> Daftar Siswa
                    </a>
                    <a class="nav-link" href="#" data-page="report">
                        <i class="bi bi-file-earmark-bar-graph"></i> Laporan
                    </a>
                </div>
            </div>

            <!-- Content Area -->
            <div class="col-md-9 col-lg-10 p-4">
                <!-- Dashboard Page -->
                <div id="dashboard-page" class="page-content">
                    <h2 class="mb-4">Dashboard Pendaftaran Siswa Baru</h2>
                    
                    <!-- Stats Cards -->
                    <div class="row">
                        <div class="col-md-3">
                            <div class="stats-card">
                                <i class="bi bi-people-fill icon"></i>
                                <h3 id="total-students">0</h3>
                                <p>Total Siswa Terdaftar</p>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="stats-card" style="background: linear-gradient(135deg, #10b981, #059669);">
                                <i class="bi bi-person-check-fill icon"></i>
                                <h3 id="today-registrations">0</h3>
                                <p>Pendaftaran Hari Ini</p>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="stats-card" style="background: linear-gradient(135deg, #f59e0b, #d97706);">
                                <i class="bi bi-graph-up icon"></i>
                                <h3 id="monthly-registrations">0</h3>
                                <p>Pendaftaran Bulan Ini</p>
                            </div>
                        </div>
                        <div class="col-md-3">
                            <div class="stats-card" style="background: linear-gradient(135deg, #8b5cf6, #7c3aed);">
                                <i class="bi bi-mortarboard-fill icon"></i>
                                <h3 id="majors-count">0</h3>
                                <p>Jurusan Tersedia</p>
                            </div>
                        </div>
                    </div>

                    <!-- Recent Registrations -->
                    <div class="card mt-4">
                        <div class="card-header bg-white">
                            <h5 class="mb-0">Pendaftaran Terbaru</h5>
                        </div>
                        <div class="card-body">
                            <div class="table-responsive">
                                <table class="table table-hover" id="recent-table">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Nama</th>
                                            <th>NISN</th>
                                            <th>Jurusan</th>
                                            <th>Tanggal Daftar</th>
                                            <th>Status</th>
                                        </tr>
                                    </thead>
                                    <tbody id="recent-tbody">
                                        <!-- Data will be populated here -->
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Form Page -->
                <div id="form-page" class="page-content" style="display: none;">
                    <h2 class="mb-4">Form Pendaftaran Siswa Baru</h2>
                    
                    <!-- Step Indicator -->
                    <div class="step-indicator">
                        <div class="step active" data-step="1">
                            <div class="step-circle">1</div>
                            <small>Data Diri</small>
                        </div>
                        <div class="step" data-step="2">
                            <div class="step-circle">2</div>
                            <small>Data Orang Tua</small>
                        </div>
                        <div class="step" data-step="3">
                            <div class="step-circle">3</div>
                            <small>Pendidikan & Dokumen</small>
                        </div>
                        <div class="step" data-step="4">
                            <div class="step-circle">4</div>
                            <small>Konfirmasi</small>
                        </div>
                    </div>

                    <!-- Progress Bar -->
                    <div class="progress mb-4">
                        <div class="progress-bar" role="progressbar" style="width: 25%"></div>
                    </div>

                    <form id="student-form">
                        <!-- Step 1: Personal Data -->
                        <div id="step-1" class="form-step">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title mb-4">Data Diri Siswa</h5>
                                    
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Nama Lengkap <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="nama_lengkap" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">NISN <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="nisn" maxlength="10" required>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Tempat Lahir <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="tempat_lahir" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Tanggal Lahir <span class="text-danger">*</span></label>
                                            <input type="date" class="form-control" name="tanggal_lahir" required>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Jenis Kelamin <span class="text-danger">*</span></label>
                                            <select class="form-select" name="jenis_kelamin" required>
                                                <option value="">Pilih...</option>
                                                <option value="L">Laki-laki</option>
                                                <option value="P">Perempuan</option>
                                            </select>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Agama <span class="text-danger">*</span></label>
                                            <select class="form-select" name="agama" required>
                                                <option value="">Pilih...</option>
                                                <option value="Islam">Islam</option>
                                                <option value="Kristen">Kristen</option>
                                                <option value="Katolik">Katolik</option>
                                                <option value="Hindu">Hindu</option>
                                                <option value="Buddha">Buddha</option>
                                                <option value="Konghucu">Konghucu</option>
                                            </select>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Jurusan <span class="text-danger">*</span></label>
                                            <select class="form-select" name="jurusan" required>
                                                <option value="">Pilih...</option>
                                                <option value="TKJ">Teknik Komputer dan Jaringan</option>
                                                <option value="RPL">Rekayasa Perangkat Lunak</option>
                                                <option value="MM">Multimedia</option>
                                                <option value="OTKP">Otomatisasi dan Tata Kelola Perkantoran</option>
                                                <option value="AKL">Akuntansi dan Keuangan Lembaga</option>
                                                <option value="BDP">Bisnis Daring dan Pemasaran</option>
                                                <option value="TBSM">Teknik Bisnis Sepeda Motor</option>
                                                <option value="TKR">Teknik Kendaraan Ringan</option>
                                            </select>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">No. HP <span class="text-danger">*</span></label>
                                            <input type="tel" class="form-control" name="no_hp" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Email</label>
                                            <input type="email" class="form-control" name="email">
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-12 mb-3">
                                            <label class="form-label">Alamat Lengkap <span class="text-danger">*</span></label>
                                            <textarea class="form-control" name="alamat" rows="3" required></textarea>
                                        </div>
                                    </div>

                                    <div class="row">
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Provinsi <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="provinsi" value="Jawa Tengah" required>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Kabupaten/Kota <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="kabupaten" value="Purbalingga" required>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Kecamatan <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="kecamatan" required>
                                        </div>
                                    </div>

                                    <div class="text-end mt-4">
                                        <button type="button" class="btn btn-primary" onclick="nextStep()">
                                            Selanjutnya <i class="bi bi-arrow-right"></i>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Step 2: Parent Data -->
                        <div id="step-2" class="form-step" style="display: none;">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title mb-4">Data Orang Tua/Wali</h5>
                                    
                                    <h6 class="mb-3">Data Ayah</h6>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Nama Ayah <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="nama_ayah" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pekerjaan Ayah <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="pekerjaan_ayah" required>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">No. HP Ayah</label>
                                            <input type="tel" class="form-control" name="no_hp_ayah">
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pendidikan Ayah</label>
                                            <select class="form-select" name="pendidikan_ayah">
                                                <option value="">Pilih...</option>
                                                <option value="SD">SD</option>
                                                <option value="SMP">SMP</option>
                                                <option value="SMA">SMA</option>
                                                <option value="D3">D3</option>
                                                <option value="S1">S1</option>
                                                <option value="S2">S2</option>
                                                <option value="S3">S3</option>
                                            </select>
                                        </div>
                                    </div>

                                    <hr class="my-4">

                                    <h6 class="mb-3">Data Ibu</h6>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Nama Ibu <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="nama_ibu" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pekerjaan Ibu <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="pekerjaan_ibu" required>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">No. HP Ibu</label>
                                            <input type="tel" class="form-control" name="no_hp_ibu">
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pendidikan Ibu</label>
                                            <select class="form-select" name="pendidikan_ibu">
                                                <option value="">Pilih...</option>
                                                <option value="SD">SD</option>
                                                <option value="SMP">SMP</option>
                                                <option value="SMA">SMA</option>
                                                <option value="D3">D3</option>
                                                <option value="S1">S1</option>
                                                <option value="S2">S2</option>
                                                <option value="S3">S3</option>
                                            </select>
                                        </div>
                                    </div>

                                    <hr class="my-4">

                                    <h6 class="mb-3">Data Wali (Jika ada)</h6>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Nama Wali</label>
                                            <input type="text" class="form-control" name="nama_wali">
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Hubungan dengan Siswa</label>
                                            <input type="text" class="form-control" name="hubungan_wali">
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pekerjaan Wali</label>
                                            <input type="text" class="form-control" name="pekerjaan_wali">
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">No. HP Wali</label>
                                            <input type="tel" class="form-control" name="no_hp_wali">
                                        </div>
                                    </div>

                                    <div class="d-flex justify-content-between mt-4">
                                        <button type="button" class="btn btn-secondary" onclick="previousStep()">
                                            <i class="bi bi-arrow-left"></i> Sebelumnya
                                        </button>
                                        <button type="button" class="btn btn-primary" onclick="nextStep()">
                                            Selanjutnya <i class="bi bi-arrow-right"></i>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Step 3: Education & Documents -->
                        <div id="step-3" class="form-step" style="display: none;">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title mb-4">Data Pendidikan & Dokumen</h5>
                                    
                                    <h6 class="mb-3">Data Pendidikan Sebelumnya</h6>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Asal Sekolah <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="asal_sekolah" required>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Alamat Sekolah <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="alamat_sekolah" required>
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">Tahun Lulus <span class="text-danger">*</span></label>
                                            <input type="number" class="form-control" name="tahun_lulus" min="2020" max="2024" required>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">No. Ijazah/SKL <span class="text-danger">*</span></label>
                                            <input type="text" class="form-control" name="no_ijazah" required>
                                        </div>
                                        <div class="col-md-4 mb-3">
                                            <label class="form-label">NEM/Nilai Rata-rata <span class="text-danger">*</span></label>
                                            <input type="number" class="form-control" name="nem" step="0.01" min="0" max="100" required>
                                        </div>
                                    </div>

                                    <hr class="my-4">

                                    <h6 class="mb-3">Upload Dokumen (Simulasi)</h6>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Pas Foto 3x4 <span class="text-danger">*</span></label>
                                            <input type="file" class="form-control" accept="image/*" onchange="previewPhoto(event)">
                                            <div class="mt-2">
                                                <img id="photo-preview" class="photo-preview d-none" src="" alt="Preview">
                                            </div>
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Scan Ijazah/SKL <span class="text-danger">*</span></label>
                                            <input type="file" class="form-control" accept=".pdf,.jpg,.jpeg,.png">
                                        </div>
                                    </div>
                                    <div class="row">
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Scan KK <span class="text-danger">*</span></label>
                                            <input type="file" class="form-control" accept=".pdf,.jpg,.jpeg,.png">
                                        </div>
                                        <div class="col-md-6 mb-3">
                                            <label class="form-label">Scan Akta Kelahiran <span class="text-danger">*</span></label>
                                            <input type="file" class="form-control" accept=".pdf,.jpg,.jpeg,.png">
                                        </div>
                                    </div>

                                    <div class="d-flex justify-content-between mt-4">
                                        <button type="button" class="btn btn-secondary" onclick="previousStep()">
                                            <i class="bi bi-arrow-left"></i> Sebelumnya
                                        </button>
                                        <button type="button" class="btn btn-primary" onclick="nextStep()">
                                            Selanjutnya <i class="bi bi-arrow-right"></i>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Step 4: Confirmation -->
                        <div id="step-4" class="form-step" style="display: none;">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title mb-4">Konfirmasi Data</h5>
                                    
                                    <div class="alert alert-info">
                                        <i class="bi bi-info-circle"></i> Silakan periksa kembali data yang Anda masukkan sebelum menyimpan.
                                    </div>

                                    <div id="confirmation-data">
                                        <!-- Data will be populated here -->
                                    </div>

                                    <div class="form-check mt-4">
                                        <input class="form-check-input" type="checkbox" id="confirm-check" required>
                                        <label class="form-check-label" for="confirm-check">
                                            Saya menyatakan bahwa data yang saya isi adalah benar dan dapat dipertanggungjawabkan.
                                        </label>
                                    </div>

                                    <div class="d-flex justify-content-between mt-4">
                                        <button type="button" class="btn btn-secondary" onclick="previousStep()">
                                            <i class="bi bi-arrow-left"></i> Sebelumnya
                                        </button>
                                        <button type="submit" class="btn btn-success">
                                            <i class="bi bi-check-circle"></i> Simpan Data
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </form>
                </div>

                <!-- List Page -->
                <div id="list-page" class="page-content" style="display: none;">
                    <div class="d-flex justify-content-between align-items-center mb-4">
                        <h2>Daftar Siswa Terdaftar</h2>
                        <div>
                            <button class="btn btn-success" onclick="exportData()">
                                <i class="bi bi-download"></i> Export Excel
                            </button>
                            <button class="btn btn-primary" onclick="window.print()">
                                <i class="bi bi-printer"></i> Cetak
                            </button>
                        </div>
                    </div>

                    <!-- Search and Filter -->
                    <div class="card mb-4">
                        <div class="card-body">
                            <div class="row">
                                <div class="col-md-4 mb-3">
                                    <label class="form-label">Cari Nama/NISN</label>
                                    <input type="text" class="form-control" id="search-input" placeholder="Ketik untuk mencari...">
                                </div>
                                <div class="col-md-3 mb-3">
                                    <label class="form-label">Filter Jurusan</label>
                                    <select class="form-select" id="filter-jurusan">
                                        <option value="">Semua Jurusan</option>
                                        <option value="TKJ">Teknik Komputer dan Jaringan</option>
                                        <option value="RPL">Rekayasa Perangkat Lunak</option>
                                        <option value="MM">Multimedia</option>
                                        <option value="OTKP">Otomatisasi dan Tata Kelola Perkantoran</option>
                                        <option value="AKL">Akuntansi dan Keuangan Lembaga</option>
                                        <option value="BDP">Bisnis Daring dan Pemasaran</option>
                                        <option value="TBSM">Teknik Bisnis Sepeda Motor</option>
                                        <option value="TKR">Teknik Kendaraan Ringan</option>
                                    </select>
                                </div>
                                <div class="col-md-3 mb-3">
                                    <label class="form-label">Filter Status</label>
                                    <select class="form-select" id="filter-status">
                                        <option value="">Semua Status</option>
                                        <option value="Baru">Baru</option>
                                        <option value="Diproses">Diproses</option>
                                        <option value="Diterima">Diterima</option>
                                    </select>
                                </div>
                                <div class="col-md-2 mb-3">
                                    <label class="form-label">&nbsp;</label>
                                    <button class="btn btn-outline-secondary w-100" onclick="resetFilters()">
                                        <i class="bi bi-arrow-clockwise"></i> Reset
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Students Table -->
                    <div class="card">
                        <div class="card-body">
                            <div class="table-responsive">
                                <table class="table table-hover" id="students-table">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Foto</th>
                                            <th>Nama</th>
                                            <th>NISN</th>
                                            <th>Jurusan</th>
                                            <th>Tanggal Daftar</th>
                                            <th>Status</th>
                                            <th>Aksi</th>
                                        </tr>
                                    </thead>
                                    <tbody id="students-tbody">
                                        <!-- Data will be populated here -->
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Report Page -->
                <div id="report-page" class="page-content" style="display: none;">
                    <h2 class="mb-4">Laporan Pendaftaran</h2>
                    
                    <!-- Report Summary -->
                    <div class="row mb-4">
                        <div class="col-md-6">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">Statistik per Jurusan</h5>
                                    <canvas id="jurusan-chart" width="400" height="200"></canvas>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">Pendaftaran per Bulan</h5>
                                    <canvas id="monthly-chart" width="400" height="200"></canvas>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Detailed Report -->
                    <div class="card">
                        <div class="card-body">
                            <h5 class="card-title mb-4">Detail Laporan</h5>
                            <div class="row">
                                <div class="col-md-3 mb-3">
                                    <div class="text-center p-3 bg-light rounded">
                                        <h3 class="text-primary" id="report-total">0</h3>
                                        <p class="mb-0">Total Pendaftar</p>
                                    </div>
                                </div>
                                <div class="col-md-3 mb-3">
                                    <div class="text-center p-3 bg-light rounded">
                                        <h3 class="text-success" id="report-accepted">0</h3>
                                        <p class="mb-0">Diterima</p>
                                    </div>
                                </div>
                                <div class="col-md-3 mb-3">
                                    <div class="text-center p-3 bg-light rounded">
                                        <h3 class="text-warning" id="report-processing">0</h3>
                                        <p class="mb-0">Diproses</p>
                                    </div>
                                </div>
                                <div class="col-md-3 mb-3">
                                    <div class="text-center p-3 bg-light rounded">
                                        <h3 class="text-info" id="report-new">0</h3>
                                        <p class="mb-0">Baru</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Success Modal -->
    <div class="modal fade" id="successModal" tabindex="-1">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Berhasil!</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body text-center">
                    <i class="bi bi-check-circle-fill text-success" style="font-size: 4rem;"></i>
                    <h4 class="mt-3">Data Siswa Berhasil Disimpan</h4>
                    <p class="text-muted">Nomor Pendaftaran: <strong id="registration-number"></strong></p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Tutup</button>
                    <button type="button" class="btn btn-primary" onclick="printRegistration()">Cetak Bukti</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Detail Modal -->
    <div class="modal fade" id="detailModal" tabindex="-1">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Detail Siswa</h5>
                    <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body" id="detail-content">
                    <!-- Detail content will be populated here -->
                </div>
            </div>
        </div>
    </div>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://code.jquery.com/jquery-3.7.0.min.js"></script>
    <script src="https://cdn.datatables.net/1.13.7/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/1.13.7/js/dataTables.bootstrap5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <script>
        // Global variables
        let currentStep = 1;
        let students = JSON.parse(localStorage.getItem('students')) || [];
        let currentStudent = null;

        // Initialize app
        document.addEventListener('DOMContentLoaded', function() {
            updateDashboard();
            loadStudents();
            initializeEventListeners();
            updateReport();
        });

        // Navigation
        function initializeEventListeners() {
            // Sidebar navigation
            document.querySelectorAll('.nav-link').forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    const page = this.getAttribute('data-page');
                    showPage(page);
                    
                    // Update active nav
                    document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
                    this.classList.add('active');
                });
            });

            // Form submission
            document.getElementById('student-form').addEventListener('submit', function(e) {
                e.preventDefault();
                saveStudent();
            });

            // Search and filter
            document.getElementById('search-input').addEventListener('input', filterStudents);
            document.getElementById('filter-jurusan').addEventListener('change', filterStudents);
            document.getElementById('filter-status').addEventListener('change', filterStudents);
        }

        function showPage(page) {
            document.querySelectorAll('.page-content').forEach(p => p.style.display = 'none');
            document.getElementById(`${page}-page`).style.display = 'block';
            
            if (page === 'dashboard') {
                updateDashboard();
            } else if (page === 'list') {
                loadStudents();
            } else if (page === 'report') {
                updateReport();
            }
        }

        // Form steps
        function nextStep() {
            if (validateStep(currentStep)) {
                if (currentStep === 3) {
                    showConfirmation();
                }
                document.getElementById(`step-${currentStep}`).style.display = 'none';
                currentStep++;
                document.getElementById(`step-${currentStep}`).style.display = 'block';
                updateStepIndicator();
                updateProgressBar();
            }
        }

        function previousStep() {
            document.getElementById(`step-${currentStep}`).style.display = 'none';
            currentStep--;
            document.getElementById(`step-${currentStep}`).style.display = 'block';
            updateStepIndicator();
            updateProgressBar();
        }

        function updateStepIndicator() {
            document.querySelectorAll('.step').forEach((step, index) => {
                if (index < currentStep - 1) {
                    step.classList.add('completed');
                    step.classList.remove('active');
                } else if (index === currentStep - 1) {
                    step.classList.add('active');
                    step.classList.remove('completed');
                } else {
                    step.classList.remove('active', 'completed');
                }
            });
        }

        function updateProgressBar() {
            const progress = (currentStep / 4) * 100;
            document.querySelector('.progress-bar').style.width = `${progress}%`;
        }

        function validateStep(step) {
            const form = document.getElementById('student-form');
            const stepElement = document.getElementById(`step-${step}`);
            const requiredFields = stepElement.querySelectorAll('[required]');
            
            let isValid = true;
            requiredFields.forEach(field => {
                if (!field.value.trim()) {
                    field.classList.add('is-invalid');
                    isValid = false;
                } else {
                    field.classList.remove('is-invalid');
                }
            });

            if (!isValid) {
                showToast('Harap lengkapi semua field yang wajib diisi!', 'warning');
            }

            return isValid;
        }

        function showConfirmation() {
            const formData = new FormData(document.getElementById('student-form'));
            let html = '<div class="row">';
            
            // Personal data
            html += '<div class="col-md-6"><h6>Data Diri</h6>';
            html += `<p><strong>Nama:</strong> ${formData.get('nama_lengkap')}</p>`;
            html += `<p><strong>NISN:</strong> ${formData.get('nisn')}</p>`;
            html += `<p><strong>Tempat/Tanggal Lahir:</strong> ${formData.get('tempat_lahir')}, ${formData.get('tanggal_lahir')}</p>`;
            html += `<p><strong>Jenis Kelamin:</strong> ${formData.get('jenis_kelamin') === 'L' ? 'Laki-laki' : 'Perempuan'}</p>`;
            html += `<p><strong>Agama:</strong> ${formData.get('agama')}</p>`;
            html += `<p><strong>Jurusan:</strong> ${formData.get('jurusan')}</p>`;
            html += '</div>';
            
            // Parent data
            html += '<div class="col-md-6"><h6>Data Orang Tua</h6>';
            html += `<p><strong>Ayah:</strong> ${formData.get('nama_ayah')}</p>`;
            html += `<p><strong>Ibu:</strong> ${formData.get('nama_ibu')}</p>`;
            html += `<p><strong>No. HP Ayah:</strong> ${formData.get('no_hp_ayah') || '-'}</p>`;
            html += `<p><strong>No. HP Ibu:</strong> ${formData.get('no_hp_ibu') || '-'}</p>`;
            html += '</div>';
            
            html += '</div>';
            
            document.getElementById('confirmation-data').innerHTML = html;
        }

        // Photo preview
        function previewPhoto(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const preview = document.getElementById('photo-preview');
                    preview.src = e.target.result;
                    preview.classList.remove('d-none');
                };
                reader.readAsDataURL(file);
            }
        }

        // Save student
        function saveStudent() {
            const formData = new FormData(document.getElementById('student-form'));
            const student = {
                id: Date.now(),
                registrationNumber: generateRegistrationNumber(),
                registrationDate: new Date().toISOString(),
                status: 'Baru',
                ...Object.fromEntries(formData)
            };
            
            students.push(student);
            localStorage.setItem('students', JSON.stringify(students));
            
            // Show success modal
            document.getElementById('registration-number').textContent = student.registrationNumber;
            const modal = new bootstrap.Modal(document.getElementById('successModal'));
            modal.show();
            
            // Reset form
            document.getElementById('student-form').reset();
            document.getElementById('photo-preview').classList.add('d-none');
            currentStep = 1;
            document.querySelectorAll('.form-step').forEach(step => step.style.display = 'none');
            document.getElementById('step-1').style.display = 'block';
            updateStepIndicator();
            updateProgressBar();
            
            // Update dashboard
            updateDashboard();
        }

        function generateRegistrationNumber() {
            const year = new Date().getFullYear();
            const month = String(new Date().getMonth() + 1).padStart(2, '0');
            const sequence = String(students.length + 1).padStart(4, '0');
            return `REG${year}${month}${sequence}`;
        }

        // Dashboard functions
        function updateDashboard() {
            document.getElementById('total-students').textContent = students.length;
            
            const today = new Date().toDateString();
            const todayCount = students.filter(s => 
                new Date(s.registrationDate).toDateString() === today
            ).length;
            document.getElementById('today-registrations').textContent = todayCount;
            
            const currentMonth = new Date().getMonth();
            const currentYear = new Date().getFullYear();
            const monthCount = students.filter(s => {
                const date = new Date(s.registrationDate);
                return date.getMonth() === currentMonth && date.getFullYear() === currentYear;
            }).length;
            document.getElementById('monthly-registrations').textContent = monthCount;
            
            const majors = [...new Set(students.map(s => s.jurusan))].length;
            document.getElementById('majors-count').textContent = majors;
            
            // Update recent registrations
            updateRecentRegistrations();
        }

        function updateRecentRegistrations() {
            const tbody = document.getElementById('recent-tbody');
            const recentStudents = students.slice(-5).reverse();
            
            tbody.innerHTML = recentStudents.map((student, index) => `
                <tr>
                    <td>${index + 1}</td>
                    <td>${student.nama_lengkap}</td>
                    <td>${student.nisn}</td>
                    <td>${student.jurusan}</td>
                    <td>${formatDate(student.registrationDate)}</td>
                    <td><span class="badge bg-${getStatusColor(student.status)}">${student.status}</span></td>
                </tr>
            `).join('');
        }

        // List functions
        function loadStudents() {
            const tbody = document.getElementById('students-tbody');
            
            tbody.innerHTML = students.map((student, index) => `
                <tr>
                    <td>${index + 1}</td>
                    <td>
                        <img src="https://picsum.photos/seed/${student.id}/50/50.jpg" 
                             class="rounded-circle" width="40" height="40">
                    </td>
                    <td>${student.nama_lengkap}</td>
                    <td>${student.nisn}</td>
                    <td>${student.jurusan}</td>
                    <td>${formatDate(student.registrationDate)}</td>
                    <td><span class="badge bg-${getStatusColor(student.status)}">${student.status}</span></td>
                    <td>
                        <button class="btn btn-sm btn-info" onclick="showDetail(${student.id})">
                            <i class="bi bi-eye"></i>
                        </button>
                        <button class="btn btn-sm btn-warning" onclick="editStudent(${student.id})">
                            <i class="bi bi-pencil"></i>
                        </button>
                        <button class="btn btn-sm btn-danger" onclick="deleteStudent(${student.id})">
                            <i class="bi bi-trash"></i>
                        </button>
                    </td>
                </tr>
            `).join('');
            
            // Initialize DataTable
            if ($.fn.DataTable.isDataTable('#students-table')) {
                $('#students-table').DataTable().destroy();
            }
            $('#students-table').DataTable({
                pageLength: 10,
                language: {
                    url: '//cdn.datatables.net/plug-ins/1.13.7/i18n/id.json'
                }
            });
        }

        function filterStudents() {
            const searchTerm = document.getElementById('search-input').value.toLowerCase();
            const jurusanFilter = document.getElementById('filter-jurusan').value;
            const statusFilter = document.getElementById('filter-status').value;
            
            const filtered = students.filter(student => {
                const matchSearch = student.nama_lengkap.toLowerCase().includes(searchTerm) ||
                                  student.nisn.includes(searchTerm);
                const matchJurusan = !jurusanFilter || student.jurusan === jurusanFilter;
                const matchStatus = !statusFilter || student.status === statusFilter;
                
                return matchSearch && matchJurusan && matchStatus;
            });
            
            const tbody = document.getElementById('students-tbody');
            tbody.innerHTML = filtered.map((student, index) => `
                <tr>
                    <td>${index + 1}</td>
                    <td>
                        <img src="https://picsum.photos/seed/${student.id}/50/50.jpg" 
                             class="rounded-circle" width="40" height="40">
                    </td>
                    <td>${student.nama_lengkap}</td>
                    <td>${student.nisn}</td>
                    <td>${student.jurusan}</td>
                    <td>${formatDate(student.registrationDate)}</td>
                    <td><span class="badge bg-${getStatusColor(student.status)}">${student.status}</span></td>
                    <td>
                        <button class="btn btn-sm btn-info" onclick="showDetail(${student.id})">
                            <i class="bi bi-eye"></i>
                        </button>
                        <button class="btn btn-sm btn-warning" onclick="editStudent(${student.id})">
                            <i class="bi bi-pencil"></i>
                        </button>
                        <button class="btn btn-sm btn-danger" onclick="deleteStudent(${student.id})">
                            <i class="bi bi-trash"></i>
                        </button>
                    </td>
                </tr>
            `).join('');
        }

        function resetFilters() {
            document.getElementById('search-input').value = '';
            document.getElementById('filter-jurusan').value = '';
            document.getElementById('filter-status').value = '';
            loadStudents();
        }

        // Detail functions
        function showDetail(id) {
            const student = students.find(s => s.id === id);
            if (!student) return;
            
            let html = `
                <div class="row">
                    <div class="col-md-4 text-center">
                        <img src="https://picsum.photos/seed/${student.id}/200/200.jpg" 
                             class="rounded mb-3" width="200" height="200">
                        <h5>${student.nama_lengkap}</h5>
                        <p class="text-muted">${student.registrationNumber}</p>
                    </div>
                    <div class="col-md-8">
                        <h6>Data Diri</h6>
                        <table class="table table-sm">
                            <tr><td>NISN</td><td>: ${student.nisn}</td></tr>
                            <tr><td>Tempat/Tanggal Lahir</td><td>: ${student.tempat_lahir}, ${formatDate(student.tanggal_lahir)}</td></tr>
                            <tr><td>Jenis Kelamin</td><td>: ${student.jenis_kelamin === 'L' ? 'Laki-laki' : 'Perempuan'}</td></tr>
                            <tr><td>Agama</td><td>: ${student.agama}</td></tr>
                            <tr><td>Jurusan</td><td>: ${student.jurusan}</td></tr>
                            <tr><td>No. HP</td><td>: ${student.no_hp}</td></tr>
                            <tr><td>Email</td><td>: ${student.email || '-'}</td></tr>
                            <tr><td>Alamat</td><td>: ${student.alamat}</td></tr>
                        </table>
                        
                        <h6>Data Orang Tua</h6>
                        <table class="table table-sm">
                            <tr><td>Ayah</td><td>: ${student.nama_ayah}</td></tr>
                            <tr><td>Ibu</td><td>: ${student.nama_ibu}</td></tr>
                            <tr><td>No. HP Ayah</td><td>: ${student.no_hp_ayah || '-'}</td></tr>
                            <tr><td>No. HP Ibu</td><td>: ${student.no_hp_ibu || '-'}</td></tr>
                        </table>
                        
                        <h6>Data Pendidikan</h6>
                        <table class="table table-sm">
                            <tr><td>Asal Sekolah</td><td>: ${student.asal_sekolah}</td></tr>
                            <tr><td>Tahun Lulus</td><td>: ${student.tahun_lulus}</td></tr>
                            <tr><td>No. Ijazah/SKL</td><td>: ${student.no_ijazah}</td></tr>
                            <tr><td>NEM</td><td>: ${student.nem}</td></tr>
                        </table>
                    </div>
                </div>
            `;
            
            document.getElementById('detail-content').innerHTML = html;
            const modal = new bootstrap.Modal(document.getElementById('detailModal'));
            modal.show();
        }

        function editStudent(id) {
            showToast('Fitur edit akan segera tersedia', 'info');
        }

        function deleteStudent(id) {
            if (confirm('Apakah Anda yakin ingin menghapus data siswa ini?')) {
                students = students.filter(s => s.id !== id);
                localStorage.setItem('students', JSON.stringify(students));
                loadStudents();
                updateDashboard();
                showToast('Data siswa berhasil dihapus', 'success');
            }
        }

        // Report functions
        function updateReport() {
            // Update statistics
            document.getElementById('report-total').textContent = students.length;
            document.getElementById('report-accepted').textContent = 
                students.filter(s => s.status === 'Diterima').length;
            document.getElementById('report-processing').textContent = 
                students.filter(s => s.status === 'Diproses').length;
            document.getElementById('report-new').textContent = 
                students.filter(s => s.status === 'Baru').length;
            
            // Update charts
            updateJurusanChart();
            updateMonthlyChart();
        }

        function updateJurusanChart() {
            const ctx = document.getElementById('jurusan-chart').getContext('2d');
            const jurusanData = {};
            
            students.forEach(student => {
                jurusanData[student.jurusan] = (jurusanData[student.jurusan] || 0) + 1;
            });
            
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: Object.keys(jurusanData),
                    datasets: [{
                        label: 'Jumlah Siswa',
                        data: Object.values(jurusanData),
                        backgroundColor: 'rgba(59, 130, 246, 0.5)',
                        borderColor: 'rgba(59, 130, 246, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                stepSize: 1
                            }
                        }
                    }
                }
            });
        }

        function updateMonthlyChart() {
            const ctx = document.getElementById('monthly-chart').getContext('2d');
            const monthlyData = new Array(12).fill(0);
            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'Mei', 'Jun', 'Jul', 'Agu', 'Sep', 'Okt', 'Nov', 'Des'];
            
            students.forEach(student => {
                const month = new Date(student.registrationDate).getMonth();
                monthlyData[month]++;
            });
            
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: months,
                    datasets: [{
                        label: 'Pendaftaran',
                        data: monthlyData,
                        borderColor: 'rgba(16, 185, 129, 1)',
                        backgroundColor: 'rgba(16, 185, 129, 0.1)',
                        tension: 0.1
                    }]
                },
                options: {
                    responsive: true,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                stepSize: 1
                            }
                        }
                    }
                }
            });
        }

        // Utility functions
        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('id-ID', options);
        }

        function getStatusColor(status) {
            const colors = {
                'Baru': 'info',
                'Diproses': 'warning',
                'Diterima': 'success'
            };
            return colors[status] || 'secondary';
        }

        function showToast(message, type = 'info') {
            const toastHtml = `
                <div class="toast align-items-center text-white bg-${type} border-0" role="alert">
                    <div class="d-flex">
                        <div class="toast-body">
                            ${message}
                        </div>
                        <button type="button" class="btn-close btn-close-white me-2 m-auto" data-bs-dismiss="toast"></button>
                    </div>
                </div>
            `;
            
            const toastContainer = document.createElement('div');
            toastContainer.className = 'toast-container position-fixed bottom-0 end-0 p-3';
            toastContainer.innerHTML = toastHtml;
            document.body.appendChild(toastContainer);
            
            const toast = new bootstrap.Toast(toastContainer.querySelector('.toast'));
            toast.show();
            
            setTimeout(() => {
                toastContainer.remove();
            }, 5000);
        }

        function exportData() {
            showToast('Fitur export akan segera tersedia', 'info');
        }

        function printRegistration() {
            window.print();
        }
    </script>
</body>
</html>
