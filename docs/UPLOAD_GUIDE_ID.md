# Panduan unggah ke GitHub

## Nama dan deskripsi

Nama yang disarankan: `ELECTRA-BiLSTM-MMCRF-ForensicNER`

Deskripsi singkat untuk kolom About/Description:

> Research code for forensic software feature extraction from news using ELECTRA, BiLSTM, a custom masked CRF, and an auxiliary MoM loss.

Topics: `named-entity-recognition`, `electra`, `bilstm`, `crf`, `pytorch`, `information-extraction`, `forensic`

## Unggah melalui browser

1. Ekstrak ZIP. Buka folder `ELECTRA-BiLSTM-MMCRF-GitHub`.
2. Login ke GitHub, buat repository baru dengan nama di atas dan tempel deskripsi.
3. Pilih Private untuk draf atau Public jika memang akan dirilis. Jangan membuat README otomatis karena paket sudah memilikinya. Tentukan lisensi hanya jika Anda sudah menetapkan hak penggunaan kode.
4. Pilih tautan upload an existing file pada repository kosong, atau Add file → Upload files pada repository berisi file.
5. Unggah ISI folder hasil ekstraksi, bukan ZIP dan bukan folder pembungkusnya. Pastikan README.md berada langsung pada root repository. Sertakan .gitignore; aktifkan tampilan file tersembunyi bila perlu.
6. Gunakan pesan commit `Add notebook and research documentation`, lalu commit.
7. Periksa tampilan README, notebook, folder data, dan panduan. Tambahkan topics di About.

## Alternatif melalui Git

Jalankan dari folder hasil ekstraksi. Ganti YOUR_USERNAME dengan akun Anda dan buat repository kosong di GitHub terlebih dahulu.

```bash
git init
git branch -M main
git add .
git commit -m "Add notebook and research documentation"
git remote add origin https://github.com/YOUR_USERNAME/ELECTRA-BiLSTM-MMCRF-ForensicNER.git
git push -u origin main
```

## Sebelum rilis penelitian

Baca KNOWN_LIMITATIONS.md. Notebook unggahan ini masih versi sebelum perbaikan word-level. Paket ini siap diunggah sebagai snapshot kode, tetapi belum membuktikan reproduksibilitas hasil jurnal. Tambahkan identitas publikasi, lisensi yang Anda pilih, prosedur memperoleh dataset, dan versi environment setelah terverifikasi.

Full dataset dan checkpoint tidak disertakan. .gitignore berlaku pada Git, bukan penyaringan otomatis untuk unggahan manual browser: pilih file browser dengan teliti.
