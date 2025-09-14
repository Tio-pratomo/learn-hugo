---
title: "Memahami Taxonomi di Hugo"
weight: 9
---

Taxonomi adalah cara untuk mengelompokkan konten secara logis agar Anda dapat mengatur sejumlah besar konten dengan lebih efisien.

## Taxonomi Bawaan Hugo

Secara default, Hugo menyediakan dua jenis taxonomi:

- **Tags (Tag):** Kata kunci atau label yang mendeskripsikan konten secara spesifik. Satu konten bisa memiliki beberapa tag.

- **Categories (Kategori):** Pengelompokan konten yang lebih luas dan umum. Satu konten biasanya masuk dalam satu kategori utama.

## Menerapkan Taxonomi pada Konten

Anda menerapkan taxonomi menggunakan **front matter** pada file markdown konten Anda. Front matter adalah bagian metadata yang diapit oleh `---` di awal file.

**Contoh Front Matter dengan Tags dan Categories:**

```yaml
---
title: "Judul Postingan Saya"
date: 2023-10-27T10:00:00+07:00
draft: false
tags: ["tag-satu", "tag-dua", "tag-tiga"]
categories: ["category-satu"]
---
```

Pada contoh di atas, konten tersebut memiliki tiga tag (`tag-satu`, `tag-dua`, `tag-tiga`) dan satu kategori (`category-satu`).

## Halaman Taxonomi Otomatis

Hal yang powerful dari Hugo adalah kemampuannya untuk **secara otomatis membuat halaman untuk setiap tag dan kategori**. Halaman-halaman ini berisi daftar semua konten yang memiliki tag atau kategori yang sama.

- Jika Anda memiliki konten dengan tag `python`, Hugo akan membuat halaman di alamat: `https://website-anda.com/tags/python/`

- Jika Anda memiliki konten dengan kategori `tutorial`, Hugo akan membuat halaman di alamat: `https://website-anda.com/categories/tutorial/`

Dengan mengklik link tag atau kategori yang ditampilkan di tema Anda, pengunjung akan diarahkan ke halaman ini untuk melihat semua konten terkait.

## Membuat Taxonomi Kustom

Anda tidak terbatas hanya pada tags dan categories. Anda bisa membuat taxonomi kustom sesuai kebutuhan website Anda. Misalnya, untuk situs ulasan film, Anda mungkin ingin taxonomi `genre` atau `director`.

**Langkah-langkah Membuat Taxonomi Kustom (contoh: "moods"):**

1.  **Tambahkan ke Front Matter:** Pertama, tambahkan taxonomi kustom Anda ke front matter konten.

    ```yaml
    ---
    title: "Postingan Bahagia"
    date: 2023-10-27T10:00:00+07:00
    draft: false
    tags: ["blog"]
    moods: ["happy", "upbeat"] # <-- Taxonomi kustom 'moods'
    ---
    ```

2.  **Konfigurasi di `config.toml`:** Anda harus memberi tahu Hugo tentang taxonomi kustom Anda dengan mendeklarasikannya di file konfigurasi (`config.toml` atau `config.yaml`).

    **Untuk TOML (`config.toml`):**

    ```toml
    # ... pengaturan lainnya ...

    [taxonomies]
      tag = "tags"
      category = "categories"
      mood = "moods" # <-- Deklarasi taxonomi kustom. Format: singular = "plural"
    ```

    > [!note]**Catatan Penting:**
    >
    > - Setelah Anda mendefinisikan taxonomi kustom, Anda **harus** juga mendeklarasikan ulang taxonomi default (`tag` dan `category`) seperti pada contoh di atas. Jika tidak, taxonomi default akan berhenti bekerja.
    >
    > - Formatnya adalah `bentuk_tunggal = "bentuk_jamak"`.

3.  **Restart Server Hugo:** Setiap kali Anda mengubah file konfigurasi, Anda perlu me-restart server development Hugo (`hugo server`) untuk melihat perubahannya.

Setelah dikonfigurasi, Hugo akan secara otomatis menghasilkan halaman untuk setiap item dalam taxonomi kustom Anda, misalnya: `https://website-anda.com/moods/happy/`.

## Ringkasan

- **Taxonomi** adalah alat pengorganisasian konten yang powerful di Hugo.

- Gunakan **tags** untuk label spesifik dan **categories** untuk pengelompokan umum.

- Terapkan taxonomi melalui **front matter** pada file konten Markdown.

- Hugo secara **otomatis menghasilkan halaman** yang mendaftarkan semua konten dengan tag atau kategori yang sama.

- Anda dapat membuat **taxonomi kustom** dengan mendeklarasikannya di file `config.toml` dan menggunakannya di front matter. **Jangan lupa untuk mendeklarasikan ulang taxonomi default saat melakukannya**.

