# 👥 QA Tech Lead — Cale de Învățare

> Leadership de echipă · Mentorat · Procese QA · Reprezentare tehnică · ~4–5 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Tranziția de la individual contributor la lider](#-faza-1--tranziția-de-la-individual-contributor-la-lider-23-săptămâni)
- [Faza 2 — Mentorat și dezvoltarea echipei](#-faza-2--mentorat-și-dezvoltarea-echipei-34-săptămâni)
- [Faza 3 — Procese QA și reprezentare în echipa de produs](#-faza-3--procese-qa-și-reprezentare-în-echipa-de-produs-34-săptămâni)
- [Faza 4 — Calitate vs viteză — gestionarea tensiunii](#-faza-4--calitate-vs-viteză--gestionarea-tensiunii-23-săptămâni)
- [Faza 5 — Metrici și vizibilitate pentru management](#-faza-5--metrici-și-vizibilitate-pentru-management-23-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)

---

## 🟢 Faza 1 — Tranziția de la individual contributor la lider (2–3 săptămâni)

> Cea mai dificilă parte a rolului nu e tehnică — e să înțelegi că succesul tău nu mai e definit de ce faci tu, ci de ce face echipa ta.

| Resursă | Durată | Link |
|---------|--------|------|
| The Definition of a Tech Lead — Patrick Kua | ~1h | [→ Deschide](https://www.patkua.com/blog/the-definition-of-a-tech-lead/) |
| Tech Lead vs Engineering Manager — LeadDev | ~1h | [→ Deschide](https://leaddev.com/leadership-skills/what-tech-lead) |
| Situational Leadership — Ken Blanchard | ~2h | [→ Deschide](https://situational.com/blog/the-four-leadership-styles-of-situational-leadership/) |
| An Elegant Puzzle — Will Larson | articole gratuite | [→ Deschide](https://lethain.com/elegant-puzzle/) |

**Ce se schimbă când devii QA Tech Lead:**

Înainte, succesul tău era măsurat în teste scrise, bug-uri găsite, automatizare livrată. Acum succesul tău e măsurat în cât de bine funcționează echipa ta fără tine.

Asta înseamnă că vei petrece mai puțin timp scriind teste și mai mult timp:
- Eliminând blocajele cu care se confruntă colegii
- Luând decizii tehnice care afectează toată echipa
- Reprezentând perspectiva QA în discuții cu developerii și managementul
- Construind un mediu în care oamenii pot lucra eficient

**Greșeala clasică a noilor tech lead-uri:**

Continuă să facă ce știau mai bine — să scrie teste și să rezolve probleme tehnice singuri. E confortabil, e familiar, produce rezultate imediate vizibile. Dar echipa nu crește, dependența de tine crește, și după 6 luni ești supraîncărcat și echipa e la același nivel.

**Regula de bază:** Dacă poți delega ceva la cineva din echipă care poate face lucrul la 70% din calitatea ta, deleagă. Ei vor ajunge la 100% mai repede dacă fac, nu dacă te privesc pe tine.

---

## 🔵 Faza 2 — Mentorat și dezvoltarea echipei (3–4 săptămâni)

> Cel mai important lucru pe care îl face un QA Tech Lead nu e să găsească bug-uri — e să construiască o echipă care găsește bug-uri mai bine decât ar face-o singur.

| Resursă | Durată | Link |
|---------|--------|------|
| The Art of Giving Feedback — HBR | ~1h | [→ Deschide](https://hbr.org/2019/03/the-feedback-fallacy) |
| Radical Candor — Kim Scott | articole gratuite | [→ Deschide](https://www.radicalcandor.com/blog/) |
| How to Run Effective 1-on-1s — LeadDev | ~1h | [→ Deschide](https://leaddev.com/team/how-run-effective-11s) |
| Coaching vs Mentoring — CCL | ~30min | [→ Deschide](https://www.ccl.org/articles/leading-effectively-articles/coaching-vs-mentoring/) |

**Feedback — cum îl dai eficient:**

Feedback-ul care ajută nu e compliment și nici critică. E observație specifică + impact + așteptare clară.

```
❌ „Trebuie să fii mai atent când scrii teste."

✅ „Am observat că testul pentru fluxul de plată nu acoperă cazul
   în care cardul expiră în timpul tranzacției. Asta înseamnă că
   putem rata bug-uri critice în producție. Data viitoare, când
   scrii teste pentru un flux financiar, adaugă explicit cazurile
   de eroare la câmpurile de card."
```

**1-on-1-uri — structura unei întâlniri utile:**

1-on-1-ul nu e o ședință de status. Status-ul îl afli din Jira. 1-on-1-ul e pentru ce nu apare în Jira.

```
Întrebări utile:
- „Ce te blochează în momentul ăsta, pe care eu te pot ajuta să rezolvi?"
- „Ce ai vrea să înveți sau să lucrezi în luna următoare?"
- „E ceva în echipă sau în proces care te frustrează?"
- „Cum te simți în raport cu volumul de muncă din ultimele săptămâni?"

Ce NU faci:
- Nu transformi 1-on-1-ul în raport de activitate
- Nu anulezi sau muți 1-on-1-urile repetat — semnalizează că nu sunt prioritare
- Nu vorbești tu mai mult de 30% din timp
```

**Niveluri de autonomie — cum delegi progresiv:**

| Nivel | Ce îi spui | Când îl folosești |
|-------|-----------|-------------------|
| 1 | „Fă exact asta, exact așa" | Sarcini noi, persoană neexperimentată |
| 2 | „Explorează opțiunile și vino cu o propunere" | Persoană cu experiență, problemă nouă |
| 3 | „Decide tu și informează-mă după" | Persoană de încredere, domeniu cunoscut |
| 4 | „Ai autoritate deplină, rezolvă" | Senior în domeniu, tu ești disponibil dacă e nevoie |

Scopul e să ajungi cât mai repede la nivelul 3–4 cu fiecare membru al echipei, pentru cât mai multe tipuri de sarcini.

**Review de cod de test — cum faci review util, nu critic:**

```
❌ „Acest test e prost scris."

✅ „Locatorul CSS de pe linia 23 e fragil — se va rupe dacă 
   designerul schimbă clasa. Sugerez getByRole('button', {name: 'Submit'})
   care e legat de semantică, nu de stilizare."
```

---

## 🟡 Faza 3 — Procese QA și reprezentare în echipa de produs (3–4 săptămâni)

> Un QA Tech Lead e vocea calității în toate discuțiile tehnice — sprint planning, refinement, design review, retrospectivă.

| Resursă | Durată | Link |
|---------|--------|------|
| QA in Agile — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/agile-testing-tutorial/) |
| Shift-Left Testing — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/shift-left-testing) |
| Three Amigos — Agile Alliance | ~1h | [→ Deschide](https://www.agilealliance.org/glossary/three-amigos/) |
| Defect Triage — Software Testing Help | ~1h | [→ Deschide](https://www.softwaretestinghelp.com/defect-triage/) |

**Sprint Planning — ce aduci ca QA Tech Lead:**
- Estimezi efortul de testare pentru fiecare user story
- Identifici dependențele de testare (ce trebuie gata înainte să poți testa)
- Ridici steagul roșu când story-urile nu au criterii de acceptare clare
- Propui împărțirea story-urilor complexe dacă testarea e imposibil de estimat

**Three Amigos — sesiunile care previn bug-urile:**

Înainte să înceapă dezvoltarea unui feature, stau la masă: BA/PO, Developer, QA. Fiecare pune întrebări din perspectiva lui.

Ca QA Tech Lead, întrebi:
- „Ce se întâmplă dacă utilizatorul face X în loc de Y?"
- „Cum testăm că asta funcționează corect?"
- „Care e comportamentul așteptat la eroare?"
- „Avem date de test disponibile pentru scenariul ăsta?"

Bug-urile găsite în Three Amigos costă zero. Bug-urile găsite în producție costă enorm.

**Triajul defectelor — proces săptămânal:**

```
Criterii de prioritizare:
  P1 — Blochează funcționalitate critică, fără workaround → reparat în același sprint
  P2 — Impact semnificativ, workaround există → reparat în sprint-ul următor
  P3 — Impact minor sau estetic → planificat în backlog
  P4 — Îmbunătățire, nu defect → discutat cu PO dacă merită efortul

Ca QA Tech Lead:
  → Conduci ședința de triaj (30 min/săptămână)
  → Asiguri că fiecare bug are suficiente informații pentru reproducere
  → Decizi împreună cu PO ce intră în sprint și ce așteaptă
```

---

## 🟣 Faza 4 — Calitate vs viteză — gestionarea tensiunii (2–3 săptămâni)

> Aceasta e tensiunea centrală a oricărui rol de calitate. Nu dispare — înveți să o gestionezi.

| Resursă | Durată | Link |
|---------|--------|------|
| Quality vs Speed — Ministry of Testing | ~1h | [→ Deschide](https://www.ministryoftesting.com/articles/quality-vs-speed) |
| Technical Debt — Martin Fowler | ~1h | [→ Deschide](https://martinfowler.com/bliki/TechnicalDebt.html) |
| The Cost of Poor Quality — ASQ | ~1h | [→ Deschide](https://asq.org/quality-resources/cost-of-quality) |

**Cum argumentezi pentru calitate fără să pari că blochezi livrările:**

Managementul înțelege bani și risc, nu principii de inginerie. Traduce:

```
❌ „Nu putem lansa, nu am terminat testele de regresie."

✅ „Putem lansa cu riscul X — am identificat 3 scenarii netestare
   în fluxul de plată. Dacă unul din ele pică în producție, impactul
   estimat e Y ore de downtime sau Z tranzacții afectate. Decizia
   de a lansa e a voastră — eu vă dau datele."
```

**Datoria tehnică în testare — când o accepți, când nu:**

Nu orice scurtătură e datorie tehnică toxică. Uneori accepți conștient că un test e mai fragil sau mai puțin acoperitor, cu planul explicit de a reveni.

Datoria tehnică devine problemă când:
- Nu e documentată — nimeni nu știe că există
- Nu are plan de rambursare — se acumulează indefinit
- Afectează încrederea în suită — testele pică des fără motiv real

**Cum spui „nu" fără să spui „nu":**

```
„Putem lansa dacă acceptăm riscul X și planificăm Y în sprint-ul următor."
„Putem reduce timpul de testare dacă renunțăm la acoperirea scenariului Z —
 vrei să documentăm asta ca risc asumat?"
„Pot livra până joi dacă renunțăm la testele de performanță din acest sprint."
```

Oferi mereu opțiuni cu consecințe clare. Nu decizi tu unilateral — dar asiguri că decizia se ia informat.

---

## 🔴 Faza 5 — Metrici și vizibilitate pentru management (2–3 săptămâni)

> Dacă munca echipei tale nu e vizibilă pentru management, nu există. Metricile sunt povestea pe care o spui cu date.

| Resursă | Durată | Link |
|---------|--------|------|
| QA Metrics that Matter — Ministry of Testing | ~2h | [→ Deschide](https://www.ministryoftesting.com/articles/qa-metrics) |
| DORA Metrics — Google | ~1h | [→ Deschide](https://cloud.google.com/blog/products/devops-sre/using-the-four-keys-to-measure-your-devops-performance) |
| Goodhart's Law in Engineering | ~30min | [→ Deschide](https://martinfowler.com/bliki/MeasuringSuccess.html) |

**Metrici utile vs metrici periculoase:**

| Metrică | Problemă dacă e singurul indicator |
|---------|-----------------------------------|
| Număr de bug-uri găsite | Stimulează raportarea de bug-uri minore, nu calitatea |
| Acoperire cod (%) | 80% acoperire cu teste proaste e mai rău decât 50% cu teste bune |
| Teste scrise per sprint | Stimulează cantitatea, nu calitatea sau relevanța |
| Timp de execuție suită | Util, dar nu spune nimic despre ce testezi |

**Metrici care dau o imagine reală:**
- Rata de bug-uri găsite în producție vs pre-producție — arată eficiența procesului
- Timpul mediu de la raportare la remediere — arată colaborarea cu dev
- Rata de regresie — bug-uri care reapar după ce au fost rezolvate
- Stabilitatea suitei — procentul de teste flaky din total

**Cum raportezi la management fără să îngropi oamenii în cifre:**

```
Format lunar — o pagină:

Starea calității în [luna]:
  ✅ 3 lansări fără incidente majore în producție
  ✅ Rata de bug-uri post-lansare: 0.8% (față de 2.3% în luna anterioară)
  ⚠️ Suita de regresie: 4% teste flaky — plan de remediere în sprint 12
  🔴 2 bug-uri P1 identificate în sprint-ul curent, ambele rezolvate înainte de lansare

Riscuri pentru luna viitoare:
  → Lansarea modulului de facturare — acoperire de testare insuficientă
    pentru scenariile de TVA internațional
```

---

## 💡 Sfaturi practice

### Ce face un QA Tech Lead bun diferit de un senior QA bun

Un senior QA bun rezolvă probleme. Un QA Tech Lead bun construiește sisteme care previn problemele.

Diferența concretă:
- Senior QA găsește bug-ul de autentificare → QA Tech Lead introduce procesul de Three Amigos care previne bug-ul
- Senior QA scrie teste de regresie → QA Tech Lead decide ce nivel de automatizare e potrivit pentru echipă și produs
- Senior QA raportează că lansarea are riscuri → QA Tech Lead prezintă riscurile cu date și opțiuni de mitigare

### Semnale că ești pe drumul cel bun

- Membrii echipei vin la tine pentru orientare, nu pentru răspunsuri
- Poți lipsi o săptămână și echipa continuă să funcționeze normal
- Managementul te întreabă perspectiva înainte să ia decizii care afectează calitatea
- Bug-urile critice sunt găsite înainte de lansare, nu după

### Traseu de carieră

```
Senior QA / Automation Engineer (3–5 ani)
    ↓
QA Tech Lead (2–4 ani)
    ↓
Test Arhitect / Engineering Manager / QA Release Manager
```

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 4–5 luni (part-time) |
| **Nivel de start** | Senior QA Engineer cu 3–5 ani experiență |
| **Nivel de final** | QA Tech Lead |
| **Focus** | Oameni, procese, reprezentare tehnică, metrici |
| **Diferență față de Test Arhitect** | Mai aproape de echipă și execuție zilnică; mai puțin strategie și arhitectură pe termen lung |
| **Diferență față de QA Release Manager** | Tech Lead-ul conduce echipa de QA; Release Manager-ul coordonează procesul de lansare cross-echipe |
