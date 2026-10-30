# Arhitektura Sistema

## Pregled direktorijuma
```text
src/
├── app/               # Next.js App Router (stranice i API rute)
│   ├── (auth)/        # Rute za login i registraciju
│   └── (dashboard)/   # Zaštićene stranice aplikacije
├── components/
│   ├── ui/            # Generičke komponente (dugmad, modal, input)
│   └── shared/        # Složenije višekratne komponente (navbar, sidebar)
├── features/          # Moduli organizovani po domenima (users, billing, projects)
│   ├── users/
│   │   ├── components/
│   │   ├── hooks/
│   │   └── types.ts
├── server/            # Backend logika
│   ├── actions/       # Server Actions
│   ├── db/            # Prisma klijent i upiti
│   └── services/      # Čista biznis logika
└── lib/               # Utility funkcije i konfiguracije (utils.ts, auth.ts)
```

## Tok podataka (Data Flow)
1. **Zahtev:** Korisnik poziva akciju sa forme (Server Action).
2. **Validacija:** Ulazni podaci se validiraju pomoću `zod` sheme.
3. **Autorizacija:** Proverava se sesija korisnika (`auth()`).
4. **Logika i Baza:** Poziva se servis iz `src/server/services/`, koji vrši upit kroz Prismu.
5. **Odgovor:** Vraća se tipiziran rezultat ili baca standardizovanu grešku.

## Autentifikacija
Koristimo Auth.js (NextAuth). Sesija se na serveru čita preko `auth()` helpera, a na klijentu preko `useSession()`.
