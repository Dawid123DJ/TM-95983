# 🏦 RAPORT Z AUDYTU BEZPIECZEŃSTWA: APIDEMOS

**Data:** 18.04.2026  
**Audytor:** Dawid 95983  
**Projekt:** Mobilny System Demonstracyjny (Android)

---

## 📊 1. OCENA KOŃCOWA (SECURITY SCORE)

**Wynik:** 0/100  
**Status:** 🔴 REJECTED – aplikacja nie spełnia minimalnych wymagań bezpieczeństwa

Aplikacja w obecnym stanie **nie może zostać dopuszczona do publikacji**. Wynik 0/100 oznacza, że wykryte problemy mają charakter krytyczny i wymagają natychmiastowej interwencji. Zidentyfikowane błędy wskazują na poważne naruszenia dobrych praktyk bezpieczeństwa oraz brak kontroli nad konfiguracją i zależnościami projektu.

---

## 🛡️ 2. KLUCZOWE OBSZARY RYZYKA

### 🔹 A. Konfiguracja systemowa
**Problem:**  
W pliku manifestu pozostawiono aktywną flagę `debuggable="true"`.

**Wpływ:**  
- umożliwia podłączenie debuggera do działającej aplikacji,  
- pozwala na analizę pamięci i procesów w czasie rzeczywistym,  
- otwiera drogę do przechwycenia danych wrażliwych.

To jeden z najpoważniejszych błędów konfiguracyjnych w aplikacjach Android.

---

### 🔹 B. Wycieki danych
**Problem:**  
W zasobach aplikacji wykryto twardo zakodowane ciągi znaków sugerujące hasła lub dane konfiguracyjne.

**Wpływ:**  
- możliwość odczytu danych przez osoby nieuprawnione,  
- ryzyko ujawnienia danych testowych lub dostępów do usług backendowych,  
- naruszenie podstawowych zasad bezpieczeństwa (hardcoded secrets).

---

### 🔹 C. Biblioteki zewnętrzne
**Problem:**  
W projekcie użyto przestarzałej biblioteki `org.apache.commons` w wersji **1.0.0**, powiązanej z podatnością **CVE‑2015‑7501 (CRITICAL)**.

**Wpływ:**  
- możliwość zdalnego wykonania kodu (RCE),  
- naruszenie integralności aplikacji,  
- wskazuje na brak kontroli nad zależnościami i aktualizacjami.

---

## 📝 3. ZALECENIA NAPRAWCZE (REMEDIATION ROADMAP)

### 🔥 Priorytet 1 – Krytyczne
1. **Zaktualizować bibliotekę `org.apache.commons`** do wersji wolnej od znanych podatności.  
2. **Wyłączyć tryb debugowania** w buildzie produkcyjnym (`debuggable="false"`).  

### ⚠️ Priorytet 2 – Wysokie
3. **Usunąć wszystkie wrażliwe dane** z plików zasobów (`strings.xml`).  
4. **Przenieść sekrety do bezpiecznego magazynu**, np. Android Keystore lub zewnętrznego Secret Managera.

### 📌 Priorytet 3 – Zalecane
5. Wykonać ponowny audyt po wdrożeniu poprawek.  
6. Wprowadzić automatyczne skanowanie zależności (np. OWASP Dependency Check).  
7. Dodać kontrolę bezpieczeństwa do pipeline CI/CD.

---

## 🎓 WNIOSKI KOŃCOWE

Aplikacja **nie spełnia podstawowych standardów bezpieczeństwa**.  
Najpoważniejsze problemy to:

- błędna konfiguracja manifestu (`debuggable="true"`),  
- ryzyko wycieku danych poprzez hardcoded secrets,  
- użycie podatnych bibliotek zewnętrznych.

Wynik 0/100 oraz status **REJECTED** są w pełni uzasadnione.  
Dopiero po wdrożeniu wszystkich poprawek aplikacja może zostać ponownie oceniona.

