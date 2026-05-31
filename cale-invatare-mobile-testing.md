# 📱 Mobile Testing — Cale de Învățare

> Testare Android & iOS · Appium · Testare în cloud · ~4–5 luni part-time

---

## 📋 Cuprins

- [Faza 1 — Fundamente mobile](#-faza-1--fundamente-mobile-23-săptămâni)
- [Faza 2 — Testare manuală pe dispozitive mobile](#-faza-2--testare-manuală-pe-dispozitive-mobile-34-săptămâni)
- [Faza 3 — Automatizare cu Appium](#-faza-3--automatizare-cu-appium-56-săptămâni)
- [Faza 4 — Testare în cloud și pe dispozitive reale](#-faza-4--testare-în-cloud-și-pe-dispozitive-reale-23-săptămâni)
- [Faza 5 — CI/CD pentru mobile](#-faza-5--cicd-pentru-mobile-12-săptămâni)
- [Sfaturi practice](#-sfaturi-practice)
- [Stack tehnologic](#-stack-tehnologic)

---

## 🟢 Faza 1 — Fundamente mobile (2–3 săptămâni)

> Testarea mobilă e fundamental diferită față de testarea web. Înainte să atingi un emulator, înțelege ecosistemul.

| Resursă | Durată | Link |
|---------|--------|------|
| Mobile Testing Tutorial — Guru99 | ~4h | [→ Deschide](https://www.guru99.com/mobile-testing.html) |
| Android Basics — Google (developer.android.com) | ~3h | [→ Deschide](https://developer.android.com/guide) |
| iOS App Architecture — Apple Developer | ~2h | [→ Deschide](https://developer.apple.com/documentation) |
| Mobile Testing Fundamentals — TAU | ~3h | [→ Deschide](https://testautomationu.applitools.com/mobile-testing-with-appium/) |

**Android vs iOS — diferențele care contează pentru testare:**

| Aspect | Android | iOS |
|--------|---------|-----|
| Fragmentare | Sute de dispozitive, versiuni diferite de OS | Ecosistem controlat, mai puține versiuni active |
| Instalare aplicație | APK, sideloading posibil | IPA, necesită device înregistrat sau distribuție enterprise |
| Permisiuni | Granulare, acordate la runtime | Granulare, acordate la prima utilizare |
| Notificări | Sistem propriu | Sistem propriu, diferit de Android |
| Back navigation | Buton dedicat (fizic sau virtual) | Gesturi swipe |
| Debugger | ADB (Android Debug Bridge) | Xcode Instruments |

**Tipuri de aplicații mobile — implică abordări de testare diferite:**

| Tip | Descriere | Exemplu | Unealtă de automatizare |
|-----|-----------|---------|------------------------|
| Nativă | Scrisă specific pentru platformă | Aplicația Bancă | Espresso (Android), XCUITest (iOS) |
| Hibridă | Web înfășurat în container nativ | Aplicații vechi | Appium |
| Web mobilă | Site accesat din browser mobil | Orice site responsive | Playwright, Selenium cu mobile config |
| Cross-platform | Cod unic pentru ambele platforme | React Native, Flutter | Appium, Detox (RN), Flutter Driver |

> ⚠️ **Alegerea uneltei de automatizare depinde de tipul aplicației.** Appium nu e întotdeauna cel mai bun răspuns — pentru aplicații native pure, Espresso (Android) și XCUITest (iOS) sunt mai rapide și mai stabile.

**Setup mediu de lucru:**
```
Android:
  → Android Studio (include emulatorul Android și ADB)
  → Java JDK 17+ sau Python 3.12+
  → SDK Platform Tools (adb, fastboot)

iOS (necesită Mac):
  → Xcode (include simulatorul iOS)
  → Xcode Command Line Tools

Fără Mac pentru iOS:
  → BrowserStack / Sauce Labs — dispozitive reale în cloud (freemium)
  → Testare manuală pe simulatoare web (nu înlocuiesc un device real)
```

---

## 🔵 Faza 2 — Testare manuală pe dispozitive mobile (3–4 săptămâni)

> Automatizarea mobilă e complexă și costisitoare. Testarea manuală acoperă scenarii pe care automatizarea nu le poate reproduce — și înțelegerea lor e prerequisit pentru automatizare.

| Resursă | Durată | Link |
|---------|--------|------|
| Mobile Testing Checklist — Software Testing Help | ~2h | [→ Deschide](https://www.softwaretestinghelp.com/mobile-application-testing/) |
| Accessibility Testing Mobile — WebAIM | ~2h | [→ Deschide](https://webaim.org/articles/mobile/) |
| Beta Testing cu Firebase App Distribution | ~1h | [→ Deschide](https://firebase.google.com/docs/app-distribution) |

**Categorii de testare specifice mobile:**

**Testare funcțională de bază:**
- Instalare, actualizare, dezinstalare — pe versiuni diferite de OS
- Lansare din diferite stări: cold start, warm start, revenire din background
- Navigare cu gesturi: swipe, pinch, tap, double tap, long press
- Orientare: portrait ↔ landscape (se păstrează starea?)

**Testare întreruperi — scenarii uitate frecvent:**
```
□ Apel telefonic primit în timpul utilizării aplicației
□ SMS primit
□ Notificare push din altă aplicație
□ Alarmă declanșată
□ Baterie scăzută / modul economisire energie activat
□ Conexiune pierdută în mijlocul unei operațiuni
□ Comutare între WiFi și date mobile
□ Mod avion activat și dezactivat
□ Ecran blocat și deblocat în mijlocul unui flux
```

**Testare permisiuni:**
```
□ Aplicația cere permisiunea la momentul potrivit, nu la pornire
□ Funcționează corect dacă permisiunea e refuzată
□ Funcționează corect dacă permisiunea e retrasă din setări ulterior
□ Nu cere permisiuni inutile (cameră, locație, contacte)
```

**Testare condiții de rețea:**
```
□ Offline — aplicația afișează mesaj clar, nu crash
□ 2G / rețea slabă — timeout-uri gestionate corect
□ Comutare între rețele în timpul unei operațiuni
□ Proxy / VPN activ
```

**Testare specifică Android:**
- Butonul Back — comportament corect în fiecare ecran
- Recent Apps — revenire corectă după switch între aplicații
- Split screen — aplicația funcționează în mod ecran împărțit?
- Permisiuni granulare Android 12+ (locație aproximativă vs exactă)

**Testare specifică iOS:**
- Gesturi de sistem (swipe din colțuri) nu interferează cu gesturi din aplicație
- Face ID / Touch ID — integrare corectă
- Dynamic Type — textul se scalează corect la mărirea fontului din setări
- Dark Mode — aspectul e corect în ambele moduri

---

## 🟡 Faza 3 — Automatizare cu Appium (5–6 săptămâni)

> Appium e alegerea principală pentru aplicații hibride și cross-platform. Pentru native pure, Espresso și XCUITest sunt superioare — dar Appium rămâne cel mai portabil.

| Resursă | Durată | Link |
|---------|--------|------|
| Appium Documentation — oficială | referință | [→ Deschide](https://appium.io/docs/en/latest/) |
| Mobile Testing with Appium — TAU | ~5h | [→ Deschide](https://testautomationu.applitools.com/mobile-testing-with-appium/) |
| Appium Inspector — GitHub | unealtă | [→ Deschide](https://github.com/appium/appium-inspector) |
| WebdriverIO + Appium — Docs | referință | [→ Deschide](https://webdriver.io/docs/appium/) |

**Instalare Appium:**
```bash
npm install -g appium
appium driver install uiautomator2   # Android
appium driver install xcuitest       # iOS (necesită Mac)
appium --version                     # verifici instalarea
```

**Appium Inspector — identifici elementele înainte să scrii cod:**

Appium Inspector e echivalentul DevTools din browser — te conectezi la o sesiune Appium și poți inspecta vizual elementele din aplicație, găsind locatorii potriviți.

**Strategii de localizare elemente în Appium:**

```python
# Android — în ordinea preferinței
driver.find_element(AppiumBy.ACCESSIBILITY_ID, "login_button")     # cel mai stabil
driver.find_element(AppiumBy.ID, "com.example.app:id/btn_login")   # resource-id
driver.find_element(AppiumBy.XPATH, "//android.widget.Button[@text='Login']")  # fallback

# iOS
driver.find_element(AppiumBy.ACCESSIBILITY_ID, "Login")
driver.find_element(AppiumBy.IOS_PREDICATE, "type == 'XCUIElementTypeButton' AND label == 'Login'")
```

**Primul test Appium — Python:**
```python
from appium import webdriver
from appium.options import UiAutomator2Options
from appium.webdriver.common.appiumby import AppiumBy

options = UiAutomator2Options()
options.platform_name = "Android"
options.device_name = "emulator-5554"
options.app = "/path/to/app.apk"
options.no_reset = True

driver = webdriver.Remote("http://127.0.0.1:4723", options=options)

# Interacțiune
driver.find_element(AppiumBy.ACCESSIBILITY_ID, "username").send_keys("user@test.com")
driver.find_element(AppiumBy.ACCESSIBILITY_ID, "password").send_keys("secret")
driver.find_element(AppiumBy.ACCESSIBILITY_ID, "login_button").click()

# Verificare
assert "Dashboard" in driver.find_element(AppiumBy.ID, "screen_title").text

driver.quit()
```

**Gesturi cu Appium:**
```python
from appium.webdriver.common.touch_action import TouchAction
from selenium.webdriver.common.action_chains import ActionChains

# Swipe
driver.swipe(start_x=500, start_y=1500, end_x=500, end_y=500, duration=800)

# Tap pe coordonate
TouchAction(driver).tap(x=300, y=600).perform()

# Scroll până la element
driver.execute_script("mobile: scroll", {"direction": "down", "element": element.id})
```

**Alternativele native — când le folosești:**

```
Espresso (Android nativ):
  + Rulează în același proces cu aplicația — mai rapid, mai stabil
  + Integrat în Android Studio
  - Funcționează doar pentru aplicații Android native
  → Folosit de echipele dev pentru unit/integration tests UI

XCUITest (iOS nativ):
  + Cel mai rapid și stabil pentru iOS
  + Integrat în Xcode
  - Necesită Mac, funcționează doar iOS
  → Folosit de echipele dev pentru UI testing pe iOS

Detox (React Native):
  + Proiectat special pentru React Native — gestionează asincronism
  + Mai stabil decât Appium pentru RN
  → Alegerea principală pentru proiecte React Native
```

---

## 🟣 Faza 4 — Testare în cloud și pe dispozitive reale (2–3 săptămâni)

> Emulatoarele nu reproduc toate comportamentele unui dispozitiv real. Platforma de cloud rezolvă problema fără să cumperi 50 de telefoane.

| Resursă | Durată | Link |
|---------|--------|------|
| BrowserStack App Automate Documentation | ~2h | [→ Deschide](https://www.browserstack.com/docs/app-automate) |
| Firebase Test Lab — Getting Started | ~1h | [→ Deschide](https://firebase.google.com/docs/test-lab/android/get-started) |
| Real Device Testing Guide — Sauce Labs | ~2h | [→ Deschide](https://docs.saucelabs.com/mobile-apps/supported-devices/) |
| Testing on Real Devices vs Emulators — BrowserStack Blog | ~1h | [→ Deschide](https://www.browserstack.com/guide/real-device-vs-emulator-simulator) |

| Platformă | Ce oferă | Tier gratuit | Link |
|-----------|---------|-------------|------|
| BrowserStack | Dispozitive reale Android + iOS, Appium, testare manuală | Trial | [→ Deschide](https://www.browserstack.com/) |
| Sauce Labs | Dispozitive reale + emulatoare, CI/CD integrat | Trial | [→ Deschide](https://saucelabs.com/) |
| Firebase Test Lab | Dispozitive reale Google, Espresso + Robo test | Gratuit (limitat) | [→ Deschide](https://firebase.google.com/docs/test-lab) |
| LambdaTest | Dispozitive reale + emulatoare | Freemium | [→ Deschide](https://www.lambdatest.com/) |

**BrowserStack — configurare Appium în cloud:**
```python
options = UiAutomator2Options()
options.platform_name = "Android"
options.platform_version = "13.0"
options.device_name = "Samsung Galaxy S23"
options.app = "bs://app_id_din_browserstack"
options.set_capability("bstack:options", {
    "userName": "your_username",
    "accessKey": "your_access_key",
    "projectName": "Mobile Tests",
    "buildName": "Sprint 42",
})

driver = webdriver.Remote(
    "https://hub-cloud.browserstack.com/wd/hub",
    options=options
)
```

**Firebase Test Lab — Robo Test:**

Robo Test e un crawler automat — fără să scrii un singur test, Firebase explorează aplicația, apasă butoane, completează formulare și raportează crash-uri și probleme. Util pentru smoke testing rapid pe aplicații noi.

**Ce testezi obligatoriu pe dispozitive reale (nu emulator):**
- Performanța reală — emulatoarele nu reproduc corect CPU/memorie
- Gesturi complexe — touch-ul real diferă de simulare
- Permisiuni hardware — cameră, GPS, senzori
- Notificări push
- Comportamentul la baterie scăzută
- Conectivitate reală (4G/5G vs WiFi)

---

## 🔴 Faza 5 — CI/CD pentru mobile (1–2 săptămâni)

> Testele mobile integrate în CI/CD rulează la fiecare modificare de cod — prinzi regresiile înainte ca cineva să le vadă în producție.

| Resursă | Durată | Link |
|---------|--------|------|
| Fastlane — automatizare build și distribuție | ~3h | [→ Deschide](https://fastlane.tools/) |
| GitHub Actions pentru Android | ~2h | [→ Deschide](https://github.com/marketplace/actions/android-emulator-runner) |
| AppCenter — Microsoft | ~2h | [→ Deschide](https://appcenter.ms/) |

**GitHub Actions — rulare teste Appium pe emulator Android:**
```yaml
name: Mobile Tests
on: [push, pull_request]

jobs:
  android-tests:
    runs-on: macos-latest    # macOS pentru emulatoare Android mai rapide
    steps:
      - uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          java-version: '17'

      - name: Start Android Emulator
        uses: reactivecircus/android-emulator-runner@v2
        with:
          api-level: 33
          arch: x86_64
          script: |
            npm install -g appium
            appium driver install uiautomator2
            appium &
            sleep 5
            pytest tests/mobile/ --alluredir=allure-results

      - uses: actions/upload-artifact@v4
        if: always()
        with:
          name: mobile-test-results
          path: allure-results/
```

**Strategia de testare mobilă în CI/CD:**
```
La fiecare commit:
  → Smoke tests pe emulator (5–10 minute) — funcționează de bază?

La fiecare Pull Request:
  → Regresie parțială pe emulator (20–30 minute)

Nightly:
  → Regresie completă pe dispozitive reale în cloud (BrowserStack/Firebase)
  → Teste de performanță
```

---

## 💡 Sfaturi practice

### Cele mai frecvente greșeli în testarea mobilă

- **Testezi doar pe emulatoare** — comportamente specifice hardware nu apar în emulator
- **Ignori fragmentarea Android** — o aplicație care funcționează pe Pixel nu funcționează neapărat pe Samsung cu One UI
- **Nu testezi întreruperile** — apeluri, notificări, comutare rețea sunt scenarii reale frecvente
- **Folosești XPATH în Appium** — e lent și fragil; preferă Accessibility ID sau resource-id
- **Nu curăți starea între teste** — testele mobile lasă date reziduale dacă nu resetezi corect

### Emulator vs dispozitiv real — regula practică

| Folosești emulator pentru | Folosești dispozitiv real pentru |
|--------------------------|----------------------------------|
| Dezvoltare și debugging rapid | Validare finală înainte de lansare |
| Teste de regresie în CI/CD | Testare performanță reală |
| Verificări de bază | Hardware specific (cameră, GPS, senzori) |
| Economie de cost | Comportamente specifice producătorului (Samsung, Huawei, Xiaomi) |

### De ce e greu să automatizezi 100% în mobile

- Emulatoarele sunt lente și instabile în CI/CD
- Dispozitivele reale în cloud sunt scumpe la scară
- Appium are latență mai mare decât Selenium
- Aplicațiile mobile se schimbă frecvent, locatorii se rup

**Recomandare:** Automatizează 20–30% din scenarii (fluxuri critice, regresie de bază) și menține restul ca testare manuală exploratorie. Mobile e domeniul unde raportul cost/beneficiu al automatizării e cel mai greu de justificat.

### Comunități și resurse continue

- [Appium Discord](https://discord.com/invite/appium) — suport oficial Appium
- [Mobile Dev Memo](https://mobiledevmemo.com/) — industria aplicațiilor mobile
- [Android Developers Blog](https://android-developers.googleblog.com/) — noutăți Android

---

## 🛠 Stack tehnologic

| Categorie | Unealtă | Cost |
|-----------|---------|------|
| Automatizare cross-platform | Appium | Gratuit |
| Automatizare Android nativ | Espresso | Gratuit |
| Automatizare iOS nativ | XCUITest | Gratuit (necesită Mac) |
| Automatizare React Native | Detox | Gratuit |
| Inspectare elemente | Appium Inspector | Gratuit |
| Emulator Android | Android Studio | Gratuit |
| Simulator iOS | Xcode | Gratuit (necesită Mac) |
| Cloud dispozitive | BrowserStack / Firebase Test Lab | Freemium |
| CI/CD | GitHub Actions | Gratuit |
| Distribuție beta | Firebase App Distribution | Gratuit |

---

## 📊 Sumar

| | |
|-|-|
| **Durată totală estimată** | 4–5 luni (part-time) |
| **Nivel de start** | Experiență de bază în testare web sau automatizare |
| **Nivel de final** | Mobile QA Engineer |
| **Cost** | Majoritar gratuit (cloud devices au costuri la scară) |
| **Limbaj** | Python sau Java pentru Appium |
| **Focus** | Android + iOS, Appium, testare manuală specifică mobile |
| **Avertisment** | iOS necesită Mac pentru testare nativă și simulatoare |
