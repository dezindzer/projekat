---
name: init-ai-docs
description: Automatski analizira bilo koji projekat i generiše optimalne .md fajlove (README.md, AGENTS.md, ARCHITECTURE.md, TESTING.md, TASK.md, updates.md) prilagođene pronađenom tech stack-u, arhetipu i strukturi, sa ugrađenim protokolom za samoučenje i samopoboljšanje.
---

# Uputstvo za kreiranje optimalnih AI .md fajlova na projektu

Ovaj skill služi za inicijalizaciju ili standardizaciju dokumentacije, pravila kodiranja, bezbednosnih ograda i delivery procesa za rad sa AI agentima na bilo kom projektu.

---

## Korak 1: Detekcija projekta, tehnologija i arhetipa

Pre kreiranja ili ažuriranja bilo kog fajla, detaljno istraži radni direktorijum i prepoznaj **arhetip projekta**:

### 1. Prepoznavanje arhetipa i tech stack-a:
- **A. Web & Fullstack aplikacije**
  - *Fajlovi za detekciju:* `package.json`, `tsconfig.json`, `next.config.*`, `vite.config.*`, `pyproject.toml`, `requirements.txt` (FastAPI/Django).
  - *Ključni elementi:* TypeScript/JavaScript, React Server/Client Components, state menadžeri (Zustand, Redux, Context), CSS framework (Tailwind), ORM/Baza (Prisma, Drizzle, SQLAlchemy).
- **B. Klijentske i mobilne aplikacije**
  - *Fajlovi za detekciju:* `build.gradle`, `build.gradle.kts`, `AndroidManifest.xml`, `Podfile`, `Package.swift`, `App.xaml.cs`.
  - *Ključni elementi:* Kotlin/Android, Swift/iOS, MAUI/Flutter/Electron, upravljanje nitima (Main UI vs Background IO), upravljanje životnim ciklusom (Activity/Fragment/Window), oslobađanje listenera i prevencija memory leak-ova, perzistencija sesije (Preferences, Keychain).
- **C. Višeslojni enterprise bekendi i servisi**
  - *Fajlovi za detekciju:* `*.sln`, `*.csproj`, `pom.xml`, `build.gradle` (Java/Spring), `go.mod`, `Cargo.toml`.
  - *Ključni elementi:* N-tier višeslojna arhitektura (Domain $\to$ Data $\to$ Core/Business $\to$ API/Presentation), asinhronost (`async/await` bez blokiranja niti), DTO mapiranje (zabrana slanja sirovih ORM entiteta), tanki kontroleri, dependency injection, migracije.
- **D. Skriptni, bazaški i ETL repozitorijumi**
  - *Fajlovi za detekciju:* `*.sql` skripte, `migrations/`, ETL folderi, `dbt_project.yml`, proceduralne Python/Bash skripte.
  - *Ključni elementi:* Projekti koji često **nemaju kompajler niti automatski test runner**. Fokus je na DDL/DML ugovorima, batch separatorima (npr. `GO`), zaštiti od destruktivnih radnji (DROP, TRUNCATE) i striktnim procedurama ručne/smoke verifikacije na neprodukcionim bazama.

### 2. Detekcija alata i procesa:
1. **Build & Compiler:** `npm run build`, `dotnet build`, `./gradlew assembleDebug`, `cargo build`, itd.
2. **Test Runner:** Vitest, Jest, Pytest, Go test, `dotnet test`, `./gradlew test`, JUnit, ili manuelni scenario provere ako runner ne postoji.
3. **Linter & Type-checker:** TypeScript (`tsc`), ESLint, Android Lint, Roslyn upozorenja, Flake8/Ruff.
4. **Verzionisanje i isporuka (Release workflow):** Gde se čuva verzija (`package.json`, `*.csproj`, `build.gradle`, `version.json`), kako se priprema paket za produkciju (npm build, dotnet publish, APK, arhiviranje u `.7z`/`.zip`, Docker).

---

## Korak 2: Generisanje fajlova

Na osnovu prikupljenih podataka kreiraj ili uskladi sledećih **6 ključnih fajlova**. Sadržaj mora biti potpuno prilagođen prepoznatom arhetipu i tehnologijama, bez ostavljanja generičkih "placeholder" vrednosti.

