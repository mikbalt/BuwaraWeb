# Buwara - Art Companion Website

Website pendamping karya seni yang diakses melalui QR code. Dibangun dengan Astro + Tailwind CSS untuk performa maksimal di mobile.

## 🎨 Fitur

- ✨ Splash screen dengan auto-dismiss (2 detik)
- 📱 Mobile-first responsive design
- ⚡ Ultra-ringan (~5-10KB bundle size)
- 🎯 Dynamic routing per artwork ID
- 🖼️ Support untuk multiple images & content blocks
- 📝 Public response section (optional)

## 🚀 Project Structure

```
buwara-companion/
├── public/
│   └── images/
│       ├── artworks/         # Gambar artwork
│       └── illustrations/     # Ilustrasi tambahan
├── src/
│   ├── components/
│   │   ├── SplashScreen.astro
│   │   ├── Header.astro
│   │   └── ArtworkContent.astro
│   ├── layouts/
│   │   └── MainLayout.astro
│   ├── pages/
│   │   ├── index.astro        # Landing/gallery page
│   │   └── artwork/
│   │       └── [id].astro     # Dynamic artwork pages
│   ├── data/
│   │   └── artworks.json      # Data karya seni
│   └── styles/
│       └── global.css
└── package.json
```

## 🧞 Commands

| Command                | Action                                     |
| :--------------------- | :----------------------------------------- |
| `npm install`          | Install dependencies                       |
| `npm run dev`          | Start dev server di `localhost:4321`       |
| `npm run build`        | Build production ke `./dist/`              |
| `npm run preview`      | Preview build locally                      |

## 📝 Cara Menambahkan Artwork Baru

### 1. Tambahkan Data Artwork

Edit file `src/data/artworks.json`:

```json
{
  "id": "artwork-id-unique",
  "title": "Judul Karya",
  "artist": "Nama Artist",
  "articleBy": "Nama Penulis",
  "location": "Lokasi",
  "questions": [
    {
      "number": 1,
      "question": "Pertanyaan pembuka?",
      "content": [
        {
          "type": "paragraph",
          "text": "Isi paragraf..."
        },
        {
          "type": "image",
          "src": "/images/artworks/nama-file.jpg",
          "alt": "Deskripsi gambar"
        }
      ]
    }
  ]
}
```

### 2. Upload Gambar

- Letakkan gambar di folder `public/images/artworks/`
- Format yang didukung: JPG, PNG, WebP
- Recommended: compress gambar untuk performa optimal

### 3. Generate QR Code

Buat QR code yang mengarah ke:
```
https://your-domain.com/artwork/[id]
```

Ganti `[id]` dengan ID artwork yang ada di JSON.

## 🌐 Deployment

### Option 1: Vercel (Recommended)

```bash
npm run build
npx vercel
```

### Option 2: Netlify

```bash
npm run build
npx netlify deploy
```

### Option 3: Cloudflare Pages

Connect repository ke Cloudflare Pages dengan settings:
- Build command: `npm run build`
- Output directory: `dist`

## 📱 Testing di Mobile

1. Run dev server: `npm run dev`
2. Akses dari mobile dengan IP lokal
3. Atau gunakan ngrok: `npx ngrok http 4321`

## 🎯 URL Pattern

- Landing page: `/`
- Artwork detail: `/artwork/[id]`
- Example: `/artwork/makassar-001`

## 🔧 Customization

### Ganti Logo

Replace placeholder logo di:
- `src/components/SplashScreen.astro`
- `src/components/Header.astro`
- `src/pages/index.astro`

### Ubah Brand Color

Edit `src/styles/global.css` untuk custom theme colors.

### Adjust Splash Duration

Edit timeout di `src/components/SplashScreen.astro:50`:
```js
setTimeout(() => {
  // Change 2000 to your desired milliseconds
}, 2000);
```

## 📦 Performance

- First Contentful Paint: < 1s
- Time to Interactive: < 2s
- Lighthouse Score: 95+
- Bundle size: ~5-10KB (gzipped)

## 🤝 Support

Untuk pertanyaan atau issue, hubungi tim development Buwara.

---

Built with ❤️ using [Astro](https://astro.build) + [Tailwind CSS](https://tailwindcss.com)
