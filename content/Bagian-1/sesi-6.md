---
Title: "Memahami Front Matter di Hugo"
Weight: 6
---

Sekarang, kita akan membahas salah satu fitur paling penting di Hugo: **Front Matter**. Anggap saja Front Matter ini seperti **metadata**

Jadi, apa itu metadata? **Metadata adalah informasi tambahan yang menjelaskan konten utama**. Bayangkan sebuah buku, isinya adalah cerita atau informasi, tetapi di sampulnya ada metadata seperti judul, nama penulis, dan tahun terbit.

Front Matter berfungsi persis seperti itu untuk setiap file konten Anda di Hugo.

## Apa Saja Isi dari Front Matter?

Ketika Anda membuat file konten baru (misalnya `.md` atau `.markdown`) di folder `content` Hugo, Hugo akan secara otomatis menambahkan beberapa informasi di bagian paling atas file. Inilah yang disebut Front Matter.

Informasi ini disimpan dalam format **"key-value pairs"** (pasangan kunci-nilai).

- **Key (Kunci)** : Nama dari variabel atau data yang Anda simpan. Contoh: `title`, `date`, `draft`.

- **Value (Nilai)** : Isi dari variabel tersebut. Contoh: `"Ini adalah Judul"`, `"2025-09-12"`, `true`.

Berikut adalah contoh Front Matter sederhana:

```markdown
---
title: "Ini adalah Judul Artikel"
date: 2025-09-12T15:43:07+07:00
draft: true
---

Isi konten Anda dimulai di sini...
```

Di contoh di atas, kita punya tiga pasangan kunci-nilai:

- **title** : Judul artikel kita.

- **date** : Tanggal artikel dibuat.

- **draft** : Variabel ini bernilai `true` (benar). Ketika `draft` diatur ke `true`, Hugo tidak akan menampilkan artikel ini di situs web yang sudah dipublikasikan. Ini sangat berguna jika Anda sedang menulis draf dan belum siap menampilkannya ke publik.

## Tiga Bahasa untuk Menulis Front Matter

Hugo mendukung tiga bahasa berbeda untuk menulis Front Matter. Anda bisa memilih salah satu yang paling Anda sukai atau yang paling cocok dengan proyek Anda.

1.  **YAML (Y-A-M-L)**

    - **Pemisah**: Tiga tanda hubung (`---`) di awal dan akhir.

    - **Sintaks**: Menggunakan titik dua (`:`) setelah kunci (`key`).

    - **Contoh**:

      ```yaml
      ---
      title: "Judul Artikel YAML"
      date: 2025-09-12
      ---
      ```

      > [!note]**Catatan** :
      > **YAML adalah bahasa default** yang digunakan Hugo untuk Front Matter.

2.  **TOML (T-O-M-L)**

    - **Pemisah**: Tiga tanda plus (`+++`) di awal dan akhir.

    - **Sintaks**: Menggunakan tanda sama dengan (`=`) setelah kunci dan nilai harus diberi tanda petik jika berupa teks.

    - **Contoh**:
      ```toml
      +++
      title = "Judul Artikel TOML"
      date = 2025-09-12
      +++
      ```
      > [!note]**Catatan**
      > TOML juga sering digunakan, terutama untuk file konfigurasi utama Hugo (`config.toml`).

3.  **JSON (J-S-O-N)**

    - **Pemisah**: Tiga tanda hubung (`---`) di awal dan akhir.

    - **Sintaks**: Menggunakan kurung kurawal (`{ }`), tanda kutip untuk kunci dan nilai, dan koma di setiap akhir baris (kecuali yang terakhir).

    - **Contoh**:
      ```json
      ---
      {
        "title": "Judul Artikel JSON",
        "date": "2025-09-12"
      }
      ---
      ```
      > [!note] **Catatan**:
      > JSON adalah bahasa yang sangat populer, tetapi sintaksnya lebih "berat" dan rumit dibandingkan YAML atau TOML.

## Mengapa Front Matter Sangat Berguna?

Front Matter sangat penting karena informasi di dalamnya bisa digunakan oleh **tema dan template Hugo** untuk menampilkan konten Anda dengan lebih baik.

Misalnya, tema yang Anda gunakan bisa mengambil `title` dan `date` dari Front Matter dan menampilkannya di halaman utama situs web Anda.

Jika Anda mengubah nilai di Front Matter, maka tampilan di situs web akan otomatis diperbarui.

- Mengubah `title` dari `"Artikel A"` menjadi `"Ini Adalah Judul Artikel A"` akan membuat judul di situs web ikut berubah.

- Mengubah `date` dari `"2025-09-12"` menjadi `"2025-10-15"` akan memperbarui tanggal publikasi artikel.

## Menambahkan Variabel Kustom (Custom Variables)

Selain variabel default seperti `title`, `date`, dan `draft`, Anda juga bisa membuat variabel kustom sendiri. Ini memungkinkan Anda menambahkan informasi unik yang sesuai dengan kebutuhan situs web Anda.

Misalnya, Anda bisa menambahkan variabel `author` untuk menunjukkan siapa penulis artikel.

```markdown {hl_lines="4"}
---
title: "Artikel Tentang Hugo"
date: 2025-09-12T15:43:07+07:00
author: "Mike"
---

Ini adalah konten artikelnya...
```

Setelah Anda menambahkan variabel `author` di Front Matter, tema atau template Hugo Anda dapat mengambil nilai `"Mike"` dan menampilkannya di halaman artikel. Jika ada file lain yang tidak memiliki variabel `author`, maka informasi penulis tidak akan ditampilkan.

Anda bisa membuat variabel kustom sebanyak yang Anda butuhkan, seperti `tags`, `categories`, atau bahkan `language`. Seiring Anda menjadi lebih mahir dengan Hugo, Anda akan belajar cara mengakses dan menampilkan variabel-variabel ini di template Anda.

Front Matter adalah alat yang sangat ampuh untuk mengelola dan mengatur konten di situs Hugo Anda. Dengan menggunakannya, Anda bisa membuat situs web yang lebih terstruktur dan informatif.