---

### 1. `README.md` (u root direktorijumu)
- **Opis projekta:** 1-2 jasne rečenice o svrsi sistema i domenu rada.
- **Tech Stack:** Tačne biblioteke, jezici, SDK i verzije pronađene u projektu.
- **Preduslovi i okruženje:** Šta je potrebno instalirati (Node, .NET SDK, Android SDK, JDK, SQL Server, Python verzija).
- **Instalacija i priprema:** Komande za preuzimanje paketa/zavisnosti.
- **Pokretanje (Dev):** Tačna komanda za lokalno pokretanje (dev server, emulator, servis).
- **Ključne skripte i komande:** Tabelarni ili bullet prikaz komandi za:
  - Build/Kompajliranje
  - Testiranje
  - Linter i type-checking
  - Publish / Pakovanje artefakata

---

### 2. `AGENTS.md` (u root direktorijumu)
Ovo je ustav i operativni priručnik za AI agente. Struktura **mora** sadržati sledećih 6 sekcija:

1. **Granice projekta i opšta pravila ponašanja:**
   - Pre predlaganja većih izmena arhitekture, objasniti plan i zatražiti potvrdu.
   - Ne nagađati o produkcionom okruženju, šemi baze, mrežnim permisijama ili konfiguraciji van dokumentovanog.
   - Očuvati postojeće komentare i dokumentaciju osim ako se neposredno odnose na promenjeni kod.
