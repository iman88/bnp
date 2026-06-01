# 🧪 Testare Manuală — Learning Path

> Fundamente solide de QA · De la zero la tester angajabil · ~3–5 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de testare software](#-faza-1--fundamente-de-testare-software-23-săptămâni)
- [Faza 2 — Tehnici de testare](#-faza-2--tehnici-de-testare-23-săptămâni)
- [Faza 3 — Test design & documentare](#-faza-3--test-design--documentare-23-săptămâni)
- [Faza 4 — Bug reporting & tracking](#-faza-4--bug-reporting--tracking-12-săptămâni)
- [Faza 5 — Unelte esențiale pentru QA](#-faza-5--unelte-esențiale-pentru-qa-23-săptămâni)
- [Faza 6 — Testare web & mobile](#-faza-6--testare-web--mobile-23-săptămâni)
- [Certificare ISTQB](#-certificare-istqb)
- [Sfaturi practice](#-sfaturi-practice)

---

## 🟢 Faza 1 — Fundamente de testare software (2–3 săptămâni)

> Înainte să testezi ceva, trebuie să înțelegi *de ce* testăm și *cum* funcționează procesul.

| Resursă | Durată | Link |
|---------|--------|------|
| Software Testing Tutorial — Guru99 | ~6h | [→ Deschide](https://www.guru99.com/software-testing.html) |
| Introduction to Software Testing — Ministry of Testing | ~3h | [→ Deschide](https://www.ministryoftesting.com/articles/an-introduction-to-software-testing) |
| SDLC & STLC Explained — Software Testing Help | ~2h | [→ Deschide](https://www.softwaretestinghelp.com/software-testing-life-cycle/) |
| Agile Testing Overview — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/agile-testing-tutorial/) |

**Ce vei învăța:**
- Ce e testarea software și de ce există — costul unui bug găsit târziu vs devreme
- Tipuri de testare: funcțională vs non-funcțională, black-box vs white-box, regresie vs smoke
- **SDLC** (Software Development Life Cycle) — de unde vine software-ul
- **STLC** (Software Testing Life Cycle) — locul testerului în proces
- Modele: Waterfall, Agile/Scrum — cum lucrează echipele în 2026
- Rolul QA în echipă: QA vs Tester vs QE

---

## 🔵 Faza 2 — Tehnici de testare (2–3 săptămâni)

> Testarea bună nu e aleatorie. Există tehnici sistematice care garantează acoperire maximă cu efort minim.

| Resursă | Durată | Link |
|---------|--------|------|
| Test Design Techniques — Guru99 | ~4h | [→ Deschide](https://www.guru99.com/software-testing-techniques.html) |
| Black Box Testing Techniques — Software Testing Help | ~3h | [→ Deschide](https://www.softwaretestinghelp.com/black-box-testing/) |
| Exploratory Testing — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/exploratory-testing) |
| Boundary Value Analysis & Equivalence Partitioning — Guru99 | ~2h | [→ Deschide](https://www.guru99.com/equivalence-partitioning-boundary-value-analysis.html) |

**Ce vei învăța:**
- **Equivalence Partitioning** — împarte datele de intrare în clase, testează câte una din fiecare
- **Boundary Value Analysis** — bug-urile stau la margini: testează min-1, min, min+1, max-1, max, max+1
- **Decision Tables** — când logica are combinații de condiții
- **State Transition Testing** — aplicații care au stări (ex: cont bancar: activ, blocat, închis)
- **Exploratory Testing** — testare liberă, bazată pe curiozitate și experiență
- **Error Guessing** — unde greșesc de obicei programatorii

**Exercițiu practic:** Aplică toate tehnicile pe un câmp simplu de introducere (ex: câmp „vârstă" care acceptă 18–99). Câte cazuri de test generează fiecare tehnică?

---

## 🟡 Faza 3 — Test design & documentare (2–3 săptămâni)

> Documentația bună e ceea ce separă un tester profesionist de unul care „dă click-uri".

| Resursă | Durată | Link |
|---------|--------|------|
| How to Write Test Cases — Software Testing Help | ~3h | [→ Deschide](https://www.softwaretestinghelp.com/how-to-write-test-cases/) |
| Test Plan Tutorial — Guru99 | ~2h | [→ Deschide](https://www.guru99.com/what-everybody-ought-to-know-about-test-planing.html) |
| Test Case vs Test Scenario — Guru99 | ~1h | [→ Deschide](https://www.guru99.com/test-case-vs-test-scenario.html) |
| Requirements Traceability Matrix — Software Testing Help | ~1h | [→ Deschide](https://www.softwaretestinghelp.com/requirements-traceability-matrix/) |

**Ce vei învăța:**
- **Test Case** — structura unui TC bun: ID, titlu, precondiții, pași, rezultat așteptat, rezultat actual
- **Test Scenario** — diferența față de test case; când folosești fiecare
- **Test Plan** — documentul care descrie ce, cum, cine și când testăm
- **Test Suite** — gruparea cazurilor de test logic
- **RTM (Requirements Traceability Matrix)** — maparea cerințelor la cazuri de test; nimeni nu scapă netestat
- **Test Report** — cum raportezi rezultatele la final de sprint

**Template util:** Creează un Google Sheet cu o suită de teste reală pentru un site pe care îl folosești zilnic (ex: un formular de login, un flux de checkout).

---

## 🟣 Faza 4 — Bug reporting & tracking (1–2 săptămâni)

> Un bug raportat prost e un bug care nu se rezolvă. Arta bug report-ului bun e subestimată.

| Resursă | Durată | Link |
|---------|--------|------|
| Bug Report Tutorial — Software Testing Help | ~2h | [→ Deschide](https://www.softwaretestinghelp.com/how-to-write-good-bug-report/) |
| Bug Life Cycle — Guru99 | ~1h | [→ Deschide](https://www.guru99.com/defect-life-cycle.html) |
| Severity vs Priority — Guru99 | ~1h | [→ Deschide](https://www.guru99.com/defect-severity-in-software-testing.html) |
| Jira for Beginners — Atlassian | ~3h | [→ Deschide](https://www.atlassian.com/software/jira/guides/getting-started/overview) |

**Ce vei învăța:**
- Structura unui bug report complet: titlu, pași de reproducere, comportament actual, comportament așteptat, severitate, prioritate, environment, atașamente
- **Severity vs Priority** — o distincție pe care intervievatorii o adoră: bug critic cu prioritate mică (ex: crash pe un browser nesuportat)
- **Bug Lifecycle** — New → Assigned → Open → Fixed → Retest → Closed (și variantele: Rejected, Deferred, Duplicate)
- **Jira** — creare ticket, tranziții de stare, filtre, dashboard, board Scrum/Kanban
- Cum să reproduci un bug înainte de a-l raporta — dacă nu poți reproduce, nu raportezi

**Exercițiu practic:** Găsește 5 bug-uri reale pe orice site/aplicație publică și scrie bug report-uri complete în Jira (cont gratuit pe jira.atlassian.com).

---

## 🔴 Faza 5 — Unelte esențiale pentru QA (2–3 săptămâni)

> Nu poți fi QA eficient fără câteva unelte de bază. Astea sunt cele care apar în orice descriere de post.

| Unealtă | Scop | Resurse |
|---------|------|---------|
| Chrome DevTools | Inspectat DOM, rețea, consolă JS, cookies | [→ Ghid oficial](https://developer.chrome.com/docs/devtools/) |
| Postman (basics) | Testare manuală API — trimis requests, verificat responses | [→ Cale Postman](./cale-invatare-postman.md) |
| SQL basics | Verificare date în baza de date, query-uri de validare | [→ SQLZoo](https://sqlzoo.net/wiki/SQL_Tutorial) |
| Git basics | Versionare, creare branch, pull request, code review | [→ Pro Git cap. 1–3](https://git-scm.com/book/en/v2) |
| Jira / TestRail | Management test cases și bug tracking | [→ TestRail Intro](https://www.gurock.com/testrail/docs/getting-started/) |

**Ce vei învăța:**

**Chrome DevTools:**
- Tab Network — verifici că request-urile se trimit corect, statusuri HTTP, corpuri de request
- Tab Console — vezi erorile JS care nu sunt vizibile în UI
- Tab Application — cookies, localStorage, sessionStorage
- Tab Elements — inspectezi DOM-ul, identifici locatori pentru automation mai târziu

**SQL pentru QA:**
- `SELECT`, `WHERE`, `JOIN`, `COUNT`, `GROUP BY` — suficient pentru 90% din nevoile unui QA
- Verifici că datele salvate în DB corespund cu ce s-a introdus în UI
- Identifici date de test existente fără să ceri ajutor dev-ilor

---

## 🟤 Faza 6 — Testare web & mobile (2–3 săptămâni)

> Specificul testării pe web și mobile — unde sunt capcanele și cum le eviți.

| Resursă | Durată | Link |
|---------|--------|------|
| Web Application Testing — Software Testing Help | ~4h | [→ Deschide](https://www.softwaretestinghelp.com/web-application-testing/) |
| Cross Browser Testing Guide — BrowserStack | ~2h | [→ Deschide](https://www.browserstack.com/guide/cross-browser-testing) |
| Mobile Testing Tutorial — Guru99 | ~3h | [→ Deschide](https://www.guru99.com/mobile-testing.html) |
| Accessibility Testing Basics — WebAIM | ~2h | [→ Deschide](https://webaim.org/intro/) |

**Ce vei învăța:**

**Testare web:**
- Cross-browser testing: Chrome, Firefox, Safari, Edge — diferențe de comportament
- Responsive testing: cum arată pe desktop, tabletă, telefon
- Testare formulare: validare câmpuri, mesaje de eroare, submit invalid
- Testare navigare: linkuri broken, breadcrumbs, comportamentul butonului Back
- Testare performanță de bază: Lighthouse în DevTools

**Testare mobile:**
- Android vs iOS — diferențe de comportament și UI
- Orientare landscape/portrait, gesturi (swipe, pinch, tap)
- Testare pe device real vs emulator — când contează diferența
- Tipuri de testare mobile: funcțională, compatibilitate, instalare/dezinstalare, întreruperi (apel primit, notificare)

**Accessibility (bonus valoros pe CV):**
- Ce e WCAG și de ce contează legal
- Testare cu screen reader (NVDA/VoiceOver)
- Contrast color, navigare cu tastatura, alt text la imagini

---

## 🏆 Certificare ISTQB

> ISTQB CTFL (Certified Tester Foundation Level) e certificarea standard a industriei. Recunoscută global, cerută în multe joburi.

> 💬 **Notă:** În România, ISTQB este rar o cerință obligatorie la angajare. Valoarea certificării pe piața locală e limitată — un portofoliu solid și experiență practică cântăresc mai mult. Înainte să investești banii personali în examen, verifică dacă angajatorul actual sau cel vizat o oferă ca beneficiu — majoritatea companiilor care o consideră relevantă suportă costul. Ceea ce rămâne cu adevărat valoros din ISTQB sunt noțiunile din syllabus: structurează gândirea unui tester și stabilesc un vocabular comun cu restul industriei. Studiază materialul indiferent de decizia privind examenul.

| Resurse de pregătire | Link |
|---------------------|------|
| Syllabus oficial ISTQB CTFL 4.0 | [→ Descarcă PDF](https://www.istqb.org/certifications/certified-tester-foundation-level) |
| Sample exams oficiale | [→ Deschide](https://www.istqb.org/certifications/certified-tester-foundation-level#exam-resources) |
| Glossar ISTQB | [→ Deschide](https://glossary.istqb.org/) |
| Curs pregătire gratuit — Guru99 | [→ Deschide](https://www.guru99.com/istqb.html) |
| Practice tests — Quizlet | [→ Deschide](https://quizlet.com/subject/istqb/) |

**Ce acoperă examenul:**
- Fundamente de testare (motivație, principii, activități)
- Testare de-a lungul SDLC
- Testare statică (reviews, analiză statică)
- Tehnici de test design (black-box, white-box, experience-based)
- Managementul testării
- Unelte de suport

> 💡 **Cost examen:** ~200 EUR în România. Pregătirea durează ~4–6 săptămâni de studiu concentrat după ce ai parcurs traseul de față. Dacă ai buget limitat, pregătirea fără examen tot îți aduce valoare — syllabus-ul structurează gândirea.

---

## 💡 Sfaturi practice

### Cum să înveți eficient
- **Practică pe produse reale** — nu există site/aplicație fără bug-uri. Testează ce folosești zilnic
- Nu nota pasiv — scrie test case-uri reale, raportează bug-uri reale (bug-urile publice se pot raporta pe GitHub sau forumuri)
- Creează-ți un **portofoliu pe Google Drive / GitHub** cu test plan-uri, test case-uri și bug report-uri scrise de tine
- Intră în **Ministry of Testing** și participă la discuții — comunitatea e activă și prietenoasă

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior QA Tester (entry level) |
| Faza 1–4 + Jira | QA Tester / Manual Tester |
| Faza 1–6 + portofoliu | QA Engineer (manual, cu tranziție spre automation) |
| + ISTQB CTFL | Orice poziție de QA; diferențiere față de candidați fără certificare |

### Ce să pui în CV
- Test case-uri scrise (link la portofoliu)
- Bug report-uri documentate
- Unelte: Jira, Postman, Chrome DevTools, SQL
- Metode: black-box testing, exploratory testing, regression testing
- Certificare ISTQB (dacă o ai)

### Comunități utile
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate globală de QA
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit, activ, cu sfaturi reale de carieră
- [Software Testing Help Forum](https://www.softwaretestinghelp.com/) — articole și forum
- Romanian QA Community — caută pe LinkedIn pentru networking local

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 3–5 luni (part-time) |
| **Nivel de start** | Zero experiență în IT |
| **Nivel de final** | Junior–Mid QA Tester angajabil |
| **Cost** | 100% gratuit (+ ~200 EUR opțional pentru examen ISTQB) |
| **Focus** | Testare funcțională web & mobile, documentație, bug reporting |
| **Certificare** | ISTQB CTFL (opțional, recomandat) |
| **Pasul următor** | [TypeScript + Playwright ⭐](./cale-invatare-de-la-testare-manuala-la-automatizare-typescript.md) · [Java + Selenium](./cale-invatare-de-la-testare-manuala-la-automatizare-java.md) · [Python + Playwright](./cale-invatare-de-la-testare-manuala-la-automatizare-python.md) · [toate opțiunile](./README.md) |