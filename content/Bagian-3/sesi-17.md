---
title: "Fungsi (Functions)"
weight: 17
---

## Apa Itu Fungsi dalam Hugo?

Fungsi adalah **blok kode yang sudah ditulis sebelumnya oleh Hugo** yang dapat Anda "panggil" untuk melakukan tugas tertentu. Fungsi menyediakan cara yang powerful untuk **memproses data, memanipulasi teks, melakukan perhitungan, dan mengontrol alur template** Anda tanpa harus menulis kode dari nol.

> [!important]**Penting**
>
> Sama seperti variabel, fungsi hanya dapat digunakan di dalam **file template** (di folder `layouts/`) dan tidak dapat digunakan langsung di dalam konten markdown.

## Cara Memanggil sebuah Fungsi

Sintaks dasar untuk memanggil fungsi adalah dengan menggunakan dua kurung kurawal `{{ }}` dan diikuti dengan nama fungsi serta parameternya (jika ada).

```go
{{ namaFungsi parameter1 parameter2 ... }}
```

Beberapa fungsi menggunakan **block** (`{{ function }} ... {{ end }}`), sementara yang lain hanya membutuhkan satu baris.

## Fungsi-Fungsi Umum yang Berguna

Berikut adalah beberapa fungsi yang sering digunakan dan sangat berguna:

**1. `truncate`**
Fungsi ini digunakan untuk **memotong sebuah string (teks) menjadi panjang tertentu**.

**Sintaks:**

```go
{{ truncate <panjang> <string> }}
```

**Contoh:**

```go
{{ "Ini adalah kalimat yang sangat panjang sekali" | truncate 20 }}
```

**Hasil:** `"Ini adalah kalimat..."`

Fungsi ini pintar, ia akan berusaha memotong pada spasi dan menambahkan elipsis (`...`) agar hasilnya rapi.

**2. Fungsi Aritmetika (`add`, `sub`, `mul`, `div`)**
Hugo menyediakan fungsi untuk **operasi matematika dasar**.

**Sintaks & Contoh:**

```go
{{ add 5 3 }}    <!-- Hasil: 8 -->
{{ sub 10 4 }}   <!-- Hasil: 6 -->
{{ mul 2 6 }}    <!-- Hasil: 12 -->
{{ div 20 5 }}   <!-- Hasil: 4 -->
```

**3. `singularize` dan `pluralize`**
Fungsi ini digunakan untuk **mengubah kata antara bentuk tunggal dan jamak**.

**Sintaks & Contoh:**

```go
{{ "dogs" | singularize }} <!-- Hasil: "dog" -->
{{ "cat" | pluralize }}    <!-- Hasil: "cats" -->
```

Ini sangat berguna untuk menampilkan teks yang dinamis, misalnya: `{{ .Pages | len }} post{{ if ne (len .Pages) 1 }}s{{ end }}` dapat diganti dengan cara yang lebih baik menggunakan `pluralize`.

**4. `range` (Fungsi yang Paling Powerful)**
Fungsi `range` digunakan untuk **melakukan perulangan (looping)** atas sebuah koleksi data, seperti semua halaman di suatu section, semua item dalam sebuah array, dll.

**Sintaks:**

```go
{{ range .Pages }}
  <!-- Kode yang diulang untuk setiap item dalam .Pages -->
  <!-- Di dalam blok ini, konteks (.) berubah menjadi halaman individual yang sedang di-loop -->
{{ end }}
```

**Contoh Praktis di `list.html`:**

```html
<!-- layouts/_default/list.html -->
<h1>Daftar Semua Artikel</h1>
<ul>
  {{ range .Pages }}
  <!-- Loop melalui semua page di section saat ini -->
  <li>
    <a href="{{ .Permalink }}">{{ .Title }}</a>
    <!-- .Title di sini adalah judul dari masing-masing artikel, bukan judul halaman list -->
  </li>
  {{ end }}
</ul>
```

**Cara Kerja `range`:**

- `{{ range .Pages }}` memulai loop terhadap kumpulan halaman.
- Di antara `{{ range }}` dan `{{ end }}`, konteks atau "dot" (`.`) **berubah maknanya**.
- Di luar loop, `.` merujuk pada **halaman list itu sendiri**.
- Di dalam loop, `.` merujuk pada **satu halaman artikel individual** yang sedang diproses saat itu. Inilah mengapa kita bisa menggunakan `.Title` dan `.Permalink` untuk masing-masing artikel.

## **Di Mana Menemukan Semua Fungsi Hugo?**

Hugo memiliki puluhan fungsi bawaan. Cara terbaik untuk menemukan fungsi yang Anda butuhkan adalah dengan menjelajahi dokumentasi resmi.

- **Hugo Functions Documentation :**  
  [https://gohugo.io/functions/](https://gohugo.io/functions/)

Dokumentasi fungsi Hugo sangat terorganisir. Fungsi-fungsi dikelompokkan menjadi beberapa kategori:

- **String Functions:** Untuk memanipulasi teks (e.g., `replace`, `lower`, `upper`).

- **Math Functions:** Untuk perhitungan (e.g., `add`, `math.Max`).

- **Date Functions:** Untuk memformat dan memproses tanggal (e.g., `format`, `now`).

- **Array & Map Functions:** Untuk menangani koleksi data (e.g., `first`, `where`).

- **Other Functions:** Berisi fungsi-fungsi inti seperti `range`, `partial`, dan `conditionals`.

## Kesimpulan

1.  **Fungsi adalah alat** untuk memanipulasi data dan konten di template Hugo.

2.  Gunakan sintaks `{{ functionName arguments }}` untuk memanggilnya.

3.  Beberapa fungsi penting:

    - `truncate`: Memendekkan teks.

    - `add`, `sub`, dll.: Untuk matematika dasar.

    - `range`: Untuk melakukan perulangan (sangat penting!).

4.  Pahami bahwa konteks (`.`) **berubah** di dalam blok `{{ range }}`.

5.  **Selalu merujuk ke dokumentasi resmi** untuk menemukan fungsi yang tepat untuk menyelesaikan masalah Anda.

Dengan menguasai fungsi, Anda dapat membuat template Hugo yang sangat dinamis dan efisien!

