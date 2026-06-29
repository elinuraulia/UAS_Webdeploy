### Draf `README.md` (Copy-Paste ke proyekmu)

```markdown
# 🚀 Deployment Proyek UAS: Web Portofolio

Repositori ini mendokumentasikan sistem deployment otomatis untuk aplikasi web statis sebagai pemenuhan tugas akhir mata kuliah **Sistem Operasi (MITI.202)** dan **Jaringan Komputer (MITI.203)**, STMIK Tazkia.

---

## 📌 Deskripsi Sistem
Aplikasi ini merupakan profil IT Student yang di-host pada environment produksi di VPS dengan konfigurasi:
* **Web Server:** Nginx (Reverse Proxy)
* **SSL:** Terjamin melalui Certbot (HTTPS)
* **Container:** Docker & Docker Compose
* **Automasi:** CI/CD via GitHub Actions
* **Monitoring:** Uptime Kuma (Real-time tracking)
* **Data Safety:** Backup otomatis via cron job

---

## 🏗️ Alur Arsitektur (Workflow)

Sistem menggunakan alur pengembangan *continuous deployment* sebagai berikut:

1. **Commit & Push:** Developer mengirim perubahan kode ke branch `main`.
2. **CI/CD Pipeline:** GitHub Actions secara otomatis membangun image aplikasi dan melakukan deployment via SSH ke VPS.
3. **Serving:** Nginx melayani request user dan meneruskannya (reverse proxy) ke container aplikasi.
4. **Maintenance:** Uptime Kuma memonitor ketersediaan aplikasi, sementara *cron job* memastikan data terbackup ke *cloud storage*.

---

## 📁 Struktur Repositori

```text
.
├── .github/workflows/  # CI/CD Pipeline (otomasi deployment)
├── html/               # Source code website (static files)
├── docker-compose.yml  # Definisi service container
└── README.md           # Dokumentasi proyek

```

---

## ⚙️ Ringkasan Konfigurasi

| Komponen | Spesifikasi |
| --- | --- |
| Domain | `[isi-domain-kamu.com]` |
| IP Server | `103.168.146.195` |
| Port Utama | 80/443 (HTTP/HTTPS) |
| Monitoring | `http://103.168.146.195:3010` |

---

## 🛠️ Runbook Operasional

### 1. Prosedur Restart

Jika layanan mengalami kendala, lakukan restart container melalui terminal VPS:

```bash
cd /home/eliaulia/UAS_WEB
docker-compose restart [nama-service]

```

### 2. Prosedur Restore (Recovery)

Apabila terjadi kehilangan data, gunakan file backup harian di direktori `/home/eliaulia/`:

```bash
# Ekstrak backup
tar -xzvf backup_YYYY-MM-DD.tar.gz

# Pindahkan ke folder web
cp -r hasil_ekstrak/* /home/eliaulia/UAS_WEB/html/

```

### 3. Monitoring & Logging

* **Dashboard:** Cek kesehatan sistem melalui dashboard Uptime Kuma.
* **Log:** Gunakan `docker logs <nama-container>` untuk melihat aktivitas aplikasi atau `tail -f /var/log/nginx/error.log` untuk masalah server.

---

## 🛡️ Troubleshooting Skenario Umum

* **Aplikasi tidak bisa diakses:** Cek status container dengan `docker ps` dan pastikan firewall mengizinkan port 80/443 (`ufw status`).
* **Error CI/CD:** Periksa *log* di tab "Actions" pada repositori GitHub untuk melihat *step* mana yang gagal.
* **Sertifikat SSL expired:** Jalankan `certbot renew --nginx` secara manual untuk memperbaharui sertifikat.

---

*Dibuat oleh: Eli Nur Aulia*

```

---

### Langkah Selanjutnya:
1.  **Simpan:** Simpan teks di atas ke dalam file `README.md` di laptopmu.
2.  **Push:** Jalankan perintah berikut di terminal VS Code:
    ```bash
    git add README.md
    git commit -m "Update dokumentasi README UAS"
    git push origin main
    ```
3.  **Cek GitHub:** Sekarang repositori GitHub kamu sudah terlihat rapi dan lengkap sesuai standar UAS.

Apakah ada bagian dari runbook ini yang ingin kamu tambahkan atau ubah agar lebih sesuai dengan kondisi servermu saat ini?

```