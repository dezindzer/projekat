# Starter Šablon za AI Dokumentaciju & Projekat

Ovaj repozitorijum sadrži primer optimalne konfiguracije `.md` fajlova za rad sa AI asistentima, kao i univerzalni skil za automatsku inicijalizaciju novih projekata.

---

## Kako ovaj skil funkcioniše u praksi?

Kada otvorite bilo koji novi ili postojeći projekat (bilo da je u pitanju Node.js, Python, Go, Java, Rust itd.), dovoljno je da kažete AI asistentu:

> **"Pokreni skil init-ai-docs i generiši dokumentaciju za ovaj projekat."**  
> *(ili jednostavno: "Inicijalizuj AI .md fajlove za ovaj projekat")*

### 1. Šta skil automatski detektuje
Pre kreiranja bilo kog fajla, asistent automatski istražuje strukturu koda i konfiguracione fajlove:
- **Jezik i framework:** Analizira `package.json`, `pyproject.toml`, `requirements.txt`, `go.mod`, `Cargo.toml`, `pom.xml` i pronalazi tačne verzije alata (npr. Next.js 15, FastAPI, Django, Spring Boot).
- **Test runner:** Prepoznaje alate za testiranje (Vitest, Jest, Pytest, Go test, Playwright).
- **Baza podataka i ORM:** Prepoznaje mehanizme za rad sa bazom (Prisma, Drizzle, SQLAlchemy, Hibernate).
- **Struktura foldera:** Mapira ključne direktorijume (`src/`, `app/`, `tests/`, `lib/`).

### 2. Šta skil automatski generiše
Na osnovu prepoznatog stanja, kreira skup fajlova potpuno prilagođenih tom konkretnom projektu:
1. `README.md` – Pregled projekta, tačan tech stack i komande za brzi start i pokretanje.
2. `AGENTS.md` – Pravila stila koda, arhitektonska ograničenja, zabrane za AI i komande za validaciju.
3. `docs/ARCHITECTURE.md` – Konceptualna mapa sistema, svrha direktorijuma i tokovi podataka.
4. `TESTING.md` – Tačne komande za pokretanje (posebno za izolovani test) i primer ispravnog testa.
5. `TASK.md` – Interaktivna lista zadataka za održavanje konteksta kroz višestruke sesije.

---

## Struktura ovog šablona

U ovom folderu se nalaze gotovi primeri dobre prakse:

```text
├── README.md                          # Ovo uputstvo i opis projekta
├── AGENTS.md                          # Pravila ponašanja i standardi za AI
├── TESTING.md                         # Strategija testiranja i komande
├── TASK.md                            # Praćenje faza rada i statusa zadataka
├── docs/
│   └── ARCHITECTURE.md                # Arhitektura sistema i mapa foldera
└── .agents/
    └── skills/
        ├── db-migration/SKILL.md      # Primer višekratne veštine za migracije
        └── init-ai-docs/SKILL.md      # Lokalna kopija skila za generisanje dokumentacije
```

> **Napomena o lokaciji skila:**  
> Skil `init-ai-docs` je instaliran i globalno u `~/.gemini/config/skills/init-ai-docs/SKILL.md`, što znači da je dostupan u svakom projektu na vašem računaru.
