# 🗄️ Testare SQL & Baze de Date — Cale de Învățare

> SQL pentru testeri · Validare date · Integritate baze de date · ~2–3 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente SQL pentru testeri](#-faza-1--fundamente-sql-pentru-testeri-34-săptămâni)
- [Faza 2 — Validarea datelor și integritatea bazei de date](#-faza-2--validarea-datelor-și-integritatea-bazei-de-date-34-săptămâni)
- [Faza 3 — Tehnici avansate de interogare](#-faza-3--tehnici-avansate-de-interogare-23-săptămâni)
- [Faza 4 — Testare baze de date în automatizare](#-faza-4--testare-baze-de-date-în-automatizare-23-săptămâni)
- [Faza 5 — Performanța interogărilor](#-faza-5--performanța-interogărilor-12-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente SQL pentru testeri (3–4 săptămâni)

> SQL e una din cele mai valoroase abilități ale unui QA — îți permite să verifici datele direct la sursă, fără să depinzi de developeri.

| Resursă | Durată | Link |
|---------|--------|------|
| SQL Tutorial — SQLZoo | ~8h | [→ Deschide](https://sqlzoo.net/wiki/SQL_Tutorial) |
| SQL pentru testeri — Guru99 | ~4h | [→ Deschide](https://www.guru99.com/sql-for-testers.html) |
| Interactive SQL — Mode Analytics | ~5h | [→ Deschide](https://mode.com/sql-tutorial/) |
| SQLite Online — practică directă în browser | referință | [→ Deschide](https://sqliteonline.com/) |

**De ce SQL e esențial pentru un QA:**

- Verifici că datele salvate în baza de date corespund cu ce ai introdus în UI
- Identifici date de test existente fără să ceri ajutor developerilor
- Depistezi bug-uri de persistență — UI arată corect, dar datele din DB sunt greșite
- Pregătești starea inițială pentru teste fără să parcurgi fluxuri întregi de UI

**Comenzi esențiale — ce folosești zilnic ca tester:**

```sql
-- Verifici că un utilizator a fost creat corect
SELECT id, email, created_at, status
FROM users
WHERE email = 'test@example.com';

-- Verifici că o comandă a fost plasată cu produsele corecte
SELECT o.id, o.status, o.total_amount,
       oi.product_id, oi.quantity, oi.unit_price
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
WHERE o.id = 12345;

-- Numeri câte înregistrări au o anumită valoare
SELECT status, COUNT(*) as count
FROM orders
WHERE created_at >= CURRENT_DATE - INTERVAL '7 days'
GROUP BY status
ORDER BY count DESC;

-- Găsești înregistrări duplicate
SELECT email, COUNT(*) as occurrences
FROM users
GROUP BY email
HAVING COUNT(*) > 1;

-- Verifici că nu există date orfane (comenzi fără utilizator)
SELECT o.id, o.user_id
FROM orders o
LEFT JOIN users u ON o.user_id = u.id
WHERE u.id IS NULL;
```

**Setup mediu de lucru:**

| Unealtă | Scop | Link |
|---------|------|------|
| DBeaver Community | Client universal pentru orice bază de date | [→ Descarcă](https://dbeaver.io/) |
| pgAdmin | Client dedicat PostgreSQL | [→ Descarcă](https://www.pgadmin.org/) |
| MySQL Workbench | Client dedicat MySQL | [→ Descarcă](https://www.mysql.com/products/workbench/) |
| TablePlus | Client modern, interfață clară (freemium) | [→ Descarcă](https://tableplus.com/) |

---

## 🔵 Faza 2 — Validarea datelor și integritatea bazei de date (3–4 săptămâni)

> Testarea bazei de date înseamnă mai mult decât „datele există" — verifici că sunt corecte, complete, consistente și respectă regulile de business.

| Resursă | Durată | Link |
|---------|--------|------|
| Database Testing Tutorial — Software Testing Help | ~3h | [→ Deschide](https://www.softwaretestinghelp.com/database-testing/) |
| Data Quality Testing — Guru99 | ~2h | [→ Deschide](https://www.guru99.com/database-testing.html) |
| SQL Constraints — W3Schools | ~2h | [→ Deschide](https://www.w3schools.com/sql/sql_constraints.asp) |

**Categorii de validare a datelor:**

**1. Validare de tip (Type Validation):**
```sql
-- Verifici că valorile respectă tipul coloanei
-- Ex: câmpul phone conține doar cifre și caractere valide
SELECT id, phone
FROM users
WHERE phone !~ '^[+]?[0-9\s\-\(\)]+$'   -- PostgreSQL regex
  AND phone IS NOT NULL;

-- Verifici că datele sunt în intervalul așteptat
SELECT id, age
FROM users
WHERE age < 0 OR age > 150;

-- Verifici că email-urile au format valid
SELECT id, email
FROM users
WHERE email NOT LIKE '%@%.%';
```

**2. Validare de completitudine (Completeness):**
```sql
-- Verifici câmpuri obligatorii care nu ar trebui să fie NULL
SELECT COUNT(*) as missing_required_fields
FROM orders
WHERE user_id IS NULL
   OR total_amount IS NULL
   OR status IS NULL;

-- Verifici că toate produsele dintr-o comandă au prețul setat
SELECT o.id as order_id, oi.product_id
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
WHERE oi.unit_price IS NULL OR oi.unit_price <= 0;
```

**3. Validare de consistență (Consistency):**
```sql
-- Verifici că totalul comenzii corespunde cu suma produselor
SELECT o.id,
       o.total_amount as stored_total,
       SUM(oi.quantity * oi.unit_price) as calculated_total,
       o.total_amount - SUM(oi.quantity * oi.unit_price) as discrepancy
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
GROUP BY o.id, o.total_amount
HAVING ABS(o.total_amount - SUM(oi.quantity * oi.unit_price)) > 0.01;

-- Verifici că datele sunt consistente între tabele
-- (stocul din products_inventory corespunde cu comenzile procesate)
SELECT p.id,
       p.stock_quantity as reported_stock,
       p.initial_stock - COALESCE(SUM(oi.quantity), 0) as calculated_stock
FROM products p
LEFT JOIN order_items oi ON p.id = oi.product_id
LEFT JOIN orders o ON oi.order_id = o.id AND o.status = 'completed'
GROUP BY p.id, p.stock_quantity, p.initial_stock
HAVING p.stock_quantity != p.initial_stock - COALESCE(SUM(oi.quantity), 0);
```

**4. Validare constrângeri (Constraints):**
```sql
-- Verifici că cheile externe există (fără a depinde de FK enforcement)
SELECT oi.order_id, oi.product_id
FROM order_items oi
WHERE NOT EXISTS (
    SELECT 1 FROM products p WHERE p.id = oi.product_id
);

-- Verifici unicitatea acolo unde e așteptată
SELECT email, COUNT(*) as duplicates
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

**Checklist de testare a bazei de date:**
```
□ Datele inserate prin UI există în DB cu valorile corecte
□ Datele șterse prin UI nu mai există în DB (sau sunt marcate corect)
□ Relațiile dintre tabele sunt respectate (FK-uri)
□ Câmpurile obligatorii nu pot fi NULL
□ Valorile unice chiar sunt unice
□ Calculele stocate corespund cu calculele din date individuale
□ Timestampurile sunt setate corect (created_at, updated_at)
□ Valorile enum/status sunt din setul permis
□ Datele sensibile sunt stocate corespunzător (parole hash-uite, nu plain text)
```

---

## 🟡 Faza 3 — Tehnici avansate de interogare (2–3 săptămâni)

> Interogările complexe îți permit să găsești bug-uri subtile de business logic care nu sunt vizibile din UI.

| Resursă | Durată | Link |
|---------|--------|------|
| Advanced SQL — Mode Analytics | ~4h | [→ Deschide](https://mode.com/sql-tutorial/sql-window-functions/) |
| Window Functions — PostgreSQL Tutorial | ~3h | [→ Deschide](https://www.postgresqltutorial.com/postgresql-window-function/) |
| CTEs and Subqueries — SQLZoo | ~2h | [→ Deschide](https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial) |

**Window Functions — analize pe seturi de date:**
```sql
-- Găsești prima comandă a fiecărui utilizator
SELECT user_id, id as order_id, created_at,
       ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY created_at) as order_rank
FROM orders
WHERE order_rank = 1;   -- sau folosești CTE

-- Calculezi valoarea cumulată a comenzilor per utilizator
SELECT user_id, id, total_amount,
       SUM(total_amount) OVER (
           PARTITION BY user_id
           ORDER BY created_at
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) as cumulative_spending
FROM orders
ORDER BY user_id, created_at;

-- Compari valoarea unei comenzi cu media utilizatorului
SELECT user_id, id, total_amount,
       AVG(total_amount) OVER (PARTITION BY user_id) as user_avg,
       total_amount - AVG(total_amount) OVER (PARTITION BY user_id) as diff_from_avg
FROM orders;
```

**CTE (Common Table Expressions) — interogări lizibile:**
```sql
-- Identifici utilizatorii care au plasat mai multe comenzi în aceeași zi
-- (posibil bug de dublare)
WITH daily_orders AS (
    SELECT user_id,
           DATE(created_at) as order_date,
           COUNT(*) as orders_count,
           SUM(total_amount) as daily_total
    FROM orders
    WHERE status != 'cancelled'
    GROUP BY user_id, DATE(created_at)
),
suspicious_activity AS (
    SELECT * FROM daily_orders
    WHERE orders_count > 3  -- mai mult de 3 comenzi/zi e neobișnuit
)
SELECT u.email, s.order_date, s.orders_count, s.daily_total
FROM suspicious_activity s
JOIN users u ON s.user_id = u.id
ORDER BY s.orders_count DESC;
```

**Scenarii de business logic pe care le testezi cu SQL:**
```sql
-- Verifici că reducerile sunt aplicate corect
SELECT o.id, o.discount_code, o.discount_amount,
       dc.discount_percentage,
       o.subtotal * dc.discount_percentage / 100 as expected_discount,
       o.discount_amount - (o.subtotal * dc.discount_percentage / 100) as discrepancy
FROM orders o
JOIN discount_codes dc ON o.discount_code = dc.code
WHERE ABS(o.discount_amount - (o.subtotal * dc.discount_percentage / 100)) > 0.01;

-- Verifici că stocul nu a scăzut sub 0 (bug de concurență)
SELECT id, name, stock_quantity
FROM products
WHERE stock_quantity < 0;

-- Verifici că un utilizator nu poate plasa o comandă dacă contul e suspendat
SELECT o.id, o.user_id, u.status as user_status
FROM orders o
JOIN users u ON o.user_id = u.id
WHERE u.status = 'suspended'
  AND o.created_at > u.suspended_at;
```

---

## 🟣 Faza 4 — Testare baze de date în automatizare (2–3 săptămâni)

> SQL integrat în testele automate elimină dependența de UI pentru verificarea datelor — testele sunt mai rapide și mai fiabile.

| Resursă | Durată | Link |
|---------|--------|------|
| Database Testing with Python — RealPython | ~3h | [→ Deschide](https://realpython.com/python-sql-libraries/) |
| pytest-postgresql — Docs | ~2h | [→ Deschide](https://pytest-postgresql.readthedocs.io/) |
| SQLAlchemy pentru teste — Docs | ~3h | [→ Deschide](https://docs.sqlalchemy.org/en/20/orm/session_basics.html) |

**Verificare date în teste Pytest:**
```python
import psycopg2
import pytest

@pytest.fixture(scope="session")
def db_connection():
    conn = psycopg2.connect(
        host="localhost", database="testdb",
        user="test", password="test"
    )
    yield conn
    conn.close()

def test_user_created_correctly(api_client, db_connection):
    # Acțiune: creezi utilizatorul prin API
    response = api_client.post("/api/users", json={
        "email": "test@example.com",
        "first_name": "Ion",
        "last_name": "Pop"
    })
    assert response.status_code == 201
    user_id = response.json()["id"]

    # Verificare: datele din DB corespund cu ce ai trimis
    cursor = db_connection.cursor()
    cursor.execute(
        "SELECT email, first_name, last_name, status FROM users WHERE id = %s",
        (user_id,)
    )
    user = cursor.fetchone()

    assert user[0] == "test@example.com"
    assert user[1] == "Ion"
    assert user[2] == "Pop"
    assert user[3] == "active"   # status implicit corect
```

**Izolarea testelor cu tranzacții — fiecare test rulează în sandbox:**
```python
@pytest.fixture
def db_session(db_connection):
    """Fiecare test rulează într-o tranzacție care e anulată la final."""
    db_connection.begin()
    yield db_connection
    db_connection.rollback()   # anulezi modificările — nu afectează alte teste

def test_order_total_calculated_correctly(api_client, db_session):
    # Testul modifică DB, dar rollback-ul curăță automat
    ...
```

**Populare date de test direct în DB:**
```python
def create_test_order(db_session, user_id: int, products: list) -> int:
    """Creezi o comandă direct în DB — mai rapid decât prin UI."""
    cursor = db_session.cursor()
    cursor.execute(
        "INSERT INTO orders (user_id, status, total_amount) VALUES (%s, 'pending', 0) RETURNING id",
        (user_id,)
    )
    order_id = cursor.fetchone()[0]

    total = 0
    for product_id, quantity, price in products:
        cursor.execute(
            "INSERT INTO order_items (order_id, product_id, quantity, unit_price) VALUES (%s, %s, %s, %s)",
            (order_id, product_id, quantity, price)
        )
        total += quantity * price

    cursor.execute("UPDATE orders SET total_amount = %s WHERE id = %s", (total, order_id))
    return order_id
```

---

## 🔴 Faza 5 — Performanța interogărilor (1–2 săptămâni)

> Un QA care înțelege performanța SQL poate identifica bug-uri de performanță în baza de date înainte ca utilizatorii să le simtă.

| Resursă | Durată | Link |
|---------|--------|------|
| EXPLAIN ANALYZE — PostgreSQL Tutorial | ~2h | [→ Deschide](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-explain/) |
| SQL Performance Explained — Use The Index, Luke | ~4h | [→ Deschide](https://use-the-index-luke.com/) |

**EXPLAIN ANALYZE — cum citești planul de execuție:**
```sql
EXPLAIN ANALYZE
SELECT u.email, COUNT(o.id) as order_count
FROM users u
JOIN orders o ON u.id = o.user_id
WHERE o.created_at >= '2025-01-01'
GROUP BY u.email
ORDER BY order_count DESC;

-- Output important:
-- Seq Scan → scanare completă a tabelei (lentă pe date mari)
-- Index Scan → folosește index (rapid)
-- actual time → timpul real de execuție
-- rows → câte rânduri a procesat
```

**Semnale de alarmă în performanța SQL:**
```
Seq Scan pe tabele mari → lipsesc index-uri relevante
Nested Loop cu multe iterații → JOIN-uri ineficiente
actual rows >> estimated rows → statistici BD depășite, rulezi ANALYZE
Execution time > 1s pentru interogări de UI → problemă de performanță
```

**Ce testezi legat de performanță în baza de date:**
```sql
-- Verifici că interogările critice folosesc index-uri
EXPLAIN SELECT * FROM orders WHERE user_id = 123;
-- Trebuie să vedem "Index Scan" nu "Seq Scan"

-- Verifici că nu există interogări N+1 (semnalate în logurile aplicației)
-- O interogare separată pentru fiecare utilizator în loc de un JOIN

-- Verifici comportamentul la volum de date realist
-- Nu testezi cu 10 rânduri când producția are 10 milioane
```

---

## 💡 Sfaturi practice

### Cele mai frecvente bug-uri găsite cu SQL

- **Date duplicate** — înregistrări create de două ori din cauza request-urilor duble
- **Stoc negativ** — bug de concurență la comenzi simultane
- **Totaluri incorecte** — calcule greșite stocate vs calculate la runtime
- **Date orfane** — înregistrări referite de altele care au fost șterse
- **Timestamp-uri greșite** — timezone incorect, created_at în viitor
- **Parole plain text** — datele sensibile nu sunt hash-uite corect
- **Câmpuri NULL acolo unde nu ar trebui** — validare server lipsă

### Cum obții acces la baza de date de test

- **Mediu local** — rulezi aplicația local cu o bază de date locală
- **Mediu de test dedicat** — acces read-only la baza de date de test (cere developerilor)
- **Nu ai acces direct** — ceri developerilor să îți creeze un utilizator read-only pe mediul de test

> ⚠️ **Reguli de bază:** Nu rulezi niciodată `UPDATE`, `DELETE` sau `INSERT` pe baza de date de producție fără aprobare explicită. Pe mediul de test, rulezi cu grijă — mai ales `DELETE` și `UPDATE` fără `WHERE`.

### Interogări utile de bookmarked

```sql
-- Ultimele N înregistrări create
SELECT * FROM table_name ORDER BY created_at DESC LIMIT 10;

-- Înregistrările modificate în ultima oră
SELECT * FROM table_name WHERE updated_at >= NOW() - INTERVAL '1 hour';

-- Structura unui tabel (PostgreSQL)
SELECT column_name, data_type, is_nullable, column_default
FROM information_schema.columns
WHERE table_name = 'orders'
ORDER BY ordinal_position;

-- Dimensiunea tabelelor
SELECT relname as table_name,
       pg_size_pretty(pg_total_relation_size(relid)) as total_size
FROM pg_catalog.pg_statio_user_tables
ORDER BY pg_total_relation_size(relid) DESC;
```

---

## 🛠 Stack tehnologic

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| Client universal BD | DBeaver Community | Gratuit |
| Client PostgreSQL | pgAdmin | Gratuit |
| Client MySQL | MySQL Workbench | Gratuit |
| Baza de date locală | PostgreSQL / MySQL / SQLite | Gratuit |
| Practică interactivă | SQLZoo, Mode Analytics | Gratuit |
| Python + PostgreSQL | psycopg2, SQLAlchemy | Gratuit |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 2–3 luni (part-time) |
| **Nivel de start** | Cunoștințe de bază în testare — nu e necesar background tehnic |
| **Nivel de final** | QA Engineer cu competențe solide de SQL și testare baze de date |
| **Cost** | 100% gratuit |
| **Focus** | Validare date, integritate, automatizare, performanță |
| **Valoare imediată** | Poți aplica cunoștințele din Faza 1–2 din prima săptămână de lucru |
| **Pasul următor** | [TypeScript + Playwright ⭐](./cale-invatare-de-la-testare-manuala-la-automatizare-typescript.md) · [Java + Selenium](./cale-invatare-de-la-testare-manuala-la-automatizare-java.md) · [Python + Playwright](./cale-invatare-de-la-testare-manuala-la-automatizare-python.md) |
