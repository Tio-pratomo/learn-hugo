---
Title: "Menggunakan Theme Di Hugo"
Weight: 4
---

Di sesi ini, kita akan membahas cara menambahkan dan mengelola tema Hugo menggunakan **Git submodule**. Metode ini sangat direkomendasikan karena memudahkan Anda untuk memperbarui tema di masa mendatang.

## Menemukan Tema yang Tepat

Hugo memiliki galeri tema resmi yang berisi banyak pilihan. Anda bisa melihat pratinjau dan memilih tema yang sesuai dengan kebutuhan Anda.

- Kunjungi **Galeri Tema Hugo** di [https://themes.gohugo.io/](https://themes.gohugo.io/).

- Temukan tema yang Anda suka, lalu klik tombol **Download**. Ini akan membawa Anda ke repositori GitHub tema tersebut.

Di halaman GitHub, cari dan salin URL repositori. Ini adalah URL yang akan kita gunakan untuk menambahkan tema sebagai submodule.

## Metode Instalasi Tema

Ada tiga cara utama untuk menginstal tema, masing-masing dengan kelebihan dan kekurangannya.

### a. Metode Git Submodule (Paling Direkomendasikan)

Ini adalah metode terbaik dan paling profesional untuk mengelola tema. Ia mengintegrasikan repositori tema sebagai sub-proyek di dalam proyek utama Anda.

- **Cara Instalasi** : Buka terminal di direktori utama proyek Anda, lalu jalankan `git submodule add <URL_repositori_tema> themes/<nama-folder-tema>`.
- **Kelebihan** :
  - **Mudah Diperbarui** : Anda bisa memperbarui semua tema (submodule) sekaligus hanya dengan satu perintah dari direktori utama proyek Anda: `git submodule update --remote --merge`.
  - **Versi Terkelola** : Proyek utama Anda mencatat versi (commit) spesifik dari tema yang Anda gunakan. Ini sangat penting untuk konsistensi dan kolaborasi tim.
- **Kekurangan**: Membutuhkan pemahaman dasar tentang Git.

---

### b. Metode Git Clone (Tidak Direkomendasikan)

Metode ini menggunakan perintah `git clone` untuk menyalin repositori tema.

- **Cara Instalasi** : Buka terminal, masuk ke folder `themes`, lalu jalankan `git clone <URL_repositori_tema>`.
- **Kelebihan** : Proses instalasi terlihat cepat di awal.
- **Kekurangan** :
  - **Sulit Diperbarui** : Meskipun tema berada dalam repositori Git-nya sendiri, proyek utama Anda tidak mencatatnya sebagai bagian dari proyek. Untuk memperbarui, Anda harus masuk ke dalam folder tema dan menjalankan `git pull` secara manual. Ini bisa merepotkan dan berisiko konflik jika ada perubahan.
  - **Tidak Terintegrasi** : Proyek utama Anda tidak "tahu" tentang repositori tema, sehingga pengelolaan versi menjadi rumit.

---

### c. Metode Zip (Unduh Manual)

Metode ini adalah cara paling sederhana, cocok untuk pemula yang ingin cepat memulai.

- **Cara Instalasi** : Di halaman GitHub tema, klik tombol **`< > Code`** lalu pilih **`Download ZIP`**. Setelah mengunduh, ekstrak file `.zip` dan salin foldernya ke dalam folder `themes` di proyek Hugo Anda.
- **Kelebihan** : Sangat mudah dan tidak memerlukan pemahaman Git.
- **Kekurangan**:
  - **Sulit Diperbarui** : Jika pengembang tema merilis pembaruan, Anda harus mengunduh ulang file `.zip`, menghapus folder tema lama, dan menyalin yang baru. Proses ini tidak efisien.
  - **Tidak Terlacak** : Proyek Git utama Anda tidak akan tahu versi tema mana yang Anda gunakan.

---

## Menambahkan Tema sebagai Git Submodule

Daripada mengunduh file `.zip`, kita akan menggunakan perintah `git submodule`. Pastikan Anda sudah menginstal Git di komputer Anda.

1.  Buka terminal atau _command line_.
2.  Masuk ke direktori utama proyek Hugo Anda.
3.  Jalankan perintah `git submodule add` dengan URL repositori tema yang sudah Anda salin.

<!-- end list -->

```bash
git submodule add <URL_repositori_tema> themes/<nama-folder-tema>
```

- **`<URL_repositori_tema>`**: Ganti dengan URL GitHub tema.
- **`themes/<nama-folder-tema>`**: Ini akan menempatkan tema di dalam folder `themes` dengan nama yang Anda tentukan.

**Contoh:**
Jika URL tema adalah `https://github.com/the-coder-01/hugo-vitae`, jalankan perintah berikut:

```bash
git submodule add https://github.com/the-coder-01/hugo-vitae themes/vitae
```

Git akan secara otomatis mengkloning tema ke dalam folder `themes` proyek Anda.

## Mengaktifkan Tema di Situs Anda

Setelah tema ditambahkan, Anda perlu mengaktifkannya melalui file konfigurasi utama situs Anda.

- Buka file **`config.toml`** di direktori utama proyek Anda.
- Tambahkan baris berikut di akhir file, dengan mengganti nama tema sesuai dengan nama folder yang Anda gunakan di langkah sebelumnya.

<!-- end list -->

```toml
theme = "nama-folder-tema"
```

**Contoh `config.toml`:**

```toml
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'vitae'
```

## Menjalankan Situs dengan Tema Baru

Sekarang saatnya melihat hasilnya\! Buka terminal di direktori utama proyek Anda dan jalankan perintah:

```bash
hugo server
```

Perintah ini akan menjalankan server lokal. Buka browser Anda dan kunjungi [http://localhost:1313/](https://www.google.com/search?q=http://localhost:1313/). Situs Anda akan tampil dengan tema yang baru saja Anda tambahkan.

---

## Mengupdate Tema yang Menggunakan Git Submodule

Salah satu keuntungan terbesar menggunakan Git submodule adalah kemudahannya dalam memperbarui tema. Jika pengembang tema merilis pembaruan, Anda hanya perlu menjalankan satu perintah sederhana di terminal.

Pastikan Anda berada di direktori utama proyek Hugo Anda, lalu jalankan perintah ini:

```bash
git submodule update --remote --merge
```

Perintah ini akan memeriksa semua submodule di proyek Anda dan memperbarui semuanya ke versi terbaru. Jika Anda hanya ingin memperbarui satu tema, Anda bisa menentukannya:

```bash
git submodule update --remote themes/<nama-folder-tema>
```

Git akan secara otomatis menarik semua perubahan baru dan memperbarui tema Anda. Ini jauh lebih efisien daripada mengunduh file `.zip` secara manual setiap kali ada pembaruan.
