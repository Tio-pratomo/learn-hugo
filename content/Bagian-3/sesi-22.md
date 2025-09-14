---
title: "Membuild dan Hosting Situs Hugo"
weight: 22
---

## 1. Konsep Dasar Build Process

**Membuild situs Hugo** adalah proses dimana Hugo mengambil semua konten, template, dan aset Anda lalu mengubahnya menjadi website statis lengkap yang siap dihosting.

**Analoginya**: Seperti membuat kue - Anda punya bahan (konten), resep (template), dan oven (Hugo) yang menghasilkan kue jadi (website statis).

## 2. Perintah Dasar Build

### Menjalankan development server:

```bash
hugo server
```

Server development akan berjalan di `http://localhost:1313` dan secara otomatis merefresh ketika ada perubahan.

### Membuild situs untuk production:

```bash
hugo
```

Perintah ini akan menghasilkan folder `public` yang berisi seluruh website statis.

## 3. Struktur Folder Setelah Build

```
your-site/
├── archetypes/
├── content/
├── layouts/
├── static/
├── config.toml
└── public/           # Folder hasil build
    ├── index.html
    ├── about/
    │   └── index.html
    ├── posts/
    │   ├── post-1/
    │   │   └── index.html
    │   └── post-2/
    │       └── index.html
    └── css/
        └── style.css
```

## 4. Best Practices untuk Build Process

### Selalu hapus folder public sebelum rebuild:

```bash
rm -rf public
hugo
```

### Atau gunakan flag untuk menghapus otomatis:

```bash
hugo --cleanDestinationDir
```

### Build untuk environment tertentu:

```bash
hugo --environment production
```

## 5. Optimasi Build

### Build dengan minifikasi:

```bash
hugo --minify
```

### Build dengan logging verbose untuk debugging:

```bash
hugo --verbose
```

### Build hanya section tertentu:

```bash
hugo --contentDir content/blog
```

## 6. Memeriksa Hasil Build

Setelah build, selalu periksa folder `public`:

1. **Pastikan semua halaman ada** - navigasi manual melalui folder
2. **Periksa link internal** - gunakan tool seperti `htmltest`
3. **Test di browser lokal** - buka file HTML langsung
4. **Verifikasi aset statis** - pastikan CSS, JS, gambar tersedia

## 7. Hosting Situs Hugo

### Opsi Hosting Populer:

| Platform           | Kelebihan                 | Cara Deploy                                    |
| ------------------ | ------------------------- | ---------------------------------------------- |
| **Netlify**        | Gratis, otomatis dari Git | Drag & drop folder `public` atau integrasi Git |
| **GitHub Pages**   | Gratis dengan GitHub      | Push ke branch `gh-pages` atau folder `docs`   |
| **Vercel**         | Performa tinggi, gratis   | Integrasi dengan Git repository                |
| **Shared Hosting** | Traditional, familiar     | Upload via FTP/SFTP                            |
| **AWS S3**         | Scalable, murah           | Upload dengan AWS CLI                          |

## 8. Deployment dengan FTP (Traditional Hosting)

### Langkah-langkah:

1. **Build situs**: `hugo`
2. **Buka client FTP** (FileZilla, Cyberduck, dll.)
3. **Connect ke server** dengan credentials yang diberikan
4. **Upload seluruh isi folder `public`** ke root directory website
5. **Verifikasi** dengan membuka domain Anda

## 9. Automated Deployment dengan Git

### Contoh dengan GitHub Pages:

1. **Inisialisasi Git** di project Anda
2. **Buat repository** di GitHub
3. **Setup GitHub Actions** (buat file `.github/workflows/deploy.yml`):

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
      - name: Build
        run: hugo --minify
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

## 10. Konfigurasi Penting untuk Production

### Pastikan `config.toml` sudah benar:

```toml
baseURL = "https://website-anda.com"
languageCode = "id-id"
title = "Website Saya"
theme = "nama-theme"

[params]
  description = "Deskripsi website saya"
```

## 11. Testing Sebelum Deployment

### Checklist pre-deployment:

- [ ] Semua halaman terbuild dengan benar
- [ ] Gambar dan aset loading properly
- [ ] Link internal tidak broken
- [ ] SEO tags ter-setup dengan baik
- [ ] Sitemap.xml terbentuk
- [ ] Robots.txt ada dan benar

## 12. Troubleshooting Build Issues

### Common issues dan solusi:

1. **Error template**: Periksa syntax di file layout
2. **Content tidak muncul**: Pastikan front matter benar
3. **Gambar tidak loading**: Cek path di konten dan template
4. **CSS/JS broken**: Pastikan path di `baseURL` benar

## 13. Tips Production Optimization

### Gunakan build flags untuk optimasi:

```bash
hugo --minify --buildFuture --buildDrafts=false
```

### Enable Google Analytics (jika perlu):

```toml
[services.googleAnalytics]
id = "UA-123456789-1"
```

## 14. Monitoring Post-Deployment

Setelah deploy, pastikan untuk:

1. **Test di berbagai browser** (Chrome, Firefox, Safari)
2. **Check mobile responsiveness**
3. **Verify SSL certificate** (jika menggunakan HTTPS)
4. **Setup Google Search Console** untuk monitoring SEO

## 15. Backup dan Version Control

### Selalu backup:

1. **Seluruh project Hugo** (kecuali folder `public`)
2. **File konfigurasi**
3. **Custom themes dan layouts**

### Gunakan Git untuk version control:

```bash
git init
git add .
git commit -m "Initial commit"
```

---

**Kesimpulan**:
Membuild dan mendeploy situs Hugo sangat straightforward:

1. 🛠 **Build** dengan perintah `hugo`
2. 📁 **Upload** folder `public` ke hosting
3. ✅ **Verify** everything works correctly
4. 🔄 **Repeat** untuk update konten

Dengan mengikuti panduan ini, Anda dapat dengan mudah mendeploy website Hugo ke berbagai platform hosting tanpa kesulitan teknis yang berarti.
