# Raport audytu POM

## Cel

Celem audytu była ocena implementacji wzorca Page Object Model oraz weryfikacja wykonania scenariusza testowego. [file:2][file:3][file:4][file:1]

## Struktura

Projekt składa się z trzech warstw: `BasePage`, `MainPage` oraz scenariusza `run_engineered_test()`. [file:3][file:4][file:2]
`BasePage` odpowiada za wczytywanie selektorów z pliku JSON, a `MainPage` udostępnia metody biznesowe zamiast bezpośredniej pracy na locatorach. [file:3][file:4]

## Wynik

Log potwierdza poprawne wykonanie trzech kroków scenariusza. [file:1]
Odnaleziono nagłówek strony, wykonano kliknięcie w element `add` oraz wpisano frazę `Automatyzacja Mobilna` do pola `search_button`. [file:1]

## Ocena

Największą zaletą rozwiązania jest czytelny podział odpowiedzialności zgodny z POM. [file:2][file:3][file:4]
Ograniczeniem pozostaje brak rzeczywistej integracji z driverem, ponieważ metody zwracają komunikaty tekstowe zamiast wykonywać realne akcje na UI. [file:4]

## Rekomendacje

- Dodać obsługę rzeczywistego drivera Appium lub Selenium. [file:4]
- Zastąpić `print()` mechanizmem logowania i mocniejszą obsługą błędów. [file:3]
- Utrzymać obecną strukturę, bo stanowi dobrą bazę do dalszej rozbudowy frameworka. [file:2][file:3][file:4]