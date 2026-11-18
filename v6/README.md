# PBB SEWAN 6.0 — Catatan Uji Coba

> Status: pengembangan dan pengujian. Jangan merge ke `main` atau menggantikan aplikasi 5.1 sebelum seluruh uji akhir lulus.

## Batas aman
- Aplikasi stabil 5.1 tetap berada di `/index.html`; versi 6.0 dikembangkan terpisah di `/v6/index.html`.
- Browser hanya menggunakan Supabase Project URL dan publishable key. Jangan pernah memasukkan `service_role` atau secret key ke HTML.
- Gunakan data uji untuk pengujian tambah, edit, hapus, pembayaran, dan restore. Jangan menghapus atau memulihkan data penting saat uji coba.
- Backup dan restore seluruh dusun hanya untuk Admin Utama. Restore menggabungkan atau memperbarui data yang cocok; data yang tidak ada di file backup tidak dihapus.
- File foto bukti tidak ikut masuk ke JSON backup. Yang tersimpan di backup hanya path foto.
- Kepala Dusun hanya boleh mengakses wajib pajak, pembayaran, riwayat, dan foto pada RT yang ditugaskan.
- Fitur metode pembayaran, status setoran, rekap posisi uang, pencatatan setoran, dan catatan dusun tidak digunakan di 6.0.

## Fitur yang tersedia di 6.0
- Login Supabase Auth, pendaftaran mandiri Kepala Dusun, dan pergantian kata sandi sementara.
- Admin Utama dapat membuat dusun, membuat akun Kepala Dusun, menyetujui/menolak permohonan, mengaktifkan/nonaktifkan akun, dan mengatur penugasan RT.
- Master wilayah sudah berisi 16 dusun dan 54 RT desa (RT 01–54 dengan pembagian sesuai daftar resmi, termasuk RT 51 dan 54 pada Jurusawah serta RT 52–53 pada Ngemplak).
- Saat membuat akun Kepala Dusun, pilihan RT hanya berasal dari master RT dusun yang dipilih. RT yang sudah ditugaskan tidak ditawarkan lagi.
- Penugasan RT dibatasi agar satu nomor RT hanya dapat ditugaskan kepada satu akun Kepala Dusun. Foreign key database memastikan RT yang ditugaskan benar-benar milik dusun tersebut.
- Data wajib pajak: tambah, edit seluruh kolom, hapus, pencarian nama/Nama sekarang/NOP/NOPD, filter status dan RT, serta pilihan data.
- Pembayaran sederhana: Catat Lunas atau Batalkan Lunas. Tidak ada pilihan Tunai/Online atau Setor/Belum Setor.
- Unggah dan lihat foto bukti pada penyimpanan privat.
- Dashboard, laporan per tahun/RT, cetak laporan, rekap per pemilik, ekspor CSV/JPG, bukti pembayaran, dan berbagi pilihan melalui WhatsApp.
- Riwayat perubahan wajib pajak dan pembayaran.
- Backup/restore JSON khusus Admin Utama.

## Urutan uji dari Android
1. Buka preview branch `pengembangan-v6`, bukan halaman utama 5.1.
2. Hubungkan menggunakan URL proyek dan publishable key.
3. Login Admin Utama dan pastikan panel Admin Utama tampil.
4. Pilih Dusun Sewan dan buka dusun. Pastikan dashboard, jumlah wajib pajak, target, lunas, dan belum lunas cocok dengan data.
5. Uji pencarian dengan nama, nama sekarang, NOP, dan NOPD; uji filter status dan RT.
6. Dengan data uji, coba tambah, edit semua kolom, dan hapus satu data uji. Pastikan riwayat mencatat perubahan.
7. Uji Catat Lunas dan Batalkan Lunas. Pastikan tanggal dan jumlah bayar terisi saat lunas dan dikosongkan saat dibatalkan.
8. Uji unggah foto bukti dan tombol Lihat Foto.
9. Uji laporan, filter RT/status, rekap per pemilik, cetak, CSV, JPG, bukti pembayaran, dan WhatsApp.
10. Unduh backup JSON. Lakukan restore hanya dengan file uji dan pastikan data yang tidak ada di backup tidak terhapus.
11. Di panel Admin Utama, pastikan daftar dusun menampilkan RT resmi sesuai pembagian wilayah.
12. Buat akun Kepala Dusun uji. Pilih dusun, lalu centang hanya RT yang muncul dari master wilayah. Pastikan RT yang sudah ditugaskan tidak muncul lagi.
13. Di bagian Atur Wilayah RT, pastikan hanya RT resmi dusun tersebut yang dapat dipilih. Coba pastikan satu RT tidak dapat ditugaskan ke akun lain.
14. Login menggunakan akun Kepala Dusun uji. Pastikan hanya data RT yang ditugaskan yang terlihat dan backup/restore tidak tersedia.
15. Uji dua akun Kepala Dusun dengan RT berbeda untuk memastikan keduanya tidak dapat saling melihat atau mengubah data.
16. Uji keluar, login ulang, dan ganti kata sandi sementara.

## Status verifikasi yang sudah tercatat
- Login Admin Utama pada preview berhasil.
- Data Dusun Sewan terbaca dan dashboard/laporan pernah cocok dengan aplikasi 5.1.
- Simulasi RLS Admin Utama sebelumnya berhasil membaca data wajib pajak dan pembayaran.
- Dry-run backup/restore sebelumnya berhasil diproses dalam transaksi yang di-rollback.
- Pemeriksaan HTML sebelumnya tidak menemukan ID ganda atau referensi ID statis yang hilang.
- Supabase Storage untuk bukti bersifat privat dan dibatasi tipe gambar serta ukuran file.
- Master wilayah 16 dusun/54 RT sudah diverifikasi di Supabase. Penugasan akun Kepala Dusun dan isolasi antar-akun masih harus diuji melalui dua akun nyata.
- Foto, cetak/JPG di Android, serta restore browser nyata tetap harus diselesaikan.
- Supabase Free tidak menyediakan perlindungan kata sandi bocor HaveIBeenPwned; fitur ini memerlukan paket Pro atau lebih tinggi. Ini bukan penghalang teknis untuk menjalankan aplikasi.

## Catatan
Peringatan Security Advisor tentang fungsi SECURITY DEFINER dan beberapa peringatan performa masih perlu ditinjau satu per satu. Jangan menghapus atau mengubah kebijakan RLS/fungsi hanya untuk menghilangkan peringatan, karena sebagian fungsi memang diperlukan oleh alur aplikasi dan harus tetap memiliki pemeriksaan peran di dalamnya.
