# Tropeninstitut.Wien — Webseiten-Relaunch

Quellcode der neuen Webseite für die Privatpraxis **Univ.-Prof. Dr. Alexander Zoufaly**, Tropeninstitut.Wien, Mariahilfer Straße 69/10, 1060 Wien.

## Tech-Stack
- Frontend: React + Vite + TypeScript + Tailwind + shadcn/ui (gebaut mit Lovable)
- Backend: externes Supabase (Frankfurt, EU-central-1) — Auth, PostgreSQL, Storage
- Hosting: Cloudflare Pages
- Redirects: Cloudflare Workers (`/workers/redirects`)
- Schriftart: Rubik (selbstgehostet woff2)

## Struktur
- `/src` — Lovable-generierter Frontend-Code
- `/content-migration` — Migrations-Skripte für die alten WordPress-Sites
- `/mockups` — Vorab-Designs (GitHub Pages)
- `/workers/redirects` — Cloudflare Worker für 301-Redirects
- `/supabase/migrations` — DB-Schema
- `/docs` — Doku für Übergabe

## Setup lokal
```bash
git clone git@github.com:tropeninstitut-wien/tropeninstitut-wien.git
cd tropeninstitut-wien
npm install
cp .env.example .env.local  # Supabase-Keys eintragen
npm run dev
```

## Owner / Verantwortlich
- Code-Hoheit: Alex Zoufaly (via Service-Email `tropeninstitut.wien@gmail.com`)
- Entwicklung & Wartung: Martin Zapart
