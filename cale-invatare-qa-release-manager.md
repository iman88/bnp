# 🚀 QA Release Manager — Cale de Învățare

> Coordonare lansări · Procese de release · Managementul calității la scară · ~4–6 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de release management](#-faza-1--fundamente-de-release-management-34-săptămâni)
- [Faza 2 — Procese și guvernanță](#-faza-2--procese-și-guvernanță-34-săptămâni)
- [Faza 3 — Unelte și automatizare](#-faza-3--unelte-și-automatizare-34-săptămâni)
- [Faza 4 — Coordonarea echipelor](#-faza-4--coordonarea-echipelor-23-săptămâni)
- [Faza 5 — Metrici și îmbunătățire continuă](#-faza-5--metrici-și-îmbunătățire-continuă-23-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)

---

## 🟢 Faza 1 — Fundamente de release management (3–4 săptămâni)

> Un QA Release Manager nu testează el însuși — coordonează procesul prin care codul ajunge în producție în siguranță.

| Resursă | Durată | Link |
|---------|--------|------|
| ITIL 4 Foundation — Axelos | ~20h | [→ Deschide](https://www.axelos.com/certifications/itil-service-management/itil-4-foundation) |
| Release Management — Atlassian | ~2h | [→ Deschide](https://www.atlassian.com/agile/software-development/release) |
| DevOps Fundamentals — Google | ~10h | [→ Deschide](https://www.cloudskillsboost.google/paths/9) |

**Ce înseamnă un release:**

Un release e procesul controlat prin care o versiune de software trece din mediul de dezvoltare în producție. Nu e un eveniment izolat — e rezultatul unui lanț de activități coordonate: testare, aprobare, planificare, execuție și validare post-lansare.

**Tipuri de strategii de lansare:**

| Strategie | Cum funcționează | Risc | Când o folosești |
|-----------|-----------------|------|-----------------|
| Big Bang | Tot odată, pentru toți utilizatorii | Ridicat | Sisteme mici, lansări rare |
| Blue-Green | Două medii identice, comutare instantă | Mediu | Când ai nevoie de rollback rapid |
| Canary | Lansezi la 1–5% din utilizatori, extinzi gradual | Scăzut | Aplicații cu milioane de utilizatori |
| Feature Flags | Cod în producție, funcționalitatea dezactivată | Scăzut | Control granular per utilizator |
| Rolling | Actualizezi instanțele pe rând, fără downtime | Mediu | Aplicații distribuite |

**Ciclul de viață al unui release:**
```
1. Planificare — ce intră în release, cine e responsabil, când
2. Dezvoltare — echipele scriu cod, branch-uri de feature
3. Testare — QA funcțional, regresie, performanță, securitate
4. Stabilizare — bug-uri critice rezolvate, code freeze
5. Aprobare — sign-off din partea QA, business, securitate
6. Lansare — deployment în producție
7. Validare — smoke tests în producție, monitorizare
8. Retrospectivă — ce a mers bine, ce îmbunătățim
```

---

## 🔵 Faza 2 — Procese și guvernanță (3–4 săptămâni)

> Rolul principal al unui QA Release Manager e să definească și să mențină procese clare — nu să rezolve problemele altora, ci să creeze cadrul în care problemele sunt prevenite.

| Resursă | Durată | Link |
|---------|--------|------|
| Release Management — Atlassian Guides | ~3h | [→ Deschide](https://www.atlassian.com/agile/software-development/release) |
| Change Management — ITIL Practitioner | ~5h | [→ Deschide](https://www.axelos.com/certifications/itil-service-management) |
| Definition of Done — Scrum.org | ~1h | [→ Deschide](https://www.scrum.org/resources/blog/done-understanding-definition-done) |
| Branching Strategies — Atlassian | ~2h | [→ Deschide](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) |

**Definition of Done (DoD) — criteriile unui release:**

Un release nu pleacă în producție dacă nu sunt îndeplinite toate criteriile. Le definești tu împreună cu echipa și le aplici fără excepții.

```
□ Toate testele de regresie au trecut (0 eșecuri)
□ Rata de erori în performanță < 1%
□ Nicio vulnerabilitate de securitate de severitate critică sau înaltă deschisă
□ Documentația actualizată
□ Planul de rollback documentat și testat
□ Monitorizarea configurată pentru noile funcționalități
□ Aprobările obținute (QA Lead, Product Owner, Security dacă e cazul)
□ Fereastra de lansare comunicată echipelor de suport
```

**Change Advisory Board (CAB):**

Comitet care aprobă modificările majore înainte de lansare. Ca QA Release Manager, pregătești și prezinți:
- Ce se lansează și de ce
- Riscurile identificate și cum sunt atenuate
- Planul de testare și rezultatele
- Planul de rollback dacă ceva merge rău
- Impactul asupra utilizatorilor și echipelor de suport

**Code Freeze și fereastra de stabilizare:**

Cu câteva zile înainte de lansare, nu mai intră cod nou în release — doar bug-uri critice cu aprobare explicită. Definești:
- Când începe code freeze-ul
- Cine aprobă excepțiile
- Criteriile pentru „critic" vs „poate aștepta"

**Planul de rollback — obligatoriu, nu opțional:**
```
Decizia de rollback se ia dacă:
  - Error rate depășește X% în primele 30 de minute
  - O funcționalitate critică nu funcționează
  - Metrici de business (vânzări, conversii) scad brusc

Procedura de rollback:
  1. Cine ia decizia și în cât timp
  2. Comanda sau procesul tehnic de revenire
  3. Comunicarea internă și externă
  4. Validarea că rollback-ul a funcționat
```

---

## 🟡 Faza 3 — Unelte și automatizare (3–4 săptămâni)

> Un QA Release Manager modern folosește unelte pentru a automatiza activitățile repetitive și a menține vizibilitate asupra stării release-ului.

| Unealtă | Scop | Link |
|---------|------|------|
| Jira + Advanced Roadmaps | Planificare și urmărire release | [→ Deschide](https://www.atlassian.com/software/jira) |
| Confluence | Documentare procese și runbook-uri | [→ Deschide](https://www.atlassian.com/software/confluence) |
| GitHub / GitLab | Gestiunea branch-urilor și aprobărilor | [→ Deschide](https://github.com/) |
| Jenkins / GitHub Actions | Automatizare pipeline CI/CD | [→ Deschide](https://www.jenkins.io/) |
| PagerDuty / Opsgenie | Alertare și management incidente | Freemium |

**Strategia de ramificare (branching strategy):**

```
GitFlow — potrivit pentru release-uri planificate:
  main (producție)
  ├── develop (integrare continuă)
  ├── feature/nume-feature (dezvoltare)
  ├── release/1.2.0 (stabilizare)
  └── hotfix/bug-critic (remedieri urgente în producție)

Trunk-based — potrivit pentru livrare continuă:
  main (tot codul, lansări frecvente cu feature flags)
  └── feature/scurt-lived (maxim 1-2 zile, merge rapid în main)
```

**Release notes — comunicare clară:**
```markdown
## v2.4.0 — 15 Noiembrie 2025

### Funcționalități noi
- Plată cu Apple Pay disponibilă în checkout
- Filtrare produse după rating minim

### Remedieri
- Corectat: eroare la salvarea adresei cu caractere speciale (#1234)
- Corectat: timeout la generarea facturii pentru comenzi mari (#1256)

### Modificări tehnice
- Actualizare dependențe de securitate
- Îmbunătățire performanță la încărcarea paginii de produs (~30%)

### Impact asupra utilizatorilor
- Nicio modificare la fluxurile existente
- Utilizatorii iOS 16+ vor vedea opțiunea Apple Pay
```

**Automatizarea verificărilor pre-release:**
```yaml
# GitHub Actions — gate de calitate înainte de merge în main
name: Release Gate
on:
  pull_request:
    branches: [release/*, main]
jobs:
  quality-gate:
    runs-on: ubuntu-latest
    steps:
      - name: Run regression tests
        run: npx playwright test --project=chromium
      - name: Check test coverage
        run: npx jest --coverage --coverageThreshold='{"global":{"lines":80}}'
      - name: Security scan
        uses: zaproxy/action-baseline@v0.10.0
        with:
          target: ${{ vars.STAGING_URL }}
```

---

## 🟣 Faza 4 — Coordonarea echipelor (2–3 săptămâni)

> Rolul e în mare parte de comunicare și coordonare — nu autoritate tehnică, ci responsabilitate pentru procesul în ansamblu.

**Comunicare în jurul unui release:**

```
Cu 2 săptămâni înainte:
  → Confirmi conținutul release-ului cu Product Owner
  → Comunici data lansării echipelor de QA, dev, ops, suport
  → Identifici dependențele și riscurile

Cu 1 săptămână înainte:
  → Statusul testării — ce e gata, ce nu
  → Decizii privind ce intră și ce amânăm
  → Pregătire runbook de lansare

Cu 1 zi înainte:
  → Code freeze anunțat
  → Toate aprobările colectate
  → Echipele de gardă notificate

În ziua lansării:
  → Briefing cu toți cei implicați
  → Lansare în fereastra stabilită
  → Monitorizare activă primele 2-4 ore

După lansare:
  → Confirmare că totul funcționează
  → Comunicare status către stakeholderi
  → Retrospectivă programată
```

**Cum gestionezi un release eșuat:**

Panica e cel mai mare inamic. Procesul salvează:
1. **Nu reacționezi impulsiv** — strângi datele înainte de orice decizie
2. **Comunici transparent și rapid** — stakeholderii află de la tine, nu din zvonuri
3. **Decizi clar: repari sau dai rollback** — cu criterii predefinite, nu în ceartă
4. **Documentezi tot** — pentru retrospectivă și prevenirea repetiției

---

## 🔴 Faza 5 — Metrici și îmbunătățire continuă (2–3 săptămâni)

> Nu poți îmbunătăți ce nu măsori. Metricile de release îți arată unde pierzi timp, unde apar problemele și unde e potențial de îmbunătățire.

**Metrici DORA — standardul industriei pentru performanța livrărilor:**

| Metrică | Ce măsoară | Performanță bună |
|---------|-----------|-----------------|
| Deployment Frequency | Cât de des lansezi în producție | Zilnic sau mai des (elite) |
| Lead Time for Changes | Timp de la commit la producție | Sub o oră (elite) |
| Change Failure Rate | % de lansări care cauzează incidente | Sub 5% (elite) |
| Time to Restore | Cât durează recuperarea după incident | Sub o oră (elite) |

**Metrici specifice calității release-ului:**
- Rata de bug-uri găsite post-lansare vs pre-lansare
- Numărul de rollback-uri pe trimestru
- Durata medie a ciclului de testare
- Procentul de teste automatizate vs manuale în regresie
- Numărul de excepții de la code freeze

**Retrospectiva de release — întrebările corecte:**
```
Nu: „Cine a greșit?"
Da: „Ce din proces a permis această problemă să ajungă în producție?"

Nu: „De ce nu ați testat mai bine?"
Da: „Ce ne-a lipsit ca să detectăm asta înainte de lansare?"

Nu: „Trebuie să fim mai atenți."
Da: „Ce verificare automată sau proces putem adăuga ca să nu mai depindem de atenție?"
```

---

## 💡 Sfaturi practice

### Ce diferențiază un QA Release Manager bun

- **Procesul înainte de urgență** — dacă ai nevoie să improvizezi la fiecare lansare, procesul e defect
- **Vizibilitate, nu control** — rolul e să știe toți ce se întâmplă, nu să aprobi tu fiecare decizie
- **Rollback e opțiune validă, nu eșec** — un rollback rapid e mai bun decât ore de remediere în producție
- **Documentezi tot** — dacă procesul există doar în capul tău, nu există

### Traseu de carieră

```
QA Engineer (3–5 ani)
    ↓
QA Lead / Senior QA Engineer
    ↓
QA Release Manager
    ↓
Release Train Engineer (SAFe) / DevOps Manager / Director of Engineering
```

### Certificări utile

| Certificare | Relevanță | Link |
|------------|-----------|------|
| ITIL 4 Foundation | Procese de release în organizații mari | [→ Deschide](https://www.axelos.com/) |
| SAFe Release Train Engineer | Organizații care lucrează în SAFe Agile | [→ Deschide](https://scaledagile.com/) |
| PMP (Project Management) | Management proiecte, util pentru coordonare | [→ Deschide](https://www.pmi.org/) |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 4–6 luni (part-time) |
| **Nivel de start** | QA Engineer cu 3–5 ani experiență, înțelegere CI/CD |
| **Nivel de final** | QA Release Manager |
| **Focus** | Procese, coordonare, metrici, comunicare |
| **Diferență față de QA clasic** | Nu testezi — creezi cadrul în care testarea se face corect |
