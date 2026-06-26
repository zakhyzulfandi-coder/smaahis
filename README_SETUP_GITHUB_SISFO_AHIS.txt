SETUP GITHUB PAGES - SISFO AHIS / MTs Abu Hurairah
====================================================

LINK APPS SCRIPT YANG DIPAKAI
https://script.google.com/a/~/macros/s/AKfycbyjPmUMzLzWMWw6IRrZpagfhs4yiWmhDsoWmNbxqPE95m12WuCDTQxFiW_HdQNoKEwY6Q/exec

LINK LOGO GITHUB
https://zakhyzulfandi-coder.github.io/abuhurairah/icons/icon-192.png

ISI FILE
1. index.html
   - Wrapper utama untuk membuka Web App Apps Script.
   - Menggunakan iframe fullscreen.
   - Ada splash screen, logo, offline banner, dan update banner.

2. config.js
   - Tempat mengganti link Apps Script jika deployment berubah.
   - APP_URL sudah diisi memakai link yang diberikan.

3. manifest.json
   - Konfigurasi PWA / install aplikasi.

4. service-worker.js
   - Cache file wrapper GitHub.
   - Menampilkan update ketika file GitHub diperbarui.

5. folder icons
   - icon-192.png
   - icon-512.png
   - maskable-192.png
   - maskable-512.png

CARA PASANG DI GITHUB
1. Upload semua isi ZIP ini ke repository/folder GitHub:
   abuhurairah/

2. Struktur akhirnya:
   abuhurairah/
   ├── index.html
   ├── config.js
   ├── manifest.json
   ├── service-worker.js
   ├── .nojekyll
   └── icons/
       ├── icon-192.png
       ├── icon-512.png
       ├── maskable-192.png
       └── maskable-512.png

3. Aktifkan GitHub Pages:
   Settings > Pages > Source: Deploy from a branch
   Branch: main
   Folder: / root
   Save

4. Link aplikasi:
   https://zakhyzulfandi-coder.github.io/abuhurairah/

UPDATE LINK APPS SCRIPT
Jika link Apps Script berubah, cukup ubah file config.js bagian:

APP_URL: "..."

GANTI LOGO "AH" DI APPS SCRIPT
Tambahkan di Code.gs:

const APP_LOGO_URL = 'https://zakhyzulfandi-coder.github.io/abuhurairah/icons/icon-192.png';

Jika doGet memakai template:

function doGet(e) {
  const template = HtmlService.createTemplateFromFile('Index');
  template.APP_LOGO_URL = APP_LOGO_URL;

  return template.evaluate()
    .setTitle('SISFO AHIS')
    .addMetaTag('viewport', 'width=device-width, initial-scale=1')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
}

Lalu di Index.html, ganti logo teks "AH":

<div class="app-logo">AH</div>

menjadi:

<div class="app-logo">
  <img src="<?= APP_LOGO_URL ?>" alt="Logo MTs Abu Hurairah" class="app-logo-img">
</div>

Tambahkan CSS:

.app-logo {
  width: 46px;
  height: 46px;
  min-width: 46px;
  border-radius: 50%;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background: transparent;
}

.app-logo-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
}
