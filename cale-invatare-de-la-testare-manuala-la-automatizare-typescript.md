# 🟦 De la Testare Manuală la Automatizare — TypeScript

> TypeScript · Playwright UI + API Testing · De la zero absolut · ~4–6 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente JavaScript & TypeScript](#-faza-1--fundamente-javascript--typescript-46-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Playwright UI Automation](#-faza-3--playwright-ui-automation-56-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing-34-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente JavaScript & TypeScript (4–6 săptămâni)

> JavaScript e limbajul web-ului. TypeScript îl face scalabil și sigur. Playwright e scris în TypeScript — e combinația naturală.

| Resursă | Durată | Link |
|---------|--------|------|
| JavaScript — The Complete Guide — freeCodeCamp | ~30h | [→ Deschide](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/) |
| JavaScript.info — The Modern JavaScript Tutorial | referință | [→ Deschide](https://javascript.info/) |
| TypeScript Handbook — Docs oficiale | ~6h | [→ Deschide](https://www.typescriptlang.org/docs/handbook/intro.html) |
| TypeScript Full Course — freeCodeCamp (YouTube) | ~3h | [→ Deschide](https://www.youtube.com/watch?v=30LWjhZzg50) |

**Ce vei învăța:**

**JavaScript esențial:**
- `let`, `const`, tipuri primitive: `string`, `number`, `boolean`, `null`, `undefined`
- Funcții: declaration, arrow functions `=>`, callback-uri
- Obiecte și array-uri: destructuring, spread `...`, `map()`, `filter()`, `find()`
- `Promise`, `async/await` — esențial pentru Playwright care e async by design
- Module ES: `import`/`export`
- Error handling: `try/catch`

**TypeScript peste JavaScript:**
```typescript
// Tipare explicite — TypeScript te avertizează înainte să rulezi
type User = {
  id: number;
  email: string;
  role: "admin" | "user" | "viewer";
};

async function getUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  return response.json() as User;
}
```

- Tipuri de bază: `string`, `number`, `boolean`, `any`, `unknown`, `void`
- Interfețe și `type` aliases — cum structurezi datele de test
- Generics: `Array<T>`, `Promise<T>` — înțelegi ce scrie Playwright în docs
- Enum-uri pentru date de test constante
- `tsconfig.json` — configurare compiler TypeScript

**Resursa cheie:** `javascript.info` e cel mai complet tutorial gratuit de JS — organizat logic, cu exerciții interactive la fiecare capitol.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Mediul modern pentru TypeScript e simplu de configurat, dar trebuie înțeles de la început.

| Unealtă | Scop | Link |
|---------|------|------|
| Node.js LTS | Runtime JavaScript | [→ Descarcă](https://nodejs.org/) |
| VS Code + extensii | IDE principal | [→ Descarcă](https://code.visualstudio.com/) |
| npm / pnpm | Gestionare pachete | [→ npm Docs](https://docs.npmjs.com/) |
| TypeScript | Compilator TS | `npm install -D typescript` |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |

**Ce vei învăța:**
- Node.js și npm: `package.json`, `node_modules`, `npm install`, `npm run`
- VS Code esențial: extensia Playwright Test for VS Code (runner + debugger integrat)
- `tsconfig.json` — `strict: true`, `target`, `module`, `paths`
- `.env` și `dotenv` — gestionare variabile de configurare (URL, credențiale de test)
- Structura unui proiect Playwright TypeScript:

```
my-playwright-ts/
├── tests/
│   ├── ui/
│   │   └── login.spec.ts
│   └── api/
│       └── users.spec.ts
├── pages/
│   ├── BasePage.ts
│   └── LoginPage.ts
├── utils/
│   └── testData.ts
├── playwright.config.ts
├── tsconfig.json
└── package.json
```

---

## 🟡 Faza 3 — Playwright UI Automation (5–6 săptămâni)

> Playwright cu TypeScript e combinația oficialmente recomandată — documentația, exemplele și comunitatea sunt toate orientate pe TS.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright Docs — Getting Started (TypeScript) | referință | [→ Deschide](https://playwright.dev/docs/intro) |
| Playwright Tutorial — TAU | ~5h | [→ Deschide](https://testautomationu.applitools.com/playwright-intro/) |
| Playwright Tips — Martijena Nikolić (YouTube) | ~4h | [→ Deschide](https://www.youtube.com/@playwrightsolutions) |
| Playwright Best Practices | referință | [→ Deschide](https://playwright.dev/docs/best-practices) |

**Ce vei învăța:**

**Instalare și primul test:**
```bash
npm init playwright@latest
# alegi TypeScript, creează exemple, instalează browsere
```

**`playwright.config.ts` — configurare globală:**
```typescript
import { defineConfig, devices } from "@playwright/test";

export default defineConfig({
  testDir: "./tests",
  fullyParallel: true,
  retries: process.env.CI ? 2 : 0,
  reporter: [["html"], ["allure-playwright"]],
  use: {
    baseURL: "https://example.com",
    screenshot: "only-on-failure",
    video: "retain-on-failure",
    trace: "on-first-retry",
  },
  projects: [
    { name: "chromium", use: { ...devices["Desktop Chrome"] } },
    { name: "firefox", use: { ...devices["Desktop Firefox"] } },
    { name: "Mobile Chrome", use: { ...devices["Pixel 5"] } },
  ],
});
```

**Locatori moderni (prioritate în această ordine):**
```typescript
page.getByRole("button", { name: "Login" })   // semantic, de preferat
page.getByLabel("Email")                        // din label asociat
page.getByPlaceholder("Enter your email")       // din placeholder
page.getByText("Welcome back")                  // din conținut text
page.getByTestId("submit-btn")                  // data-testid atribut
page.locator(".css-class")                      // CSS ca fallback
```

**Page Object Model cu TypeScript:**
```typescript
import { Page, Locator, expect } from "@playwright/test";

export class LoginPage {
  private readonly emailInput: Locator;
  private readonly passwordInput: Locator;
  private readonly loginButton: Locator;

  constructor(private page: Page) {
    this.emailInput = page.getByLabel("Email");
    this.passwordInput = page.getByLabel("Password");
    this.loginButton = page.getByRole("button", { name: "Login" });
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.loginButton.click();
  }

  async expectLoginError(message: string) {
    await expect(this.page.getByRole("alert")).toContainText(message);
  }
}
```

**Fixtures și `test.extend()`:**
```typescript
// fixtures.ts — extinde test-ul de bază cu obiecte reutilizabile
import { test as base } from "@playwright/test";
import { LoginPage } from "./pages/LoginPage";

type Fixtures = { loginPage: LoginPage };

export const test = base.extend<Fixtures>({
  loginPage: async ({ page }, use) => {
    await use(new LoginPage(page));
  },
});
```

**Funcții avansate:**
- **Codegen**: `npx playwright codegen https://site.com`
- **Trace Viewer**: `npx playwright show-trace trace.zip`
- **UI Mode**: `npx playwright test --ui` — runner vizual cu time-travel debugging
- Network interception: `page.route()` — mockezi API-uri direct din test
- `expect.soft()` — continuă testul chiar dacă un assertion pică

**Proiect practic:** Automatizează un flux complet pe [playwright.dev](https://playwright.dev) sau [demoqa.com](https://demoqa.com) — minim 15 teste, POM structurat, rulare pe 2+ browsere.

> ⭐ **UI Mode** e funcționalitatea de top: rulezi testele vizual, vezi fiecare pas, dai time-travel înapoi să înțelegi exact ce s-a întâmplat la eșec.

---

## 🟣 Faza 4 — API Testing (3–4 săptămâni)

> Playwright are API testing built-in — nu ai nevoie de librărie separată. Un singur tool pentru UI și API.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright API Testing — Docs | referință | [→ Deschide](https://playwright.dev/docs/api-testing) |
| API Testing with Playwright — tutorial | ~3h | [→ Deschide](https://www.youtube.com/watch?v=mH7e1KKF9vc) |
| Postman — Testare manuală API | referință | [→ Cale Postman](./cale-invatare-postman.md) |

**Ce vei învăța:**

**API Testing cu Playwright `request` fixture:**
```typescript
import { test, expect } from "@playwright/test";

test.describe("Users API", () => {
  test("GET /users returns list", async ({ request }) => {
    const response = await request.get("/api/users");
    expect(response.status()).toBe(200);
    const body = await response.json();
    expect(body.data).toHaveLength(6);
  });

  test("POST /users creates user", async ({ request }) => {
    const response = await request.post("/api/users", {
      data: { name: "Ion Pop", job: "QA Engineer" },
    });
    expect(response.status()).toBe(201);
    const body = await response.json();
    expect(body.name).toBe("Ion Pop");
    expect(body.id).toBeTruthy();
  });
});
```

**Ce vei acoperi:**
- `request.get()`, `.post()`, `.put()`, `.patch()`, `.delete()` cu headers și body
- Autentificare: Bearer Token în headers, API Key, Basic Auth
- `APIRequestContext` — sesiune reutilizabilă cu `baseURL` și headers globale
- Validare schema cu `zod` sau `ajv` — tipare la runtime pentru răspunsuri API
- **Combinare UI + API** — setup stare via API, verificare UI, teardown via API (testele sunt mai rapide)

```typescript
// Pattern hybrid: creezi resursa via API, verifici UI-ul
test("order appears in dashboard after API creation", async ({ page, request }) => {
  // Setup rapid via API
  const order = await request.post("/api/orders", { data: orderPayload });
  const { id } = await order.json();

  // Verificare în UI
  await page.goto(`/dashboard/orders/${id}`);
  await expect(page.getByText("Order confirmed")).toBeVisible();
});
```

**Proiect practic:** Suită completă de teste API + UI pentru un flux E2E (ex: creare cont via API → login în UI → verificare dashboard → ștergere via API cleanup).

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (3–4 săptămâni)

> Framework-ul tău rulează în cloud, rapoartele sunt vizibile pentru toată echipa, testele flaky sunt detectate automat.

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions + Playwright | ~3h | [→ Deschide](https://playwright.dev/docs/ci-intro) |
| Allure with Playwright — Docs | ~2h | [→ Deschide](https://allurereport.org/docs/playwright/) |
| Playwright Sharding — paralelism CI | ~1h | [→ Deschide](https://playwright.dev/docs/test-sharding) |
| Playwright Docker | ~2h | [→ Deschide](https://playwright.dev/docs/docker) |

**Ce vei învăța:**

**GitHub Actions CI:**
```yaml
# .github/workflows/playwright.yml
name: Playwright Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: mcr.microsoft.com/playwright:v1.52.0-jammy
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - run: npm ci
      - run: npx playwright test
        env:
          BASE_URL: ${{ vars.BASE_URL }}
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: playwright-report
          path: playwright-report/
```

**Sharding — rulezi testele în paralel pe mai mulți runneri CI:**
```yaml
strategy:
  matrix:
    shardIndex: [1, 2, 3, 4]
    shardTotal: [4]
steps:
  - run: npx playwright test --shard=${{ matrix.shardIndex }}/${{ matrix.shardTotal }}
```

**Allure Reports:**
```bash
npm install -D allure-playwright allure-commandline
# în playwright.config.ts: reporter: [["allure-playwright"]]
npx allure serve allure-results
```

**Proiect final — Framework complet:**
```
my-playwright-ts-framework/
├── pages/
│   ├── BasePage.ts
│   ├── LoginPage.ts
│   └── DashboardPage.ts
├── tests/
│   ├── ui/
│   │   ├── login.spec.ts
│   │   └── checkout.spec.ts
│   └── api/
│       └── users.spec.ts
├── utils/
│   ├── testData.ts
│   └── apiHelpers.ts
├── fixtures/
│   └── customFixtures.ts
├── playwright.config.ts
├── tsconfig.json
├── package.json
└── .github/
    └── workflows/
        └── playwright.yml
```

> 💼 **Primul job:** TypeScript + Playwright e combinația cea mai cerută în anunțurile de QA Automation din 2026–2027. Cu Fazele 1–3 și un portofoliu de pe GitHub, poți aplica la Junior Automation QA. Mulți angajatori preferă Playwright față de Selenium pentru proiectele noi.

---

## 💡 Sfaturi practice

### Cum să înveți eficient
- **30–45 minute zilnic** — constanța bate intensitatea pentru memorare pe termen lung
- Pornește `npx playwright test --ui` și experimentează înainte de a citi docs — interfața e intuitivă
- Folosește `codegen` pentru a învăța cum Playwright gândește locatorii: `npx playwright codegen`
- Activează `strict: true` în `tsconfig.json` de la început — TypeScript te va învăța să scrii cod corect

### Avantajele TypeScript față de JavaScript pur

| JavaScript | TypeScript |
|-----------|-----------|
| Erori descoperite la runtime | Erori descoperite la compilare |
| Fără autocompletare precisă | Autocompletare completă în VS Code |
| Refactorizare riscantă | Refactorizare sigură (IDE știe toate utilizările) |
| Documentație implicită | Tipurile sunt documentație |

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA (Playwright/TS) |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile
- [Playwright Discord](https://discord.com/invite/playwright-807756831384403968) — comunitatea oficială, răspunsuri rapide
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate globală de testeri
- [TypeScript Community Discord](https://discord.com/invite/typescript) — pentru întrebări TS specifice

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | TypeScript | 5.x |
| Runtime | Node.js | 22 LTS |
| IDE | VS Code + Playwright extension | latest |
| Build tool | npm / pnpm | latest |
| UI + API Automation | Playwright | 1.52+ |
| Test framework | Playwright Test (built-in) | — |
| Reporting | Allure + Playwright HTML | latest |
| CI/CD | GitHub Actions | — |
| Containers | Docker (Playwright image oficial) | latest |
| Version control | Git + GitHub | — |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 4–6 luni (part-time) |
| **Nivel de start** | Zero experiență de programare |
| **Nivel de final** | Junior–Mid Automation QA Engineer |
| **Cost** | 100% gratuit |
| **Limbaj** | TypeScript |
| **Focus** | Playwright UI + API Testing (all-in-one) |
| **Avantaj față de Java** | Sintaxă modernă, UI Mode, test runner built-in, ecosistem web nativ |
| **Avantaj față de Python** | Tipare strictă, autocompletare superioară, sharding nativ în Playwright |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [AI pentru Automation Engineers](./cale-invatare-ai-in-testare-automatizare.md) |
