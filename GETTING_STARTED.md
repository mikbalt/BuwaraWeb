# Getting Started - Buwara Art Companion

## Quick Start

```bash
# 1. Install dependencies (sudah dilakukan)
npm install

# 2. Start development server
npm run dev

# 3. Buka browser ke http://localhost:4321
```

Server sudah running! ✅

## 🎯 Next Steps - Yang Perlu Dilakukan

### 1. **Ganti Logo Buwara**

Placeholder logo saat ini adalah lingkaran hitam dengan huruf "B". Ganti dengan logo asli di 3 tempat:

**File yang perlu diedit:**
- `src/components/SplashScreen.astro` (line 7-9)
- `src/components/Header.astro` (line 14-16)
- `src/pages/index.astro` (line 14-16)

**Cara ganti:**
```astro
<!-- Ganti ini -->
<div class="w-24 h-24 rounded-full bg-gray-900 flex items-center justify-center">
  <span class="text-white text-3xl font-bold">B</span>
</div>

<!-- Dengan ini -->
<img src="/images/logo.svg" alt="Buwara" class="w-24 h-24" />
```

### 2. **Upload Assets (Gambar)**

**Folder structure:**
```
public/
  images/
    logo.svg              # Logo Buwara
    artworks/             # Gambar artwork
      makassar-001-1.jpg
      makassar-001-2.jpg
      [id]-[number].jpg
    illustrations/        # Ilustrasi tambahan (optional)
```

**Tips:**
- Compress gambar menggunakan TinyPNG atau Squoosh
- Recommended format: WebP (paling efisien) atau JPG
- Max width: 1200px untuk mobile optimization

### 3. **Edit Data Artwork**

Edit file: `src/data/artworks.json`

**Contoh struktur lengkap:**
```json
[
  {
    "id": "makassar-001",
    "title": "Go to Makassar",
    "artist": "Nama Artist",
    "articleBy": "Nama Penulis Artikel",
    "location": "Makassar",
    "questions": [
      {
        "number": 1,
        "question": "What brought you to this place?",
        "content": [
          {
            "type": "paragraph",
            "text": "Paragraf pembuka yang menceritakan tentang artwork..."
          },
          {
            "type": "image",
            "src": "/images/artworks/makassar-001-1.jpg",
            "alt": "Deskripsi gambar untuk accessibility"
          },
          {
            "type": "paragraph",
            "text": "Paragraf lanjutan setelah gambar..."
          }
        ]
      },
      {
        "number": 2,
        "question": "What did you find there?",
        "content": [
          {
            "type": "image",
            "src": "/images/artworks/makassar-001-2.jpg",
            "alt": "Another image"
          },
          {
            "type": "paragraph",
            "text": "Penjelasan untuk pertanyaan kedua..."
          }
        ],
        "publicResponse": true
      }
    ]
  }
]
```

**Penjelasan fields:**
- `id`: Unique identifier (akan dipakai di URL dan QR code)
- `title`: Judul artwork
- `artist`: Nama pembuat karya
- `articleBy`: Nama penulis narasi/artikel
- `location`: Lokasi terkait artwork
- `questions`: Array berisi pertanyaan dan konten
  - `number`: Nomor urut pertanyaan
  - `question`: Teks pertanyaan
  - `content`: Array berisi paragraf dan gambar
  - `publicResponse`: (optional) tampilkan form response

### 4. **Tambah Artwork Baru**

Cukup tambahkan object baru ke array `artworks.json`:

```json
[
  {
    "id": "makassar-001",
    ...
  },
  {
    "id": "yogyakarta-002",
    "title": "Journey to Yogya",
    "artist": "Another Artist",
    ...
  }
]
```

Astro akan otomatis generate:
- ✅ `/artwork/makassar-001`
- ✅ `/artwork/yogyakarta-002`

### 5. **Generate QR Codes**

Setelah deploy, buat QR code untuk setiap artwork:

**URL Pattern:**
```
https://buwara.vercel.app/artwork/makassar-001
https://buwara.vercel.app/artwork/yogyakarta-002
```

**Tools untuk generate QR:**
- QR Code Generator: https://www.qr-code-generator.com/
- QR Code Monkey: https://www.qrcode-monkey.com/
- Atau gunakan library: `npm install qrcode` (jika mau auto-generate)

**Recommended QR Settings:**
- Error correction: Medium (15%)
- Size: Minimum 300x300px
- Format: SVG atau PNG high-res

### 6. **Customization (Optional)**

**Ubah warna theme:**
Edit `src/styles/global.css`:
```css
body {
  @apply bg-white text-gray-900;
  /* Ganti dengan brand colors */
}
```

**Adjust splash screen duration:**
Edit `src/components/SplashScreen.astro` line 50:
```js
setTimeout(() => {
  // Ganti 2000 (2 detik) sesuai kebutuhan
}, 2000);
```

**Ganti font:**
Edit `src/styles/global.css`:
```css
@import url('https://fonts.googleapis.com/css2?family=Your+Font');

html {
  font-family: 'Your Font', sans-serif;
}
```

## 🚀 Build & Deploy

### Build Production

```bash
npm run build
```

Output akan ada di folder `dist/`

### Deploy ke Vercel (Recommended)

1. **Install Vercel CLI:**
```bash
npm i -g vercel
```

2. **Deploy:**
```bash
vercel
```

3. **Follow the prompts:**
- Link to existing project? No
- Project name? buwara-companion
- Directory? ./
- Want to override settings? No

4. **Production deploy:**
```bash
vercel --prod
```

### Deploy ke Netlify

1. **Install Netlify CLI:**
```bash
npm i -g netlify-cli
```

2. **Deploy:**
```bash
netlify deploy
```

3. **Directory to deploy:** dist
4. **Production deploy:**
```bash
netlify deploy --prod
```

### Atau GitHub + Vercel (No CLI)

1. Push ke GitHub
2. Import project di vercel.com
3. Auto-deploy setiap push to main

## 📱 Testing

### Local Testing

```bash
npm run dev
# Buka http://localhost:4321
```

### Mobile Testing (Same Network)

1. Check IP local: `ifconfig | grep inet`
2. Akses dari HP: `http://192.168.x.x:4321`

### Mobile Testing (Public URL)

```bash
npx ngrok http 4321
# Dapat public URL untuk testing
```

## 🔍 Troubleshooting

### Dev server tidak jalan
```bash
# Kill process di port 4321
lsof -ti:4321 | xargs kill -9

# Start ulang
npm run dev
```

### Build error
```bash
# Clean cache
rm -rf node_modules .astro dist
npm install
npm run build
```

### Gambar tidak muncul
- Check path: `/images/artworks/filename.jpg` (harus ada leading slash)
- Check file ada di `public/images/artworks/`
- Case-sensitive: `Image.jpg` ≠ `image.jpg`

## 📚 Resources

- [Astro Docs](https://docs.astro.build)
- [Tailwind Docs](https://tailwindcss.com/docs)
- [Vercel Deploy Guide](https://vercel.com/docs)

---

**Current Status:**
- ✅ Project setup complete
- ✅ Dev server running at http://localhost:4321
- ⏳ Pending: Upload logo & artwork images
- ⏳ Pending: Edit artworks.json dengan data real
- ⏳ Pending: Deploy to production

Selamat mengerjakan! 🎨
