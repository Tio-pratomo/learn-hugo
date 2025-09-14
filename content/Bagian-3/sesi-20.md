---
title: "Memahami Partial Templates di Hugo"
weight: 20
---

## 1. Konsep Dasar Partial Templates

**Partial templates** adalah komponen template yang dapat digunakan kembali di berbagai bagian website Hugo. Mereka membantu membuat struktur website menjadi lebih modular dan terorganisir.

**Analoginya**: Seperti menyusun Lego - Anda membuat blok-blok kecil (partials) yang dapat disusun menjadi berbagai bentuk (halaman) yang berbeda.

## 2. Struktur Folder Partial

```
layouts/
└── partials/
    ├── header.html
    ├── footer.html
    ├── navigation.html
    └── components/
        ├── card.html
        └── banner.html
```

## 3. Membuat Partial Pertama

### Contoh: Header Partial

```html
<!-- layouts/partials/header.html -->
<header>
  <h1>{{ .Title }}</h1>
  <p>{{ .Date.Format "2 January 2006" }}</p>
  <hr />
</header>
```

## 4. Menggunakan Partial di Template

### Cara memanggil partial:

```go-html-template
{{ partial "header.html" . }}
```

**Penjelasan**:

- `partial`: Fungsi Hugo untuk memanggil partial
- `"header.html"`: Nama file partial yang akan dipanggil
- `.`: Context yang diteruskan ke partial (biasanya current context)

### Contoh dalam template lengkap:

```html
<!-- layouts/_default/single.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>{{ .Title }}</title>
  </head>
  <body>
    {{ partial "header.html" . }}

    <main>{{ .Content }}</main>

    {{ partial "footer.html" . }}
  </body>
</html>
```

## 5. Memahami Context dan Scope

**Penting**: Variabel yang tersedia di partial tergantung pada context yang diteruskan:

```go-html-template
<!-- Meneruskan seluruh context current page -->
{{ partial "header.html" . }}

<!-- Meneruskan context tertentu -->
{{ partial "header.html" .Site }}

<!-- Meneruskan custom data -->
{{ partial "header.html" (dict "Title" "Custom Title" "Date" "2023-01-01") }}
```

## 6. Partial dengan Parameter Custom

### Partial yang menerima parameter custom:

```html
<!-- layouts/partials/custom-header.html -->
<header>
  <h1>{{ .myTitle }}</h1>
  <p>{{ .myDate }}</p>
  <hr />
</header>
```

### Cara memanggil dengan parameter custom:

```go-html-template
{{ partial "custom-header.html" (dict "myTitle" "Judul Kustom" "myDate" "1 Januari 2023") }}
```

## 7. Best Practices untuk Partial Templates

1. **Gunakan nama yang deskriptif**

   - ✅ `article-card.html`
   - ❌ `partial1.html`

2. **Kelompokkan partial terkait dalam subfolder**

   ```
   partials/
   ├── header/
   │   ├── main.html
   │   └── navigation.html
   └── footer/
       └── main.html
   ```

3. **Dokumentasi parameter** yang diperlukan:

```html
{{/* Partial: article-card Parameters: - title: Judul artikel - date: Tanggal publikasi - summary: Ringkasan artikel */}}
```

## 8. Contoh Praktis: Navigation Partial

```html
<!-- layouts/partials/navigation.html -->
<nav>
  <ul>
    {{ $currentPage := . }}
    {{ range .Site.Menus.main }}
      <li class="{{ if $currentPage.IsMenuCurrent "main" . }}active{{ end }}">
        <a href="{{ .URL }}">{{ .Name }}</a>
      </li>
    {{ end }}
  </ul>
</nav>
```

## 9. Partial Caching untuk Performa

Gunakan `partialCached` untuk partial yang jarang berubah:

```go-html-template
{{ partialCached "footer.html" . }}
```

Untuk partial yang tergantung pada parameter tertentu:

```go-html-template
{{ partialCached "article-card.html" . .Permalink }}
```

## 10. Error Handling

Selalu periksa jika partial ada sebelum digunakan:

```go-html-template
{{ if templates.Exists "partials/header.html" }}
  {{ partial "header.html" . }}
{{ else }}
  <p>Header partial tidak ditemukan</p>
{{ end }}
```

## 11. Tips Organisasi Partial yang Efektif

1. **Buat partial untuk komponen yang digunakan kembali**
2. **Pisahkan concerns** - setiap partial sebaiknya memiliki satu tanggung jawab
3. **Gunakan naming convention yang konsisten**
4. **Simpan partial yang terkait dalam subfolder**

## 12. Contoh Layout dengan Multiple Partials

```html
<!-- layouts/_default/baseof.html -->
<!DOCTYPE html>
<html>
  <head>
    {{ partial "head/meta.html" . }} {{ partial "head/styles.html" . }}
  </head>
  <body>
    {{ partial "header.html" . }}

    <main>{{ block "main" . }}{{ end }}</main>

    {{ partial "footer.html" . }} {{ partial "scripts.html" . }}
  </body>
</html>
```

## 13. Latihan Praktis

Coba buat partial untuk:

1. **Header** dengan judul dan tanggal
2. **Footer** dengan copyright tahun dinamis
3. **Card component** untuk menampilkan artikel
4. **Banner** dengan parameter custom

Contoh card component:

```html
<!-- layouts/partials/components/card.html -->
<div class="card">
  <h3>{{ .title }}</h3>
  <p>{{ .content }}</p>
  {{ with .link }}
  <a href="{{ . }}">Baca selengkapnya</a>
  {{ end }}
</div>
```

```go-html-template
{{ partial "components/card.html" (dict
  "title" "Judul Artikel"
  "content" "Ringkasan artikel..."
  "link" "/artikel-1"
) }}
```

---

**Kesimpulan**:
Partial templates adalah fitur powerful Hugo yang memungkinkan:

- **Reusability** - komponen dapat digunakan kembali
- **Modularity** - kode terpecah menjadi bagian-bagian kecil
- **Maintainability** - lebih mudah dikelola dan diupdate
- **Performance** - dengan caching untuk partial yang statis

Dengan menguasai partial templates, Anda dapat membangun website Hugo yang lebih terstruktur, efisien, dan mudah dikembangkan.

