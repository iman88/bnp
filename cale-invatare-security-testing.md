# 🔐 Security Testing — Cale de Învățare

> Testare de securitate · OWASP · Burp Suite · API Security · ~3–5 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente de securitate web](#-faza-1--fundamente-de-securitate-web-34-săptămâni)
- [Faza 2 — OWASP Top 10](#-faza-2--owasp-top-10-34-săptămâni)
- [Faza 3 — Unelte de testare manuală](#-faza-3--unelte-de-testare-manuală-46-săptămâni)
- [Faza 4 — Testare securitate API](#-faza-4--testare-securitate-api-34-săptămâni)
- [Faza 5 — Integrare în procesul de dezvoltare](#-faza-5--integrare-în-procesul-de-dezvoltare-23-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente de securitate web (3–4 săptămâni)

> Înainte să găsești vulnerabilități, trebuie să înțelegi cum funcționează web-ul și unde apar problemele de securitate.

| Resursă | Durată | Link |
|---------|--------|------|
| Web Security Academy — PortSwigger | referință completă | [→ Deschide](https://portswigger.net/web-security) |
| CS50's Introduction to Cybersecurity — Harvard | ~10h | [→ Deschide](https://cs50.harvard.edu/cybersecurity/) |
| HTTP în detaliu — TryHackMe | ~2h | [→ Deschide](https://tryhackme.com/room/howwebsiteswork) |

**Ce vei învăța:**
- Cum funcționează HTTP/HTTPS: cereri, răspunsuri, headere, cookie-uri, sesiuni
- Autentificare vs autorizare — diferența fundamentală în securitate
- Same-Origin Policy și CORS — de ce browserul blochează anumite cereri
- Certificate SSL/TLS — ce protejează și ce nu protejează
- Cum funcționează sesiunile și token-urile JWT
- Concepte de bază: vulnerabilitate, exploit, vector de atac, suprafață de atac

> ⚠️ **Cadru legal important:** Testarea de securitate se face **exclusiv pe sisteme pentru care ai autorizare explicită** — propriile aplicații, medii de test dedicate sau platforme de tip CTF (Capture The Flag). Testarea neautorizată e ilegală indiferent de intenție.

---

## 🔵 Faza 2 — OWASP Top 10 (3–4 săptămâni)

> Lista OWASP Top 10 e standardul global pentru cele mai critice vulnerabilități web. Orice tester de securitate trebuie să o cunoască complet.

| Resursă | Durată | Link |
|---------|--------|------|
| OWASP Top 10 — Documentație oficială | referință | [→ Deschide](https://owasp.org/www-project-top-ten/) |
| OWASP Top 10 — TryHackMe (practic) | ~8h | [→ Deschide](https://tryhackme.com/room/owasptop10) |
| WebGoat — Aplicație vulnerabilă pentru practică | self-hosted | [→ Deschide](https://owasp.org/www-project-webgoat/) |
| DVWA (Damn Vulnerable Web App) | self-hosted | [→ Deschide](https://github.com/digininja/DVWA) |

**OWASP Top 10 — 2021:**

| # | Vulnerabilitate | Ce înseamnă |
|---|----------------|-------------|
| A01 | Broken Access Control | Utilizatorul accesează resurse la care nu ar trebui să aibă acces |
| A02 | Cryptographic Failures | Date sensibile neprotejate sau criptate slab |
| A03 | Injection (SQL, XSS, etc.) | Date nevalidate executate ca și cod |
| A04 | Insecure Design | Arhitectură cu probleme de securitate din faza de design |
| A05 | Security Misconfiguration | Configurări implicite nesigure, permisiuni excesive |
| A06 | Vulnerable Components | Biblioteci și dependențe cu vulnerabilități cunoscute |
| A07 | Auth Failures | Autentificare și gestionare sesiuni defectuoasă |
| A08 | Integrity Failures | Cod și date fără verificare de integritate |
| A09 | Logging Failures | Lipsa jurnalizării evenimentelor de securitate |
| A10 | SSRF | Serverul face cereri către resurse interne nepermise |

**Practică recomandată:** Instalează DVWA local și reproduce fiecare vulnerabilitate din OWASP Top 10 în mediu controlat. Înțelegi cum funcționează atacul înainte să înveți cum să îl detectezi.

---

## 🟡 Faza 3 — Unelte de testare manuală (4–6 săptămâni)

> Burp Suite e unealta standard a industriei pentru testare de securitate web. Versiunea Community e gratuită și suficientă pentru început.

| Unealtă | Scop | Cost | Link |
|---------|------|------|------|
| Burp Suite Community | Proxy + interceptare trafic + scanner | Gratuit | [→ Deschide](https://portswigger.net/burp/communitydownload) |
| OWASP ZAP | Alternativă open-source la Burp | Gratuit | [→ Deschide](https://www.zaproxy.org/) |
| TryHackMe | Mediu de practică ghidată | Freemium | [→ Deschide](https://tryhackme.com/) |
| HackTheBox | Practică avansată CTF | Freemium | [→ Deschide](https://www.hackthebox.com/) |

**Burp Suite — concepte esențiale:**

**Proxy — interceptezi traficul dintre browser și server:**
```
Browser → Burp Proxy (localhost:8080) → Server
```
- Modifici cereri înainte să ajungă la server
- Observi răspunsuri complete, inclusiv headere și cookie-uri
- Repeater — retrimiți aceeași cerere cu modificări

**Vulnerabilități pe care le testezi manual cu Burp:**

*SQL Injection:*
```
# Câmp normal
username=admin&password=secret

# Test SQLi
username=admin'--&password=anything
username=' OR '1'='1
```

*XSS (Cross-Site Scripting):*
```html
# Input de testat în câmpuri de text, URL-uri, headere
<script>alert('XSS')</script>
"><script>alert(1)</script>
javascript:alert(1)
```

*IDOR (Insecure Direct Object Reference):*
```
# Dacă URL-ul tău e:
/api/users/1234/orders

# Testezi:
/api/users/1235/orders  → poți vedea comenzile altui utilizator?
```

*Broken Authentication:*
- Parole slabe acceptate fără restricții
- Lipsă limitare încercări de autentificare (brute force posibil)
- Token-uri predictibile sau neinvalidate la deconectare
- Cookie-uri fără flag-urile `Secure` și `HttpOnly`

**OWASP ZAP — pentru scanare automată de bază:**
- Spider — descoperă automat toate paginile aplicației
- Active Scan — testează automat vulnerabilități comune
- Util pentru rapoarte rapide, mai puțin precis decât testarea manuală

---

## 🟣 Faza 4 — Testare securitate API (3–4 săptămâni)

> API-urile sunt ținta principală în aplicațiile moderne — adesea expun mai multă logică de business decât interfața grafică.

| Resursă | Durată | Link |
|---------|--------|------|
| API Security — OWASP API Top 10 | referință | [→ Deschide](https://owasp.org/www-project-api-security/) |
| Testare API cu Postman + securitate | ~3h | [→ Deschide](https://academy.postman.com/) |
| crAPI — API vulnerabil pentru practică | self-hosted | [→ Deschide](https://github.com/OWASP/crAPI) |

**OWASP API Top 10 — cele mai frecvente probleme:**

| Vulnerabilitate | Exemplu concret |
|----------------|-----------------|
| Broken Object Level Auth | `GET /api/orders/5678` returnează comenzile altui utilizator |
| Broken Auth | Token-uri JWT acceptate după expirare sau deconectare |
| Excessive Data Exposure | API returnează toate câmpurile din baza de date, nu doar cele necesare |
| Rate Limiting absent | Poți face 10.000 de cereri pe secundă fără blocare |
| Mass Assignment | `POST /users` acceptă câmpul `"role": "admin"` din cerere |

**Ce testezi la fiecare endpoint API:**
```
□ Autentificarea e necesară? (încearcă fără token)
□ Autorizarea e corectă? (încearcă cu token de utilizator simplu pentru resurse admin)
□ Ce date returnează? (mai mult decât e necesar?)
□ Există limitare a numărului de cereri?
□ Inputul e validat? (trimite valori neașteptate: null, string în loc de int, array imens)
□ Headerele de securitate sunt prezente? (Content-Security-Policy, X-Frame-Options, etc.)
```

**Proiect practic:** Instalează crAPI local și identifică toate vulnerabilitățile din OWASP API Top 10. Documentează fiecare cu: descriere, pași de reproducere, impact și recomandare de remediere.

---

## 🔴 Faza 5 — Integrare în procesul de dezvoltare (2–3 săptămâni)

> Security testing nu e un eveniment izolat — e o activitate continuă integrată în ciclul de dezvoltare.

**SAST vs DAST vs IAST:**

| Tip | Ce face | Când rulează |
|-----|---------|-------------|
| SAST (Static) | Analizează codul sursă fără să ruleze aplicația | În CI/CD, la fiecare commit |
| DAST (Dynamic) | Testează aplicația rulând, din exterior | Pe mediu de test, înainte de release |
| IAST (Interactive) | Combină ambele, monitorizează din interior | În timpul testelor funcționale |

**Unelte SAST gratuite:**
| Unealtă | Limbaj | Link |
|---------|--------|------|
| Semgrep | Multi-limbaj | [→ Deschide](https://semgrep.dev/) |
| Bandit | Python | [→ Deschide](https://bandit.readthedocs.io/) |
| SpotBugs + FindSecBugs | Java | [→ Deschide](https://find-sec-bugs.github.io/) |

**OWASP ZAP în CI/CD:**
```yaml
# GitHub Actions — scanare DAST automată
- name: ZAP Baseline Scan
  uses: zaproxy/action-baseline@v0.10.0
  with:
    target: 'https://staging.example.com'
    rules_file_name: '.zap/rules.tsv'
    cmd_options: '-a'
```

**Ce include un raport de securitate profesionist:**
```
1. Rezumat executiv — riscul general, număr vulnerabilități pe severitate
2. Metodologie — ce s-a testat, ce unelte, ce perioadă
3. Constatări — pentru fiecare vulnerabilitate:
   - Titlu și clasificare (OWASP, CVE dacă există)
   - Severitate: Critică / Înaltă / Medie / Scăzută / Informațională
   - Descriere tehnică
   - Pași de reproducere
   - Impact
   - Recomandare de remediere
4. Concluzii și pași următori
```

**Clasificarea severității (CVSS):**
| Severitate | Scor CVSS | Exemple |
|-----------|----------|---------|
| Critică | 9.0–10.0 | SQL Injection cu acces la date sensibile |
| Înaltă | 7.0–8.9 | Autentificare ocolită |
| Medie | 4.0–6.9 | XSS stocat |
| Scăzută | 0.1–3.9 | Headere de securitate lipsă |
| Informațională | 0 | Versiuni software expuse |

---

## 💡 Sfaturi practice

### Mindset-ul unui tester de securitate

Security testing e diferit de testarea funcțională — gândești ca un atacator, nu ca un utilizator. Întrebarea nu e „funcționează corect?" ci „cum aș putea abuza de asta?"

Întrebări utile în fața oricărei funcționalități:
- Ce se întâmplă dacă trimit date pe care aplicația nu le așteaptă?
- Pot accesa resursele altui utilizator?
- Există operațiuni care ar trebui să necesite autentificare dar nu o cer?
- Ce informații sensibile sunt expuse în răspunsuri, headere sau mesaje de eroare?

### Certificări relevante

| Certificare | Nivel | Cost aproximativ |
|------------|-------|-----------------|
| CompTIA Security+ | Fundamente | ~350 USD |
| eWPT (eLearnSecurity) | Web App Penetration Testing | ~200 USD |
| OSCP (Offensive Security) | Avansat, recunoscut în industrie | ~1.499 USD |

> Spre deosebire de ISTQB, certificările de securitate sunt mai apreciate pe piață — mai ales OSCP, care implică un examen practic de 24 de ore. Nu sunt obligatorii pentru un rol de QA cu componență de securitate, dar fac diferența pentru roluri dedicate de penetration testing.

### Comunități și resurse continue

- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — cel mai bun curs gratuit de securitate web
- [TryHackMe](https://tryhackme.com/) — practică ghidată, ideal pentru început
- [HackTheBox](https://www.hackthebox.com/) — provocări mai avansate
- [OWASP](https://owasp.org/) — resurse, ghiduri și proiecte open-source de referință

---

## 🛠 Stack tehnologic

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| Proxy / Interceptare | Burp Suite Community | Gratuit |
| Scanner automat | OWASP ZAP | Gratuit |
| Practică web | DVWA, WebGoat, crAPI | Gratuit |
| Platforme CTF | TryHackMe, HackTheBox | Freemium |
| SAST | Semgrep, Bandit, SpotBugs | Gratuit |
| Documentare | OWASP Testing Guide | Gratuit |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 3–5 luni (part-time) |
| **Nivel de start** | Cunoștințe de bază în testare web și HTTP |
| **Nivel de final** | QA cu competențe de securitate / Junior Security Tester |
| **Cost** | 100% gratuit |
| **Focus** | Vulnerabilități web, API security, integrare în CI/CD |
| **Avertisment** | Testează exclusiv pe sisteme autorizate |
| **Pasul următor** | [SDET](./cale-invatare-sdet.md) · [QA Tech Lead](./cale-invatare-qa-tech-lead.md) |
