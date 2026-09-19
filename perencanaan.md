# Dokumen Perancangan Antarmuka dan Basis Data
**Nama:** Rifky Irvianto  
**No. Absen:** 25  
**Milestone:** Pekan 3 - Wireframing (Stitch / Figma)

---

## 1. Hirarki Menu (Sidebar / Navbar)
Struktur navigasi utama aplikasi dirancang untuk mempermudah alur kerja admin dalam mengelola data master dan memantau ringkasan sistem.

*   **Dashboard**
    *   Ringkasan Statistik (Total Data, Aktivitas Terbaru)
    *   Grafik Pertumbuhan
*   **Data Master**
    *   Kelola Pengguna (Admin / Staf)
    *   Kelola Kategori Produk
    *   Kelola Data Produk / Katalog
*   **Pengaturan**
    *   Profil Akun
    *   Pengaturan Tampilan Sistem
*   **Logout**

---

## 2. Entity Relationship Diagram (ER-D) Dasar
Berikut adalah rancangan struktur basis data sederhana untuk mendukung kebutuhan halaman Dashboard dan Data Master menggunakan sintaks Mermaid.js.

```mermaid
erDiagram
    PENGGUNA {
        int id_user PK
        string nama_lengkap
        string username
        string password
        string role
    }
    KATEGORI {
        int id_kategori PK
        string nama_kategori
        string deskripsi
    }
    OBAT {
        int id_obat PK
        string nama_obat
        int id_kategori FK
        int id_user FK
        float harga
        string komposisi
        string status_aktif
    }
    TRANSAKSI {
        int id_transaksi PK
        date tanggal_transaksi
        int id_user FK
        float total_harga
        string status_pesanan
    }
    DETAIL_TRANSAKSI {
        int id_detail PK
        int id_transaksi FK
        int id_obat FK
        int jumlah
        float subtotal
    }

    PENGGUNA ||--o{ OBAT : "mengelola"
    PENGGUNA ||--o{ TRANSAKSI : "melakukan"
    KATEGORI ||--|{ OBAT : "mengelompokkan"
    TRANSAKSI ||--|{ DETAIL_TRANSAKSI : "memiliki"
    OBAT ||--o{ DETAIL_TRANSAKSI : "termasuk dalam"

LINK DESIGN BY STITCH : https://stitch.withgoogle.com/projects/1252282857195522976?pli=1