# AI Pravila i Konvencije Kodiranja

Ovaj dokument definiše standarde koje AI asistent MORA poštovati pri generisanju i izmeni koda.

## 1. Opšta pravila ponašanja
- Pre predlaganja velikih promena arhitekture, objasni plan i zatraži potvrdu.
- Ne ostavljaj nedovršen kod (`// TODO: implement later` ili `// implement logic here`).
- Nemoj brisati postojeće komentare ili dokumentaciju osim ako se direktno odnose na promenjeni kod.
- Ne instaliraj nove pakete (`npm install <paket>`) bez prethodne saglasnosti.

## 2. Standardi koda (TypeScript / React)
- **Striktni tipovi:** Nikada ne koristi `any`. Koristi `unknown` uz type guards ili definiši eksplicitne interfejse.
- **Komponente:** Koristi isključivo funkcionalne komponente.
- **Server vs Client:** Podrazumevano koristi React Server Components. Dodaj `'use client'` samo kada su neophodni state, effects ili browser API.
- **Stilovi:** Koristi isključivo Tailwind CSS klase. Izbegavaj inline stilove.
- **Forme i validacija:** Koristi `react-hook-form` u kombinaciji sa `zod`.

## 3. Arhitektonska pravila
- Biznis logika NE sme biti u UI komponentama; smešta se u servise ili server actions (`src/server/actions/`).
- Bazi pristupati isključivo kroz Prisma repozitorijume u `src/server/db/`.
- Sve greške u API rutama moraju vraćati standardizovan JSON format: `{ error: string, code: number }`.

## 4. Validacija rada
Nakon svake izmene koda, proveri sledeće komande:
- `npm run type-check` (mora proći bez grešaka)
- `npx vitest run <izmenjeni-fajl>.test.ts` (test mora prolaziti)
