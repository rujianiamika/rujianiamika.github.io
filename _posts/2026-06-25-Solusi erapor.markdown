---
layout: post
title: "Solusi Mudah Mengembalikan Environment Variable PATH Windows yang Hilang Akibat eRapor SD"
date: 2026-06-25 11:00:00 +0700
categories: Tutorial, Erapor
tags: erapor sd, windows, tips, operator sekolah
author: "Operator Sekolah"
---

Halo rekan-rekan operator sekolah (ops) seluruh Indonesia! Semoga tetap semangat ya ngurusin data dapodik, arkas, dan perintilan administrasi sekolah lainnya. 

Pernah nggak sih, setelah install atau malah setelah *uninstall* aplikasi **eRapor SD Versi 2025.1**, tiba-tiba laptop atau komputer server sekolah jadi aneh? Mau ngecek koneksi jaringan pakai perintah `ping` di Command Prompt (CMD) nggak bisa, mau cek IP pakai `ipconfig` error, bahkan perintah dasar kayak `wmic` atau `systeminfo` juga ikutan mogok. 

Kalau rekan-rekan ngalamin hal ini, jangan panik dulu sampai kepikiran instal ulang Windows ya! Masalah ini terjadi karena **Variable PATH Windows** terhapus secara tidak sengaja oleh sistem installer aplikasi tersebut.

Yuk, kita bahas santai penyebabnya dan bagaimana cara gampang mengembalikannya lewat panduan di bawah ini!

---

### Kenapa Kok Bisa Terhapus? (Biar Nggak Penasaran)

Biar tambah ilmu, kita cari tahu dulu nih biang keroknya. Berdasarkan bedah sistem, ada dua penyebab utama kenapa hal ini bisa terjadi:

1. **Kesalahan Script Batch (.bat):** Di dalam file installer, ada perintah yang tujuannya mendaftarkan folder aplikasi ke dalam sistem Windows. Sayangnya, penulisan tanda kutip atau perintah modifikasi registry-nya kurang tepat, sehingga bukannya *menambahkan* data baru, script tersebut malah *menimpa (overwrite)* seluruh PATH bawaan Windows.
2. **Konfigurasi Inno Setup yang Keliru:** Saat proses *uninstall*, ada perintah `uninsdeletevalue` pada registry PATH. Efeknya fatal, sistem mengira harus menghapus seluruh isi PATH, padahal di sana ada lokasi folder krusial milik Windows itu sendiri (seperti folder `System32`).

Akibatnya, Windows jadi kebingungan mencari letak perintah dasar seperti `ping.exe` atau `ipconfig.exe` karena peta jalannya (PATH) hilang total.

---

### Cara Mengembalikan PATH Windows yang Hilang (Paling Aman untuk Pemula)

Cara paling aman dan direkomendasikan adalah menggunakan tampilan grafis (**GUI**). Cara ini sangat ramah untuk operator sekolah karena kita tidak perlu ketik-ketik perintah rumit di CMD atau otak-atik registry secara langsung yang berisiko.

Silakan ikuti langkah-langkah simpel berikut:

#### Langkah 1: Masuk ke Menu Environment Variables
1. Klik tombol **Start** Windows atau tekan tombol Windows di keyboard.
2. Ketik kata kunci: `Environment Variables`.
3. Pilih menu **"Edit the system environment variables"** yang muncul.
4. Jendela baru bernama *System Properties* akan terbuka. Langsung saja klik tombol **"Environment Variables..."** yang ada di bagian bawah.

#### Langkah 2: Edit Bagian System Variables
1. Perhatikan kotak bagian bawah yang berjudul **System variables**.
2. Cari variabel yang bernama **`Path`** (atau `PATH`), klik satu kali pada nama tersebut sampai tersorot.
3. Klik tombol **Edit...**.

#### Langkah 3: Isi Kembali Nilai Default Windows
Jika setelah diklik isi di dalamnya kosong, atau hanya tersisa folder eRapor saja, berarti PATH bawaan Windows memang sudah terhapus. 

Nah, sekarang tugas kita adalah memasukkan kembali baris-baris standar bawaan Windows. Klik tombol **New** di sebelah kanan, lalu masukkan baris-baris berikut satu per satu:

* `C:\Windows\System32`
* `C:\Windows`
* `C:\Windows\System32\Wbem`
* `C:\Windows\System32\WindowsPowerShell\v1.0\`
* `C:\Windows\System32\OpenSSH\`

> **Tips Tambahan:** Jika aplikasi eRapor SD masih terpasang dan ingin tetap bisa diakses dengan normal, masukkan juga baris lokasi PHP eRapor Anda, contohnya:
> `C:\newappraporsd2025\php` (sesuaikan dengan folder instalasi di komputer Anda).

#### Langkah 4: Simpan dan Restart
1. Setelah semua baris di atas dimasukkan, klik tombol **OK**.
2. Klik **OK** lagi pada jendela Environment Variables.
3. Klik **OK** sekali lagi pada jendela System Properties.
4. Terakhir, **Restart (Mulai Ulang)** komputer server atau laptop Anda agar perubahan ini diterapkan secara sempurna oleh Windows.

---

### Cara Alternatif (Bagi yang Suka Copy-Paste Teks)

Jika menu edit di komputer Anda tampilannya berupa satu baris teks panjang (biasanya pada Windows versi lama), rekan-rekan bisa langsung menyalin (*copy*) baris teks di bawah ini dan menempelkannya (*paste*) ke dalam nilai variable tersebut:

```text
C:\Windows\System32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Windows\System32\OpenSSH\;C:\newappraporsd2025\php