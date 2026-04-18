# 🛡️ AUDYT BEZPIECZEŃSTWA: MANIFEST SCANNER

**Status:** Wykonano automatyczną ekstrakcję ryzyka.

---

### 📝 1. Zawartość *RiskyPermission.xml*

Zidentyfikowano następujące wpisy krytyczne:

- **Debuggable:** `true`  
  ⚠️ **Wysokie ryzyko** — aplikacja może być podatna na analizę działania oraz inżynierię wsteczną w trakcie uruchomienia.

- **Permissions:**  
  Wykryto uprawnienia umożliwiające dostęp do:  
  - sieci (`INTERNET`),  
  - pamięci zewnętrznej.  
  Zwiększa to potencjalną powierzchnię ataku.

---

### 🧠 2. Interpretacja inżynierska

Najpoważniejszym zagrożeniem jest ustawienie flagi **`debuggable="true"`**.  
Pozwala to osobom nieupoważnionym na:

- monitorowanie działania aplikacji,  
- podłączanie narzędzi debugujących (np. `adb jdwp`),  
- śledzenie procesów uruchomionych na urządzeniu.

Takie zachowanie znacząco obniża poziom bezpieczeństwa aplikacji produkcyjnej.

---

### 🛠️ 3. Akcja korygująca

Rekomenduje się:

- wdrożenie kontroli w procesie **CI/CD** (np. Jenkins, GitHub Actions),  
  która **zablokuje build**, jeśli w pliku *RiskyPermission.xml* wykryta zostanie flaga `debuggable="true"`;
- okresowy przegląd deklarowanych uprawnień i ograniczenie ich wyłącznie do niezbędnego minimum.

---

### 🧾 Raport wykonany przez:

**Imię:** Dawid  
**Numer studenta:** 95983  
**Data:** 18.04.2026
