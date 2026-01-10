# 🚀 BedulTech Company Profile (DevOps Project)

Project ini adalah implementasi *Modern DevOps Workflow* untuk aplikasi web Company Profile. Menggunakan pendekatan **Infrastructure as Code** dan **Observability Stack**.

## 🏗️ Arsitektur Sistem

Sistem ini berjalan di atas VM Ubuntu 20.04 (Local VirtualBox) dengan eksposur publik via Cloudflare Tunnel.

**Topologi Singkat:**
`User` -> `Cloudflare Tunnel` -> `VM (Docker)` -> `Nginx Containers`

### 🛠️ Tech Stack
| Komponen | Teknologi | Fungsi |
| :--- | :--- | :--- |
| **Containerization** | Docker & Docker Compose | Manajemen environment terisolasi |
| **Web Server** | Nginx (Alpine) | Serving static files (HTML/CSS/JS) |
| **CI/CD** | GitHub Actions (Self-Hosted) | Otomatisasi deployment (Rsync strategy) |
| **Monitoring** | Grafana + Prometheus | Visualisasi metric CPU, RAM, & Disk |
| **Logging** | PLG Stack (Promtail, Loki, Grafana) | Sentralisasi log akses Nginx |
| **Networking** | Tailscale & Cloudflare Zero Trust | Secure public access tanpa buka port router |

---

## 🔄 CI/CD Flow (Deployment Strategy)

Kami menggunakan strategi **Static File Sync** untuk deployment yang super cepat (Zero Downtime).

1. **Dev Push:** Push ke branch `dev` -> Runner melakukan rsync ke folder `/apps/dev` (Port 8080).
2. **Prod Push:** Push ke branch `main` -> Runner melakukan rsync ke folder `/apps/prod` (Port 80).

*Note: Tidak ada rebuild image Docker saat deploy konten, sehingga proses deploy hanya butuh waktu < 3 detik.*

---

## 📊 Monitoring & Logging

Dashboard Grafana terintegrasi menampilkan:
1. **Resource Usage:** Penggunaan CPU dan RAM VM.
2. **Live Logs:** Log akses HTTP dari Nginx yang ditangkap oleh Promtail dan disimpan di Loki.

---

## 💻 Cara Menjalankan (Local Development)

1. Clone repository ini.
2. Edit file yang ada didalam `src`.
3. Push ke branch yang sesuai (`dev` atau `main`).
4. Perubahan akan otomatis terdeploy ke server.