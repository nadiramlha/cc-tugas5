# CI/CD for Kubernetes

## 📋 Deskripsi
Repository ini berisi workflow **CI/CD untuk Kubernetes** menggunakan **GitHub Actions**. Pipeline ini mendukung:
- **Multi-environment deployment** (Staging dan Production).
- **Auto-rollback** jika deployment gagal.
- Logging deployment.
- Notifikasi email menggunakan **SendGrid API**.

---

## 🚀 Fitur Utama
- **Multi-Environment Deployment**: Deployment otomatis ke environment **Staging** dan **Production**.
- **Auto-Rollback**: Secara otomatis mengembalikan deployment ke versi sebelumnya jika gagal.
- **Log Deployment**: Log disimpan dan dapat diakses melalui tab **Actions** di GitHub.
- **Notifikasi Email**: Mengirimkan notifikasi email setelah deployment berhasil atau gagal.

---

## 📂 Struktur Repository
📦 cc-tugas5
├── 📁 .github
│   └── 📁 workflows
│       └── 📄 deploy.yml         # Workflow CI/CD untuk Kubernetes
├── 📁 apps
│   └── 📁 nginx-deployment
│       ├── 📄 nginx-deployment.yaml  # File Deployment untuk Kubernetes
│       └── 📄 nginx-ingress.yaml     # File Ingress untuk Kubernetes
└── 📄 README.md

---

## ⚙️ Cara Menggunakan

### 1️⃣ Persiapan
1. **Tambahkan Secrets ke Repository**:
   - **KUBECONFIG_STAGING**: File kubeconfig untuk environment **Staging**.
   - **KUBECONFIG_PRODUCTION**: File kubeconfig untuk environment **Production**.
   - **SENDGRID_API_KEY**: API Key dari akun SendGrid untuk notifikasi email.

   **Cara menambahkan Secrets**:
   - Masuk ke repository di GitHub.
   - Buka **Settings > Secrets and variables > Actions**.
   - Tambahkan setiap secret dengan nama dan value yang sesuai.

2. **Pastikan Cluster Kubernetes Aktif**:
   - Cluster untuk **Staging** dan **Production** harus berjalan dengan baik.

---

### 2️⃣ File Workflow
Workflow `deploy.yml` terletak di folder: .github/workflows/deploy.yml

Pipeline akan berjalan otomatis setiap ada **push ke branch `main`**.

---

### 3️⃣ Langkah-Langkah Workflow
1. **Checkout Repository**: Mengambil file dari branch `main`.
2. **Set Up kubectl**: Mengatur kubectl untuk berinteraksi dengan cluster Kubernetes.
3. **Deploy ke Staging**: Melakukan deployment aplikasi ke environment **Staging**.
4. **Verifikasi Deployment**: Memastikan Pods berjalan dengan status **Running**.
5. **Deploy ke Production**: Melakukan deployment aplikasi ke environment **Production**.
6. **Rollback Jika Gagal**: Mengembalikan deployment ke versi sebelumnya jika terjadi error.
7. **Upload Log Deployment**: Menyimpan log deployment ke tab Actions di GitHub.
8. **Notifikasi Email**: Mengirimkan notifikasi status pipeline ke email Anda.

---

## 📧 Notifikasi Email
Pipeline menggunakan **SendGrid API** untuk mengirimkan notifikasi email. Email akan mencakup:
- Status pipeline: **Success** atau **Failure**.
- Informasi untuk melihat log lengkap di GitHub.

---

## 🛠️ Cara Menjalankan Ulang Workflow
1. Buka tab **Actions** di repository GitHub.
2. Pilih workflow yang ingin dijalankan ulang.
3. Klik tombol **Re-run jobs**.

---

## 🌐 Endpoint API Server
Pastikan kubeconfig memiliki konfigurasi API server yang benar:
- **Staging**: `https://<staging-cluster-ip>:6443`
- **Production**: `https://<production-cluster-ip>:6443`

---
