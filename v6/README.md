# PBB SEWAN 6.0 — Catatan Uji Coba

> Status: pengembangan. Belum untuk dipakai sebagai aplikasi utama dan belum boleh di-merge ke `main`.

## Batas aman
- Aplikasi stabil 5.1 tetap berada di `/index.html`; pengembangan 6.0 ada di `/v6/index.html`.
- 6.0 memakai Supabase Auth dan hanya boleh memakai URL proyek serta publishable key di browser. Jangan pernah menaruh `service_role` atau secret key di HTML.
- Gunakan data uji saat mencoba fitur tulis. Jangan menguji hapus atau restore pada data penting.
- Backup/restore seluruh dusun hanya untuk Admin Utama. Restore menggabungkan/memperbarui data yang cocok; data yang tidak ada di backup tidak dihapus.
- File foto sebenarnya tidak ikut masuk ke JSON backup. Yang tersimpan hanya path foto.
- Kepala Dusun hanya dapat mengakses wajib pajak, pembayaran, riwayat, dan foto pada RT yang ditugaskan. Catatan dan register setoran merupakan data bersama tingkat dusun.
- Register setoran bank terpisah dari transaksi pembayaran dan tidak otomatis mengubah status pembayaran.

## Urutan uji dari Android
1. Buka halaman preview branch/deploy preview yang disediakan hosting untuk branch `pengembangan-v6`; jangan buka aplikasi utama 5.1 untuk pengujian ini.
2. Masukkan Supabase Project URL dan publishable key, lalu hubungkan.
3. Login sebagai Admin Utama.
4. Pilih dusun yang sudah memiliki pengelola, lalu buka dusun.
5. Uji tambah wajib pajak dengan NOP uji, RT yang memang ditugaskan, nominal, dan nama.
6. Uji pencatatan pembayaran Khanief dan Online, pembatalan lunas, filter status/metode/RT, laporan, CSV, cetak, dan JPG.
7. Uji foto bukti dengan gambar uji; pastikan tombol Lihat Foto dapat membuka foto.
8. Uji catatan dusun dan pencatatan setoran dengan data uji.
9. Unduh backup JSON. Periksa file tersedia, lalu lakukan dry-run/pengujian restore hanya pada data uji.
10. Buat akun Kepala Dusun uji dari panel Admin Utama atau lakukan pendaftaran mandiri. Jika mendaftar mandiri, Admin Utama pilih dusun tujuan yang benar saat menyetujui.
11. Tetapkan RT untuk akun uji. Login dengan akun tersebut dan pastikan hanya data RT yang ditugaskan yang terlihat.
12. Pastikan akun Kepala Dusun tidak dapat membuka backup/restore seluruh dusun atau data RT lain.

## Belum diverifikasi di browser nyata
- Login dan pembuatan akun Kepala Dusun end-to-end.
- Isolasi RT antar dua akun berbeda.
- Upload dan tampilan foto pada Android.
- Cetak dan ekspor JPG pada browser Android.
- Alur backup/restore dengan data uji lengkap.
- Audit akhir peringatan keamanan Supabase. Leaked-password protection HaveIBeenPwned tidak aktif karena fitur tersebut memerlukan paket Pro atau lebih tinggi.

## Pemeriksaan teknis yang sudah dilakukan
- Sintaks JavaScript halaman 6.0 valid.
- Referensi ID statis tidak ada yang hilang dan tidak ada ID HTML duplikat.
- Simulasi RLS Admin Utama membaca 2 wajib pajak dan 7 pembayaran.
- Dry-run backup/restore memproses 2 wajib pajak dan 7 pembayaran dalam transaksi yang di-rollback.
- Dry-run tambah catatan/setoran dan persiapan pembayaran berjalan dalam transaksi rollback.
