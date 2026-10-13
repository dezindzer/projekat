---
name: init-ai-docs
description: Automatski analizira bilo koji projekat i generiše optimalne .md fajlove (README.md, AGENTS.md, docs/ARCHITECTURE.md, TESTING.md, TASK.md) prilagođene pronađenom tech stack-u i strukturi.
---

# Uputstvo za kreiranje optimalnih AI .md fajlova na projektu

Ovaj skill služi za inicijalizaciju ili standardizaciju dokumentacije i pravila za rad sa AI na bilo kom projektu.

## Korak 1: Detekcija projekta i tehnologija
Pre nego što kreiraš bilo koji fajl, istraži radni direktorijum projekta:
1. **Identifikuj jezik i framework:**
   - Pogledaj konfiguracione fajlove u root-u: `package.json`, `requirements.txt`, `pyproject.toml`, `go.mod`, `pom.xml`, `Cargo.toml`, itd.
   - Odredi tačne verzije ključnih alata (npr. TypeScript, Python 3.12, Next.js 15, FastAPI, Django, Spring Boot).
2. **Identifikuj test runner:**
   - Proveri šta se koristi za testove: Vitest, Jest, Pytest, Go test, JUnit, Playwright, Cypress.
3. **Identifikuj bazu i ORM:**
   - Prisma, Drizzle, SQLAlchemy, Hibernate, raw SQL, itd.
4. **Pregledaj strukturu direktorijuma:**
   - Pregledaj glavne foldere (`src/`, `app/`, `tests/`, `lib/`, `api/`) kako bi razumeo postojeću organizaciju.

---

## Korak 2: Generisanje fajlova

Na osnovu prikupljenih podataka, kreiraj ili dopuni sledećih 5 ključnih fajlova. **Sadržaj prilagodi tačno pronađenom stack-u, nemoj ostavljati generičke "placeholder" vrednosti.**

### 1. `README.md` (u root direktorijumu)
- **Šta projekat radi:** 1-2 rečenice rezimea.
- **Tech stack:** Tačne pronađene biblioteke i verzije.
- **Preduslovi i instalacija:** Koraci za instalaciju zavisnosti.
- **Pokretanje:** Tačna komanda za lokalni dev server / aplikaciju.
- **Ključne skripte:** Komande za build, lint, formatiranje i testove.

### 2. `AGENTS.md` (u root direktorijumu)
- **Stil koda i konvencije:**
  - Pravila tipizacije (npr. TypeScript striktni tipovi, Python type hints).
  - Konvencije imenovanja promenljivih, funkcija i fajlova.
  - Ograničenja (npr. "ne koristi `any`", "koristi funkcionalne komponente", "zabrana inline stilova").
- **Arhitektonska pravila:** Gde smešta biznis logiku, a gde UI komponente.
- **Zabrane za AI:**
  - "Ne instaliraj nove biblioteke bez pitanja."
  - "Ne ostavljaj TODO komentare bez implementacije."
  - "Ne diraj konfiguraciju baze / migracije bez prethodnog odobrenja."
- **Validacija:** Tačne komande koje AI mora proveriti nakon svake izmene (npr. type-check, linter, single test).

### 3. `docs/ARCHITECTURE.md`
- **Pregled direktorijuma:** Stablo sa opisom samo ključnih foldera (šta se gde nalazi i koja mu je svrha).
- **Tok podataka (Data Flow):** Kako teče zahtev od klijenta, preko validacije i servisa, do baze i nazad.
- **Stanje i sesije:** Kako se čuva stanje (Zustand, Redux, Context) i kako radi autentifikacija (ako postoji).

### 4. `TESTING.md`
- **Komande:**
  - Komanda za pokretanje svih testova.
  - Komanda za pokretanje samo jednog pojedinačnog testa (veoma bitno za AI!).
  - Komanda za test watch mod ili coverage.
- **Pravila:**
  - Šta se mock-uje, a šta se testira realno.
  - Zahtev za testiranje i uspešnih scenarija i edge-case grešaka.
  - Gde se nalaze fixture i mock podaci.
- **Template:** Primer jednog dobro napisanog testa u stilu tog projekta.

### 5. `TASK.md`
- Kreiraj početni `TASK.md` koji sadrži:
  - Trenutni status projekta.
  - Checklistu (checkboxes `[ ]`) za tekuće planirane stavke ili početnu inicijalizaciju.
  - Sekciju za "Poznati problemi / Napomene".

---

## Korak 3: Prijavljivanje rezultata korisniku
Nakon kreiranja fajlova:
- Prikaži listu generisanih fajlova kao klikabilne markdown linkove (`file://...`).
- Ukratko navedi koje su tehnologije prepoznate i primenjene u pravilima.
