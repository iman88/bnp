# 🤖 AI în Testare — pentru Automation Engineers

> AI Coding Assistants · Generare automată teste · Autonomous Testing · ~2–3 luni part-time

---

## 📋 Cuprins

- [Faza 1 — AI Coding Assistants](#-faza-1--ai-coding-assistants-23-săptămâni)
- [Faza 2 — Generare automată de teste din cod](#-faza-2--generare-automată-de-teste-din-cod-12-săptămâni)
- [Faza 3 — Platforme AI-powered cu integrare în cod](#-faza-3--platforme-ai-powered-cu-integrare-în-cod-23-săptămâni)
- [Faza 4 — Autonomous Testing & Agent-based QA](#-faza-4--autonomous-testing--agent-based-qa-23-săptămâni)
- [Faza 5 — AI în pipeline-ul CI/CD](#-faza-5--ai-în-pipeline-ul-cicd-12-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack AI pentru Automation](#-stack-ai-pentru-automation)

---

## 🟢 Faza 1 — AI Coding Assistants (2–3 săptămâni)

> Cel mai rapid ROI din tot traseul. Instalezi Copilot azi, ești mai productiv mâine.

| Unealtă | Scop | Cost | Link |
|---------|------|------|------|
| GitHub Copilot | Autocompletare + chat în orice IDE | $10/lună | [→ Deschide](https://github.com/features/copilot) |
| Cursor | IDE cu AI integrat — chat, edit, generare | Freemium | [→ Deschide](https://www.cursor.com/) |
| Claude Code | CLI agent — scrie, refactorizează, debuggează | Pay-per-use | [→ Deschide](https://claude.ai/code) |
| Codeium | Alternativă gratuită la Copilot | Gratuit | [→ Deschide](https://codeium.com/) |

**Ce vei învăța:**

**GitHub Copilot — fluxul de lucru:**
```python
# Scrii un comentariu descriptiv, Copilot completează testul
# Test că login cu email invalid returnează 400 și mesaj de eroare explicit

def test_login_invalid_email_format(api_client):
    # Copilot generează de aici încolo
    response = api_client.post("/auth/login", json={
        "email": "not-an-email",
        "password": "validPass123"
    })
    assert response.status_code == 400
    assert "invalid email" in response.json()["message"].lower()
```

- `@workspace` în Copilot Chat — context din întregul proiect, nu doar fișierul curent
- Generare teste din codul de producție selectat: `Ctrl+I` → „Write tests for this function"
- Explicare cod: selectezi o funcție complexă → „Explain this"
- Refactorizare POM: „Convert this test to use Page Object Model"

**Cursor — mai puternic decât Copilot pentru proiecte mari:**
- **Composer** (`Ctrl+Shift+I`) — descrii în text ce vrei, Cursor scrie fișiere întregi
- **`Ctrl+K`** — editezi codul selectat cu instrucțiuni în limbaj natural
- **`.cursorrules`** — fișier de configurare cu convențiile proiectului tău:
```
You are helping write Playwright TypeScript tests.
Always use Page Object Model pattern.
Locators priority: getByRole > getByLabel > getByTestId > CSS.
Use async/await, never .then() chains.
Add Allure annotations for all tests.
```
- Chat cu codebase: „Unde sunt definite fixture-urile pentru autentificare?" → răspuns cu link la fișier și linie

**Claude Code — pentru sarcini complexe de refactorizare:**
```bash
# În terminal, în directorul proiectului
claude "Analizează toate testele din /tests/ui și identifică:
- Locatori CSS hardcodați care ar trebui mutați în POM
- Teste fără assertions suficiente
- Duplicate de logică care pot fi extrase în helpers
Listează fișierele și liniile specifice."
```

**Exerciții practice — Săptămâna 1:**
1. Instalează Copilot și scrie 10 teste noi folosind doar comentarii ca indiciu
2. Compară viteza: scrii același test manual vs cu Copilot — notează diferența
3. Cere Copilot Chat să refactorizeze un test existent să folosească POM

---

## 🔵 Faza 2 — Generare automată de teste din cod (1–2 săptămâni)

> AI analizează codul de producție și generează teste — fără să scrii tu un singur test case.

| Unealtă | Limbaj | Ce generează | Link |
|---------|--------|-------------|------|
| Diffblue Cover | Java | Teste unitare JUnit din bytecode | [→ Deschide](https://www.diffblue.com/) |
| CodiumAI (Qodo) | Python, JS, TS, Java | Teste unitare + edge cases | [→ Deschide](https://www.qodo.ai/) |
| Pynguin | Python | Teste unitare automate | [→ Deschide](https://github.com/se2p/pynguin) |
| GitHub Copilot `/tests` | Orice | Teste din fișierul curent | built-in |

**CodiumAI — cel mai accesibil pentru începători:**
- Extensie VS Code / JetBrains — instalezi și e gata
- Selectezi o funcție → „Generate Tests" → primești teste cu edge cases incluse
- Explică de ce a generat fiecare test — înveți să gândești în edge cases

**Diffblue Cover — pentru proiecte Java enterprise:**
```bash
# Rulezi pe un modul Maven, generează teste JUnit automat
./dcover create --class com.example.UserService
# Output: UserServiceTest.java cu metode de test generate
```
- Acoperire de cod 50–80% fără să scrii un test manual
- Detectează regresii când codul de producție se schimbă

**Fluxul recomandat:**
```
1. Rulezi generatorul pe codul de producție
2. Revizuiești testele generate — sunt logice? Acoperă cazurile importante?
3. Adaugi teste pentru logica de business pe care AI nu o cunoaște
4. Adaugi teste de integrare pe care generatorul nu le poate produce
```

> ⚠️ **Regula de aur:** Testele generate de AI testează *ce face codul acum*, nu *ce ar trebui să facă*. Tu adaugi testele pentru cerințele de business.

---

## 🟡 Faza 3 — Platforme AI-powered cu integrare în cod (2–3 săptămâni)

> Unelte care se integrează în framework-ul tău existent și adaugă AI deasupra — nu le înlocuiesc.

| Platformă | Ce adaugă AI | Integrare | Link |
|-----------|-------------|-----------|------|
| Applitools Eyes | Visual AI — detectează regresii vizuale inteligent | Selenium, Playwright, WebdriverIO | [→ Deschide](https://applitools.com/) |
| Testim | Self-healing locators + AI authoring | Selenium, Playwright | [→ Deschide](https://www.testim.io/) |
| Mabl | Auto-healing + ML anomaly detection | SDK propriu | [→ Deschide](https://www.mabl.com/) |

**Applitools Eyes — Visual AI Testing:**

```python
# Python + Playwright + Applitools
from applitools.playwright import Eyes, Target

eyes = Eyes()
eyes.open(page, "My App", "Login Test")
eyes.check("Login Page", Target.window().fully())
# AI compară cu baseline — detectează orice diferență vizuală reală
# ignoră automat anti-aliasing, font rendering, variații acceptabile
eyes.close()
```

- **Ultrafast Grid** — un singur test rulat pe toate browserele și rezoluțiile simultan
- **Root Cause Analysis** — AI îți arată exact ce element s-a schimbat și de ce a picat
- Baseline management — approvi schimbările vizuale intenționate cu un click

**Self-Healing Locators — de ce contează:**
```python
# Înainte: testul pică dacă data-testid se schimbă
page.locator("[data-testid='submit-button']").click()

# Cu Testim self-healing: AI găsește butonul chiar dacă atributul s-a schimbat
# folosind combinație de: poziție, text, context vizual, structură DOM
```

**Curs recomandat:**
| Resursă | Durată | Link |
|---------|--------|------|
| Automated Visual Testing with Java — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/automated-visual-testing-a-fast-path-to-test-automation-success/) |

---

## 🟣 Faza 4 — Autonomous Testing & Agent-based QA (2–3 săptămâni)

> Frontiera actuală. AI nu mai asistă — execută. Relevant pentru exploratory testing și smoke checks, nu pentru regresie completă.

| Unealtă | Ce face | Link |
|---------|---------|------|
| AgentQL | Locatori în limbaj natural — AI găsește elementul indiferent de DOM | [→ Deschide](https://www.agentql.com/) |
| Browser Use | Agent AI care navighează browser autonom | [→ Deschide](https://github.com/browser-use/browser-use) |
| Playwright MCP + Claude | Claude Code controlează un browser real prin MCP | [→ Deschide](https://playwright.dev/docs/getting-started-mcp) |

**AgentQL — locatori care nu se rup:**
```python
import agentql
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch()
    page = agentql.wrap(browser.new_page())
    page.goto("https://example.com")

    # Descrii ce vrei în limbaj natural — AI găsește elementul
    response = page.query_elements("""
    {
        login_button
        email_input
        password_field
    }
    """)
    response.email_input.fill("user@test.com")
    response.login_button.click()
```

**Playwright MCP + Claude Code — test explorator autonom:**
```bash
# Cu MCP Playwright configurat în Claude Code
claude "Testează fluxul de checkout pe [URL]:
- Adaugă 2 produse din categorii diferite
- Aplică codul DISCOUNT10
- Verifică că reducerea se aplică corect în coș
- Raportează orice eroare sau comportament neașteptat
Fă screenshot la fiecare pas important."
```

**Browser Use — agent complet autonom:**
```python
from browser_use import Agent
from langchain_anthropic import ChatAnthropic

agent = Agent(
    task="Mergi pe site-ul X, loghează-te cu credențialele Y, \
          verifică că dashboard-ul se încarcă și raportează orice eroare.",
    llm=ChatAnthropic(model="claude-sonnet-4-6"),
)
result = agent.run()
```

**Unde funcționează autonomous testing:**
- Exploratory testing rapid pe o funcționalitate nouă
- Smoke check pe un environment de staging
- Verificare ad-hoc după un deploy

**Unde NU funcționează:**
- Regresie completă — nedeterminist și costisitor
- Teste care necesită date precise și assertions exacte
- Înlocuirea testelor de regresie scriptate

---

## 🔴 Faza 5 — AI în pipeline-ul CI/CD (1–2 săptămâni)

> Ultimul nivel: AI decide ce teste să rulezi, analizează eșecurile și prezice riscul unui merge.

**Impact Analysis — rulezi doar testele relevante:**

Unelte precum **Launchable** sau **Trunk** analizează ce cod s-a schimbat și prezic ce teste au cea mai mare șansă să pice — rulezi 20% din suită și depistezi 80% din bug-uri.

```yaml
# GitHub Actions cu Launchable
- name: Subset tests with AI
  run: launchable subset --target 20% pytest tests/ > test_subset.txt
- name: Run subset
  run: pytest $(cat test_subset.txt)
```

**Analiză automată a eșecurilor:**
```bash
# Post-run: trimiți log-ul de eșec la Claude
claude "Analizează acest log de test eșuat și spune-mi:
1. Care e cauza root — bug în cod sau test fragil?
2. Ce fișier și linie din cod e probabil responsabil?
3. E un test flaky sau o regresie reală?
Log: $(cat test-output.log)"
```

**Flaky test detection cu AI:**
- **Currents** sau **BuildPulse** — monitorizează istoric și marchează automat testele flaky
- AI grupează eșecurile cu pattern similar — nu raportezi același bug de 10 ori

| Unealtă | Scop | Link |
|---------|------|------|
| Launchable | Test selection inteligentă în CI | [→ Deschide](https://www.launchableinc.com/) |
| BuildPulse | Flaky test detection automat | [→ Deschide](https://buildpulse.io/) |
| Currents | Analytics CI + flaky detection | [→ Deschide](https://currents.dev/) |

---

## 💡 Sfaturi practice

### Fluxul de lucru AI-augmented — un sprint complet

```
Luni (planning):
  → Claude analizează story-urile și generează test cases + scenarii Gherkin
  → Tu validezi și adaugi contextul de business

Marți–Joi (development):
  → Copilot/Cursor scriu 60–70% din codul de test
  → Tu scrii logica complexă, assertions de business, fixtures

Vineri (review):
  → CodiumAI verifică acoperirea
  → Claude Code identifică locatori fragili și duplicate
  → Pipeline rulează subset inteligent cu Launchable
```

### Ce rămâne la tine

- Decizia de release — AI nu are context de business și risc
- Arhitectura framework-ului — AI sugerează, tu decizi
- Validarea testelor generate — codul AI e corect sintactic, dar poate testa ce nu trebuie
- Debugging eșecuri complexe — AI ajută, dar nu înlocuiește înțelegerea sistemului

### Cum să rămâi la curent

- [The Pragmatic Engineer Newsletter](https://newsletter.pragmaticengineer.com/) — AI în engineering
- [Playwright Discord](https://discord.com/invite/playwright-807756831384403968) — discuții despre AI + Playwright
- [Ministry of Testing — AI](https://www.ministryoftesting.com/articles?q=AI) — perspectivă QA practică

---

## 🛠 Stack AI pentru Automation

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| AI coding assistant | GitHub Copilot | $10/lună |
| IDE cu AI | Cursor | Freemium |
| Generare teste unitare | CodiumAI (Qodo) | Freemium |
| Generare teste Java | Diffblue Cover | Trial |
| Visual AI testing | Applitools Eyes | Trial |
| Self-healing locators | Testim | Freemium |
| Locatori naturali | AgentQL | Freemium |
| Agent autonom | Browser Use | Open-source |
| MCP browser control | Playwright MCP + Claude Code | Pay-per-use |
| CI test selection | Launchable | Freemium |
| Flaky detection | BuildPulse | Freemium |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 2–3 luni (part-time) |
| **Nivel de start** | Automation engineer cu experiență de bază (Selenium/Playwright) |
| **Câștig principal** | Productivitate 3–5x în scrierea și mentenanța testelor |
| **Cost** | Mixt — unele gratuite, unele $10–20/lună |
| **Pasul următor** | [AI în Testare — Full Stack](./cale-invatare-ai-in-testare.md) pentru o perspectivă completă |
