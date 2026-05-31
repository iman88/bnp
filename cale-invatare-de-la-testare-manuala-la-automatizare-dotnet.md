# 🔷 De la Testare Manuală la Automatizare — .NET + Playwright

> C# · Playwright UI + API Testing · De la zero absolut · ~5–7 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de programare C#](#-faza-1--fundamente-de-programare-c-57-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Playwright UI Automation](#-faza-3--playwright-ui-automation-56-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing-34-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de programare C# (5–7 săptămâni)

> C# e un limbaj puternic, tipat static, cu o sintaxă mai verbosă decât Python sau TypeScript — dar extrem de răspândit în enterprise și în ecosistemul Microsoft. Merită investiția.

| Resursă | Durată | Link |
|---------|--------|------|
| C# Fundamentals — Microsoft Learn | ~40h | [→ Deschide](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/) |
| C# Tutorial — W3Schools | referință | [→ Deschide](https://www.w3schools.com/cs/) |
| C# for Beginners — freeCodeCamp (YouTube) | ~4h | [→ Deschide](https://www.youtube.com/watch?v=GhQdlIFylQ8) |
| .NET Developer Track — Hyperskill | ~50h | [→ Deschide](https://hyperskill.org/tracks/37) |

**Ce vei învăța:**
- Sintaxă de bază: variabile, tipuri de date (`int`, `string`, `bool`, `decimal`)
- Structuri de control: `if/else`, bucle `for`/`foreach`/`while`
- Metode și funcții, parametri `out` și `ref`
- OOP: clase, obiecte, moștenire, interfețe, `abstract`
- Colecții: `List<T>`, `Dictionary<K,V>`, `IEnumerable<T>`
- Gestionarea erorilor: `try/catch/finally`
- `async`/`await` — esențial, Playwright .NET e async by design
- LINQ — interogări pe colecții, util pentru validarea datelor de test
- `record` și `nullable` types — moderne, apar frecvent în cod nou

**Specificul C# față de alte limbaje:**
```csharp
// Tipare strictă — compilatorul prinde erorile înainte să rulezi
string email = "test@example.com";
int age = 25;
// age = email;  // eroare la compilare, nu la runtime

// async/await — Playwright e async, înțelegi de ce e important
public async Task<string> GetPageTitle(Page page) {
    await page.GotoAsync("https://example.com");
    return await page.TitleAsync();
}

// LINQ — util pentru validarea listelor de date de test
var activeUsers = users.Where(u => u.Status == "active")
                       .OrderBy(u => u.Email)
                       .Select(u => u.Email)
                       .ToList();
```

**Resursa cheie:** Microsoft Learn e creat de Microsoft pentru .NET — documentația e completă, gratuită și actualizată permanent. E standardul de referință pentru ecosistemul .NET.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Ecosistemul .NET e dominat de Visual Studio și Visual Studio Code — ambele excelente, cu suport nativ pentru Playwright.

| Resursă | Durată | Link |
|---------|--------|------|
| .NET Getting Started — Microsoft Learn | ~3h | [→ Deschide](https://dotnet.microsoft.com/en-us/learn/dotnet/hello-world-tutorial/intro) |
| NUnit Quick Start — NUnit Docs | ~2h | [→ Deschide](https://docs.nunit.org/articles/nunit/getting-started/installation.html) |
| Git Handbook — GitHub Guides | ~1h | [→ Deschide](https://guides.github.com/introduction/git-handbook/) |
| Visual Studio for Beginners — Microsoft Learn | ~2h | [→ Deschide](https://learn.microsoft.com/en-us/visualstudio/get-started/visual-studio-ide) |

| Unealtă | Scop | Link |
|---------|------|------|
| .NET SDK 8 LTS | Runtime și compilator C# | [→ Descarcă](https://dotnet.microsoft.com/download) |
| Visual Studio 2022 Community | IDE complet, gratuit | [→ Descarcă](https://visualstudio.microsoft.com/vs/community/) |
| VS Code + extensia C# | IDE mai ușor, bun pentru proiecte mici | [→ Descarcă](https://code.visualstudio.com/) |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |

**Crearea primului proiect de test:**
```bash
# Creare proiect NUnit cu Playwright
dotnet new nunit -n MyPlaywrightTests
cd MyPlaywrightTests

# Adăugare pachet Playwright
dotnet add package Microsoft.Playwright.NUnit

# Build și instalare browsere
dotnet build
pwsh bin/Debug/net8.0/playwright.ps1 install
```

**Structura unui proiect .NET + Playwright:**
```
MyPlaywrightTests/
├── Pages/
│   ├── BasePage.cs
│   └── LoginPage.cs
├── Tests/
│   ├── UI/
│   │   └── LoginTests.cs
│   └── API/
│       └── UsersApiTests.cs
├── Helpers/
│   └── TestDataHelper.cs
├── playwright.config.json
└── MyPlaywrightTests.csproj
```

**`csproj` — dependențe de start:**
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <IsPackable>false</IsPackable>
    <IsTestProject>true</IsTestProject>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Microsoft.Playwright.NUnit" Version="1.44.0" />
    <PackageReference Include="NUnit" Version="4.1.0" />
    <PackageReference Include="NUnit3TestAdapter" Version="4.5.0" />
  </ItemGroup>
</Project>
```

---

## 🟡 Faza 3 — Playwright UI Automation (5–6 săptămâni)

> Playwright .NET e varianta oficială Microsoft pentru C# — API identic cu TypeScript, aceeași calitate, aceeași comunitate.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright for .NET — Docs oficiale | referință | [→ Deschide](https://playwright.dev/dotnet/docs/intro) |
| Playwright .NET — GitHub Examples | referință | [→ Deschide](https://github.com/microsoft/playwright-dotnet) |
| NUnit Documentation | referință | [→ Deschide](https://docs.nunit.org/) |

**Ce vei învăța:**

**Configurare globală cu `playwright.config.json`:**
```json
{
  "timeout": 30000,
  "use": {
    "baseURL": "https://example.com",
    "screenshot": "only-on-failure",
    "video": "retain-on-failure",
    "trace": "on-first-retry"
  }
}
```

**Clasa de bază pentru toate testele:**
```csharp
using Microsoft.Playwright.NUnit;

[Parallelizable(ParallelScope.Self)]
[TestFixture]
public class BaseTest : PageTest
{
    // PageTest oferă automat: Page, Browser, BrowserContext, Playwright
    // Nu trebuie să le inițializezi manual

    public override BrowserNewContextOptions ContextOptions()
    {
        return new BrowserNewContextOptions
        {
            ViewportSize = new ViewportSize { Width = 1920, Height = 1080 },
            Locale = "ro-RO",
            TimezoneId = "Europe/Bucharest",
        };
    }
}
```

**Locatori moderni — prioritate în această ordine:**
```csharp
// Semantic — de preferat întotdeauna
Page.GetByRole(AriaRole.Button, new() { Name = "Login" })
Page.GetByLabel("Email")
Page.GetByPlaceholder("Introdu emailul")
Page.GetByText("Bun venit")
Page.GetByTestId("submit-btn")   // data-testid atribut

// CSS/XPath ca fallback
Page.Locator(".btn-primary")
Page.Locator("//button[@type='submit']")
```

**Page Object Model cu C#:**
```csharp
public class LoginPage
{
    private readonly IPage _page;
    private readonly ILocator _emailInput;
    private readonly ILocator _passwordInput;
    private readonly ILocator _loginButton;
    private readonly ILocator _errorMessage;

    public LoginPage(IPage page)
    {
        _page = page;
        _emailInput = page.GetByLabel("Email");
        _passwordInput = page.GetByLabel("Parolă");
        _loginButton = page.GetByRole(AriaRole.Button, new() { Name = "Autentificare" });
        _errorMessage = page.GetByRole(AriaRole.Alert);
    }

    public async Task GotoAsync() =>
        await _page.GotoAsync("/login");

    public async Task LoginAsync(string email, string password)
    {
        await _emailInput.FillAsync(email);
        await _passwordInput.FillAsync(password);
        await _loginButton.ClickAsync();
    }

    public async Task<string> GetErrorMessageAsync() =>
        await _errorMessage.TextContentAsync() ?? string.Empty;
}

// Test care folosește POM
[TestFixture]
public class LoginTests : BaseTest
{
    private LoginPage _loginPage = null!;

    [SetUp]
    public void SetUp() => _loginPage = new LoginPage(Page);

    [Test]
    public async Task LoginWithValidCredentials_RedirectsToDashboard()
    {
        await _loginPage.GotoAsync();
        await _loginPage.LoginAsync("user@test.com", "secret123");
        await Expect(Page).ToHaveURLAsync(new Regex(".*/dashboard"));
    }

    [Test]
    public async Task LoginWithInvalidPassword_ShowsErrorMessage()
    {
        await _loginPage.GotoAsync();
        await _loginPage.LoginAsync("user@test.com", "gresit");
        await Expect(Page.GetByRole(AriaRole.Alert))
            .ToContainTextAsync("Credențiale invalide");
    }
}
```

**Parametrizare teste cu NUnit:**
```csharp
[TestCase("", "secret123", "Emailul este obligatoriu")]
[TestCase("invalid-email", "secret123", "Email invalid")]
[TestCase("user@test.com", "", "Parola este obligatorie")]
public async Task LoginValidation_ShowsCorrectError(
    string email, string password, string expectedError)
{
    await _loginPage.GotoAsync();
    await _loginPage.LoginAsync(email, password);
    await Expect(Page.GetByRole(AriaRole.Alert)).ToContainTextAsync(expectedError);
}
```

**Funcții avansate:**
- **Codegen**: `pwsh bin/Debug/net8.0/playwright.ps1 codegen https://site.com`
- **Trace Viewer**: `pwsh bin/Debug/net8.0/playwright.ps1 show-trace trace.zip`
- **UI Mode**: `dotnet test -- NUnit.NumberOfTestWorkers=1` + `PWDEBUG=1`
- Network mocking: `await Page.RouteAsync("**/api/users", route => route.FulfillAsync(...))`

**Proiect practic:** Automatizează un flux complet pe [demoqa.com](https://demoqa.com) — formular, tabele, alerts, navigare. Minim 15 teste cu POM complet.

---

## 🟣 Faza 4 — API Testing (3–4 săptămâni)

> Playwright .NET are API testing built-in — același framework pentru UI și API, fără dependențe externe.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright API Testing (.NET) — Docs | referință | [→ Deschide](https://playwright.dev/dotnet/docs/api-testing) |
| RestSharp — alternativă populară | referință | [→ Deschide](https://restsharp.dev/) |
| Postman — testare manuală API | referință | [→ Cale Postman](./cale-invatare-postman.md) |

**API Testing cu Playwright `APIRequestContext`:**
```csharp
[TestFixture]
public class UsersApiTests : PlaywrightTest
{
    private IAPIRequestContext _request = null!;

    [SetUp]
    public async Task SetUpApiContext()
    {
        _request = await Playwright.APIRequest.NewContextAsync(new()
        {
            BaseURL = "https://reqres.in",
            ExtraHTTPHeaders = new Dictionary<string, string>
            {
                ["Content-Type"] = "application/json",
            }
        });
    }

    [Test]
    public async Task GetUsers_Returns200WithData()
    {
        var response = await _request.GetAsync("/api/users?page=1");

        Assert.That(response.Status, Is.EqualTo(200));
        Assert.That(response.Ok, Is.True);

        var body = await response.JsonAsync();
        Assert.That(body?.GetProperty("data").GetArrayLength(), Is.GreaterThan(0));
    }

    [Test]
    public async Task CreateUser_Returns201WithId()
    {
        var response = await _request.PostAsync("/api/users", new APIRequestContextOptions
        {
            DataObject = new { name = "Ion Pop", job = "QA Engineer" }
        });

        Assert.That(response.Status, Is.EqualTo(201));

        var body = await response.JsonAsync();
        Assert.That(body?.GetProperty("id").GetString(), Is.Not.Null.And.Not.Empty);
    }

    [TearDown]
    public async Task TearDownApiContext() => await _request.DisposeAsync();
}
```

**Pattern hibrid — setup stare prin API, verificare prin UI:**
```csharp
[Test]
public async Task OrderAppearsInDashboard_AfterApiCreation()
{
    // Setup rapid prin API
    var orderResponse = await _request.PostAsync("/api/orders", new APIRequestContextOptions
    {
        DataObject = new { userId = 1, productId = 42, quantity = 2 }
    });
    var orderId = (await orderResponse.JsonAsync())?.GetProperty("id").GetInt32();

    // Verificare în UI
    await Page.GotoAsync($"/dashboard/orders/{orderId}");
    await Expect(Page.GetByText("Comandă confirmată")).ToBeVisibleAsync();
}
```

**Proiect practic:** Suită completă de teste API pentru [reqres.in](https://reqres.in) — CRUD, autentificare, validare răspunsuri, teste negative, parametrizare cu `[TestCase]`.

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (3–4 săptămâni)

> Framework-ul tău rulează automat la fiecare modificare de cod, rapoartele sunt clare pentru toată echipa.

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions + .NET | ~3h | [→ Deschide](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-net) |
| Playwright .NET Docker | ~2h | [→ Deschide](https://playwright.dev/dotnet/docs/docker) |
| Allure cu NUnit | ~2h | [→ Deschide](https://allurereport.org/docs/nunit/) |

**GitHub Actions CI:**
```yaml
name: Playwright .NET Tests
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: mcr.microsoft.com/playwright/dotnet:v1.44.0-jammy
    steps:
      - uses: actions/checkout@v4

      - name: Build
        run: dotnet build

      - name: Run Playwright tests
        run: dotnet test --logger "trx;LogFileName=results.trx"
        env:
          BASE_URL: ${{ vars.STAGING_URL }}

      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: test-results
          path: "**/*.trx"
```

**Allure Reports cu NUnit:**
```bash
dotnet add package Allure.NUnit
dotnet test --logger "allure;LogFilePath=allure-results"
allure serve allure-results
```

**Rulare paralelă cu NUnit:**
```csharp
// La nivel de assembly — toate fixture-urile rulează în paralel
[assembly: Parallelizable(ParallelScope.Fixtures)]

// La nivel de fixture — toate testele din fixture rulează în paralel
[Parallelizable(ParallelScope.All)]
[TestFixture]
public class LoginTests : BaseTest { ... }
```

**Proiect final — Framework complet:**
```
MyPlaywrightTests/
├── Pages/
│   ├── BasePage.cs
│   ├── LoginPage.cs
│   └── DashboardPage.cs
├── Tests/
│   ├── UI/
│   │   ├── LoginTests.cs
│   │   └── CheckoutTests.cs
│   └── API/
│       └── UsersApiTests.cs
├── Helpers/
│   ├── TestDataHelper.cs
│   └── ApiClientHelper.cs
├── .github/
│   └── workflows/
│       └── playwright.yml
├── playwright.config.json
└── MyPlaywrightTests.csproj
```

> 💼 **Primul job:** .NET + Playwright e combinația dominantă în companiile enterprise cu ecosistem Microsoft — bănci, asigurări, retail mare. Dacă vrei să lucrezi în enterprise și organizații cu stack Microsoft, aceasta e alegerea strategică.

---

## 💡 Sfaturi practice

### Când să alegi .NET față de alte variante

| Alege .NET + Playwright dacă... | Alege altceva dacă... |
|--------------------------------|----------------------|
| Echipa de dev lucrează în C# | Preferi sintaxă mai simplă pentru start (→ Python) |
| Compania are ecosistem Microsoft | Vrei cel mai mare ecosistem de resurse (→ TypeScript) |
| Lucrezi în enterprise, bănci, asigurări | Echipa folosește alt limbaj |

### Visual Studio vs VS Code pentru .NET

| Visual Studio 2022 Community | VS Code + extensia C# |
|-----------------------------|----------------------|
| IDE complet, debugger puternic | Mai ușor, pornire rapidă |
| Refactorizare avansată built-in | Necesită extensii suplimentare |
| Bun pentru proiecte mari | Bun pentru proiecte mici și medii |
| Disponibil doar pe Windows/Mac | Cross-platform |

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA (.NET/Playwright) |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile

- [Playwright Discord](https://discord.com/invite/playwright-807756831384403968) — comunitatea oficială
- [.NET Foundation Community](https://dotnetfoundation.org/) — ecosistemul .NET
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | C# | 12 (.NET 8 LTS) |
| Runtime | .NET | 8 LTS |
| IDE | Visual Studio 2022 Community | latest |
| UI + API Automation | Playwright for .NET | 1.44+ |
| Test framework | NUnit | 4.x |
| Reporting | Allure + TRX | latest |
| CI/CD | GitHub Actions | — |
| Containers | Docker (Playwright .NET image) | latest |
| Version control | Git + GitHub | — |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 5–7 luni (part-time) |
| **Nivel de start** | Zero experiență de programare |
| **Nivel de final** | Junior–Mid Automation QA Engineer |
| **Cost** | 100% gratuit |
| **Limbaj** | C# (.NET 8) |
| **Framework** | Playwright |
| **Avantaj principal** | Ecosistem Microsoft, ideal pentru enterprise și organizații cu stack .NET |
