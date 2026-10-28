# Versi Full HTML

`dist/public/kilas-bimais-full.html` adalah versi satu berkas HTML hasil build. CSS dan JavaScript antarmuka disisipkan langsung di dalam HTML. Generatornya ada di `scripts/create-full-html.mjs`, dan dijalankan otomatis oleh `pnpm build`.

Berkas ini bukan aplikasi mandiri berbasis `file://`: autentikasi, akun, berita, penyimpanan media, dan pengaturan tetap memakai API backend pada origin yang sama. Sajikan berkas di server situs ini bersama seluruh API, database, dan logo (`/kemenag-logo.png`). Untuk mencoba di Preview, gunakan alamat situs yang sama dengan path `/kilas-bimais-full.html`.

Tidak ada kredensial yang ditulis ke berkas HTML. Backend menggunakan variabel lingkungan/runtime yang telah dikonfigurasi di proyek. Untuk mengubah antarmuka, edit sumber React/CSS, lalu jalankan `pnpm build` agar file full HTML dibuat ulang.
