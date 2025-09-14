---
title: "Menguasai Archetypes di Hugo"
weight: 7
draft: false
---

Kita akan membahas **Archetypes**. Jika Front Matter adalah metadata untuk setiap file konten, maka **Archetypes** adalah **template untuk Front Matter**.

Sederhananya, Archetypes adalah cetakan yang menentukan apa saja yang akan muncul secara otomatis di Front Matter setiap kali Anda membuat file konten baru menggunakan perintah `hugo new`.

## Perintah Dasar: `hugo new`

Mari kita lihat cara kerjanya. Buka terminal Anda dan jalankan perintah berikut:

```bash
hugo new posts/artikel-pertama.md
```

Setelah perintah ini dijalankan, buka file `posts/artikel-pertama.md`. Anda akan melihat Front Matter yang sudah terisi secara otomatis, seperti ini:

```markdown
---
title: "Artikel Pertama"
date: 2025-09-12T15:43:07+07:00
draft: true
---

Isi konten Anda di sini...
```

Secara default, Hugo selalu menambahkan tiga variabel ini: **title**, **date**, dan **draft**. Lalu, dari mana Hugo mendapatkan template ini? Jawabannya ada di dalam folder **archetypes**.

## Folder Archetypes

Setiap proyek Hugo memiliki folder `archetypes` di direktori utama. Di dalamnya, Anda akan menemukan file bernama `default.md`.

File `default.md` inilah yang menjadi template utama untuk semua file konten baru yang Anda buat. Isinya akan terlihat mirip dengan Front Matter yang kita lihat sebelumnya, tetapi dengan beberapa variabel khusus.

Contoh isi file `archetypes/default.md`:

```markdown
---
title: "{{ replace .Name "-" " " | title }}"
date: "{{ .Date }}"
draft: true
---
```

- **`{{ .Name }}`**: Ini adalah variabel khusus yang akan digantikan dengan nama file yang Anda buat. Misalnya, jika Anda membuat file `artikel-pertama.md`, maka `.Name` akan menjadi `artikel-pertama`.

- **`{{ .Date }}`**: Ini akan digantikan dengan tanggal dan waktu saat file dibuat.

- **`draft: true`**: Ini adalah nilai statis. Artinya, setiap file baru akan memiliki `draft` yang diatur ke `true`.

## Mengubah Template Default

Anda bisa memodifikasi file `archetypes/default.md` untuk mengubah Front Matter default.

Misalnya, Anda ingin setiap artikel baru memiliki `draft` yang diatur ke `false` dan secara otomatis menambahkan `author` sebagai penulis.

Caranya, buka file `archetypes/default.md` dan ubah isinya menjadi seperti ini:

```markdown
---
title: "{{ replace .Name "-" " " | title }}"
date: "{{ .Date }}"
draft: false
author: "Mike"
---
```

Sekarang, setiap kali Anda membuat file baru dengan `hugo new`, Front Matter-nya akan memiliki `draft: false` dan `author: Mike`.

## Archetypes Kustom untuk Direktori Khusus

Hugo juga memungkinkan Anda membuat template Front Matter yang berbeda untuk direktori (folder) tertentu. Ini sangat berguna jika Anda memiliki tipe konten yang berbeda, seperti blog posts, portfolio projects, atau pages.

Mari kita asumsikan Anda memiliki folder `posts` dan `projects` di dalam folder `content`.

1.  **Template Default untuk `posts`**:

    - Buat file baru di folder `archetypes` dan beri nama `posts.md`.

    - Isinya bisa seperti ini:

    ```markdown
    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: "{{ .Date }}"
    author: "Mike"
    type: "post"
    ---
    ```

2.  **Template Default untuk `projects`**:

    - Buat file baru di folder `archetypes` dan beri nama `projects.md`.
    - Isinya bisa seperti ini:

    ```markdown
    ---
    title: "{{ replace .Name "-" " " | title }}"
    date: "{{ .Date }}"
    client: ""
    type: "project"
    ---
    ```

## Cara Hugo Memilih Archetype

Ketika Anda menjalankan perintah `hugo new`, Hugo akan melakukan pemeriksaan ini:

1.  **Cek Nama Direktori**: Hugo akan mencari file archetype yang namanya sama dengan nama direktori yang Anda tentukan.

    - Contoh: `hugo new posts/artikel-kedua.md`. Hugo akan mencari file `archetypes/posts.md`.

    - Jika file `posts.md` ada, Hugo akan menggunakan template itu.

2.  **Gunakan Default**: Jika Hugo tidak menemukan file archetype yang sesuai dengan nama direktori (misalnya, `archetypes/posts.md` tidak ada), maka Hugo akan kembali menggunakan file `archetypes/default.md` sebagai template.

Dengan Archetypes, Anda bisa memastikan setiap file konten baru memiliki struktur dan metadata yang konsisten, menghemat waktu, dan menghindari kesalahan. Ini adalah fitur yang sangat kuat untuk mengelola situs web besar dengan banyak jenis konten.
