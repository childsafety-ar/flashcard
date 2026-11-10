# Safety Child Transportation — 72 QR Flashcard

**Dokumen pengingat utama untuk pemeliharaan QR permanen (10 November 2026).**

## A. Dua akun GitHub — jangan sampai tertukar

| Peran | Repository | Status |
|---|---|---|
| **PRODUKSI / QR CETAK** | https://github.com/childsafety-ar/flashcard | **WAJIB digunakan bila ingin memperbarui QR yang sudah tercetak** |
| Salinan/cadangan | https://github.com/mis-net1/flashcard-safety-child | Salinan 72 file, tidak otomatis tersinkron |

Akun `childsafety-ar` dan `mis-net1` **berbeda**, meskipun pada audit 10 November 2026, 72 file `index.html` memiliki SHA identik. `mis-net1` telah diundang sebagai collaborator di repository produksi. Status collaborator bukan jaminan aplikasi/connector tertentu diberi izin API untuk menulis.

**QR cetak tetap:** `https://childsafety-ar.github.io/flashcard/<KODE>`.

Contoh: `https://childsafety-ar.github.io/flashcard/A1`.

**Dilarang mengganti** URL cetak, domain GitHub Pages, folder `A1` dan seterusnya, file `index.html`, atau rumus pembangkit QR hanya karena filter TikTok berubah.

## B. Spreadsheet sumber data

https://docs.google.com/spreadsheets/d/1t-MtEQCExRd69u8ph6Vv1COMWmcRZKzIA7hvnpRl5o0/edit

Tab **QR Code**: A = kode, B = judul, C = checklist lama (bukan trigger), D = URL TikTok, E = URL QR permanen, F = status lama, G = formula QR, H = checkbox kirim, I = status sinkronisasi, J = waktu WIB, K = commit GitHub, L = keterangan, M = verifikasi Share Effect.

Tab **Riwayat Sinkronisasi**: audit semua pembaruan, termasuk gagal dan waktu/commit. Tab **Audit 72 QR**: pemetaan kode dan verifikasi. Tab **Panduan Update**: petunjuk operasional yang diperbarui.

Ada **72 QR individu**: A1–A16, B1–B4, C1–C12, D1.1–D5.5, dan E1–E8. Baris D1–D5 adalah judul kelompok, **bukan** QR individu.

## C. Cara rutin mengganti link filter TikTok

**Hanya setelah Apps Script + trigger aktif dan teruji:**

1. Buka TikTok Effect House → Manage Effects → pilih efek yang aktif → Share → Copy Link. Cocokkan nama dengan kode flashcard dan uji di ponsel.
2. Di tab QR Code, cari kode pada kolom A; ganti hanya URL TikTok **kolom D** pada baris tersebut.
3. Centang **H (Kirim ke GitHub)** pada baris yang sama. Checkbox kembali kosong seusai pemrosesan.
4. Periksa **I (status)**, **J (waktu WIB)**, **K (tautan commit)**, **L (keterangan)**, dan tab **Riwayat Sinkronisasi**.
5. Setelah commit sukses dan GitHub Pages menerbitkan perubahannya, uji tautan permanen kolom E serta QR fisik.

- `SUKSES DI GITHUB` = GitHub menerima commit; **belum membuktikan** GitHub Pages atau TikTok dapat dibuka.
- `TIDAK BERUBAH` = URL meta refresh dan JavaScript sudah sama seperti kolom D.
- `GAGAL` = periksa kolom L dan log Apps Script, terutama token/izin GitHub.
- `BELUM DIVERIFIKASI` pada M **bukan** berarti efek mati; berarti belum ada pengujian Share Effect.

**Catatan:** tidak semua 72 efek bisa diverifikasi otomatis melalui profil TikTok. Jangan mengganti URL berdasarkan perkiraan dari nama filter saja.

## D. Satu kali memasang/memperbaiki algoritma Apps Script

1. Sebelum mengedit, cadangkan kode `Kode.gs` dan catat tanggal serta perubahan.
2. Kode sumber referensi bernama `SafetyChild_SinkronQR_72.gs` (paket pemasangan). Script yang benar-benar aktif berada di proyek **Google Apps Script**, bukan file README ini. Mengedit README/GitHub tidak otomatis mengubah proyek Apps Script yang terpasang.
3. Kode harus menggunakan spreadsheet ID `1t-MtEQCExRd69u8ph6Vv1COMWmcRZKzIA7hvnpRl5o0`, tab `QR Code`, repository **`childsafety-ar/flashcard`**, dan domain permanen di atas.
4. Pada Apps Script → Project Settings → Script Properties, simpan `GITHUB_TOKEN` hasil fine-grained PAT dari akun pemilik `childsafety-ar`, hanya untuk repository `flashcard` dengan izin **Contents: Read and write**. **Jangan** masukkan token dalam GitHub, Sheets, file kode, maupun screenshot.
5. Jalankan fungsi `ujiKoneksi`, kemudian `pasangSistem` satu kali. Periksa trigger fungsi `sinkronSaatDicentang` berupa **From spreadsheet → On edit**. Tidak memerlukan Deploy sebagai Web App.
6. Uji **satu** filter yang URL-nya benar-benar aktif; verifikasi commit, publikasi GitHub Pages, dan pemindaian QR fisik. Jangan mengirim seluruh 72 sekaligus sebelum uji ini lolos.
7. Jangan mengubah dua metode redirect secara terpisah: `meta http-equiv="refresh"` dan `window.location.replace(...)` harus menuju URL TikTok yang sama.
8. Saat pemulihan, gunakan riwayat commit pada repository **produksi** dan backup script, jangan memperbaiki masalah dengan membuat QR baru.

## E. Status kerja saat catatan ini ditulis

- Pemetaan 72 kode dan folder: **cocok**; sumber QR cetak adalah `childsafety-ar/flashcard`.
- Dua repository mengandung 72 redirect identik pada audit, tetapi **tidak otomatis saling memperbarui**.
- Spreadsheet telah ditambahkan checkbox H, status I–M, audit dan panduan.
- **Trigger Apps Script belum aktif**; status sementara **menunggu** setup token dan trigger. Jangan klik H dulu.
- Integrasi GitHub ChatGPT mengakui `mis-net1` sebagai collaborator dengan hak push, tetapi saat mencoba menulis README mengembalikan **HTTP 403: Resource not accessible by integration**. Jika ingin menyimpan README ini langsung di repository, buka akun `childsafety-ar`, gunakan **Add file → Create new file** dengan nama `README.md` dan tempel isinya; alternatifnya perbarui izin integrasi GitHub yang terhubung, baru ulangi penulisan.
- Status aktif dari 72 efek TikTok **belum dapat diverifikasi satu per satu lewat menu Share Effect**.

## F. Cara menyimpan catatan ini ke repo tanpa menyentuh QR

1. Masuk `https://github.com/childsafety-ar/flashcard`.
2. Pada tab **Code**, klik **Add file → Upload files**, lalu unggah file `README_SafetyChild_QR.md` ini (atau buat `README.md` via **Create new file** agar tampil sebagai halaman utama repo).
3. Isi commit message misalnya `docs: catat repo produksi dan prosedur update 72 QR`.
4. Klik **Commit changes**. Pastikan hanya file dokumentasi yang berubah, **bukan** 72 file `index.html`.

Simpan file panduan ini bersama arsip proyek sebagai pengingat jika kelak akun, developer, atau pengelola konten berganti.
