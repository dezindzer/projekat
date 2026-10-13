# Pravila i Strategija Testiranja

## Komande za testove
- Pokreni sve unit testove: `npm test`
- Pokreni jedan test fajl: `npx vitest run src/features/users/user.service.test.ts`
- Pokreni u watch modu: `npm run test:watch`
- E2E testovi: `npx playwright test`

## Pravila za testiranje
1. **Bez lažnog uspeha:** Ne mock-uj funkciju koju direktno testiraš.
2. **Testiraj granične slučajeve (Edge Cases):**
   - Neispravan unos (prazan string, negativan broj, nepostojeći ID).
   - Neautorizovan pristup (korisnik bez permisija).
   - Greške sa servera/baze (timeout, unique constraint violation).
3. **Lokacija testova:** Test fajlovi stoje pored koda koji testiraju sa ekstenzijom `.test.ts` ili `.test.tsx`.

## Primer dobrog testa (Template)
```typescript
import { describe, it, expect, vi, beforeEach } from 'vitest';
import { calculateDiscount } from './pricing.service';

describe('calculateDiscount', () => {
  it('primenjuje popust od 10% za račune veće od 100$', () => {
    const result = calculateDiscount(120);
    expect(result).toBe(108);
  });

  it('baca grešku ako je iznos negativan', () => {
    expect(() => calculateDiscount(-10)).toThrow('Iznos ne može biti negativan');
  });
});
```
