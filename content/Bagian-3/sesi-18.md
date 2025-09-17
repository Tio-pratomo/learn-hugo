---
title: "Memahami Conditional Statements (If-Else) di Hugo"
weight: 18
---

## Konsep Dasar Conditional Statements

**Conditional statements** (pernyataan kondisional) adalah fitur pemrograman yang memungkinkan Anda mengontrol alur eksekusi program berdasarkan kondisi tertentu. Dalam Hugo, fitur ini sangat berguna untuk membuat template yang dinamis dan responsif.

**Analoginya**: Seperti pengambilan keputusan sehari-hari - "JIKA hujan turun, MAKA bawa payung, LAINNYA pakai topi".

## Operator Perbandingan di Hugo

Hugo menggunakan operator dua karakter untuk perbandingan:

| Operator | Arti                         | Contoh Penggunaan   |
| -------- | ---------------------------- | ------------------- |
| `eq`     | Sama dengan                  | `if eq $var1 $var2` |
| `ne`     | Tidak sama dengan            | `if ne $var1 $var2` |
| `lt`     | Kurang dari                  | `if lt $var1 $var2` |
| `le`     | Kurang dari atau sama dengan | `if le $var1 $var2` |
| `gt`     | Lebih dari                   | `if gt $var1 $var2` |
| `ge`     | Lebih dari atau sama dengan  | `if ge $var1 $var2` |

## Contoh Dasar If-Else

```go-html-template {title="go html template"}
{{ $var1 := "dog" }}
{{ $var2 := "cat" }}

{{ if eq $var1 $var2 }}
  <p>True - Kedua variabel sama</p>
{{ else }}
  <p>False - Kedua variabel berbeda</p>
{{ end }}
```

**Penjelasan Kode:**

- `{{ $var1 := "dog" }}`: Membuat variabel `$var1` dengan nilai "dog"

- `{{ if eq $var1 $var2 }}`: Memeriksa apakah `$var1` sama dengan `$var2`

- `{{ else }}`: Blok kode yang dijalankan jika kondisi tidak terpenuhi

- `{{ end }}`: Menutup blok conditional

## Penggunaan Operator NOT

Anda dapat membalikkan kondisi dengan operator `not`:

```go-html-template
{{ if not (eq $var1 $var2) }}
  <p>Kondisi terbalik: Variabel tidak sama</p>
{{ end }}
```

> [!important] **Penting**
>
> Perhatikan penggunaan tanda kurung saat menggunakan `not` - ini penting untuk memastikan urutan evaluasi yang benar.

## Operator Logika AND dan OR

Untuk menggabungkan multiple conditions:

```go-html-template
{{ $var1 := 1 }}
{{ $var2 := 2 }}
{{ $var3 := 3 }}

<!-- Operator AND (kedua kondisi harus true) -->
{{ if and (lt $var1 $var2) (lt $var1 $var3) }}
  <p>$var1 adalah nilai terkecil</p>
{{ end }}

<!-- Operator OR (salah satu kondisi true) -->
{{ if or (eq $var1 5) (eq $var2 2) }}
  <p>Salah satu kondisi terpenuhi</p>
{{ end }}
```

## Else If untuk Multiple Conditions

```go-html-template
{{ if eq $var1 1 }}
  <p>Nilai adalah 1</p>
{{ else if eq $var1 2 }}
  <p>Nilai adalah 2</p>
{{ else }}
  <p>Nilai bukan 1 atau 2</p>
{{ end }}
```

## Contoh Praktis: Highlight Halaman Aktif

```go-html-template
<!-- Simpan judul halaman saat ini -->
{{ $currentPageTitle := .Title }}

<!-- Iterasi melalui semua halaman -->
<ul>
  {{ range .Site.Pages }}
    <li>
      <a href="{{ .Permalink }}"
         style="{{ if eq .Title $currentPageTitle }}background-color: yellow;{{ end }}">
        {{ .Title }}
      </a>
    </li>
  {{ end }}
</ul>
```

**Penjelasan Kode:**

- `{{ $currentPageTitle := .Title }}`: Menyimpan judul halaman saat ini

- `{{ range .Site.Pages }}`: Iterasi melalui semua halaman situs

- `{{ if eq .Title $currentPageTitle }}`: Memeriksa apakah halaman yang diiterasi adalah halaman saat ini

- `background-color: yellow;`: Gaya yang diterapkan hanya pada halaman aktif

## Tips dan Best Practices

1. **Gunakan variabel untuk menyimpan nilai yang kompleks** - membuat kode lebih mudah dibaca

2. **Perhatikan urutan dan nesting parentheses** - kesalahan kecil dapat menyebabkan error

3. **Hindari conditional yang terlalu kompleks** - jika logika terlalu rumit, pertimbangkan untuk memindahkannya ke partial template

4. **Gunakan whitespace dengan baik** - formatting yang rapi membantu pembacaan kode

## Kesalahan Umum dan Solusi

**Masalah**: Conditional tidak bekerja seperti yang diharapkan
**Solusi**:
Pastikan:

- Semua parentheses tertutup dengan benar

- Tidak ada typo dalam nama variabel

- Menggunakan operator yang tepat untuk tipe data yang dibandingkan

## Latihan Praktis

Coba implementasikan conditional statements untuk:

1. Menampilkan konten khusus untuk halaman tertentu

2. Mengubah layout berdasarkan section content

3. Menampilkan atau menyembunyikan elemen berdasarkan parameter front matter
