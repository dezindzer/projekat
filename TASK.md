# Trenutni Zadatak: Implementacija sistema za pretplatu (Stripe)

## Status: U TOKU 🟡

## Faze rada:

### Faza 1: Baza i Model [ZAVRŠENO ✅]
- [x] Dodati `Subscription` model u `schema.prisma`
- [x] Napraviti i primeniti migraciju
- [x] Napisati Prisma seed skriptu za testne planove

### Faza 2: Stripe Integracija [TRENUTNO SE RADI ⏳]
- [x] Kreirati Stripe klijenta u `src/lib/stripe.ts`
- [ ] Implementirati webhook handler u `src/app/api/webhooks/stripe/route.ts`
- [ ] Testirati webhook događaj `checkout.session.completed`

### Faza 3: UI i Testovi [ČEKA ⏸️]
- [ ] Napraviti stranicu sa cenovnikom (`src/app/pricing/page.tsx`)
- [ ] Napisati unit testove za webhook logiku

## Poznate prepreke / Beleške
- Webhook potpis (secret) mora biti podešen u `.env.local` pre lokalnog testiranja preko Stripe CLI.

## Naučene lekcije i retrospektiva
- Pre pokretanja integracionih testova, osigurati pokrenut lokalni Stripe CLI listener (`stripe listen`) radi stabilnosti webhook okruženja.
