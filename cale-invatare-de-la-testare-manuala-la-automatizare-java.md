# 🤖 De la Testare Manuală la Automatizare — Java

> Java · Selenium UI + API Testing · De la zero absolut · ~5–7 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de programare Java](#-faza-1--fundamente-de-programare--java-68-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Selenium WebDriver UI Automation](#-faza-3--selenium-webdriver--ui-automation-68-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing--rest-assured--postman-46-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-46-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de programare — Java (6–8 săptămâni)

> Fundația e totul. Nu poți scrie teste automate fără să înțelegi codul. Nu sări peste această fază.

| Resursă | Durată | Link |
|---------|--------|------|
| Learn Java — Codecademy | ~25h | [→ Deschide](https://www.codecademy.com/learn/learn-java) |
| Java Developer Track — Hyperskill (JetBrains) | ~60h | [→ Deschide](https://hyperskill.org/tracks/1) |
| Java Reference — W3Schools | referință | [→ Deschide](https://www.w3schools.com/java/) |

**Ce vei învăța:**
- Sintaxă de bază: variabile, tipuri de date, operatori
- Structuri de control: `if/else`, bucle `for`/`while`
- Metode și funcții
- OOP: clase, obiecte, moștenire, interfețe
- Colecții: `List`, `Map`, `Set`
- Excepții și error handling

**Resursa cheie:** Hyperskill — cel mai complet track gratuit pentru Java, cu proiecte practice după fiecare concept.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Configurează mediul de lucru o dată, corect, și nu mai pierzi timp cu el.

| Unealtă | Scop | Link |
|---------|------|------|
| IntelliJ IDEA Community | IDE principal pentru Java | [→ Descarcă](https://www.jetbrains.com/idea/download/) |
| Apache Maven | Gestionare dependențe | [→ Ghid](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |
| Java JDK 21+ | Runtime Java | [→ Adoptium](https://adoptium.net/) |

**Ce vei învăța:**
- Cum funcționează un proiect Maven (`pom.xml`, dependențe, lifecycle)
- Git esențial: `clone`, `commit`, `push`, `pull`, `branch`
- Navigarea IntelliJ: proiecte, run configurations, debugger de bază

---

## 🟡 Faza 3 — Selenium WebDriver — UI Automation (6–8 săptămâni)

> Automatizarea interfeței grafice — click-uri, completare formulare, verificare elemente.

| Resursă | Durată | Link |
|---------|--------|------|
| Selenium WebDriver with Java — TAU | ~8h | [→ Deschide](https://testautomationu.applitools.com/selenium-webdriver-tutorial-java/) |
| JUnit 5 — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/junit5-tutorial/) |
| Page Object Model — TAU | ~2h | [→ Deschide](https://testautomationu.applitools.com/page-object-model-java/) |
| Selenium 4 Official Docs | referință | [→ Deschide](https://www.selenium.dev/documentation/) |

**Ce vei învăța:**
- Setup Selenium WebDriver cu ChromeDriver
- Locatori: `id`, `name`, `xpath`, `cssSelector`
- Interacțiuni: click, type, select, hover, drag & drop
- Waits: `ImplicitWait`, `ExplicitWait`, `FluentWait`
- JUnit 5: `@Test`, `@BeforeEach`, `@AfterEach`, assertions
- **Page Object Model (POM)** — design pattern esențial pentru teste mentenabile
- Screenshot la eșec, headless mode

**Proiect practic:** Automatizează un flux complet pe un site demo (ex: [automationpractice.pl](http://automationpractice.pl) sau [the-internet.herokuapp.com](https://the-internet.herokuapp.com)) — login, adaugă în coș, checkout.

> ⭐ **Test Automation University (TAU)** — toate cursurile sunt 100% gratuite, create de experți din industrie. Bookmark: [testautomationu.applitools.com](https://testautomationu.applitools.com)

---

## 🟣 Faza 4 — API Testing — REST Assured + Postman (4–6 săptămâni)

> Testarea la nivel de API e mai rapidă, mai stabilă și mai valoroasă decât UI automation. Le vei folosi pe amândouă.

| Resursă | Durată | Link |
|---------|--------|------|
| API Testing Path (v12) — Postman Academy | ~2h 35min | [→ Deschide](https://academy.postman.com/path/api-testing-path-v12) |
| REST Assured — TAU | ~4h | [→ Deschide](https://testautomationu.applitools.com/automating-your-api-tests-with-rest-assured/) |
| REST Assured Official Docs | referință | [→ Deschide](https://rest-assured.io/) |
| Contract Testing cu Pact — TAU | ~2h | [→ Deschide](https://testautomationu.applitools.com/contract-tests/) |

**Ce vei învăța:**
- HTTP methods: `GET`, `POST`, `PUT`, `DELETE`, `PATCH`
- Status codes, headers, request/response body
- REST Assured: sintaxa `given().when().then()`
- Autentificare: Basic Auth, Bearer Token, OAuth 2.0
- Validare JSON cu JsonPath
- JSON Schema validation
- Contract testing (nivel avansat — valoros pe CV)

**Proiect practic:** Scrie o suită completă de teste pentru un API public (ex: [reqres.in](https://reqres.in) sau [jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com)).

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (4–6 săptămâni)

> Diferența dintre un junior și un automation engineer serios.

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/github-actions-tutorial/) |
| Allure Reports — TAU | ~2h | [→ Deschide](https://testautomationu.applitools.com/test-reporting-with-allure/) |
| Selenium Grid + Docker | ~3h | [→ Ghid](https://www.lambdatest.com/blog/docker-selenium-grid/) |
| Portofoliu GitHub public | continuu | [→ GitHub](https://github.com/) |

**Ce vei învăța:**
- CI/CD cu GitHub Actions — rulează testele automat la fiecare `push`
- Rapoarte vizuale cu Allure — stakeholderii văd clar rezultatele
- Selenium Grid — rulează teste în paralel pe multiple browsere
- Docker basics pentru Selenium Grid
- Structura unui framework profesionist

**Proiect final — Frameworkul tău complet:**

```
my-test-framework/
├── src/
│   ├── main/java/
│   │   └── pages/          # Page Object classes
│   └── test/java/
│       ├── ui/             # Selenium tests
│       └── api/            # REST Assured tests
├── .github/
│   └── workflows/
│       └── test.yml        # GitHub Actions CI
├── pom.xml
└── README.md
```

> 💼 **Primul job:** După Faza 3 poți aplica la poziții de Junior Automation QA. Nu aștepta să termini totul — portofoliul tău de pe GitHub vorbește mai tare decât orice certificat.

---

## 💡 Sfaturi practice

### Cum să înveți eficient
- **30–45 minute zilnic** bate 4 ore la weekend. Consistența e singurul secret real
- Scrie cod în timp ce urmărești cursul — nu doar viziona
- Dacă ești blocat mai mult de 30 de minute, caută pe Stack Overflow sau întreabă un model AI
- Commit pe GitHub chiar și codul imperfect — arată progresul

### Când ești gata de job
| Fază completă | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA (Selenium) |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate de testeri
- [TAU Slack](https://testautomationu.applitools.com/) — comunitatea Test Automation University

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | Java | 21 LTS |
| IDE | IntelliJ IDEA Community | latest |
| Build tool | Maven | 3.9+ |
| UI Automation | Selenium WebDriver | 4.x |
| Test framework | JUnit 5 | 5.11+ |
| API Testing | REST Assured | 5.x |
| API Client | Postman | latest |
| Reporting | Allure | 2.x |
| CI/CD | GitHub Actions | — |
| Containers | Docker | latest |
| Version control | Git + GitHub | — |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 5–7 luni (part-time) |
| **Nivel de start** | Zero experiență de programare |
| **Nivel de final** | Junior–Mid Automation QA Engineer |
| **Cost** | 100% gratuit |
| **Limbaj** | Java |
| **Focus** | Selenium UI + REST API Testing |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [AI pentru Automation Engineers](./cale-invatare-ai-in-testare-automatizare.md) |
