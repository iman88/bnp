# 🐍 De la Testare Manuală la Automatizare — Python

> Python · Playwright UI + API Testing · De la zero absolut · ~4–6 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de programare Python](#-faza-1--fundamente-de-programare-python-46-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Playwright UI Automation](#-faza-3--playwright-ui-automation-56-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing-34-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de programare Python (4–6 săptămâni)

> Python e cel mai ușor limbaj de start pentru QA — sintaxă clară, biblioteci bogate, comunitate uriașă. Nu sări peste fundamente.

| Resursă | Durată | Link |
|---------|--------|------|
| Python for Everybody — Dr. Chuck (Coursera) | ~30h | [→ Deschide](https://www.coursera.org/specializations/python) |
| Python Tutorial — W3Schools | referință | [→ Deschide](https://www.w3schools.com/python/) |
| Automate the Boring Stuff with Python — Al Sweigart | ~20h | [→ Deschide](https://automatetheboringstuff.com/) |
| Python Track — Hyperskill (JetBrains) | ~40h | [→ Deschide](https://hyperskill.org/tracks/2) |

**Ce vei învăța:**
- Sintaxă de bază: variabile, tipuri de date (`int`, `str`, `list`, `dict`, `bool`)
- Structuri de control: `if/elif/else`, bucle `for`/`while`
- Funcții, argumente, valori de return
- OOP: clase, obiecte, moștenire, `__init__`
- List comprehensions, `lambda`, decoratori (nivel de bază)
- Lucrul cu fișiere: citire/scriere JSON, CSV, TXT
- Gestionarea erorilor: `try/except/finally`
- Module esențiale: `os`, `json`, `re`, `datetime`

**Resursa cheie:** „Automate the Boring Stuff" e scrisă special pentru non-programatori și conține exerciții practice imediat aplicabile — ideal pentru QA.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Configurează mediul o singură dată, corect, și economisești ore de debugging mai târziu.

| Unealtă | Scop | Link |
|---------|------|------|
| Python 3.13+ | Runtime Python | [→ Descarcă](https://www.python.org/downloads/) |
| VS Code + extensia Python | IDE principal | [→ Descarcă](https://code.visualstudio.com/) |
| pip + venv | Gestionare pachete și medii virtuale | [→ Ghid](https://docs.python.org/3/library/venv.html) |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |
| pytest | Framework de testare | [→ Docs](https://docs.pytest.org/en/stable/) |

**Ce vei învăța:**
- `venv` — de ce izolezi dependențele per proiect și cum creezi/activezi un virtual environment
- `pip install`, `requirements.txt`, `pyproject.toml`
- VS Code: Python interpreter, debugger, pytest runner integrat
- Git esențial: `clone`, `commit`, `push`, `pull`, `branch`
- Structura unui proiect de testare Python:

```
my-test-project/
├── tests/
│   ├── ui/
│   └── api/
├── pages/              # Page Object classes
├── conftest.py         # fixture-uri pytest globale
├── pytest.ini          # configurare pytest
└── requirements.txt
```

---

## 🟡 Faza 3 — Playwright UI Automation (5–6 săptămâni)

> Playwright e alegerea modernă pentru UI automation — mai rapid decât Selenium, auto-wait built-in, trace viewer inclus.

| Resursă | Durată | Link |
|---------|--------|------|
| Playwright for Python — Docs oficiale | referință | [→ Deschide](https://playwright.dev/python/docs/intro) |
| Getting Started with Playwright — TAU | ~4h | [→ Deschide](https://testautomationu.applitools.com/playwright-intro/) |
| pytest-playwright — Plugin oficial | referință | [→ Deschide](https://playwright.dev/python/docs/test-runners) |
| Playwright YouTube Channel | ~5h | [→ Deschide](https://www.youtube.com/@Playwrightdev) |

**Ce vei învăța:**

**Instalare și configurare:**
```bash
pip install playwright pytest-playwright
playwright install  # descarcă Chromium, Firefox, WebKit
```

**Concepte fundamentale:**
- `Page`, `Browser`, `BrowserContext` — arhitectura Playwright
- Locatori moderni: `page.get_by_role()`, `get_by_text()`, `get_by_label()`, `get_by_placeholder()`
- XPath și CSS ca fallback: `page.locator("css=.btn-primary")`
- **Auto-waiting** — Playwright așteaptă automat ca elementul să fie acționabil (nu mai scrii `sleep()`)
- Acțiuni: `click()`, `fill()`, `select_option()`, `check()`, `hover()`, `drag_to()`
- Assertions moderne: `expect(page).to_have_url()`, `expect(locator).to_be_visible()`

**pytest-playwright:**
```python
# conftest.py — fixture-uri globale
import pytest
from playwright.sync_api import Page

@pytest.fixture(scope="session")
def browser_context_args(browser_context_args):
    return {**browser_context_args, "viewport": {"width": 1920, "height": 1080}}

# test_login.py
def test_login_valid(page: Page):
    page.goto("https://example.com/login")
    page.get_by_label("Email").fill("user@test.com")
    page.get_by_label("Password").fill("secret123")
    page.get_by_role("button", name="Login").click()
    expect(page).to_have_url("https://example.com/dashboard")
```

**Page Object Model cu Python:**
```python
class LoginPage:
    def __init__(self, page: Page):
        self.page = page
        self.email_input = page.get_by_label("Email")
        self.password_input = page.get_by_label("Password")
        self.login_button = page.get_by_role("button", name="Login")

    def login(self, email: str, password: str):
        self.email_input.fill(email)
        self.password_input.fill(password)
        self.login_button.click()
```

**Funcții avansate:**
- **Trace Viewer** — `playwright show-trace trace.zip` — debugging vizual complet
- **Screenshot și video** la eșec: configurat din `pytest.ini`
- `codegen` — înregistrezi acțiuni în browser, Playwright generează codul
- Multiple browsere: `pytest --browser firefox --browser webkit`
- **API requests din Playwright**: `page.request.get()` / `.post()`

**Proiect practic:** Automatizează un flux complet pe [playwright.dev/python](https://playwright.dev/python) sau [demoqa.com](https://demoqa.com) — login, navigare, formular, validare rezultat. Folosește POM și cel puțin 10 teste.

> ⭐ **Avantaj față de Selenium:** Playwright are built-in `codegen`, trace viewer, auto-wait și suport nativ pentru shadow DOM și iframes — fără configurare suplimentară.

---

## 🟣 Faza 4 — API Testing (3–4 săptămâni)

> Python + `requests` e cea mai populară combinație pentru testarea API-urilor. Simplă, puternică, omniprezentă.

| Resursă | Durată | Link |
|---------|--------|------|
| requests Library — Docs oficiale | referință | [→ Deschide](https://requests.readthedocs.io/en/latest/) |
| API Testing with Python — RealPython | ~3h | [→ Deschide](https://realpython.com/api-integration-in-python/) |
| pytest + requests — Tutorial practic | ~2h | [→ Deschide](https://testdriven.io/blog/pytest-for-beginners/) |
| Postman — Testare manuală API | referință | [→ Cale Postman](./cale-invatare-postman.md) |

**Ce vei învăța:**

```python
import requests
import pytest

BASE_URL = "https://reqres.in/api"

class TestUsers:
    def test_get_users_returns_200(self):
        response = requests.get(f"{BASE_URL}/users", params={"page": 1})
        assert response.status_code == 200
        assert response.json()["data"] is not None

    def test_create_user(self):
        payload = {"name": "Ion Pop", "job": "QA Engineer"}
        response = requests.post(f"{BASE_URL}/users", json=payload)
        assert response.status_code == 201
        assert response.json()["name"] == "Ion Pop"
```

**Ce vei acoperi:**
- HTTP methods cu `requests`: `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
- Headers, autentificare: Basic Auth, Bearer Token, API Key
- Parsing JSON: `response.json()`, validare structură cu `jsonschema`
- pytest fixtures pentru sesiunea HTTP și date de test reutilizabile
- Parametrizare teste: `@pytest.mark.parametrize`
- **Playwright API Testing** — alternativă la `requests` pentru proiecte Playwright-only:

```python
def test_api_with_playwright(playwright):
    api = playwright.request.new_context(base_url="https://reqres.in")
    response = api.get("/api/users/1")
    assert response.ok
    assert response.json()["data"]["id"] == 1
```

**Proiect practic:** Suită completă de teste API pentru [reqres.in](https://reqres.in) sau [jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com) — CRUD complet, autentificare, validare schema, teste negative.

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (3–4 săptămâni)

> Diferența dintre un script de test și un framework profesionist folosit în producție.

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions — Docs | ~3h | [→ Deschide](https://docs.github.com/en/actions) |
| Allure with pytest — Docs | ~2h | [→ Deschide](https://allurereport.org/docs/pytest/) |
| Playwright Test Reports | ~1h | [→ Deschide](https://playwright.dev/python/docs/test-reporters) |
| Playwright Docker — Docs | ~2h | [→ Deschide](https://playwright.dev/python/docs/docker) |

**Ce vei învăța:**

**Allure Reports cu pytest:**
```bash
pip install allure-pytest
pytest --alluredir=allure-results
allure serve allure-results
```

**GitHub Actions CI:**
```yaml
# .github/workflows/tests.yml
name: Playwright Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.13"
      - run: pip install -r requirements.txt
      - run: playwright install --with-deps chromium
      - run: pytest tests/ --alluredir=allure-results
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: allure-results
          path: allure-results/
```

**Pytest avansat:**
- `conftest.py` — fixture-uri partajate între module
- `pytest.ini` / `pyproject.toml` — configurare globală (markers, timeout, paths)
- Markers: `@pytest.mark.smoke`, `@pytest.mark.regression`
- Rulare paralelă: `pytest-xdist` — `pytest -n auto`
- Retry la eșec: `pytest-rerunfailures` — `pytest --reruns 2`

**Proiect final — Frameworkul tău:**
```
my-playwright-framework/
├── pages/
│   ├── base_page.py
│   ├── login_page.py
│   └── dashboard_page.py
├── tests/
│   ├── ui/
│   │   └── test_login.py
│   └── api/
│       └── test_users_api.py
├── utils/
│   └── test_data.py
├── conftest.py
├── pytest.ini
├── requirements.txt
└── .github/
    └── workflows/
        └── tests.yml
```

> 💼 **Primul job:** Cu Faza 1–3 completă și un portofoliu de pe GitHub cu Playwright, poți aplica la Junior Automation QA. Playwright e extrem de căutat în 2026–2027.

---

## 💡 Sfaturi practice

### Cum să înveți eficient
- **30–45 minute zilnic** bate 4 ore la weekend — creierul consolidează în somn
- Folosește `playwright codegen https://site.com` pentru a vedea cum Playwright gândește locatorii
- Când un test pică, deschide trace viewer înainte să cauți în cod: `playwright show-trace`
- Commit pe GitHub chiar și codul imperfect — portofoliul contează mai mult decât perfecțiunea

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA (Playwright) |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA
- [Playwright Discord](https://discord.com/invite/playwright-807756831384403968) — comunitatea oficială Playwright
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate de testeri

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | Python | 3.13+ |
| IDE | VS Code | latest |
| UI Automation | Playwright | 1.52+ |
| Test framework | pytest | 8.x |
| API Testing | requests / Playwright API | latest |
| Reporting | Allure + pytest-playwright HTML | latest |
| CI/CD | GitHub Actions | — |
| Containers | Docker (Playwright image) | latest |
| Version control | Git + GitHub | — |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 4–6 luni (part-time) |
| **Nivel de start** | Zero experiență de programare |
| **Nivel de final** | Junior–Mid Automation QA Engineer |
| **Cost** | 100% gratuit |
| **Limbaj** | Python |
| **Focus** | Playwright UI + API Testing |
| **Avantaj față de Java** | Sintaxă mai simplă, setup mai rapid, `codegen` + trace viewer built-in |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [AI pentru Automation Engineers](./cale-invatare-ai-in-testare-automatizare.md) |
