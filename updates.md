# Istorija Izmena i Verzija (Updates)

Ovaj dokument služi kao zvanični hronološki dnevnik izmena projekta (*changelog*). Prate ga i održavaju programeri i AI asistenti nakon svakog ciklusa implementacije, popravke ili objave nove verzije.

> [!NOTE]
> **Pravilo vođenja:** Svaka nova verzija ili veći skup izmena dodaje se **na sam vrh** ovog dokumenta (hronološki unazad), sa datumom i tačnim opisom unetih promena.

---

## [v1.0.0] — 2026-10-30

### Dodato / Funkcionalnosti:
- Inicijalizovan projekat i definisana standardna AI dokumentacija (`README.md`, `AGENTS.md`, `ARCHITECTURE.md`, `TESTING.md`, `TASK.md`, `updates.md`).
- Postavljen univerzalni skil `init-ai-docs` u `.agents/skills/init-ai-docs/` za automatsku detekciju stack-a i pripremu pravila na novim projektima.
- Uspostavljena pravila za 4 glavna arhetipa sistema (Fullstack/Web, Klijentske/Mobilne aplikacije, Višeslojni Enterprise bekendi, Skriptni/Bazaški repozitorijumi).

### Arhitektura i Standardi:
- Definisana stroga tipizacija i pravila asinhronog programiranja (zabrana blokiranja niti i sync-over-async poziva).
- Razdvojeni slojevi odgovornosti (separacija domena, logike servisa, baze i tankih prezentacionih kontrolera/komponenti).
- Uvedene bezbednosne restrikcije za AI (zaštita kredencijala, zabrana destruktivnih operacija nad bazom i zabrana samoinicijativnog dodavanja paketa).

### Validacija i Release:
- Uspostavljena obavezna provera kompajliranja (0 grešaka), pokretanja jediničnih testova i statičke analize pre završetka rada.
- Definisan protokol za automatsko podizanje verzije (*version bump*) i pripremu distribucijskog paketa.

