# mcpena (Make Container/Pod Enabled)
*Baca dalam bahasa lain: [English](README.md)*

`mcpena` adalah sebuah shell script untuk mengotomatisasi proses pembuatan *service startup* (agar otomatis berjalan saat *boot/reboot*) untuk container atau pod yang dibuat menggunakan **Podman** atau **Docker**. 

## Fitur Utama
1. **Deteksi OS dan Sistem Init**: Mendukung deteksi otomatis sistem operasi Linux Anda (mendukung deteksi `systemd`, `OpenRC`, dan `SysVinit`).
2. **Dukungan Podman & Docker**: Secara otomatis mendeteksi apakah container Anda berada di Podman atau Docker. 
3. **Kompatibilitas Versi Podman**: Mendukung perintah `podman generate systemd` (untuk podman versi lawas) dan memiliki mekanisme *fallback* untuk podman versi terbaru (v5+) yang perintah tersebut sudah di-*deprecated*/*removed*.
4. **Deteksi Level User**: Mendukung penyesuaian otomatis untuk eksekusi sebagai `root` (system-wide service) maupun eksekusi sebagai *user* biasa (`rootless` dengan `systemctl --user`).
5. **Kustomisasi Docker**: Memungkinkan Anda untuk memilih apakah akan menggunakan *Docker Restart Policy* (secara *default* lebih disarankan di Docker) atau memaksa agar dibuatkan *Systemd Service* untuk Docker.
6. **Penamaan Cerdas & Anti Bentrok**: Secara otomatis menyederhanakan nama service yang dihasilkan (membuang awalan seperti `container-` atau `pod_`), mencegah file tertimpa secara tidak sengaja, dan mendukung pemberian nama kustom melalui opsi `--name`.

## Instalasi

Unduh script `mcpena`, beri hak akses *executable*, dan letakkan di folder bin sistem agar bisa dipanggil darimana saja.

```bash
curl -O https://raw.githubusercontent.com/salmankalista/mcpena/master/mcpena
chmod +x mcpena
sudo mv mcpena /usr/local/bin/
```

## Cara Penggunaan

Penggunaan dasar (script akan otomatis mendeteksi *engine*, sistem init, dan user):
```bash
mcpena nama-container-anda
```

Menjalankan service secara langsung (setelah *enable* via opsi `--now`):
```bash
mcpena nama-container-anda --now
```

### Opsi Tambahan / Lanjutan

Anda dapat menentukan *engine*, metode, atau nama service secara eksplisit jika diperlukan:

```bash
# Menentukan nama service kustom (misal: menghasilkan 'my-app.service' alih-alih 'web-server.service')
mcpena web-server --name my-app

# Memaksa menggunakan engine Podman
mcpena web-server --engine podman

# Memaksa menggunakan engine Docker
mcpena db-server --engine docker

# Untuk Docker, secara default menggunakan fitur 'restart policy'. 
# Jika ingin dibuatkan systemd service untuk Docker:
mcpena cache-server --engine docker --method systemd
```

## Dukungan & Traktir Kopi ☕

Jika script ini membantu pekerjaan Anda dan menghemat waktu Anda, silakan dukung pengembang melalui tautan berikut:
- **Ko-fi**: [https://ko-fi.com/abgtg](https://ko-fi.com/abgtg)
- **Saweria**: [https://saweria.co/abggtg](https://saweria.co/abggtg)

Terima kasih atas dukungan Anda!
