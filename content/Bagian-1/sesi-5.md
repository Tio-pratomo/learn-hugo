---
Title: "Mengelola Konten di Hugo"
Weight: 5
---

Kali ini, kita akan belajar cara membuat konten di Hugo, mengorganisirnya, dan memahami bagaimana Hugo membedakan jenis-jenis halaman.

## Membuat Halaman Konten Baru

Di Hugo, setiap halaman di situs web Anda dibuat dari sebuah file. File-file ini disimpan di dalam folder **`content`**. Untuk membuat file baru, Anda akan menggunakan terminal.

Pastikan terminal Anda berada di direktori utama proyek Hugo Anda, lalu jalankan perintah ini:

```bash
hugo new <path-dan-nama-file>
```

**Contoh:**

- **Untuk membuat file di root folder `content`**:

  ```bash
  hugo new a.md
  ```

  Ini akan membuat file `content/a.md`.

- **Untuk membuat file di dalam subdirektori**:

  ```bash
  hugo new dir1/b.md
  ```

  Jika folder `dir1` belum ada, Hugo akan membuatnya secara otomatis dan menempatkan file `b.md` di dalamnya, sehingga menjadi `content/dir1/b.md`.

Saat file baru dibuat, Hugo secara otomatis menyertakan **Front Matter**. Ini adalah metadata (data tentang data) yang terletak di bagian atas file. Secara default, ia berisi judul (`title`), tanggal (`date`), dan status draf (`draft`).

**Contoh isi file `b.md`:**

```markdown
---
title: "B"
date: 2024-09-12T00:00:00+07:00
draft: true
---

Ini adalah konten dari halaman B.
```

Setelah Anda menambahkan konten di bawah Front Matter, Anda bisa menjalankan situs dan melihat hasilnya.

## Menjalankan Server Hugo dan Menampilkan Draf

Secara _default_, Hugo tidak akan menampilkan halaman yang berstatus `draft: true`. Untuk melihatnya saat mengembangkan situs, Anda harus menambahkan _flag_ `-D` (atau `--buildDrafts`) saat menjalankan server.

```bash
hugo server -D
```

Sekarang, buka browser Anda di `http://localhost:1313/` dan lihat halaman yang sudah Anda buat. Perhatikan bahwa URL akan mencerminkan struktur folder Anda. Misalnya, `content/dir1/b.md` akan menjadi `http://localhost:1313/dir1/b/`.

{{< tabs >}}
{{% tab title="root" %}}
![gambar-1](/content-images/bagian-1/gambar-1-sesi5.jpg)
{{% /tab %}}

{{% tab title="dir1/b.md" %}}
![gambar-1](/content-images/bagian-1/gambar-2-sesi5.jpg)

{{% /tab %}}

{{% tab title="a.md" %}}
![gambar-1](/content-images/bagian-1/gambar-3-sesi5.jpg)
{{% /tab %}}
{{< /tabs >}}

## Memahami Dua Jenis Halaman di Hugo

Hugo membagi semua konten menjadi dua jenis halaman utama:

### **a. Halaman Tunggal (Single Pages)**

- **Fungsi**: Halaman yang menampilkan satu unit konten secara spesifik, seperti postingan blog, halaman "Tentang Saya", atau entri portofolio.
- **Contoh**: `a.md` dan `dir1/b.md` yang kita buat adalah halaman tunggal.

### **b. Halaman Daftar (List Pages)**

- **Fungsi**: Halaman yang bertugas untuk menampilkan daftar dari halaman lain. Ini sering kali berfungsi sebagai direktori atau indeks.
- **Contoh**: Halaman beranda (`/`) adalah halaman daftar yang menampilkan semua halaman tunggal Anda. Hugo juga secara otomatis membuat halaman daftar untuk setiap folder di level root (misalnya, `/dir1/`) yang akan menampilkan semua konten di dalamnya.

## Mengelola Halaman Daftar (`List Pages`)

Hugo akan membuat halaman daftar secara otomatis untuk folder-folder di level atas (root) folder `content`. Namun, untuk sub-sub-folder, Anda harus membuat halaman daftar secara manual.

## Membuat Halaman Daftar Manual

Untuk membuat halaman daftar untuk sebuah sub-folder yang tidak berada di level root (misalnya `content/dir1/dir2/`), Anda bisa membuat file khusus bernama **`_index.md`** di dalam folder tersebut.

**Contoh:**

```bash
hugo new dir1/dir2/_index.md
```

File `_index.md` ini akan menjadi halaman daftar untuk folder `dir2`. Anda bisa menambahkan konten dan Front Matter di file ini untuk kustomisasi.

**Contoh isi file `_index.md`:**

```markdown
---
title: "Direktori Dua"
---

Ini adalah halaman daftar khusus untuk konten di direktori dua.
```

Dengan cara ini, Anda bisa memberikan konten unik pada halaman daftar, bukan hanya daftar kosong.

## Catatan Penting untuk Tema

Setiap tema Hugo memiliki cara sendiri dalam menampilkan konten. Beberapa tema mungkin memiliki struktur folder yang spesifik (misalnya, semua postingan blog harus berada di folder `content/posts/`). Selalu periksa dokumentasi tema Anda untuk panduan yang lebih terperinci.

Namun, prinsip dasar tentang **halaman tunggal**, **halaman daftar**, dan penggunaan **`_index.md`** tetap berlaku di semua tema.

