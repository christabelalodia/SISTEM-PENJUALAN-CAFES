# Ruang Rasa

Web app sederhana untuk penjualan makanan/minuman ke cafe dan persediaan bahan baku.

## Struktur

- `frontend/` - HTML, CSS, dan JavaScript dashboard.
- `backend/app.js` - server Node.js tanpa dependency eksternal.
- `backend/schema.sql` - tabel, data awal, dan fungsi transaksi produksi untuk Supabase/Postgres.

## Menjalankan

### Menghubungkan langsung ke Supabase (tanpa instalasi)

1. Jalankan seluruh `backend/schema.sql` di Supabase SQL Editor. File ini membuat tabel, data awal, dan fungsi produksi `record_production` dalam satu langkah.
   - Jika tabel `production_records` sudah ada, SQL ini juga melengkapi kolom yang diperlukan (`product_id`, `product_name`, `quantity`, dan `created_at`).
2. Buka `frontend/index.html` di browser.
3. Pada dialog **Hubungkan Supabase**, masukkan **Project URL** dan **anon/publishable key** dari Supabase → **Project Settings → API**.
4. Simpan koneksi. Data berikutnya akan dibaca dan ditulis langsung oleh browser ke Supabase. Pengaturan koneksi disimpan di browser ini.

### Menjalankan dari GitHub Pages

1. Unggah file `index.html` dan `app.js` dari root proyek ini ke root repository pada branch `main`. Jika file bernama sama sudah ada, timpa dengan versi terbaru.
2. Pastikan file `styles.css`, `theme.css`, dan `logo-cafe.png` juga berada di root repository. GitHub Pages peka terhadap huruf besar/kecil pada nama file.
3. Di repository, buka **Settings → Pages**, pilih **Deploy from a branch**, lalu pilih branch `main` dan folder `/(root)`.
4. Buka URL GitHub Pages. Untuk menyimpan data bersama di cloud, hubungkan Supabase dari tombol **Hubungkan Supabase**. Tanpa Supabase, data hanya tersimpan di browser/perangkat yang sedang digunakan.

Jangan masukkan `service_role` atau secret key ke aplikasi browser. Kebijakan RLS di skema contoh mengizinkan akses umum untuk penggunaan lokal; batasi kebijakan tersebut sebelum mempublikasikan aplikasi. Jika koneksi ditolak, periksa kebijakan RLS dan izin tabel di Supabase. Tanpa konfigurasi Supabase, aplikasi tetap bisa dipakai dalam mode lokal; data lokal tidak otomatis disalin ke cloud.

`backend/app.js` tetap tersedia sebagai opsi bila Node.js sudah terpasang, tetapi tidak diperlukan untuk koneksi browser langsung.

Model data menggunakan empat entitas: `raw_materials`, `products`, `orders`, dan `production_records`. Resep produk serta detail item pesanan disimpan sebagai JSONB, sedangkan setiap produksi dicatat sebagai riwayat pada `production_records`.
