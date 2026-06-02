# 🤖 AI în Testare — Full Stack

> Prompt Engineering · AI Coding Assistants · Platforme AI-powered · CI/CD cu AI · Strategie echipă · ~3–4 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente AI pentru QA](#-faza-1--fundamente-ai-pentru-qa-12-săptămâni)
- [Faza 2 — Prompt Engineering pentru testeri](#-faza-2--prompt-engineering-pentru-testeri-23-săptămâni)
- [Faza 3 — AI Coding Assistants](#-faza-3--ai-coding-assistants-23-săptămâni)
- [Faza 4 — Platforme de testare AI-powered](#-faza-4--platforme-de-testare-ai-powered-34-săptămâni)
- [Faza 5 — AI pentru date de test & analiză](#-faza-5--ai-pentru-date-de-test--analiza-bugurilor-23-săptămâni)
- [Faza 6 — Autonomous Testing & Agent-based QA](#-faza-6--autonomous-testing--agent-based-qa-23-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack AI pentru QA](#-stack-ai-pentru-qa)

---

## 🟢 Faza 1 — Fundamente AI pentru QA (1–2 săptămâni)

> Nu trebuie să devii data scientist. Trebuie să înțelegi *ce poți cere* AI-ului și *de ce* funcționează sau nu.

| Resursă | Durată | Link |
|---------|--------|------|
| AI for Everyone — Andrew Ng (Coursera) | ~6h | [→ Deschide](https://www.coursera.org/learn/ai-for-everyone) |
| How Large Language Models Work — 3Blue1Brown | ~1h | [→ Deschide](https://www.youtube.com/watch?v=wjZofJX0v4M) |
| Introduction to Generative AI — Google Cloud | ~45min | [→ Deschide](https://www.cloudskillsboost.google/course_templates/536) |
| AI Testing Landscape — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/ai-in-software-testing) |

**Ce vei învăța:**
- Ce e un LLM (Large Language Model) și cum generează text — fără matematică, cu sens practic
- Diferența dintre AI generativ, ML clasic și automatizare scriptată
- Hallucination — de ce AI-ul „inventează" și cum să verifici rezultatul
- Tokenizare, context window, temperatura — parametrii care afectează calitatea răspunsurilor
- Limitele actuale ale AI în testare: ce poate face bine, ce face prost
- De ce AI nu înlocuiește testerul — ci îl face de 2–5x mai productiv

> ⚠️ **Mindset corect:** AI în testare nu e „click și gata". E un colaborator care scrie rapid, dar greșește des. Tu ești cel care validează, rafinează și decide.

---

## 🔵 Faza 2 — Prompt Engineering pentru testeri (2–3 săptămâni)

> Calitatea rezultatelor AI depinde 80% de calitatea promptului tău. Asta e abilitatea de bază.

| Resursă | Durată | Link |
|---------|--------|------|
| Prompt Engineering Guide — promptingguide.ai | ~4h | [→ Deschide](https://www.promptingguide.ai/) |
| ChatGPT Prompt Engineering for Developers — DeepLearning.AI | ~2h | [→ Deschide](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) |
| Claude for QA — Anthropic Docs | referință | [→ Deschide](https://docs.anthropic.com/en/docs/welcome) |
| ChatGPT Prompt Engineering for Developers — DeepLearning.AI | ~3h | [→ Deschide](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) |

**Ce vei învăța:**
- **Zero-shot vs Few-shot prompting** — când să dai exemple și când nu e nevoie
- **Chain-of-Thought** — cere AI-ului să gândească pas cu pas înainte de a răspunde
- **Role prompting** — „Ești un QA senior cu 10 ani experiență în testarea aplicațiilor financiare..."
- **Structured output** — cere răspunsuri în format tabel, JSON, Gherkin, TestNG, etc.
- **Prompting iterativ** — cum rafinezi un prompt în mai mulți pași, nu dintr-o singură cerere

**Prompturi esențiale pentru QA:**

```
# Generare test cases din cerință
"Ești un QA senior. Analizează această cerință și generează test cases complete
în format tabel (ID, Titlu, Precondiții, Pași, Rezultat Așteptat, Prioritate).
Acoperă: happy path, edge cases, negative testing și boundary values.
Cerința: [cerința ta]"

# Generare scenarii Gherkin
"Scrie scenarii BDD în Gherkin pentru funcționalitatea de [descriere].
Folosește Given/When/Then. Include cel puțin 3 scenarii: happy path, eroare validare,
și un edge case. Datele de test să fie în tabele Scenario Outline."

# Review test cases existente
"Revizuiește aceste test cases și identifică: gaps în acoperire, cazuri lipsă,
pași neclari și duplicate. [test cases]"
```

**Exerciții practice zilnice — Săptămâna 1:**
1. Ia o cerință din Jira (sau o invenți) și generează 20 de test cases
2. Compară rezultatele ChatGPT vs Claude vs Gemini — observă diferențele
3. Rafinează promptul de 3 ori și notează cum se îmbunătățește calitatea

---

## 🟡 Faza 3 — AI Coding Assistants (2–3 săptămâni)

> Dacă scrii deja teste automate, AI te face de 3–5x mai rapid. Dacă nu scrii, te ajută să înveți scriind.

| Unealtă | Scop | Link |
|---------|------|------|
| GitHub Copilot | Autocompletare și generare cod în IDE | [→ Deschide](https://github.com/features/copilot) |
| Cursor | IDE cu AI integrat (chat + edit + generation) | [→ Deschide](https://www.cursor.com/) |
| Claude Code | CLI AI agent pentru scriere și refactorizare teste | [→ Deschide](https://claude.ai/code) |
| Codeium (gratuit) | Alternativă gratuită la Copilot | [→ Deschide](https://codeium.com/) |

**Ce vei învăța:**

**GitHub Copilot:**
- Activare și configurare în VS Code / IntelliJ
- Autocompletare inteligentă — cum să ghidezi sugestiile prin comentarii
- Copilot Chat — întrebi în limbaj natural, primești cod
- `@workspace` — context din întregul proiect, nu doar fișierul curent
- Generare de teste din codul de producție cu un singur click

**Cursor:**
- Chat cu codebase-ul tău — „Explică cum funcționează fluxul de login"
- Composer mode — scrie fișiere întregi de test din descriere
- `Ctrl+K` — editează codul selectat cu instrucțiuni în limbaj natural
- Context rules — `.cursorrules` pentru a instrui AI-ul cu convențiile proiectului tău

**Fluxul de lucru recomandat:**
```
1. Scrie un comentariu care descrie testul: # Test că login cu parolă greșită returnează 401
2. Lasă Copilot să genereze codul
3. Revizuiește: logica e corectă? Assertion-urile sunt suficiente?
4. Adaugă edge cases pe care AI le-a omis
5. Rulează testul și iterează dacă pică
```

**Proiect practic:** Ia un proiect de automatizare existent (sau unul de pe GitHub) și redu cu 50% timpul de scriere folosind Copilot. Notează câte linii ai scris manual vs AI-generate.

---

## 🟣 Faza 4 — Platforme de testare AI-powered (3–4 săptămâni)

> Unelte specializate care integrează AI direct în ciclul de testare — self-healing, generare automată, analiză vizuală.

| Platformă | Ce face AI-ul | Tier gratuit | Link |
|-----------|--------------|--------------|------|
| Applitools Eyes | Visual AI — detectează diferențe vizuale inteligent | Da (trial) | [→ Deschide](https://applitools.com/) |
| Testim | Generează și auto-repară teste E2E | Da | [→ Deschide](https://www.testim.io/) |
| Mabl | Testare E2E cu auto-healing și ML analytics | Trial | [→ Deschide](https://www.mabl.com/) |
| Katalon AI | AI assistant în Katalon Studio | Da | [→ Deschide](https://katalon.com/) |
| Diffblue Cover | Generare automată teste unitare Java | Trial | [→ Deschide](https://www.diffblue.com/) |

**Ce vei învăța:**

**Applitools — Visual AI Testing:**
- Cum AI-ul diferențiază un bug real de o diferență acceptabilă (anti-aliasing, font rendering)
- Ultrafast Grid — rulezi un test pe toate browserele simultan
- Root Cause Analysis — AI-ul îți spune *de ce* a picat testul vizual
- Integrare cu Selenium, Playwright, WebdriverIO

**Testim — Self-Healing Tests:**
- Recorder AI — înregistrezi un test în browser, AI generează codul
- **Self-healing** — când un locator se schimbă, AI-ul îl găsește singur fără să pice testul
- AI Authoring — descrii în text ce vrei testat, Testim scrie testul
- Analytics AI — identifică automat testele flaky și cauzele lor

**Mabl — Intelligent Test Automation:**
- Auto-healing locators — nu mai petreci ore actualizând xpath-uri rupte
- Anomaly Detection — ML detectează regresia de performanță
- Impact Analysis — AI-ul prezice ce teste să rulezi bazat pe ce cod s-a schimbat

**Curs recomandat:**
| Resursă | Durată | Link |
|---------|--------|------|
| Automated Visual Testing with Java — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/automated-visual-testing-a-fast-path-to-test-automation-success/) |
| Modern Functional Testing Through Visual AI — TAU | ~4h | [→ Deschide](https://testautomationu.applitools.com/modern-functional-testing/) |

---

## 🔴 Faza 5 — AI pentru date de test & analiza bugurilor (2–3 săptămâni)

> Două dintre cele mai consumatoare de timp activități în QA — rezolvate parțial cu AI.

### 5a — Generare date de test cu AI

| Resursă / Unealtă | Scop | Link |
|-------------------|------|------|
| Faker.js / Faker (Python/Java) | Date false realiste (nume, email, IBAN, etc.) | [→ Deschide](https://fakerjs.dev/) |
| Mostly AI | Date sintetice care respectă structura datelor reale | [→ Deschide](https://mostly.ai/) |
| ChatGPT + structura tabelei | Generare SQL inserts, CSV, JSON din descriere | — |

**Prompturi pentru generare date de test:**

```
# Date de test structurate
"Generează 20 de utilizatori de test în format JSON cu câmpurile:
id (UUID), firstName, lastName, email (domeniu @test.com), age (18-80),
country (Romania/Bulgaria/Hungary), role (admin/user/viewer).
Include cazuri edge: caractere speciale în nume, email cu subdomeniu, vârsta limită."

# Date pentru SQL
"Generează 50 de INSERT-uri SQL pentru tabela orders cu coloanele:
order_id, customer_id (1-100), product_id (1-20), quantity (1-10),
total_price, status (pending/shipped/delivered/cancelled), created_at.
Distribuie statusurile realist: 60% delivered, 20% shipped, 15% pending, 5% cancelled."
```

### 5b — AI pentru analiza bugurilor

**Ce vei învăța:**
- **Root Cause Analysis cu AI** — pasezi stack trace-ul și AI-ul îți explică cauza
- **Bug deduplication** — AI identifică bug-uri duplicate înainte să le raportezi
- **Predictive defect detection** — ML-ul analizează codul și prezice zone cu risc mare de bug
- **Log analysis** — AI parsează mii de linii de log și găsește anomaliile

**Flux practic pentru analiza unui bug:**
```
1. Copiază stack trace-ul complet
2. Prompt: "Analizează acest stack trace și explică:
   - Care e cauza root a erorii
   - Ce cod a triggeruit-o
   - Ce ar trebui verificat pentru a reproduce
   - Ce fix ar rezolva problema
   Stack trace: [paste]"
3. Verifică explicația față de codul real
4. Adaugă concluziile în bug report
```

| Unealtă | Scop | Link |
|---------|------|------|
| Sentry + AI | Grupare și analiză automată erori | [→ Deschide](https://sentry.io/) |
| LinearB / Squadcast | AI pentru incident analysis | [→ Deschide](https://linearb.io/) |
| GitHub Copilot Chat | Explică orice stack trace pe loc | — |

---

## ⚫ Faza 6 — Autonomous Testing & Agent-based QA (2–3 săptămâni)

> Frontiera actuală — unde AI nu mai asistă, ci execută. Tehnologie emergentă, dar deja în producție la unele companii.

| Resursă | Durată | Link |
|---------|--------|------|
| AgentQL — AI Web Scraping & Testing | ~2h | [→ Deschide](https://www.agentql.com/) |
| Playwright MCP + Claude | tutorial | [→ Deschide](https://playwright.dev/docs/getting-started-mcp) |
| Browser Use — AI Browser Automation | ~2h | [→ Deschide](https://github.com/browser-use/browser-use) |
| AI in Testing — Ministry of Testing | ~1h | [→ Deschide](https://www.ministryoftesting.com/topics/ai-testing) |

**Ce vei învăța:**

**AI Agents pentru testare:**
- Ce e un AI Agent — un LLM care poate lua decizii și executa acțiuni în buclă
- **AgentQL** — descrii în limbaj natural ce element vrei, AI-ul îl găsește indiferent de DOM
- **Browser Use** — un agent AI care navighează un browser autonom și raportează ce găsește
- **Playwright MCP** — Claude Code controlează un browser real prin Model Context Protocol

**Exemplu real — test autonom cu Claude:**
```
Pornești Claude Code cu MCP Playwright activ și îi spui:
"Testează fluxul de checkout pe [site]. Adaugă 3 produse diferite în coș,
aplică codul de discount TEST10, completează adresa cu date fictive valide,
verifică că suma totală e corectă și că pagina de confirmare apare.
Raportează orice anomalie vizuală sau eroare."

Claude navighează, execută, face screenshots și îți dă un raport.
```

**Limite importante de știut:**
- Testele autonome sunt nedeterministe — același prompt poate da rezultate diferite
- Nu înlocuiesc testele de regresie clasice — sunt complementare, pentru exploratory
- Cost per run — fiecare test autonom consumă tokeni LLM
- Debugging dificil — când agentul eșuează, înțelegerea cauzei e complexă

> 🔬 **Statusul din 2026:** Autonomous testing e real și funcțional pentru exploratory testing și smoke checks. Pentru regresie completă, modelele clasice (Selenium, Playwright scriptat) rămân mai fiabile și mai ieftine.

---

## 💡 Sfaturi practice

### Cum să integrezi AI în munca zilnică — de mâine

| Task QA | Cum folosești AI |
|---------|-----------------|
| Analizezi o cerință nouă | Paste în Claude/ChatGPT → „Generează test cases și identifică ambiguitățile" |
| Scrii test cases | AI generează primul draft, tu rafinezi și adaugi context de business |
| Dai de un bug ciudat | Paste stack trace → AI explică root cause |
| Scrii un test automat | Copilot/Cursor scrie codul, tu validezi logica |
| Review test cases ale unui coleg | AI identifică lacunele și cazurile lipsă |
| Generezi date de test | Prompt cu structura tabelei → AI generează JSON/SQL |
| Explici un bug în Jira | AI rescrie descrierea ta în format clar și complet |

### Ce NU să lași pe seama AI-ului

- **Decizia finală de release** — AI nu are context de business și risc
- **Testarea de securitate** — hallucination-urile sunt periculoase în security testing
- **Exploratory testing creativ** — AI testează ce îi spui, nu ce n-ai gândit încă
- **Validarea cerințelor cu stakeholderii** — conversațiile umane nu se înlocuiesc
- **Acceptarea codului generat fără review** — AI face greșeli subtile și logice

### Cum să rămâi la curent (domeniu care se schimbă lunar)

- [The Pragmatic Engineer Newsletter](https://newsletter.pragmaticengineer.com/) — AI în engineering
- [Ministry of Testing — AI](https://www.ministryoftesting.com/articles?q=AI) — articole practice QA + AI
- [Lenny's Newsletter](https://www.lennysnewsletter.com/) — produse și unelte AI noi
- Urmărește pe LinkedIn: Angie Jones, Richard Bradshaw, Marcel Veselka — lideri de opinie în QA+AI

### Când ești gata de job ca AI-augmented QA

| Abilități dobândite | Titlu țintit |
|---------------------|-------------|
| Prompt engineering + AI pentru test cases | QA Engineer (with AI skills) |
| + AI coding assistant + test generation | Automation QA Engineer |
| + platforme AI-powered (Applitools/Mabl) | Senior QA / AI Test Engineer |
| + agent-based testing + MCP workflows | AI Quality Engineer / QA Tech Lead |

---

## 🛠 Stack AI pentru QA

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| LLM general | Claude Sonnet 4.6 / ChatGPT-4o | Freemium |
| AI coding assistant | GitHub Copilot | $10/lună |
| IDE cu AI | Cursor | Freemium |
| Visual AI testing | Applitools Eyes | Trial gratuit |
| Self-healing E2E | Testim / Mabl | Trial gratuit |
| AI test generation | Diffblue Cover (Java) | Trial gratuit |
| Date sintetice | Faker + ChatGPT prompt | Gratuit |
| Autonomous browsing | Browser Use | Open-source |
| Log analysis | Sentry | Freemium |
| AI CLI agent | Claude Code | Pay-per-use |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 3–4 luni (part-time) |
| **Nivel de start** | QA tester sau automation engineer cu experiență de bază |
| **Nivel de final** | AI-augmented QA Engineer |
| **Cost** | Majoritar gratuit (unele unelte au trial sau tier gratuit) |
| **Focus** | Productivitate 3–5x, nu înlocuirea rolului |
| **Pasul următor** | Automatizare cu [Java](./cale-invatare-de-la-testare-manuala-la-automatizare-java.md) sau [Playwright](./cale-invatare-de-la-testare-manuala-la-automatizare-typescript.md) ca fundament solid |
| **Avertisment** | Domeniu în schimbare rapidă — reevaluează uneltele la 6 luni |