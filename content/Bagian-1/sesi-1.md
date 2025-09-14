---
Title: "Pendahuluan Hugo"
Weight: 1
---

Selamat datang di materi pengantar Hugo! Pada sesi pertama ini, kita akan membahas apa itu Hugo, mengapa Anda mungkin ingin menggunakannya, dan perbedaan mendasar antara situs web statis dan dinamis.

## **Apa itu Generator Situs Statis?**

Generator situs statis (Static Site Generator/SSG) adalah sebuah alat yang menjembatani dua pendekatan utama dalam membuat situs web:

1.  **Menulis halaman HTML statis secara manual:** Metode ini sederhana, tapi memakan waktu dan sulit untuk dikelola, terutama jika situs Anda memiliki banyak halaman.

2.  **Menggunakan Sistem Manajemen Konten (CMS) yang berat:** CMS seperti WordPress atau Wix sangat fleksibel, tapi bisa lambat dan mahal karena membutuhkan server yang terus-menerus memproses permintaan.

SSG seperti Hugo menawarkan kompromi terbaik. Anda dapat menulis konten Anda dalam format yang sederhana (seperti Markdown), lalu SSG akan mengubahnya menjadi halaman HTML statis yang siap digunakan.

**Mengapa Memilih Hugo?**
Hugo adalah salah satu SSG yang paling populer dan istimewa karena satu hal: **kecepatannya**.

- **Sangat Cepat**: Hugo ditulis menggunakan bahasa pemrograman **Go**, yang dirancang untuk performa dan dapat memproses banyak tugas sekaligus (multi-threading). Ini menjadikannya sangat efisien dalam menghasilkan halaman web statis, bahkan untuk situs yang sangat besar.

- **Gratis dan Sumber Terbuka**: Hugo 100% gratis dan memiliki komunitas yang aktif.

- **Fleksibel**: Hugo menawarkan fleksibilitas yang luar biasa, cocok untuk pemula dan pengguna tingkat lanjut:

  - **Untuk Pemula**: Anda bisa menggunakan tema yang sudah ada dari komunitas. Cukup tulis konten Anda di file Markdown, dan Hugo akan secara otomatis memformatnya menjadi situs web yang rapi tanpa perlu menyentuh kode HTML sama sekali.

  - **Untuk Pengguna Lanjut**: Jika Anda ingin mengontrol setiap detail situs Anda, Anda bisa membuat tata letak (layout) dan template kustom. Anda bahkan bisa menggunakan logika kondisional dan variabel di dalamnya.

---

## **Situs Statis vs. Situs Dinamis**

Untuk memahami mengapa Hugo sangat berguna, penting untuk memahami perbedaan antara dua jenis situs web: **statis** dan **dinamis**.

| **Fitur**      | **Situs Dinamis**                                                                                                             | **Situs Statis**                                                                                             |
| :------------- | :---------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------- |
| **Definisi**   | Konten dibuat dan disajikan secara _real-time_ setiap kali pengguna mengakses situs.                                          | Kontennya sudah jadi dan tidak berubah. Pengguna akan melihat halaman yang sama.                             |
| **Contoh**     | Facebook. Konten di beranda Anda berbeda dengan konten di beranda teman Anda.                                                 | Situs web portofolio atau blog sederhana. Semua pengunjung melihat halaman "Tentang Saya" yang sama.         |
| **Cara Kerja** | Saat Anda meminta halaman, server akan memproses permintaan, mengambil data dari database, lalu merangkai halaman untuk Anda. | Saat Anda meminta halaman, server hanya memberikan file HTML yang sudah jadi. Tidak ada pemrosesan tambahan. |
| **Keuntungan** | Sangat fleksibel, mudah dikelola, dan dapat menyajikan konten yang dipersonalisasi.                                           | Sangat **cepat**, aman, dan biayanya lebih murah karena tidak membutuhkan sumber daya server yang besar.     |
| **Kekurangan** | Cenderung lebih lambat karena ada proses di server. Biaya _hosting_ bisa lebih mahal.                                         | Kurang fleksibel. Jika tidak menggunakan SSG, pembaruan konten bisa merepotkan.                              |

Hugo mengambil keuntungan dari **kecepatan situs statis** dengan menyediakan **kemudahan pengelolaan seperti situs dinamis**. Anda menulis konten di file Markdown, dan Hugo akan melakukan semua pekerjaan berat untuk mengubahnya menjadi situs web statis yang super cepat.
