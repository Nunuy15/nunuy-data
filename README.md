# Keuangan 2026

Aplikasi manajemen keuangan pribadi yang berjalan sepenuhnya di browser. Data tersimpan di `localStorage` (tidak perlu database, tidak perlu login), bisa diinstall ke home screen HP sebagai PWA, dan bekerja offline.

## Isi paket

```
keuangan-app/
├── index.html       ← aplikasi utama (semua kode di sini)
├── manifest.json    ← konfigurasi PWA
├── sw.js            ← service worker (untuk mode offline)
├── vercel.json      ← konfigurasi khusus Vercel
└── README.md        ← file ini
```

Tidak perlu build, tidak perlu install dependency apapun. Cukup upload folder ini ke hosting statis.

---

## Cara deploy

### Opsi 1 — Netlify Drop (paling cepat, tanpa akun)

1. Buka https://app.netlify.com/drop
2. Drag-and-drop folder `keuangan-app` ke halaman tersebut
3. Langsung dapat URL seperti `https://random-name.netlify.app`
4. Selesai

Catatan: untuk URL permanen dan custom domain, buat akun gratis Netlify lalu klaim site-nya.

### Opsi 2 — Vercel (rekomendasi)

**Via web (drag-drop):**
1. Buat akun gratis di https://vercel.com (bisa login pakai GitHub/Google)
2. Buka https://vercel.com/new
3. Pilih "Import Third-Party Git Repository" atau langsung drag folder ke deployment area
4. Klik Deploy → langsung jadi

**Via CLI:**
```bash
npm install -g vercel
cd keuangan-app
vercel
```
Ikuti prompt-nya. Pilih default semua. Selesai dalam ~30 detik.

URL hasil: `https://keuangan-app-xxx.vercel.app`

### Opsi 3 — Cloudflare Pages

1. Buat akun gratis di https://pages.cloudflare.com
2. Klik "Create a project" → "Direct Upload"
3. Upload folder `keuangan-app` atau zip-nya
4. Selesai

Cloudflare gratis sampai 500 deployment/bulan dengan bandwidth unlimited.

### Opsi 4 — GitHub Pages

1. Buat repo baru di GitHub (publik), misal `keuangan-2026`
2. Upload semua file di folder ini ke repo
3. Buka Settings → Pages → Source: pilih branch `main`, folder `/ (root)`
4. Save → tunggu ~1 menit
5. URL: `https://USERNAME.github.io/keuangan-2026`

---

## Install ke HP (PWA)

Setelah app online, buka di browser HP lalu:

**Android (Chrome/Edge):**
- Tap menu (3 titik) → "Tambahkan ke Layar utama" atau "Install aplikasi"

**iPhone (Safari):**
- Tap tombol Share (kotak dengan panah) → "Add to Home Screen"

Setelah diinstall, app jalan layaknya aplikasi native — tanpa address bar, ada di home screen, bekerja offline.

---

## Tentang data

- **Penyimpanan:** semua data tersimpan di `localStorage` browser. Tidak ada server, tidak ada cloud.
- **Privacy:** data tidak pernah dikirim ke mana pun. Tetap di perangkat masing-masing.
- **Backup:** gunakan tombol **Ekspor** di tab Dasbor untuk download backup JSON. Lakukan rutin (mis. sebulan sekali).
- **Pindah perangkat:** ekspor di perangkat lama → impor di perangkat baru lewat tombol **Impor**.
- **Hapus data browser = hilang data:** kalau bersihkan storage browser, data ikut hilang. Pastikan ada backup.

---

## Fitur

- **Dasbor**: ringkasan saldo akhir tahun, total pemasukan/pengeluaran, jumlah cicilan aktif, beban bulanan, ringkasan 11 bulan
- **Transaksi**: input transaksi harian per bulan (Feb-Des), saldo berjalan otomatis, checklist *done*, edit/hapus
- **Pelunasan**: timeline cicilan dengan status Aktif/Lunas dan hemat per bulan
- **Tabungan**: rekap tabungan (uang tunai + non-tunai seperti emas/perak)
- **Ekspor/impor JSON**: backup & restore
- **PWA**: install ke home screen, bisa offline
- **Dark mode**: otomatis ikut setting sistem
- **Bilingual format**: angka format Rupiah Indonesia (Rp 1.234.567)

---

## Custom

Mau modifikasi data awal? Edit object `RAW`, `PEL`, dan `TAB` di dalam `index.html`. Cari komentar `const RAW={` — semua data preload ada di sana.

Mau ganti tahun (mis. ke 2027)? Search-replace `2026` di `index.html`, lalu edit isi `RAW` sesuai data baru.

Mau tambah bulan Januari? Tambahkan `'Jan'` di awal array `const M=[...]` dan tambah entry `Jan:{s:0,t:[]}` di object `RAW`.

---

## Troubleshooting

**App tampil putih kosong:** browser-nya terlalu lawas. Pakai Chrome/Safari/Firefox versi 2 tahun terakhir.

**Service worker error di console:** abaikan, tidak mempengaruhi fungsi. Worker hanya untuk offline mode. Pastikan domain pakai HTTPS (Vercel/Netlify otomatis HTTPS).

**Data hilang setelah update browser:** localStorage seharusnya aman, tapi *private/incognito mode* tidak menyimpan permanen. Pakai mode normal.

**Icon Tabler tidak muncul:** koneksi internet pertama kali dibutuhkan untuk cache icon dari CDN. Setelahnya tersedia offline.

---

Dibuat dengan ❤️ — gratis, open, milik sendiri.
