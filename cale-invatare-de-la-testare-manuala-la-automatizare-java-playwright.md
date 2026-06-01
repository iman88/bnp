# ☕ De la Testare Manuală la Automatizare — Java + Playwright

> Java · Playwright UI + API Testing · De la zero absolut · ~5–7 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de programare Java](#-faza-1--fundamente-de-programare-java-68-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Playwright UI Automation](#-faza-3--playwright-ui-automation-56-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing-34-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de programare Java (6–8 săptămâni)

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
- Generics — înțelegi ce scrie Playwright în API-ul Java

**Resursa cheie:** Hyperskill — cel mai complet track gratuit pentru Java, cu proiecte practice după fiecare concept.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Playwright pentru Java se integrează nativ cu Maven și JUnit 5 — același toolchain ca Selenium, fără configurare suplimentară.

| Unealtă | Scop | Link |
|---------|------|------|
| IntelliJ IDEA Community | IDE principal pentru Java | [→ Descarcă](https://www.jetbrains.com/idea/download/) |
| Apache Maven | Gestionare dependențe | [→ Ghid](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |
| Java JDK 21+ | Runtime Java | [→ Adoptium](https://adoptium.net/) |

**`pom.xml` — dependențe de start:**
```xml
<dependencies>
    <dependency>
        <groupId>com.microsoft.playwright</groupId>
        <artifactId>playwright</artifactId>
        <version>1.52.0</version>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.11.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

**Ce vei învăța:**
- Cum funcționează un proiect Maven (`pom.xml`, dependențe, lifecycle)
- Git esențial: `clone`, `commit`, `push`, `pull`, `branch`
- Instalare browsere Playwright: `mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="install"`
- Structura unui proiect Playwright Java:

```
my-playwright-java/
├── src/
│   └── test/
│       └── java/
│           ├── pages/
│           │   └── LoginPage.java
│           └── tests/
│               ├── ui/
│               │   └── LoginTest.java
│               └── api/
│                   └── UsersApiTest.java
├── pom.xml
└── .github/
    └── workflows/
        └── tests.yml
```

---

## 🟡 Faza 3 — Playwright UI Automation (5–6 săptămâni)

> Playwright Java e API-ul oficial Microsoft pentru Java — stabil, complet și activ menținut. Mai modern decât Selenium, fără WebDriver Protocol overhead.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright for Java — Docs oficiale | referință | [→ Deschide](https://playwright.dev/java/docs/intro) |
| Playwright Java Tutorial — Applitools | ~3h | [→ Deschide](https://testautomationu.applitools.com/playwright-intro/) |
| Playwright Java — GitHub Examples | referință | [→ Deschide](https://github.com/microsoft/playwright-java) |

**Ce vei învăța:**

**Arhitectura Playwright Java:**
```java
// Playwright creează browsere și pagini
try (Playwright playwright = Playwright.create()) {
    Browser browser = playwright.chromium().launch(
        new BrowserType.LaunchOptions().setHeadless(false)
    );
    BrowserContext context = browser.newContext();
    Page page = context.newPage();
    page.navigate("https://example.com");
}
```

**Locatori moderni — prioritate în această ordine:**
```java
page.getByRole(AriaRole.BUTTON, new Page.GetByRoleOptions().setName("Login"))
page.getByLabel("Email")
page.getByPlaceholder("Enter email")
page.getByText("Welcome back")
page.getByTestId("submit-btn")
page.locator(".css-selector")   // CSS ca fallback
```

**JUnit 5 + Playwright — setup cu `@BeforeAll` / `@BeforeEach`:**
```java
public class BaseTest {
    static Playwright playwright;
    static Browser browser;
    BrowserContext context;
    Page page;

    @BeforeAll
    static void launchBrowser() {
        playwright = Playwright.create();
        browser = playwright.chromium().launch();
    }

    @BeforeEach
    void createContextAndPage() {
        context = browser.newContext();
        page = context.newPage();
    }

    @AfterEach
    void closeContext() {
        context.close();
    }

    @AfterAll
    static void closeBrowser() {
        playwright.close();
    }
}
```

**Page Object Model cu Java:**
```java
public class LoginPage {
    private final Page page;
    private final Locator emailInput;
    private final Locator passwordInput;
    private final Locator loginButton;

    public LoginPage(Page page) {
        this.page = page;
        this.emailInput = page.getByLabel("Email");
        this.passwordInput = page.getByLabel("Password");
        this.loginButton = page.getByRole(AriaRole.BUTTON,
            new Page.GetByRoleOptions().setName("Login"));
    }

    public void login(String email, String password) {
        emailInput.fill(email);
        passwordInput.fill(password);
        loginButton.click();
    }
}

// Test care folosește POM
class LoginTest extends BaseTest {
    @Test
    void loginWithValidCredentials() {
        LoginPage loginPage = new LoginPage(page);
        page.navigate("https://example.com/login");
        loginPage.login("user@test.com", "secret123");
        assertThat(page).hasURL("https://example.com/dashboard");
    }
}
```

**Assertions native Playwright:**
```java
import static com.microsoft.playwright.assertions.PlaywrightAssertions.assertThat;

assertThat(page).hasURL("https://example.com/dashboard");
assertThat(page.getByRole(AriaRole.HEADING)).containsText("Welcome");
assertThat(page.locator(".error-msg")).isVisible();
assertThat(page.locator(".error-msg")).hasText("Invalid credentials");
```

**Funcții avansate:**
- **Codegen**: `mvn exec:java -e -D exec.mainClass=com.microsoft.playwright.CLI -D exec.args="codegen https://site.com"`
- **Trace Viewer** — debugging vizual complet: `playwright show-trace trace.zip`
- Network interception: `page.route("**/api/**", route -> route.fulfill(...))`
- Screenshot la eșec: `page.screenshot(new Page.ScreenshotOptions().setPath(Paths.get("screenshot.png")))`
- Rulare paralelă cu JUnit 5: `@TestMethodOrder` + thread-local `Page`

**Proiect practic:** Automatizează un flux complet pe [demoqa.com](https://demoqa.com) sau [the-internet.herokuapp.com](https://the-internet.herokuapp.com) — login, formular, navigare, validare. Minim 10 teste cu POM.

> ⭐ **Avantaj Playwright față de Selenium:** Auto-waiting pentru toate acțiunile, trace viewer built-in, codegen, și assertions specifice pentru browser — toate fără configurare extra.

---

## 🟣 Faza 4 — API Testing (3–4 săptămâni)

> Playwright Java include API testing built-in — sau poți folosi REST Assured, standardul industriei Java pentru API testing.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright API Testing (Java) — Docs | referință | [→ Deschide](https://playwright.dev/java/docs/api-testing) |
| REST Assured — TAU | ~4h | [→ Deschide](https://testautomationu.applitools.com/automating-your-api-tests-with-rest-assured/) |
| REST Assured Official Docs | referință | [→ Deschide](https://rest-assured.io/) |

**Opțiunea 1 — Playwright API Testing (recomandat pentru proiecte Playwright-only):**
```java
@Test
void getUsersReturns200() {
    APIRequestContext request = playwright.request().newContext(
        new APIRequest.NewContextOptions().setBaseURL("https://reqres.in")
    );
    APIResponse response = request.get("/api/users?page=1");
    assertEquals(200, response.status());
    assertTrue(response.ok());
}
```

**Opțiunea 2 — REST Assured (recomandat dacă ai deja proiecte cu Selenium/REST Assured):**
```java
given()
    .baseUri("https://reqres.in")
    .contentType(ContentType.JSON)
    .body("""{"name": "Ion Pop", "job": "QA Engineer"}""")
.when()
    .post("/api/users")
.then()
    .statusCode(201)
    .body("name", equalTo("Ion Pop"))
    .body("id", notNullValue());
```

**Ce vei acoperi:**
- HTTP methods: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
- Autentificare: Bearer Token, Basic Auth, API Key în headers
- Validare JSON cu JsonPath
- Pattern hybrid: setup stare via API → verificare UI → teardown via API

**Proiect practic:** Suită API completă pentru [reqres.in](https://reqres.in) — CRUD complet, autentificare, validare răspuns, teste negative.

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (3–4 săptămâni)

> Framework-ul rulează în cloud, rapoartele sunt clare, testele sunt stabile și ușor de menținut.

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions + Maven | ~3h | [→ Deschide](https://docs.github.com/en/actions) |
| Allure with JUnit 5 — Docs | ~2h | [→ Deschide](https://allurereport.org/docs/junit5/) |
| Playwright Docker (Java) | ~2h | [→ Deschide](https://playwright.dev/java/docs/docker) |

**GitHub Actions CI:**
```yaml
name: Playwright Java Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: mcr.microsoft.com/playwright/java:v1.52.0-jammy
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: mvn test
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: allure-results
          path: target/allure-results/
```

**Allure Reports:**
```xml
<!-- pom.xml -->
<dependency>
    <groupId>io.qameta.allure</groupId>
    <artifactId>allure-junit5</artifactId>
    <version>2.27.0</version>
    <scope>test</scope>
</dependency>
```
```bash
mvn allure:serve
```

**Rulare paralelă cu JUnit 5:**
```
# junit-platform.properties
junit.jupiter.execution.parallel.enabled=true
junit.jupiter.execution.parallel.mode.default=concurrent
junit.jupiter.execution.parallel.config.strategy=dynamic
```

> 💼 **Primul job:** Java + Playwright e o combinație mai rară decât Java + Selenium, ceea ce te diferențiază. Mulți angajatori enterprise migrează spre Playwright — cunoașterea ambelor te face candidatul ideal.

---

## 💡 Sfaturi practice

### Când să alegi Java + Playwright față de alte variante

| Alege Java + Playwright dacă... | Alege altceva dacă... |
|--------------------------------|----------------------|
| Echipa lucrează deja în Java | Ești la zero și vrei cel mai simplu start (→ Python) |
| Vrei Playwright modern dar rămâi în JVM | Vrei ecosistemul TS/JS complet (→ TypeScript) |
| Compania migrează de la Selenium la Playwright | Ai deja un framework Selenium Java funcțional (→ păstrează-l) |

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile
- [Playwright Discord](https://discord.com/invite/playwright-807756831384403968) — comunitatea oficială
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate de testeri

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | Java | 21 LTS |
| IDE | IntelliJ IDEA Community | latest |
| Build tool | Maven | 3.9+ |
| UI + API Automation | Playwright for Java | 1.52+ |
| Test framework | JUnit 5 | 5.11+ |
| API Testing (alternativ) | REST Assured | 5.x |
| Reporting | Allure | 2.x |
| CI/CD | GitHub Actions | — |
| Containers | Docker (Playwright Java image) | latest |
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
| **Framework** | Playwright (modern) |
| **Față de Java + Selenium** | Auto-wait, trace viewer, codegen, assertions native — fără configurare extra |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [AI pentru Automation Engineers](./cale-invatare-ai-in-testare-automatizare.md) |
