# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Buwara Companion is a mobile-first art companion website accessed via QR codes at physical art installations. Built with Astro + Tailwind CSS v4 for maximum performance on mobile devices.

The site displays artwork information in an editorial layout with:
- Artwork image
- 3 descriptive paragraphs
- Photo map showing the location/context of the artwork
- Artist and location metadata

## Development Commands

```bash
npm install              # Install dependencies
npm run dev              # Start dev server at localhost:4321
npm run build            # Build for production to ./dist/
npm run preview          # Preview production build locally
```

## Architecture

### Data-Driven Static Generation

The app uses **static site generation (SSG)** with dynamic routes. All artwork pages are pre-rendered at build time from a single JSON data source:

- **Data Source**: `src/data/artworks.json` contains all artwork metadata
- **Dynamic Routes**: `src/pages/artwork/[id].astro` uses `getStaticPaths()` to generate one page per artwork
- **Build Output**: Each artwork ID becomes a static HTML page (e.g., `/artwork/makassar-001`)

### JSON Schema

Each artwork in `artworks.json` has:
```
{
  id: string,              // Used for URL routing
  title: string,           // Main title of artwork
  subtitle?: string,       // Optional subtitle
  artist: string,          // Artist name
  location: string,        // Location of artwork
  date: string,            // Year or date
  artworkImage: string,    // Path to main artwork image
  mapImage: string,        // Path to location/context map image
  mapCaption?: string,     // Optional caption for map
  paragraphs: string[]     // Array of 3 paragraphs
}
```

### Design System & Color Palette

The site uses a **topographic-inspired color palette** defined in `src/styles/global.css`:

- `--color-hot`: #e8e4dc (Beige background)
- `--color-warm`: #c4c5be (Light gray)
- `--color-slate`: #8c9490 (Medium gray)
- `--color-urbanite`: #5b6b6e (Blue-gray)
- `--color-ink`: #3d4f53 (Dark teal - primary)

Semantic aliases:
- `--color-primary`: Main brand color (ink)
- `--color-secondary`: Secondary text (urbanite)
- `--color-background`: Page background (hot)
- `--color-text`: Body text (ink)

Typography uses **Crimson Text** (Google Fonts) for an editorial feel.

### Component Structure

- `MainLayout.astro`: Root layout with meta tags, font imports, splash screen
- `SplashScreen.astro`: Auto-dismissing splash (2s), shows brand logo
- `PhotoMap.astro`: Displays location map with optional caption
- `index.astro`: Gallery view with artwork cards
- `artwork/[id].astro`: Editorial layout for individual artworks

### Splash Screen Behavior

The `SplashScreen.astro` component:
- Auto-dismisses after 2 seconds (configurable at line 108)
- Can be tapped to skip immediately
- Only shown when `showSplash={true}` is passed to `MainLayout`
- Uses brand color palette

### Page Structure

**Artwork Detail Page** (`/artwork/[id]`):
1. Header with title, subtitle, artist, location, date
2. Main artwork image (full-width, responsive)
3. Article content (3 paragraphs with justified text)
4. Photo map section
5. Footer with branding

## Adding New Artwork

1. Add entry to `src/data/artworks.json` with unique ID:
   ```json
   {
     "id": "unique-id",
     "title": "Artwork Title",
     "subtitle": "Optional Subtitle",
     "artist": "Artist Name",
     "location": "City, Region",
     "date": "2024",
     "artworkImage": "/images/artworks/id-artwork.jpg",
     "mapImage": "/images/artworks/id-map.jpg",
     "mapCaption": "Map description",
     "paragraphs": ["Para 1...", "Para 2...", "Para 3..."]
   }
   ```

2. Place images in `public/images/artworks/`:
   - `{id}-artwork.jpg` - Main artwork image
   - `{id}-map.jpg` - Location/context map

3. Run `npm run build` to regenerate static pages

4. Generate QR code pointing to `https://your-domain.com/artwork/{id}`

## Deployment

The site is framework-agnostic SSG output. Deploy to:
- **Vercel**: Auto-detects Astro, just connect repo
- **Netlify**: Build command `npm run build`, output `dist`
- **Cloudflare Pages**: Same as Netlify

## Mobile Testing

Access dev server from mobile device:
```bash
npm run dev
# Then access via local IP (e.g., http://192.168.1.x:4321)
```

Or use tunneling:
```bash
npx ngrok http 4321
```

## Tailwind Configuration

Using **Tailwind CSS v4** via Vite plugin (`@tailwindcss/vite`). Custom theme variables are defined in `src/styles/global.css` using the `@theme` directive.
