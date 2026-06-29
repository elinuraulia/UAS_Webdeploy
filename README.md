# UAS Web Deployment - Eli Nur Aulia

## 1. Arsitektur Sistem
- **Flow:** Developer (`git push`) -> GitHub Actions (CI/CD) -> VPS (`docker-compose`) -> HTTPS (Nginx).
- **Monitoring:** Uptime Kuma melakukan polling setiap menit (Port 3010).

## 2. CI/CD Pipeline
Otomatisasi dijalankan via GitHub Actions setiap kali ada perubahan pada branch `main`. Pipeline melakukan SSH ke VPS, menarik kode terbaru, dan melakukan restart pada container aplikasi.

## 3. Runbook (Operational Procedures)
- **Restart Aplikasi:** `docker-compose restart web-uas`
- **Cek Log:** `docker logs web-uas`
- **Prosedur Backup:** Sistem melakukan backup harian ke folder lokal via cron job: `0 2 * * * tar -czvf /home/eliaulia/backup_$(date +\%F).tar.gz /home/eliaulia/UAS_WEB/html`
- **Prosedur Restore:** Ekstrak file backup (`tar -xzvf backup_file.tar.gz`) dan salin kembali ke direktori `/html`.

## 4. Troubleshooting
- **Error 403:** Masalah permission, gunakan `chmod -R o+rx html/`.
- **Layanan Down:** Periksa status dengan `docker ps` dan jalankan `docker-compose up -d`.