2. **Stil koda, asinhronost i tipizacija (prilagođeno jeziku):**
   - *Stroga tipizacija & Null-safety:* Zabrana `any` / `dynamic` bez type guard-a; zabrana nekontrolisanog forsirano un-wrap-a (`!`, `!!`); poštovanje nullable anotacija i eliminacija upozorenja kompajlera.
   - *Asinhrono programiranje i rad sa nitima:*
     - Zabrana blokiranja asinhronih niti (npr. `.Wait()`, `.Result`, `.GetAwaiter().GetResult()`).
     - Zabrana lažnih asinhronih metoda koje nemaju `await` (ukloniti lažni `async` ili vratiti gotov `Task`/`Promise`).
     - Strogo razdvajanje niti: I/O, rad sa bazom i mrežni pozivi isključivo u pozadinskim nitima; UI ažuriranja isključivo na glavnoj (Main) niti.
   - *Konvencije imenovanja:* Definisana pravila za klase, interfejse (npr. `I` prefiks u C#), promenljive, privatna polja (npr. `_camelCase`), DTO objekte i bazu.
   - *Mapiranje i DTO:* Zabrana slanja sirovih entiteta baze direktno na klijentski sloj bez DTO projekcije.
3. **Arhitektonska pravila i granice slojeva (Separation of Concerns):**
   - *Razdvajanje odgovornosti:* Jasna podela slojeva (Domen / Baza i repozitorijumi / Poslovna logika / Prezentacija).
   - *Tanki kontroleri / UI:* Zabrana stavljanja biznis logike u UI komponente, kontrolere ili rute.
   - *Upravljanje stanjem, sesijama i resursima:* Pravilno korišćenje autorizacije/tokena, sprečavanje memory leak-ova (deregistracija listenera, zatvaranje konekcija/streamova).
4. **Stroge zabrane za AI (Strict Constraints & Safety):**
   - *Paketi:* Zabrana instalacije novih paketa/biblioteka bez izričitog odobrenja.
   - *Kvalitet koda:* Zabrana lažnih implementacija, `TODO` komentara, praznih `catch` blokova koji gutaju greške, ili hardkodovanih mock podataka u produkcionim tokovima.
   - *Bezbednost baze podataka:* Zabrana automatskih destruktivnih izmena (DROP, TRUNCATE, nekontrolisano pokretanje produkcionih migracija `database update`).
   - *Kredencijali:* Zabrana upisivanja lozinki, produkcionih connection stringova ili API ključeva u kod, git commit-ove ili javne logove (uz navođenje eksplicitnih lokalnih izuzetaka ukoliko postoje).
   - *Integritet ugovora:* Zabrana menjanja Application ID-a, JWT algoritama/shema ili postojećih API/tabelarnih ugovora bez saglasnosti.
5. **Validacija rada, Build i Delivery ciklus:**
   - 1. **Kompajliranje i Verifikacioni Build:**
     - Svaka izmena koda mora proći verifikacioni build sa 0 grešaka i 0 novih upozorenja (npr. `npm run build`, `dotnet build`, `./gradlew assembleDebug`).
   - 2. **Provera testova:** Komanda za pokretanje svih i/ili pojedinačnog testa (npr. `npm test`, `dotnet test`, `./gradlew test`).
   - 3. **Statička analiza / Linter:** Provera tipova i koda (`npm run type-check`, `eslint`, `lint`).
   - 4. **Delivery, Version Bump i .7z Pakovanje:**
     - Kada se završi ciklus funkcionalnih izmena ili priprema release:
       - Inkrementirati verziju (version bump u `package.json`, `build.gradle`, `*.csproj`).
       - Dodati novu sekciju na sam vrh `updates.md` sa datumom i detaljnim spiskom svih izmena.
       - **Pravilo za Publish pakete sa više fajlova:** Ako projekat kao rezultat publish-a ili build-a generiše folder sa više fajlova (npr. `publish/`, `dist/`, `.next/standalone`), **obavezno je komprimovanje u `.7z` arhivu** pomoću 7-Zip alata sa standardizovanim formatom naziva:
         `%version% - publish %datetime%.7z` (primer: `1.0.0.9 - publish 20261030-145046.7z`), kako bi paket uvek bio spreman za brz i bezbedan prenos na server.

---

6. **Protokol za samoučenje i kontinuirano poboljšanje (Self-Learning & Feedback Loop):**
   - *Trajno beleženje ispravki korisnika:* Kada korisnik ispravi agenta ili ukaže na lokalnu specifičnost, agent ima obavezu da to znanje odmah trajno zabeleži u podsekciju `### Naučene lekcije i specifičnosti projekta` unutar `AGENTS.md` (ili preporuči `/learn` komandu). Zabranjeno je ponavljati istu ispravljenu grešku u narednim sesijama.
   - *Analiza korena uzroka (Root Cause Analysis):* Kada dođe do greške ili neočekivanog ponašanja, agent ne rešava samo simptom površinski, već preispituje pretpostavku koja je do greške dovela i dopunjuje pravila u `AGENTS.md` kako bi se sprečili slični propusti.
   - *Samoevaluacija pre završetka rada (Self-Review Checklist):* Pre nego što označi zadatak završenim, agent postavlja sebi tri kontrolna pitanja:
     1. Da li sam doneo neproverenu pretpostavku o kodu ili okruženju?
     2. Da li postoje neobrađeni granični slučajevi (edge-cases) ili rizik od curenja resursa/memorije?
     3. Da li je rešenje u potpunosti usklađeno sa pravilima iz `AGENTS.md` i `ARCHITECTURE.md`?
   - *Proaktivno unapređenje dokumentacije:* Ako agent uoči pod-dokumentovan deo koda ili zastarela pravila, predlaže dopunu `ARCHITECTURE.md` ili `README.md`.

---

### 3. `ARCHITECTURE.md` (u root direktorijumu)
- **Pregled strukture direktorijuma:** Stablo sa opisom ključnih modula/foldera i njihovih odgovornosti.
- **Arhitektonski model (prilagođen arhetipu):**
  - *Fullstack:* Odnos klijenta, server actions/API ruta, servisa i baze.
  - *Višeslojni backend:* Odnos `Domain` $\to$ `Database` $\to$ `Core/Services` $\to$ `API/Controllers`.
  - *Mobilne aplikacije:* Modularna struktura, integracija hardverskih SDK-ova, background servisi.
  - *Baze/ETL:* Šeme (staging, dwh, prod), zavisnosti skripti, smer punjenja podataka.
- **Tok podataka (Data Flow):** Detaljan opis kako podaci putuju od ulaza (HTTP/UI/Event), preko validacije i poslovne logike, do perzistencije i nazad.
- **Upravljanje stanjem i autorizacija:** Kako funkcionišu tokeni, sesije, keširanje i lokalna perzistencija.

---

### 4. `TESTING.md`
- **Ako projekat ima automatizovani test runner:**
  - Komanda za pokretanje svih testova.
  - Komanda za pokretanje **samo jednog pojedinačnog testa** (ključno za efikasan AI ciklus!).
  - Komanda za test coverage ili watch mod.
  - Pravila mock-ovanja (šta se mock-uje, a šta se testira realno).
  - Primer jednog dobro napisanog testa u stilu projekta.
- **Ako projekat NEMA automatski test runner (npr. čisti SQL / Skriptni repozitorijum):**
  - Metodologija bezbedne ručne / smoke verifikacije.
  - Pravila provere DDL i DML ugovora (nazivi, tipovi, nullability, batch separatori).
  - Obavezna izolacija testiranja: zabrana pokretanja skripti nad deljenom/produkcionom bazom; testiranje isključivo na lokalnoj/test instanci sa reprezentativnim podacima.
  - Lista graničnih slučajeva (edge-cases) koje programer/AI mora ručno pregledati.

---

### 5. `TASK.md`
- Služi za operativno praćenje radnih zadataka:
  - **Trenutni status:** Faza u kojoj se projekat trenutno nalazi.
  - **Checklista radnih stavki (`[ ]` / `[x]`):** Planirani koraci, implementacije novih funkcija ili refaktorisanja.
  - **Poznate napomene i dug (Technical Debt):** Specifičnosti sistema, privremena ograničenja ili kritične tačke na koje treba obratiti pažnju.
  - **Naučene lekcije i retrospektiva:** Beleške o specifičnim preprekama na koje se naišlo tokom zadatka i kako su prevaziđene kako bi kontekst ostao sačuvan za naredne sesije.

---

### 6. `updates.md` (u root direktorijumu)
`updates.md` služi kao formalni, trajni dnevnik izmena (changelog) projekta koji prate i održavaju AI agenti i tim:
- **Pravilo pozicioniranja:** Svaka nova verzija/izmena dodaje se **na sam vrh** fajla (hronološki unazad).
- **Format zapisa svake verzije:**
  ```markdown
  ## [Verzija] — YYYY-MM-DD
  ### Dodato / Izmenjeno:
  - Stavka 1: Detaljan opis šta je implementirano ili izmenjeno.
  - Stavka 2: Arhitektonski ili logički detalji od značaja.
  ### Ispravke grešaka (Fixes):
  - Opis otklonjenog problema.
  ### Napomene za Release / Deploy:
  - Posebna uputstva za konfiguraciju, publish komande ili migracije (ako postoje).
  ```
- **Integracija sa AI agentom:** AI agent na kraju uspešno obavljenog zadatka unosi sažetak izvršenih izmena u `updates.md`, što omogućava potpunu trasabilnost svih promena kroz vreme.

---

## Korak 3: Prijavljivanje rezultata korisniku

Nakon kreiranja ili osvežavanja dokumentacije:
1. Prikaži listu generisanih fajlova kao klikabilne markdown linkove:
   - [`README.md`](file:///README.md)
   - [`AGENTS.md`](file:///AGENTS.md)
   - [`ARCHITECTURE.md`](file:///ARCHITECTURE.md)
   - [`TESTING.md`](file:///TESTING.md)
   - [`TASK.md`](file:///TASK.md)
   - [`updates.md`](file:///updates.md)
2. Sažeto navedi:
   - Koji je arhetip projekta prepoznat.
   - Koje su ključne tehnologije, alati i mehanizmi validacije ugrađeni u pravila.
   - Koje su specifične bezbednosne zabrane i release koraci definisani.

---

## Korak 4: Samousavršavanje samog skila (Skill Self-Evolution)

Ovaj skil nije statičan. Kada agent na novom projektu prepozna:
1. Novu tehnologiju, biblioteku ili radni okvir koji nije pokriven u arhetipovima,
2. Novu komandu za build, test, linter ili pakovanje,
3. Novu specifičnu bezbednosnu restrikciju ili delivery proces,
agent je dužan da proaktivno korisniku predloži **ažuriranje samog `init-ai-docs/SKILL.md` fajla** sa tim obrascima, kako bi svi budući projekti imali korist od tog novog znanja i kako bi sistem kontinuirano napredovao.
