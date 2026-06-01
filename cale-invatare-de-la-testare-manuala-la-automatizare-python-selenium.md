# 🐍 De la Testare Manuală la Automatizare — Python + Selenium

> Python · Selenium WebDriver UI + API Testing · De la zero absolut · ~4–6 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de programare Python](#-faza-1--fundamente-de-programare-python-46-săptămâni)
- [Faza 2 — Setup & unelte esențiale](#-faza-2--setup--unelte-esențiale-12-săptămâni)
- [Faza 3 — Selenium WebDriver UI Automation](#-faza-3--selenium-webdriver-ui-automation-56-săptămâni)
- [Faza 4 — API Testing](#-faza-4--api-testing-34-săptămâni)
- [Faza 5 — Nivel profesionist & CI/CD](#-faza-5--nivel-profesionist--cicd-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de programare Python (4–6 săptămâni)

> Python e cel mai accesibil limbaj de start pentru QA — sintaxă clară, fără boilerplate, comunitate uriașă.

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
- List comprehensions și `lambda`
- Lucrul cu fișiere: citire/scriere JSON, CSV, TXT
- Gestionarea erorilor: `try/except/finally`
- Module esențiale: `os`, `json`, `re`, `datetime`

**Resursa cheie:** „Automate the Boring Stuff" e scrisă special pentru non-programatori — exercițiile sunt imediat aplicabile și relevante pentru QA.

---

## 🔵 Faza 2 — Setup & unelte esențiale (1–2 săptămâni)

> Python + Selenium are cel mai simplu setup din toate combinațiile — SeleniumManager descarcă driverele automat din Selenium 4.6+.

| Unealtă | Scop | Link |
|---------|------|------|
| Python 3.13+ | Runtime Python | [→ Descarcă](https://www.python.org/downloads/) |
| VS Code + extensia Python | IDE principal | [→ Descarcă](https://code.visualstudio.com/) |
| pip + venv | Gestionare pachete și medii virtuale | [→ Ghid](https://docs.python.org/3/library/venv.html) |
| Git (cap. 1–3) | Control de versiune | [→ Pro Git Book](https://git-scm.com/book/en/v2) |
| pytest | Framework de testare | [→ Docs](https://docs.pytest.org/en/stable/) |

**Instalare Selenium:**
```bash
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS/Linux
pip install selenium pytest allure-pytest
```

> Din Selenium 4.6+ nu mai ai nevoie să descarci manual ChromeDriver — **SeleniumManager** îl gestionează automat.

**Structura proiectului:**
```
my-selenium-python/
├── tests/
│   ├── ui/
│   │   └── test_login.py
│   └── api/
│       └── test_users.py
├── pages/
│   ├── base_page.py
│   └── login_page.py
├── utils/
│   └── test_data.py
├── conftest.py
├── pytest.ini
└── requirements.txt
```

---

## 🟡 Faza 3 — Selenium WebDriver UI Automation (5–6 săptămâni)

> Selenium rămâne cel mai răspândit framework de UI automation. Dacă știi Selenium Python, poți lucra în orice companie care are teste web.

| Resursă | Durată | Link |
|---------|--------|------|
| Selenium with Python — Docs oficiale | referință | [→ Deschide](https://selenium-python.readthedocs.io/) |
| Selenium WebDriver with Python — TAU | ~5h | [→ Deschide](https://testautomationu.applitools.com/selenium-webdriver-tutorial-python/) |
| Selenium 4 Official Docs | referință | [→ Deschide](https://www.selenium.dev/documentation/) |

**Ce vei învăța:**

**Setup și primul test:**
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()   # SeleniumManager găsește ChromeDriver automat
driver.get("https://example.com/login")

email_field = driver.find_element(By.ID, "email")
email_field.send_keys("user@test.com")

driver.find_element(By.CSS_SELECTOR, "button[type='submit']").click()
driver.quit()
```

**Locatori — de la preferabil la fallback:**
```python
By.ID            # cel mai rapid și stabil
By.NAME          # pentru câmpuri de formular
By.CSS_SELECTOR  # flexibil, performant
By.XPATH         # pentru structuri complexe sau text
By.CLASS_NAME    # evită dacă clasa e generată dinamic
By.LINK_TEXT     # pentru linkuri cu text exact
```

**Waits — esențial pentru teste stabile:**
```python
# Implicit Wait — se setează o dată pentru tot driver-ul
driver.implicitly_wait(10)

# Explicit Wait — recomandat, mai controlat
wait = WebDriverWait(driver, timeout=10)
element = wait.until(EC.element_to_be_clickable((By.ID, "submit-btn")))
element.click()

# FluentWait — polling configurabil
from selenium.webdriver.support.wait import WebDriverWait
wait = WebDriverWait(driver, timeout=15, poll_frequency=0.5,
                     ignored_exceptions=[NoSuchElementException])
```

**Page Object Model cu Python:**
```python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class LoginPage:
    EMAIL_INPUT = (By.ID, "email")
    PASSWORD_INPUT = (By.ID, "password")
    LOGIN_BUTTON = (By.CSS_SELECTOR, "button[type='submit']")
    ERROR_MESSAGE = (By.CLASS_NAME, "error-msg")

    def __init__(self, driver):
        self.driver = driver
        self.wait = WebDriverWait(driver, 10)

    def login(self, email: str, password: str):
        self.wait.until(EC.visibility_of_element_located(self.EMAIL_INPUT)).send_keys(email)
        self.driver.find_element(*self.PASSWORD_INPUT).send_keys(password)
        self.driver.find_element(*self.LOGIN_BUTTON).click()

    def get_error_message(self) -> str:
        return self.wait.until(
            EC.visibility_of_element_located(self.ERROR_MESSAGE)
        ).text
```

**Pytest + Selenium — fixtures în `conftest.py`:**
```python
import pytest
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

@pytest.fixture(scope="function")
def driver():
    options = Options()
    options.add_argument("--headless")          # rulare fără browser vizibil
    options.add_argument("--window-size=1920,1080")
    driver = webdriver.Chrome(options=options)
    yield driver
    driver.quit()

# Folosit în test
def test_login_valid(driver):
    driver.get("https://example.com/login")
    page = LoginPage(driver)
    page.login("user@test.com", "secret123")
    assert "dashboard" in driver.current_url
```

**Acțiuni Selenium 4:**
```python
from selenium.webdriver import ActionChains

actions = ActionChains(driver)
actions.move_to_element(element).click().perform()      # hover + click
actions.drag_and_drop(source, target).perform()         # drag & drop
actions.double_click(element).perform()                 # double click
actions.context_click(element).perform()                # right click
```

**Funcții avansate:**
- Screenshot la eșec în pytest:
```python
@pytest.hookimpl(hookwrapper=True)
def pytest_runtest_makereport(item, call):
    outcome = yield
    rep = outcome.get_result()
    if rep.failed:
        driver = item.funcargs.get("driver")
        if driver:
            driver.save_screenshot(f"screenshots/{item.name}.png")
```
- `execute_script()` — JavaScript direct din Python pentru acțiuni imposibile altfel
- Selenium Grid — rulare distribuită pe multiple mașini/browsere

**Proiect practic:** Automatizează un flux complet pe [the-internet.herokuapp.com](https://the-internet.herokuapp.com) sau [automationpractice.pl](http://automationpractice.pl) — login, formular, tabele, alerts. Minim 10 teste cu POM complet.

---

## 🟣 Faza 4 — API Testing (3–4 săptămâni)

> `requests` e librăria Python standard pentru HTTP — simplă, puternică, documentată excepțional.

| Resursă | Durată | Link |
|---------|--------|------|
| requests Library — Docs oficiale | referință | [→ Deschide](https://requests.readthedocs.io/en/latest/) |
| API Testing with Python — RealPython | ~3h | [→ Deschide](https://realpython.com/api-integration-in-python/) |
| Postman — Testare manuală API | referință | [→ Cale Postman](./cale-invatare-postman.md) |

**Ce vei învăța:**

```python
import requests
import pytest

BASE_URL = "https://reqres.in/api"

class TestUsersAPI:
    def test_get_users_list(self):
        response = requests.get(f"{BASE_URL}/users", params={"page": 1})
        assert response.status_code == 200
        data = response.json()
        assert len(data["data"]) > 0

    def test_create_user(self):
        payload = {"name": "Ion Pop", "job": "QA Engineer"}
        response = requests.post(f"{BASE_URL}/users", json=payload)
        assert response.status_code == 201
        body = response.json()
        assert body["name"] == "Ion Pop"
        assert "id" in body

    def test_delete_user(self):
        response = requests.delete(f"{BASE_URL}/users/1")
        assert response.status_code == 204

    @pytest.mark.parametrize("user_id,expected_status", [
        (1, 200),
        (999, 404),
    ])
    def test_get_user_by_id(self, user_id, expected_status):
        response = requests.get(f"{BASE_URL}/users/{user_id}")
        assert response.status_code == expected_status
```

**Ce vei acoperi:**
- `requests.Session()` — sesiune reutilizabilă cu headers globale și autentificare
- Bearer Token, Basic Auth, API Key în headers
- Validare schema cu `jsonschema` sau `pydantic`
- Fixture pytest pentru sesiunea API:
```python
@pytest.fixture(scope="session")
def api_session():
    session = requests.Session()
    session.headers.update({"Authorization": f"Bearer {TOKEN}"})
    session.base_url = "https://reqres.in/api"
    return session
```

**Proiect practic:** Suită API completă pentru [reqres.in](https://reqres.in) — CRUD, autentificare, validare schema, teste negative, parametrizare.

---

## 🔴 Faza 5 — Nivel profesionist & CI/CD (3–4 săptămâni)

| Resursă | Durată | Link |
|---------|--------|------|
| GitHub Actions — Docs | ~3h | [→ Deschide](https://docs.github.com/en/actions) |
| Allure with pytest — Docs | ~2h | [→ Deschide](https://allurereport.org/docs/pytest/) |
| Selenium Grid — Ghid | ~3h | [→ Deschide](https://www.selenium.dev/documentation/grid/) |

**Ce vei învăța:**

**Allure Reports:**
```bash
pip install allure-pytest
pytest --alluredir=allure-results
allure serve allure-results
```

**GitHub Actions CI:**
```yaml
name: Selenium Python Tests
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
      - run: pytest tests/ --alluredir=allure-results --headless
      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: allure-results
          path: allure-results/
```

**Pytest avansat:**
- `conftest.py` cu fixture-uri partajate la nivel de sesiune, modul, funcție
- Markers: `@pytest.mark.smoke`, `@pytest.mark.regression`
- `pytest-xdist` — rulare paralelă: `pytest -n auto`
- `pytest-rerunfailures` — retry pentru teste flaky: `pytest --reruns 2`
- `pytest.ini` — configurare globală

**Proiect final — Framework complet:**
```
my-selenium-python-framework/
├── pages/
│   ├── base_page.py
│   ├── login_page.py
│   └── dashboard_page.py
├── tests/
│   ├── ui/
│   │   └── test_login.py
│   └── api/
│       └── test_users.py
├── utils/
│   └── test_data.py
├── conftest.py
├── pytest.ini
├── requirements.txt
└── .github/
    └── workflows/
        └── tests.yml
```

> 💼 **Primul job:** Python + Selenium e extrem de cerut — cele mai multe framework-uri de QA în companii mid-size folosesc exact această combinație. Cu Fazele 1–3 și un portofoliu GitHub, poți aplica la Junior Automation QA.

---

## 💡 Sfaturi practice

### Când să alegi Python + Selenium față de alte variante

| Alege Python + Selenium dacă... | Alege altceva dacă... |
|--------------------------------|----------------------|
| Compania are deja framework Selenium | Pornești un proiect nou (→ Playwright e mai modern) |
| Echipa cunoaște Python | Preferi Java în ecosistem enterprise |
| Vrei să combini testele cu AI/data science | Vrei trace viewer și auto-wait fără configurare (→ Playwright) |

### Când ești gata de job

| Faze complete | Poți aplica la |
|---------------|----------------|
| Faza 1–3 | Junior Automation QA (Selenium/Python) |
| Faza 1–4 | Automation QA Engineer |
| Faza 1–5 + portofoliu | QA Automation Engineer (mid-level) |

### Comunități utile
- [r/QualityAssurance](https://www.reddit.com/r/QualityAssurance/) — Reddit QA
- [Ministry of Testing](https://www.ministryoftesting.com/) — cea mai mare comunitate globală
- [Selenium Discord](https://discord.com/invite/selenium-807756831384403968) — suport oficial

---

## 🛠 Stack tehnologic

| Categorie | Tehnologie | Versiune recomandată |
|-----------|-----------|----------------------|
| Limbaj | Python | 3.13+ |
| IDE | VS Code | latest |
| UI Automation | Selenium WebDriver | 4.21+ |
| Test framework | pytest | 8.x |
| API Testing | requests | 2.x |
| Reporting | Allure + pytest-html | latest |
| CI/CD | GitHub Actions | — |
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
| **Framework** | Selenium WebDriver 4.x |
| **Față de Python + Playwright** | Selenium e mai răspândit în companii mature; Playwright e mai modern pentru proiecte noi |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [AI pentru Automation Engineers](./cale-invatare-ai-in-testare-automatizare.md) |
