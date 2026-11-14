# Invoice Rental Mobil (Android)

Aplikasi Android untuk membuat invoice rental mobil dan menghasilkan **file PDF** dengan tata letak seperti invoice UD. Amanda Wisata.

## Fitur

- **Daftar invoice**: semua invoice tersimpan di HP dan bisa dibuka, diedit, dicetak ulang, atau dihapus.
- **Form invoice**:
  - Nomor otomatis berformat `INV/AW-02/X/2026` (urut per tahun, bulan Romawi). Nomor tetap bisa diubah manual.
  - Kostumer dan tanggal invoice.
  - Armada sebanyak yang diperlukan, masing-masing berisi nama, jumlah unit, tanggal mulai/selesai, durasi, dan tarif.
  - Durasi dihitung otomatis dari tanggal (6 s.d 11 = 6 hari) dan masih bisa diubah.
  - Subtotal = tarif × unit × durasi, lalu TOTAL dijumlahkan otomatis.
- **PDF A4**: kop berisi INVOICE, logo, nama usaha, serta baris telepon dan alamat; tabel rincian berwarna; total; rekening pembayaran; kota dan tanggal; stempel, tanda tangan, dan nama penanda tangan; ucapan terima kasih. Jika armadanya banyak, tabel lanjut ke halaman berikutnya.
- **Pratinjau** PDF langsung di aplikasi, **Simpan ke HP** (folder `Download/Invoice Rental`), dan **Bagikan** ke WhatsApp, email, atau Drive.
- **Pengaturan usaha**: nama usaha, alamat, rekening, penanda tangan, ucapan, awalan nomor, serta gambar logo kop, stempel, dan tanda tangan (diambil dari galeri).

Teks bawaan sudah terisi sesuai contoh invoice. Stempel bawaan diambil dari contoh. **Tanda tangan sengaja tidak ditanam** di aplikasi supaya tidak bisa disalahgunakan: pilih sendiri lewat Pengaturan → Gambar → Tanda tangan, sebaiknya PNG berlatar transparan.

## Cara membuat file APK

### Opsi A: lewat GitHub, tanpa komputer (bisa dari HP)
1. Buat repository baru di github.com, lalu upload seluruh isi folder ini (termasuk folder `.github`).
2. Buka tab **Actions** → **Build APK**. Workflow berjalan otomatis setiap ada push, atau bisa dijalankan manual lewat "Run workflow".
3. Tunggu sekitar 5 menit. Setelah selesai, unduh **InvoiceRental-apk** di bagian *Artifacts*, ekstrak zip-nya, lalu pasang `app-debug.apk` di HP. Izinkan "Instal dari sumber tidak dikenal" jika diminta.

### Opsi B: Android Studio (komputer)
1. Buka Android Studio → **Open** → pilih folder `RentalInvoice`.
2. Tunggu proses Gradle sync selesai (butuh internet).
3. Pilih **Build → Build App Bundle(s)/APK(s) → Build APK(s)**, atau tekan Run jika HP tersambung lewat USB.

## Struktur kode

```
app/src/main/java/com/rentalinvoice/app/
├── MainActivity.kt          navigasi antar layar
├── data/
│   ├── Models.kt            Invoice, InvoiceItem, CompanyProfile
│   ├── Format.kt            format Rupiah, tanggal Indonesia, bulan Romawi
│   └── Repository.kt        penyimpanan lokal & penomoran
├── pdf/
│   ├── InvoicePdf.kt        menggambar PDF (ubah tata letak di sini)
│   └── PdfActions.kt        pratinjau, simpan, bagikan
└── ui/                      layar daftar, form, pratinjau, pengaturan
```

Teknologi: Kotlin, Jetpack Compose (Material 3), `android.graphics.pdf.PdfDocument`. Tidak memakai library PDF pihak ketiga dan tidak membutuhkan internet. Minimal Android 8.0.
