# Warungin — Multi‑Store UMKM Management SaaS

Warungin adalah aplikasi web untuk membantu pelaku UMKM mengelola **multi‑toko**: produk & stok, transaksi penjualan, pelanggan, laporan, sampai pembayaran online terintegrasi.

> **SaaS Model:** Gratis hingga **5 produk** per UMKM. Untuk menampilkan lebih banyak produk, biaya **Rp50.000/bulan/UMKM**.

---

## ✨ Fitur Utama

* **Manajemen Produk & Stok**: kategori, varian, stok in/out, penyesuaian stok.
* **Transaksi Penjualan**: pencatatan penjualan, diskon, pajak, cetak struk.
* **Customer Management (CRM ringan)**: data pelanggan & riwayat belanja.
* **Multi Toko / Cabang**: satu akun UMKM dapat memiliki beberapa toko.
* **Dashboard & Laporan**: penjualan, produk terlaris, pelanggan aktif.
* **Payment Gateway (Midtrans)**: Snap/VT-Web, status pembayaran & notifikasi.
* **Subscription SaaS**: pembatasan produk free tier, penagihan bulanan.
* **Admin Panel** (Filament): kelola pengguna, toko, langganan, dan konfigurasi.

> Catatan: Beberapa fitur lanjutan seperti pembelian/supplier, multi‑gudang, PWA POS offline-first — berada di roadmap.

---

## 🧰 Tech Stack

* **Backend**: Laravel **12** (PHP **8.3+**)
* **Frontend**: Inertia.js (**React + Vite**), Tailwind CSS
* **Admin**: **Filament v3**
* **Database**: MySQL 8+
* **Payments**: Midtrans (Snap, Notifications)
* **Optional**: Redis (cache/queue), Docker, Nginx

---

## 🏗️ Arsitektur Singkat

* **Domain utama**: UMKM (tenant ringan) → Store (toko) → Product, Inventory, Transaction, Customer.
* **SaaS Guard**: policy & middleware membatasi jumlah produk pada free tier.
* **Pembayaran**: integrasi Midtrans untuk order subscription & penandaan status.
* **UI/UX**: Inertia React untuk halaman pengguna, Filament untuk panel admin.

---

## 🔐 Peran & Hak Akses

* **Super Admin**: manajemen sistem, UMKM, billing, konfigurasi global (Filament).
* **Owner UMKM**: kelola toko, produk, stok, transaksi, pelanggan, laporan.
* **Staf/Kasir**: akses POS/penjualan & stok terbatas.

> *Customer* di sini berupa entri CRM (bukan akun login) untuk rekam riwayat belanja.

---

## 🚀 Quick Start

### Prasyarat

* PHP 8.3+, Composer 2.x
* Node.js 20+ (NPM/PNPM/Bun), Vite
* MySQL 8+

### Instalasi

```bash
# 1) Clone repo
git clone https://github.com/<org-or-username>/warungin.git
cd warungin

# 2) Environment
cp .env.example .env

# 3) Backend deps
composer install
php artisan key:generate

# 4) Database
php artisan migrate --seed
php artisan storage:link

# 5) Frontend deps
npm install
npm run dev   # atau npm run build untuk produksi

# 6) Jalankan server
php artisan serve
```

> Seeder menyiapkan data contoh (role, toko, produk, dsb.) — lihat `database/seeders`.

---

## ⚙️ Konfigurasi Environment

Contoh `.env` penting:

```env
APP_NAME="Warungin"
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=warungin
DB_USERNAME=root
DB_PASSWORD=

QUEUE_CONNECTION=database
CACHE_DRIVER=file
SESSION_DRIVER=file

# Midtrans
MIDTRANS_IS_PRODUCTION=false
MIDTRANS_SERVER_KEY=your_server_key
MIDTRANS_CLIENT_KEY=your_client_key
MIDTRANS_MERCHANT_ID=your_merchant_id

# SaaS
SUBSCRIPTION_FREE_PRODUCT_LIMIT=5
SUBSCRIPTION_PRICE_MONTHLY=50000
```

**Webhook/Callback Midtrans**: arahkan notifikasi ke endpoint aplikasi (mis. `/payments/midtrans/notify`). Pastikan URL publik dapat diakses Midtrans.

---

## 🧾 Aturan Bisnis (Ringkas)

* Free tier: maksimal **5 produk** per **akun UMKM** (lintas toko). Upgrade membuka limit.
* Biaya langganan: **Rp50.000/bulan/UMKM** (harga dapat disesuaikan via konfigurasi/admin).
* Multi‑toko: setiap transaksi & stok selalu terikat ke `store_id`.

---

## 🧪 Testing & QA

```bash
# Linting & Static Analysis (opsional)
./vendor/bin/pint
./vendor/bin/phpstan analyse

# Test
php artisan test
```

---

## 🗺️ Roadmap Pendek

* POS layar kasir (touch‑friendly), barcode/QR printing
* Pembelian & Supplier, penyesuaian biaya (COGS)
* Multi‑gudang & transfer stok antar toko
* PWA offline-first untuk transaksi
* Integrasi WhatsApp (nota & pengingat)
* Laporan keuangan lanjutan (arus kas, profit per toko)

---

## 🤝 Kontribusi

Kontribusi sangat terbuka!

1. Fork & buat branch fitur: `feat/nama-fitur`
2. Gunakan **Conventional Commits**
3. Buka Pull Request disertai deskripsi & screenshot/video

---


## 💬 Dukungan

Pertanyaan & diskusi: buka **Issues** atau **Discussions** di GitHub repo ini.

> Dibangun untuk mendukung digitalisasi UMKM Indonesia — cepat, sederhana, dan terukur.
