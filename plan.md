# Rencana implementasi — Kilas Bimais Touna

## Pendekatan

Situs memakai starter WebDev React/Express/tRPC/Drizzle yang sudah terpasang, dengan Express sebagai API, MySQL terkelola sebagai penyimpanan permanen, serta object storage untuk berkas media. Halaman publik membaca berita yang berstatus terbit dan pengaturan tampilan terbaru dari API. Halaman admin menggunakan sesi cookie HTTP-only, CSRF token, dan pemeriksaan otorisasi pada setiap endpoint admin. Tidak ada berita contoh. Akun pertama `admin` dibuat satu kali dengan sandi rahasia proyek `BOOTSTRAP_ADMIN_PASSWORD`; sandi disimpan sebagai hash scrypt. Sesi disimpan sebagai token acak yang hash-nya tersimpan di database, bukan sebagai password atau credential di frontend.

Skema tambahan mencakup akun admin/editor, sesi admin, berita, indeks media, dan pengaturan situs. API menyediakan login/logout, pengelolaan berita dan status terbit, upload media dengan validasi tipe serta ukuran, pengelolaan user, penggantian kredensial sendiri, dan penyimpanan layout. Berkas foto/video dikirim dari admin ke server, diunggah melalui helper storage resmi, lalu alamat stabil dan metadata disimpan di database. Upload dibatasi ke jenis gambar/video yang dikenali dan maksimum 40 MB per berkas.

## Struktur proyek

- `client/src/pages/Home.tsx`: portal publik, keadaan kosong, daftar dan detail berita.
- `client/src/pages/Admin.tsx`: login, dashboard berita, editor berita/media, akun, user, dan layout.
- `client/src/App.tsx`: route `/`, `/berita/:slug`, `/admin`, serta route 404.
- `client/src/index.css`: sistem visual responsif portal institusional.
- `client/public/manus-routes.json`: deklarasi route halaman sebelum server pertama dijalankan.
- `client/public/kemenag-logo.png`: lambang Kementerian Agama pada header/footer.
- `server/portal.ts`: API portal Express, bootstrap akun, sesi, CSRF, endpoint publik dan admin.
- `server/db.ts` dan `drizzle/schema.ts`: akses query dan tabel MySQL.
- `drizzle/`: migrasi tambahan idempotent untuk data portal; tabel starter tetap dipertahankan.
- `server/storage.ts`: helper unggah media ke object storage terkelola.
- `app.config.ts`: logo metadata proyek menggunakan URL HTTPS aset yang tahan lama.

## Desain

Mengikuti rujukan portal Kemenag.go.id: tampilan berita pemerintahan yang rapi dan editorial, tetapi dengan identitas Kilas Bimais Touna sendiri. Palet dasar putih gading, hijau institusional pekat, emas sebagai penanda, dan abu hangat untuk teks sekunder. Header bertingkat menempatkan lambang dan identitas di kiri, navigasi berita ringkas di bawah, serta aksen garis emas. Judul editorial menggunakan serif system yang tegas; UI dan metadata memakai sans-serif sistem untuk keterbacaan. Kartu berita memakai hierarki jelas, bukan berita placeholder. Admin menggunakan pola panel kerja ringkas dengan navigasi samping yang beradaptasi menjadi tab di ponsel.

Identitas: kanal informasi kegiatan dan layanan Bimas Islam Tojo Una Una; resmi, informatif, dekat. Suara editorial lugas dan faktual, misalnya “Kabar terbaru dari Bimas Islam Tojo Una Una” dan “Belum ada berita yang diterbitkan. Berita terbaru akan tampil di sini.” Logo pemerintah ditampilkan sebagai identitas institusi dan wordmark “Kilas Bimais Touna” sebagai nama publikasi.

## Sajian dan penyajian data

Portal menyajikan `/`, `/berita/:slug`, dan `/admin`; halaman yang diminta tetap berupa situs web yang dirender ke HTML melalui React/Vite. Metadata artikel dan tautan berbagi menggunakan path relatif situs. WhatsApp dan Facebook memperoleh tautan berbagi, sedangkan Instagram memiliki tombol salin tautan karena alur web Instagram tidak menyediakan share-link yang setara. Backend berjalan pada port yang telah dikonfigurasi proyek. Semua perubahan berita, akun, media, dan layout dibaca kembali dari database/storage agar tidak hilang setelah refresh.
