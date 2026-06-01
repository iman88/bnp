# ⚙️ Software Development Engineer in Test (SDET) — Cale de Învățare

> Inginerie software aplicată în testare · Infrastructură de testare · ~6–9 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de inginerie software](#-faza-1--fundamente-de-inginerie-software-46-săptămâni)
- [Faza 2 — Proiectarea și construirea infrastructurii de testare](#-faza-2--proiectarea-și-construirea-infrastructurii-de-testare-46-săptămâni)
- [Faza 3 — Testare la nivel de cod](#-faza-3--testare-la-nivel-de-cod-34-săptămâni)
- [Faza 4 — Observabilitate și monitorizare](#-faza-4--observabilitate-și-monitorizare-23-săptămâni)
- [Faza 5 — Contribuție la codul de producție](#-faza-5--contribuție-la-codul-de-producție-34-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)

---

## 🟢 Faza 1 — Fundamente de inginerie software (4–6 săptămâni)

> Un SDET e în primul rând un inginer software. Diferența față de un automation engineer e că SDET-ul scrie cod de calitate producție — nu doar scripturi de test.

| Resursă | Durată | Link |
|---------|--------|------|
| Clean Code Principles — Refactoring.guru | ~5h | [→ Deschide](https://refactoring.guru/refactoring) |
| Design Patterns — Refactoring.guru | ~8h | [→ Deschide](https://refactoring.guru/design-patterns) |
| Data Structures & Algorithms in Python — Runestone Academy | ~10h | [→ Deschide](https://runestone.academy/ns/books/published/pythonds3/index.html) |
| Git Advanced — Atlassian | ~3h | [→ Deschide](https://www.atlassian.com/git/tutorials/advanced-overview) |

**Ce diferențiază codul unui SDET de codul unui automation engineer:**

| Automation Engineer | SDET |
|--------------------|------|
| Scrie teste care funcționează | Scrie infrastructură pe care alții o folosesc pentru a scrie teste |
| Folosește framework-uri existente | Construiește și menține framework-uri |
| Codul e folosit intern în echipa QA | Codul e folosit de dev, QA, DevOps |
| Bug în test → testul eșuează | Bug în infrastructură → toată echipa e blocată |

**Principii de cod pe care le aplici la alt nivel:**

- **SOLID** — mai ales Single Responsibility și Dependency Inversion în design-ul framework-urilor
- **DRY** — deduplicare la nivel de librărie, nu de test
- **Defensive programming** — codul tău va fi folosit greșit — gestionezi și cazurile de utilizare incorectă
- **Versionare semantică** — framework-urile pe care le construiești au versiuni, breaking changes, changelog

**Structuri de date relevante pentru SDET:**
```python
# Queue — pentru gestionarea cozilor de teste în execuție paralelă
from queue import Queue

# Graph — pentru modelarea dependențelor dintre teste
# Ex: testul B necesită starea creată de testul A
dependencies = {
    "test_checkout": ["test_login", "test_add_to_cart"],
    "test_payment": ["test_checkout"],
}

# Heap — pentru prioritizarea execuției testelor după risc
import heapq
test_queue = [(risk_score, test_name) for ...]
heapq.heapify(test_queue)
```

---

## 🔵 Faza 2 — Proiectarea și construirea infrastructurii de testare (4–6 săptămâni)

> Un SDET nu scrie teste — construiește platforma pe care alții scriu teste mai ușor și mai fiabil.

| Resursă | Durată | Link |
|---------|--------|------|
| Test Infrastructure at Scale — Google Testing Blog | ~2h | [→ Deschide](https://testing.googleblog.com/) |
| Building Test Frameworks — TAU | ~4h | [→ Deschide](https://testautomationu.applitools.com/test-automation-framework-intro/) |
| Docker pentru developeri — Play with Docker | ~4h | [→ Deschide](https://training.play-with-docker.com/) |
| Kubernetes Basics — kubernetes.io | ~5h | [→ Deschide](https://kubernetes.io/docs/tutorials/kubernetes-basics/) |

**Ce construiește un SDET — exemple concrete:**

**Librării de utilități partajate:**
```python
# utils/api_client.py — client HTTP reutilizabil pentru toate testele
class ApiClient:
    def __init__(self, base_url: str, auth_token: str = None):
        self.session = requests.Session()
        self.session.base_url = base_url
        if auth_token:
            self.session.headers["Authorization"] = f"Bearer {auth_token}"

    def get(self, endpoint: str, **kwargs) -> Response:
        return self._request("GET", endpoint, **kwargs)

    def post(self, endpoint: str, data: dict, **kwargs) -> Response:
        return self._request("POST", endpoint, json=data, **kwargs)

    def _request(self, method: str, endpoint: str, **kwargs) -> Response:
        response = self.session.request(method, f"{self.session.base_url}{endpoint}", **kwargs)
        self._log_request(method, endpoint, response)
        return response
```

**Sistem de gestiune date de test:**
```python
# factories/user_factory.py — generare date de test reproductibile
from faker import Faker
from dataclasses import dataclass

fake = Faker("ro_RO")

@dataclass
class TestUser:
    email: str
    password: str
    first_name: str
    last_name: str

class UserFactory:
    @staticmethod
    def create_standard() -> TestUser:
        return TestUser(
            email=f"test_{fake.uuid4()[:8]}@test.com",
            password="Test@1234",
            first_name=fake.first_name(),
            last_name=fake.last_name(),
        )

    @staticmethod
    def create_admin() -> TestUser:
        user = UserFactory.create_standard()
        user.email = f"admin_{user.email}"
        return user
```

**Plugin pytest personalizat:**
```python
# conftest.py la nivel de organizație — distribuit ca pachet intern
import pytest

def pytest_configure(config):
    config.addinivalue_line("markers", "smoke: teste de smoke pentru release rapid")
    config.addinivalue_line("markers", "critical: teste pentru fluxuri critice de business")

@pytest.fixture(scope="session")
def api_client(request):
    env = request.config.getoption("--env", default="staging")
    base_url = ENV_URLS[env]
    client = ApiClient(base_url)
    yield client
    client.session.close()

def pytest_runtest_makereport(item, call):
    # Atașează automat screenshot la orice test UI care pică
    if call.when == "call" and call.excinfo:
        if "page" in item.fixturenames:
            page = item.funcargs["page"]
            page.screenshot(path=f"screenshots/{item.nodeid.replace('/', '_')}.png")
```

**Medii de testare izolate cu Docker:**
```yaml
# docker-compose.test.yml
services:
  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: testdb
      POSTGRES_USER: test
      POSTGRES_PASSWORD: test
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U test"]
      interval: 5s

  redis:
    image: redis:7-alpine

  app:
    build: .
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      DATABASE_URL: postgresql://test:test@postgres:5432/testdb
      REDIS_URL: redis://redis:6379

  tests:
    build:
      dockerfile: Dockerfile.test
    depends_on: [app]
    command: pytest tests/ -x --tb=short
```

---

## 🟡 Faza 3 — Testare la nivel de cod (3–4 săptămâni)

> Un SDET lucrează alături de developeri la niveluri de testare la care QA-ul clasic nu ajunge.

| Resursă | Durată | Link |
|---------|--------|------|
| Unit Testing Best Practices — Martin Fowler | ~2h | [→ Deschide](https://martinfowler.com/bliki/UnitTest.html) |
| Mutation Testing — Pitest (Java) / mutmut (Python) | ~3h | [→ Deschide](https://pitest.org/) |
| Property-Based Testing — Hypothesis (Python) | ~3h | [→ Deschide](https://hypothesis.readthedocs.io/) |
| Contract Testing cu Pact | ~4h | [→ Deschide](https://docs.pact.io/) |

**Testare prin mutație — verifici că testele tale verifică ceva:**

Mutation testing modifică automat codul de producție (schimbă `>` cu `>=`, șterge linii, inversează condiții) și verifică dacă testele tale detectează modificarea. Dacă un test nu pică când codul e greșit — testul nu testează nimic util.

```bash
# Python — mutmut
pip install mutmut
mutmut run --paths-to-mutate src/
mutmut results  # câți mutanți au supraviețuit (nedetectați de teste)?
```

**Property-based testing — găsești cazuri pe care nu le-ai gândit:**

```python
from hypothesis import given, strategies as st

# În loc să scrii 10 cazuri de test cu valori fixe,
# Hypothesis generează automat sute de cazuri
@given(
    amount=st.floats(min_value=0.01, max_value=1_000_000),
    currency=st.sampled_from(["RON", "EUR", "USD"]),
)
def test_currency_conversion_never_negative(amount, currency):
    result = convert_currency(amount, currency, "EUR")
    assert result >= 0, f"Conversie negativă: {amount} {currency} → {result} EUR"
```

**Testare la nivelul bazei de date:**
```python
# Verifici că migrările de bază de date nu rup datele existente
def test_migration_preserves_user_data(db_session):
    # Inserezi date înainte de migrare
    user = User(email="test@example.com", role="admin")
    db_session.add(user)
    db_session.commit()

    # Rulezi migrarea
    run_migration("0042_add_user_preferences")

    # Verifici că datele existente sunt intacte
    migrated_user = db_session.query(User).filter_by(email="test@example.com").first()
    assert migrated_user.role == "admin"
    assert migrated_user.preferences == {}  # coloana nouă cu default corect
```

---

## 🟣 Faza 4 — Observabilitate și monitorizare (2–3 săptămâni)

> Un SDET înțelege că testele nu se termină la lansare. Producția e cel mai mare mediu de testare.

| Resursă | Durată | Link |
|---------|--------|------|
| Observability Engineering — Honeycomb | articole gratuite | [→ Deschide](https://www.honeycomb.io/blog) |
| OpenTelemetry — Docs oficiale | ~4h | [→ Deschide](https://opentelemetry.io/docs/) |
| Grafana Stack — Tutorials | ~4h | [→ Deschide](https://grafana.com/tutorials/) |

**Cele trei piloni ai observabilității:**

| Pilon | Ce e | Unealtă |
|-------|------|---------|
| Jurnale (Logs) | Înregistrări text ale evenimentelor | ELK Stack, Loki |
| Metrici | Valori numerice în timp | Prometheus, Grafana |
| Urme (Traces) | Parcursul unei cereri prin sistem | Jaeger, Zipkin |

**Un SDET adaugă testabilitate în codul de producție:**
```python
# Instrumentare OpenTelemetry — SDET-ul o adaugă, toată echipa beneficiază
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

def process_payment(order_id: str, amount: float) -> PaymentResult:
    with tracer.start_as_current_span("process_payment") as span:
        span.set_attribute("order.id", order_id)
        span.set_attribute("payment.amount", amount)

        result = payment_gateway.charge(amount)

        span.set_attribute("payment.success", result.success)
        span.set_attribute("payment.transaction_id", result.transaction_id)

        return result
```

---

## 🔴 Faza 5 — Contribuție la codul de producție (3–4 săptămâni)

> Diferența fundamentală față de orice alt rol QA: un SDET contribuie la baza de cod de producție, nu doar la codul de test.

| Resursă | Durată | Link |
|---------|--------|------|
| Code Review Best Practices — Google | ~1h | [→ Deschide](https://google.github.io/eng-practices/review/) |
| Refactoring pentru testabilitate — Martin Fowler | ~3h | [→ Deschide](https://martinfowler.com/articles/refactoring-video.html) |
| Feature Flags — LaunchDarkly Blog | ~2h | [→ Deschide](https://launchdarkly.com/blog/) |

**Ce modificări face un SDET în codul de producție:**

- **Adaugă testabilitate** — injectare dependențe, interfețe pentru mock-uri, endpoint-uri de health check
- **Instrumentare** — logging structurat, metrici, urme distribuite
- **Feature flags** — posibilitatea de a activa/dezactiva funcționalități fără deployment
- **Seeding de date** — scripturi de inițializare medii de test
- **Refactorizare pentru testabilitate** — cod legacy greu de testat devine testabil

**Exemplu — adaugi testabilitate fără să schimbi comportamentul:**
```python
# Înainte — greu de testat, EmailService e hardcodat
class OrderService:
    def confirm_order(self, order_id: str):
        order = self.db.get_order(order_id)
        EmailService().send_confirmation(order.user_email, order)  # hardcodat!

# După — ușor de testat cu mock
class OrderService:
    def __init__(self, db: Database, email_service: EmailService):
        self.db = db
        self.email_service = email_service  # injectat

    def confirm_order(self, order_id: str):
        order = self.db.get_order(order_id)
        self.email_service.send_confirmation(order.user_email, order)

# În test — mock-uiești serviciul de email fără să trimiți emailuri reale
def test_order_confirmation_sends_email():
    mock_email = Mock(spec=EmailService)
    service = OrderService(db=real_db, email_service=mock_email)
    service.confirm_order("ORDER-123")
    mock_email.send_confirmation.assert_called_once()
```

---

## 💡 Sfaturi practice

### Ești potrivit pentru rolul de SDET dacă

- Îți place să scrii cod și te deranjează codul scris prost — inclusiv în teste
- Vrei să construiești unelte pe care alții le folosesc, nu să le folosești pe ale altora
- Ești confortabil cu code review-uri unde developerii îți corectează codul
- Ai răbdare pentru probleme de infrastructură — debugging de CI/CD, Docker, rețea

### Nu e rolul potrivit dacă

- Vrei să rămâi aproape de produsul final și de utilizator
- Preferi să găsești bug-uri, nu să construiești sisteme
- Nu vrei să investești serios în programare la nivel de developer

### Traseu de carieră

```
Automation Engineer (2–4 ani)
    ↓ înveți să scrii cod de calitate producție
SDET (3–5 ani)
    ↓
Staff SDET / Principal Engineer / Engineering Manager
```

### Diferența față de Software Developer

Un developer construiește funcționalități pentru utilizatori. Un SDET construiește infrastructură pentru ca echipa să livreze funcționalități mai rapid și cu mai puține bug-uri. Audiența ta e internă — developerii și QA-ul, nu utilizatorul final.

---

## 🛠 Stack SDET

| Categorie | Tehnologie | Versiune/Note |
|-----------|-----------|--------------|
| Limbaj | Python sau Java | 3.13+ / 21 LTS |
| Mutation testing | mutmut (Python) / Pitest (Java) | latest |
| Property-based testing | Hypothesis (Python) | latest |
| Contract testing | Pact | latest |
| Containerizare | Docker | latest |
| Orkestrare | Kubernetes | latest |
| Observabilitate | OpenTelemetry + Grafana + Prometheus | latest |
| Distributed tracing | Jaeger / Zipkin | latest |
| CI/CD | GitHub Actions | — |
| Version control | Git + GitHub | — |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 6–9 luni (part-time) |
| **Nivel de start** | Automation Engineer cu experiență solidă în programare |
| **Nivel de final** | SDET / Software Development Engineer in Test |
| **Cost** | 100% gratuit |
| **Focus** | Infrastructură de testare, cod de calitate producție, observabilitate |
| **Avertisment** | Cel mai apropiat rol de software developer din lumea QA — necesită fundamente solide de programare |
| **Pasul următor** | [QA Tech Lead](./cale-invatare-qa-tech-lead.md) · [Test Arhitect](./cale-invatare-test-arhitect.md) |
