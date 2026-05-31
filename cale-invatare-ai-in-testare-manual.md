# 🤖 AI în Testare — pentru Testeri Manuali

> Fără cod · Prompt Engineering · Platforme no-code AI · ~1–2 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Prompt Engineering pentru QA](#-faza-1--prompt-engineering-pentru-qa-23-săptămâni)
- [Faza 2 — AI pentru analiză cerințe & test design](#-faza-2--ai-pentru-analiză-cerințe--test-design-23-săptămâni)
- [Faza 3 — AI pentru bug reporting & analiză](#-faza-3--ai-pentru-bug-reporting--analiză-12-săptămâni)
- [Faza 4 — Platforme de testare no-code AI-powered](#-faza-4--platforme-de-testare-no-code-ai-powered-23-săptămâni)
- [Faza 5 — Integrare în fluxul zilnic](#-faza-5--integrare-în-fluxul-zilnic-1-săptămână)
- [Sfaturi practice](#-sfaturi-practice)

---

## 🟢 Faza 1 — Prompt Engineering pentru QA (2–3 săptămâni)

> Abilitatea de bază. Calitatea a ceea ce primești de la AI depinde direct de calitatea a ceea ce îi ceri.

| Resursă | Durată | Link |
|---------|--------|------|
| Prompt Engineering Guide — promptingguide.ai | ~3h | [→ Deschide](https://www.promptingguide.ai/) |
| Prompt Engineering for QA — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/ai-and-prompt-engineering-for-test-automation/) |

**Ce vei învăța:**
- **Zero-shot vs Few-shot** — când dai exemple AI-ului și când nu e nevoie
- **Role prompting** — „Ești un QA senior cu 10 ani în testarea aplicațiilor financiare..."
- **Structured output** — ceri răspunsul în format tabel, Gherkin, JSON, etc.
- **Prompting iterativ** — rafinezi în pași, nu aștepți rezultat perfect din prima
- Diferența dintre ChatGPT, Claude și Gemini pentru sarcini QA — când contează

**Prompturi esențiale — copiază și adaptează:**

```
# Test cases dintr-o cerință
Ești un QA senior. Analizează această cerință și generează test cases complete
în format tabel cu coloanele: ID | Titlu | Precondiții | Pași | Rezultat Așteptat | Prioritate.
Acoperă: happy path, edge cases, negative testing și boundary values.
Cerința: [cerința ta]

# Scenarii Gherkin / BDD
Scrie scenarii BDD în Gherkin pentru funcționalitatea de [descriere].
Folosește Given/When/Then. Include: happy path, eroare de validare, un edge case.
Datele variabile să fie în Scenario Outline cu Examples.

# Review test cases existente
Revizuiește aceste test cases și identifică: gaps în acoperire, pași neclari,
cazuri lipsă (negative testing, boundary values) și duplicate.
[lipește test cases-urile tale]

# Test plan dintr-o descriere de feature
Scrie un test plan sumar pentru funcționalitatea de [descriere].
Include: obiectiv, tipuri de testare, criterii de intrare/ieșire, riscuri,
medii necesare și estimare de efort.
```

**Exercițiu zilnic — Săptămâna 1:**
- Zi 1–2: Generează test cases pentru o funcționalitate reală din munca ta
- Zi 3–4: Compară rezultatele ChatGPT vs Claude — notează diferențele calitative
- Zi 5: Rafinează același prompt de 3 ori, observă cum se îmbunătățesc rezultatele

---

## 🔵 Faza 2 — AI pentru analiză cerințe & test design (2–3 săptămâni)

> Cel mai mare câștig de timp pentru un tester manual: AI analizează cerințele și găsește ambiguitățile înaintea ta.

**Ce poți delega AI-ului:**

**Analiză cerințe:**
```
Analizează această cerință și identifică:
1. Ambiguități — ce nu e clar definit
2. Cazuri neacoperite — scenarii posibile nemenționate
3. Conflicte — contradicții față de alte cerințe
4. Întrebări pentru BA/PO — ce ai nevoie să clarifici înainte să testezi
Cerința: [cerința ta]
```

**Matrice de acoperire:**
```
Am aceste cerințe: [lista cerințelor]
Și aceste test cases: [lista TC-urilor]
Creează o matrice de trasabilitate și identifică cerințele fără acoperire.
```

**Tehnici de test design aplicate automat:**
```
Aplică Boundary Value Analysis și Equivalence Partitioning pe câmpul:
- Tip: numeric
- Valori acceptate: 18–65
- Mesaj eroare sub limită: "Vârsta minimă este 18 ani"
- Mesaj eroare peste limită: "Vârsta maximă este 65 ani"
Generează toate cazurile de test rezultate.
```

**Generare date de test:**
```
Generează 15 seturi de date de test pentru un formular de înregistrare cu câmpurile:
firstName, lastName, email, phone (RO format), birthDate, country.
Include: date valide, date invalide pentru fiecare câmp, caractere speciale,
câmpuri goale, valori la limită. Format: tabel markdown.
```

**Resurse suplimentare:**
| Resursă | Durată | Link |
|---------|--------|------|
| AI for Test Design — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/ai-in-software-testing) |
| ChatGPT for Testers — Udemy (gratuit periodic) | ~3h | [→ Caută](https://www.udemy.com/) |

---

## 🟡 Faza 3 — AI pentru bug reporting & analiză (1–2 săptămâni)

> Două lucruri consumatoare de timp rezolvate rapid: scrieri de bug reports clare și înțelegerea erorilor tehnice.

| Resursă | Durată | Link |
|---------|--------|------|
| How to Write Better Bug Reports Using AI — Ministry of Testing | ~1h | [→ Deschide](https://www.ministryoftesting.com/articles/using-ai-to-improve-bug-reports) |
| ChatGPT Prompt Engineering for Developers — DeepLearning.AI | ~2h | [→ Deschide](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) |
| Using AI to Analyze Log Files — Semaphore CI Blog | ~1h | [→ Deschide](https://semaphoreci.com/blog/ai-software-testing) |

**Îmbunătățire bug reports:**
```
Rescrie acest bug report în format profesionist, clar și complet.
Adaugă: titlu concis în format "[Componentă] — Descriere scurtă",
pași de reproducere numerotați, comportament actual vs așteptat,
severitate sugerată și ce informații lipsesc pentru reproducere.
Bug report original: [textul tău]
```

**Înțelegerea erorilor tehnice din consolă:**
```
Explică această eroare din consola browser-ului în termeni simpli,
fără jargon tehnic. Spune-mi: ce a cauzat-o, ce componentă e afectată
și ce informații ar ajuta un developer să o rezolve.
Eroarea: [paste din consolă]
```

**Prioritizare backlog de buguri:**
```
Am aceste buguri raportate: [lista cu titluri și descrieri scurte]
Sugerează o prioritizare bazată pe: impact asupra utilizatorului,
frecvența probabilă de întâlnire și severitate tehnică.
Explică raționamentul pentru primele 3.
```

**Detectarea duplicatelor:**
```
Verifică dacă aceste două bug reports descriu același defect sau defecte diferite.
Dacă sunt duplicate, care e cel mai complet?
Bug 1: [descriere]
Bug 2: [descriere]
```

---

## 🟣 Faza 4 — Platforme de testare no-code AI-powered (2–3 săptămâni)

> Unelte care automatizează fără să scrii cod — potrivite dacă nu vrei sau nu ai nevoie de programare.

| Platformă | Ce face AI-ul | Tier gratuit | Link |
|-----------|--------------|--------------|------|
| Testim | Recorder + auto-healing teste E2E | Da | [→ Deschide](https://www.testim.io/) |
| Mabl | Teste E2E cu ML + anomaly detection | Trial | [→ Deschide](https://www.mabl.com/) |
| Katalon AI | Recorder + AI authoring în Katalon Studio | Da | [→ Deschide](https://katalon.com/) |
| Rainforest QA | Teste scrise în limbaj natural, executate de AI | Trial | [→ Deschide](https://www.rainforestqa.com/) |

**Ce vei învăța:**

**Testim — Self-Healing Recorder:**
- Înregistrezi un flux în browser — AI generează testul
- Când un buton sau câmp se schimbă în UI, AI-ul îl găsește singur (self-healing)
- Nu scrii nicio linie de cod — descrii pașii, Testim îi execută
- Analytics AI — detectează testele flaky și cauzele

**Mabl — Intelligent E2E Testing:**
- Recorder inteligent — înregistrezi o dată, rulezi pe orice browser
- Auto-healing locators — nu mai petreci ore actualizând teste rupte
- Anomaly Detection — ML-ul detectează regresii de performanță și UI
- Rapoarte clare pentru stakeholderi non-tehnici

**Rainforest QA — Limbaj natural:**
- Scrii testele exact ca pași manuali: „Click pe butonul Login, verifică că apare pagina Dashboard"
- AI execută și raportează — tu nu scrii cod, nu configurezi browsere
- Potrivit dacă echipa ta are deja Rainforest implementat

> ⚠️ **Limitele platformelor no-code:** Self-healing nu e magie — dacă UI-ul se schimbă dramatic, testele pică oricum. Aceste unelte reduc mentenanța, nu o elimină. Pentru testare complexă cu logică de business, codul rămâne mai flexibil.

---

## 🔴 Faza 5 — Integrare în fluxul zilnic (1 săptămână)

> Obiectivul final nu e să știi să folosești AI — e să îl folosești fără să te gândești că îl folosești.

| Resursă | Durată | Link |
|---------|--------|------|
| AI in Your QA Workflow — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/ai-in-software-testing) |
| Practical AI for Testers — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/ai-and-prompt-engineering-for-test-automation/) |
| Getting Started with Claude — Anthropic Docs | ~1h | [→ Deschide](https://docs.anthropic.com/en/docs/welcome) |

**Rutina zilnică recomandată:**

| Activitate QA | Cu AI | Timp economisit |
|---------------|-------|-----------------|
| Citești o cerință nouă | Paste în Claude → „Identifică ambiguitățile și generează primele 20 TC" | 60–70% |
| Scrii un bug report | AI rescrie draft-ul tău în format complet | 40–50% |
| Pregătești un sprint de testare | AI generează test plan sumar din descrierea funcționalităților | 50–60% |
| Primești o eroare din consolă | Paste în ChatGPT → explicație simplă + ce raportezi în Jira | 80% |
| Review test cases colegi | AI identifică lacunele și cazurile lipsă | 30–40% |

**Limite pe care le accepți conștient:**
- Verifici întotdeauna rezultatele AI — hallucination-urile sunt reale
- Test cases generate de AI nu cunosc contextul de business — tu adaugi asta
- Nu lași AI să ia decizia de release — asta rămâne la tine

---

## 💡 Sfaturi practice

### Cele mai frecvente greșeli

- **Prompt vag** → rezultat vag. „Generează teste" nu funcționează. „Generează 15 test cases negative pentru câmpul email, format tabel, include mesajele de eroare așteptate" — funcționează.
- **Acceptarea primului rezultat** — rafinează de cel puțin 2 ori înainte să folosești rezultatul
- **Folosit pentru decizii de business** — AI nu știe că modulul X e critic pentru client Y

### Cum să rămâi la curent

- [Ministry of Testing — AI](https://www.ministryoftesting.com/articles?q=AI) — articole practice, fără hype
- [The Pragmatic Engineer](https://newsletter.pragmaticengineer.com/) — AI în engineering, nivel înalt
- Testează un tool nou pe lună — peisajul se schimbă rapid

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 1–2 luni (part-time) |
| **Nivel de start** | tester manual cu experiență de bază |
| **Cod necesar** | Zero |
| **Cost** | Majoritar gratuit |
| **Câștig principal** | Productivitate 2–3x pe activitățile repetitive de documentare și analiză |
| **Pasul următor** | [AI în Testare — Automatizare](./cale-invatare-ai-in-testare-automatizare.md) sau [De la Manuală la Automatizare](./cale-invatare-testare-manuala.md) |
