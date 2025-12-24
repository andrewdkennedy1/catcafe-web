# CatCafe Space ✨

This repository contains the source code for [catcafe.space](https://catcafe.space) - a kawaii-themed web hub that serves as the central portal for various cat-related web applications and interactive experiences.

## About CatCafe Space

CatCafe Space is a charming, space-themed website featuring:

- **Kawaii aesthetic** with soft gradients and cute typography
- **Interactive links** to various cat-themed web applications:
  - **Cat-a-log** (`log.catcafe.space`) - Your cosmic logbook for cataloging every feline friend you meet
  - **Cat String Physics** (`string.catcafe.space`) - An interactive physics-based string simulation playground

## Tech Stack

- **SvelteKit** - Modern web framework
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **Three.js** - 3D graphics and particle effects
- **Cloudflare Pages** - Deployment platform

## Development

Install dependencies:
```bash
npm install
```

Start the development server:
```bash
npm run dev
```

## Building & Deployment

Build for production:
```bash
npm run build
```

Deploy to Cloudflare Pages:
```bash
npm run deploy
```

## Project Structure

- `src/lib/components/` - Reusable Svelte components
  - `ParticleBackground.svelte` - Three.js particle animation
  - `HeroSection.svelte` - Main title with kawaii styling
  - `ContentSection.svelte` - Application links and cards
  - `ScrollArrow.svelte` - Smooth scroll navigation
- `src/routes/` - SvelteKit pages and layouts
- `static/` - Static assets (images, icons)

---

Visit [catcafe.space](https://catcafe.space) to experience the magic! 🐱✨
