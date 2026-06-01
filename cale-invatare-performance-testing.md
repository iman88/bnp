# ⚡ Performance Testing — Cale de Învățare

> Testare de performanță · JMeter · k6 · Monitorizare · ~3–4 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de testare a performanței](#-faza-1--fundamente-de-testare-a-performanței-23-săptămâni)
- [Faza 2 — Apache JMeter](#-faza-2--apache-jmeter-46-săptămâni)
- [Faza 3 — k6 — alternativa modernă](#-faza-3--k6--alternativa-modernă-34-săptămâni)
- [Faza 4 — Analiză rezultate și identificare blocaje](#-faza-4--analiză-rezultate-și-identificare-blocaje-23-săptămâni)
- [Faza 5 — Integrare în CI/CD și monitorizare](#-faza-5--integrare-în-cicd-și-monitorizare-23-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de testare a performanței (2–3 săptămâni)

> Înainte să rulezi orice test de performanță, trebuie să înțelegi ce măsori, de ce și ce înseamnă rezultatele.

| Resursă | Durată | Link |
|---------|--------|------|
| Performance Testing Guide — Guru99 | ~4h | [→ Deschide](https://www.guru99.com/performance-testing.html) |
| Performance Testing — BlazeMeter University | ~3h | [→ Deschide](https://www.blazemeter.com/university) |
| Introduction to Performance Testing — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/performance-testing-tutorial/) |

**Tipuri de teste de performanță:**

| Tip | Ce simulează | Când îl folosești |
|-----|-------------|-------------------|
| Load Testing | Numărul așteptat de utilizatori simultani | Înainte de orice lansare |
| Stress Testing | Peste capacitatea maximă — până când cedează | Găsești limita sistemului |
| Spike Testing | Creștere bruscă și masivă de trafic | Promoții, evenimente, campanii |
| Soak / Endurance | Număr normal de utilizatori, timp îndelungat | Depistezi scurgeri de memorie |
| Scalability Testing | Creștere graduală — observi cum scalează | Planificare de capacitate |

**Metrici esențiale de înțeles:**

| Metrică | Definiție | Valoare bună |
|---------|-----------|-------------|
| Response Time | Timpul de la cerere la răspuns complet | < 2s pentru 95% din cereri |
| Throughput | Cereri procesate pe secundă (TPS/RPS) | Depinde de aplicație |
| Error Rate | Procentul de cereri eșuate | < 1% |
| Concurrency | Numărul de utilizatori activi simultan | Definit de business |
| Percentile P95/P99 | Timpul sub care se încadrează 95%/99% din cereri | P95 < 3s, P99 < 5s |

**De ce percentilele contează mai mult decât media:**
Media ascunde problemele. Dacă 99% din cereri durează 100ms dar 1% durează 30 de secunde, media arată 400ms — acceptabil. Dar 1% din utilizatorii tăi au o experiență dezastruoasă. P99 arată adevărul.

**Concepte fundamentale:**
- **Think time** — pauza dintre acțiunile unui utilizator real (nu trimiți 100 cereri pe secundă fără pauză)
- **Ramp-up** — creșterea graduală a numărului de utilizatori, nu toți deodată
- **Baseline** — măsurarea performanței actuale înainte de orice optimizare
- **Bottleneck** — componenta care limitează performanța întregului sistem

---

## 🔵 Faza 2 — Apache JMeter (4–6 săptămâni)

> JMeter e unealta standard a industriei pentru testare de performanță — gratuită, open-source, cu interfață grafică și suport larg.

| Resursă | Durată | Link |
|---------|--------|------|
| JMeter — Docs oficiale | referință | [→ Deschide](https://jmeter.apache.org/usermanual/index.html) |
| JMeter Tutorial — Guru99 | ~5h | [→ Deschide](https://www.guru99.com/jmeter-tutorials.html) |
| JMeter — BlazeMeter Academy | ~4h | [→ Deschide](https://www.blazemeter.com/university) |

**Instalare:**
```bash
# Necesită Java 8+
java -version

# Descarcă și dezarhivează JMeter de pe jmeter.apache.org
# Pornire interfață grafică:
./bin/jmeter.sh      # macOS/Linux
bin\jmeter.bat       # Windows
```

**Structura unui plan de test JMeter:**
```
Test Plan
└── Thread Group (simulează utilizatorii)
    ├── HTTP Request Defaults (URL de bază, port)
    ├── HTTP Cookie Manager (gestionare cookie-uri sesiune)
    ├── HTTP Request — Login
    ├── HTTP Request — Pagina principală
    ├── HTTP Request — Căutare produs
    └── Listeners (rapoarte)
        ├── View Results Tree (debugging)
        ├── Summary Report
        └── Aggregate Report
```

**Configurare Thread Group:**
```
Number of Threads (users): 100     # utilizatori simultani
Ramp-Up Period (seconds): 60       # 60s să pornească toți (1.67 useri/secundă)
Loop Count: 10                     # fiecare utilizator execută scenariul de 10 ori
```

**Parametrizare cu CSV — date de test diferite per utilizator:**
```csv
# users.csv
username,password
user1@test.com,pass123
user2@test.com,pass456
user3@test.com,pass789
```
```
CSV Data Set Config:
  Filename: users.csv
  Variable Names: username,password
  Delimiter: ,
  Recycle on EOF: True

HTTP Request Body:
  {"email": "${username}", "password": "${password}"}
```

**Corelație — extragere date din răspuns:**
```
# Extragi token-ul din răspunsul de login
Regular Expression Extractor:
  Reference Name: authToken
  Regular Expression: "token":"(.+?)"
  Template: $1$

# Folosești în cererea următoare
HTTP Header Manager:
  Authorization: Bearer ${authToken}
```

**Proiect practic:** Scrie un scenariu complet pentru un site demo (ex: [reqres.in](https://reqres.in)) — autentificare, operațiuni CRUD, deconectare. Rulează cu 50 utilizatori simultani și analizează raportul.

---

## 🟡 Faza 3 — k6 — alternativa modernă (3–4 săptămâni)

> k6 e alegerea modernă pentru testare de performanță — scriptare în JavaScript, integrat nativ cu CI/CD, rezultate clare.

| Resursă | Durată | Link |
|---------|--------|------|
| k6 Documentation — Grafana | referință | [→ Deschide](https://k6.io/docs/) |
| k6 Learn — Grafana | ~4h | [→ Deschide](https://k6.io/learn/) |
| k6 School — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/k6-load-testing-tutorial/) |

**Instalare:**
```bash
# Windows (cu Chocolatey)
choco install k6

# macOS
brew install k6

# Linux
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/k6-archive-keyring.gpg \
  --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C5AD17C747E3415A3642D57D77C6C491D6AC1D69
echo "deb [signed-by=/usr/share/keyrings/k6-archive-keyring.gpg] https://dl.k6.io/deb stable main" \
  | sudo tee /etc/apt/sources.list.d/k6.list
sudo apt-get update && sudo apt-get install k6
```

**Primul test k6:**
```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  vus: 50,           // 50 utilizatori virtuali
  duration: '2m',   // timp total de rulare
};

export default function () {
  const response = http.get('https://reqres.in/api/users');

  check(response, {
    'status este 200': (r) => r.status === 200,
    'timp răspuns < 500ms': (r) => r.timings.duration < 500,
    'are date utilizatori': (r) => JSON.parse(r.body).data.length > 0,
  });

  sleep(1); // think time — pauza între acțiuni
}
```

**Scenarii avansate — ramp-up progresiv:**
```javascript
export const options = {
  scenarios: {
    ramp_up: {
      executor: 'ramping-vus',
      startVUs: 0,
      stages: [
        { duration: '2m', target: 50 },   // crește la 50 utilizatori în 2 min
        { duration: '5m', target: 50 },   // menține 50 utilizatori 5 min
        { duration: '2m', target: 100 },  // crește la 100 utilizatori
        { duration: '5m', target: 100 },  // menține 100 utilizatori
        { duration: '2m', target: 0 },    // reduce la 0
      ],
    },
  },
  thresholds: {
    http_req_duration: ['p(95)<2000'],  // 95% din cereri sub 2s — dacă nu, testul pică
    http_req_failed: ['rate<0.01'],     // mai puțin de 1% erori
  },
};
```

**k6 vs JMeter — când alegi ce:**

| Criteriu | JMeter | k6 |
|---------|--------|-----|
| Interfață | Grafică (GUI) | Linie de comandă + cod |
| Limbaj | GUI / Groovy | JavaScript |
| Integrare CI/CD | Posibilă, mai complexă | Nativă, simplă |
| Resurse sistem | Mai multe | Foarte eficient |
| Comunitate | Matură, mai mare | Modernă, în creștere |
| Rapoarte | Built-in, vizuale | Text + Grafana (opțional) |

---

## 🟣 Faza 4 — Analiză rezultate și identificare blocaje (2–3 săptămâni)

> Un test de performanță fără analiză corectă a rezultatelor e inutil. Asta e partea care diferențiază un tester mediocru de unul valoros.

**Cum citești un raport JMeter:**
```
Samples:     10.000    # total cereri executate
Average:     342ms     # media timpului de răspuns (cu grijă!)
Min:         45ms
Max:         8.432ms   # există cereri foarte lente — problemă
Std. Dev.:   890ms     # variație mare — instabilitate
Error %:     2.3%      # PROBLEMĂ — peste 1% e inacceptabil
Throughput:  48.2/sec  # cereri procesate pe secundă
```

**Unde se ascund blocajele (bottleneck-uri):**

| Componentă | Simptome | Ce verifici |
|------------|----------|-------------|
| Baza de date | Timp de răspuns crește cu încărcarea, erori de timeout | Query-uri lente, index-uri lipsă, conexiuni epuizate |
| Aplicație | CPU ridicat pe server, memory leaks | Cod ineficient, cache absent, scurgeri de resurse |
| Rețea | Latență mare, pachete pierdute | Bandă, CDN, DNS |
| Server web | Coadă de așteptare lungă | Număr de conexiuni, fire de execuție |

**Unelte de monitorizare în timpul testului:**

| Unealtă | Ce monitorizează | Link |
|---------|-----------------|------|
| Grafana + InfluxDB | Metrici k6 în timp real | [→ Deschide](https://grafana.com/) |
| JMeter + Grafana | Metrici JMeter în timp real | [→ Deschide](https://grafana.com/) |
| htop / top | CPU și memorie pe server | built-in Linux |
| New Relic / Datadog | APM — urmărire cereri end-to-end | Freemium |

**Grafana + k6 — vizualizare în timp real:**
```bash
# Pornești InfluxDB și Grafana cu Docker
docker-compose up -d influxdb grafana

# Rulezi k6 cu output spre InfluxDB
k6 run --out influxdb=http://localhost:8086/k6 script.js
```

---

## 🔴 Faza 5 — Integrare în CI/CD și monitorizare (2–3 săptămâni)

> Testele de performanță rulate o dată înainte de lansare sunt insuficiente. Integrate în CI/CD, detectează regresiile de performanță la fiecare modificare.

**k6 în GitHub Actions:**
```yaml
name: Performance Tests
on:
  push:
    branches: [main]
  schedule:
    - cron: '0 2 * * *'  # rulează și noaptea, zilnic

jobs:
  performance:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run k6 load test
        uses: grafana/k6-action@v0.3.0
        with:
          filename: tests/performance/load-test.js
        env:
          BASE_URL: ${{ vars.STAGING_URL }}
      - name: Upload results
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: k6-results
          path: results/
```

**Strategia de testare a performanței:**

```
Mediu de dezvoltare:
  → Smoke test (1-5 utilizatori, 1 minut) — funcționează de bază?

Mediu de testare:
  → Load test (utilizatori normali, 10-30 minute) — comportament normal
  → Stress test (depășire capacitate) — unde se rupe?

Înainte de lansare:
  → Soak test (12-24 ore, sarcină normală) — scurgeri de memorie?
  → Spike test (vârf brusc) — rezistă la trafic neașteptat?
```

**Criterii de acceptare a performanței (SLA):**
```javascript
// Definite în k6 ca thresholds — testul pică dacă nu sunt respectate
export const options = {
  thresholds: {
    'http_req_duration': ['p(95)<2000', 'p(99)<5000'],
    'http_req_failed': ['rate<0.01'],
    'http_reqs': ['rate>100'],  // minim 100 cereri/secundă
  },
};
```

---

## 💡 Sfaturi practice

### Greșeli frecvente în testarea de performanță

- **Testezi direct în producție** — nu face asta niciodată fără aprobare explicită și fereastră de mentenanță
- **Nu incluzi think time** — utilizatorii reali nu trimit 1.000 de cereri pe secundă fără pauze
- **Analizezi doar media** — folosește percentile P95 și P99
- **Nu monitorizezi serverul** — un test fără metrici de server nu îți spune unde e problema
- **Rulezi testul o singură dată** — rulează de cel puțin 3 ori și compară rezultatele
- **Testezi fără date realiste** — 100 utilizatori care citesc aceeași pagină nu e realist

### Cum prezinți rezultatele

Nu prezenta tabele de numere brute stakeholderilor non-tehnici. Traduce în impact:

| În loc de | Spune |
|-----------|-------|
| „P95 = 4.2s" | „1 din 20 utilizatori așteaptă peste 4 secunde la fiecare acțiune" |
| „Error rate = 3%" | „3 din 100 utilizatori primesc eroare" |
| „Throughput = 45 RPS" | „Sistemul poate servi maxim 45 cereri pe secundă — la 100 de utilizatori simultani, începe să aibă probleme" |

### Comunități și resurse continue

- [k6 Community Forum](https://community.grafana.com/c/grafana-k6/) — suport oficial k6
- [BlazeMeter Blog](https://www.blazemeter.com/blog) — articole practice despre JMeter și testare de performanță
- [Performance Testing Guidance — Microsoft](https://learn.microsoft.com/en-us/azure/architecture/best-practices/performance-efficiency) — bune practici arhitecturale

---

## 🛠 Stack tehnologic

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| Testare de performanță (GUI) | Apache JMeter | Gratuit |
| Testare de performanță (cod) | k6 | Gratuit |
| Vizualizare metrici | Grafana + InfluxDB | Gratuit |
| Monitorizare server | Grafana, New Relic (free tier) | Freemium |
| CI/CD | GitHub Actions | Gratuit |
| Platformă de practică | reqres.in, httpbin.org | Gratuit |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 3–4 luni (part-time) |
| **Nivel de start** | Cunoștințe de bază în testare și HTTP |
| **Nivel de final** | QA cu competențe de performanță / Junior Performance Engineer |
| **Cost** | 100% gratuit |
| **Limbaje** | JavaScript (k6) / GUI (JMeter) |
| **Focus** | Load testing, analiză blocaje, integrare CI/CD |
| **Avertisment** | Nu rula teste de performanță în producție fără aprobare |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [QA Tech Lead](./cale-invatare-qa-tech-lead.md) |
