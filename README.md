# Moje polisy

Prywatny rejestr polis ubezpieczeniowych na telefon i komputer. Wgrywasz PDF albo zdjęcie polisy (najlepiej razem z OWU), a Claude sam odczytuje:

- co jest ubezpieczone i na jaką kwotę, udział własny, limity i wyłączenia;
- co zrobić, gdy coś się stanie: kontakt do zgłoszenia szkody, kroki, termin zgłoszenia, potrzebne dokumenty;
- okres ochrony, raty i odnowienie;
- na co uważać w OWU.

Lista pokazuje kolorami, co wymaga uwagi: nieopłaconą ratę, polisę, która się kończy, i termin wypowiedzenia. Przycisk **Kalendarz** zapisuje terminy z przypomnieniami do kalendarza w telefonie albo w Outlooku.

## Jak to działa

- **Strona** (ten kod) leży w publicznym repozytorium i jest wystawiona przez GitHub Pages. Nie ma w niej żadnych danych ani kluczy.
- **Dane** (polisy i pliki PDF) leżą w osobnym, **prywatnym** repozytorium `polisy-dane`. Strona zapisuje do niego i czyta z niego Twoim tokenem.
- **Odczyt dokumentów** robi Claude przez Twój klucz API. Płacisz za każdy odczyt, zwykle od kilkudziesięciu groszy do kilku złotych za polisę z OWU.
- Klucz API i token wpisujesz raz na każdym urządzeniu. Zostają tylko w tej przeglądarce.

## Uruchomienie (jednorazowo)

### 1. Repozytorium z aplikacją (publiczne)

1. Na github.com załóż repozytorium **`polisy`**, widoczność **Public**.
2. Wgraj do niego pliki z folderu `C:\polisy`.
3. W repozytorium: **Settings → Pages → Build and deployment**, Source: **Deploy from a branch**, Branch: **main**, folder **/ (root)**, **Save**.
4. Po minucie strona działa pod adresem `https://<twoja-nazwa>.github.io/polisy/`.

### 2. Repozytorium na dane (prywatne)

1. Załóż drugie repozytorium **`polisy-dane`**, widoczność **Private**. Może być puste albo z plikiem README.
2. Niczego do niego nie wgrywasz. Aplikacja sama założy w nim plik `polisy.json` i katalog `pliki/`.

### 3. Token GitHub (dostęp tylko do danych)

1. GitHub → zdjęcie profilowe → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Nazwa: np. `polisy`. Expiration: najdłuższa dostępna (np. 1 rok; przed wygaśnięciem wygeneruj nowy).
3. **Repository access: Only select repositories → `polisy-dane`**.
4. **Permissions → Repository permissions → Contents: Read and write**. Nic więcej.
5. **Generate token** i skopiuj go (zaczyna się od `github_pat_`). Pokazuje się tylko raz.

### 4. Klucz API Claude

1. Wejdź na **console.anthropic.com** i załóż konto (to osobne konto, niezależne od subskrypcji claude.ai).
2. **Billing**: dodaj kartę i doładuj saldo. Ustaw limit wydatków i wyłącz automatyczne doładowanie, jeśli chcesz mieć pewność, że nie wydasz więcej.
3. **API Keys → Create Key**, skopiuj klucz (zaczyna się od `sk-ant-`).

### 5. Pierwsze uruchomienie

1. Otwórz stronę na komputerze, wejdź w **Ustawienia** (ikona zębatki).
2. Wpisz klucz API, nazwę konta GitHub, repozytorium `polisy-dane` i token. Kliknij **Sprawdź klucz Claude**, potem **Zapisz i połącz**.
3. Na iPhonie otwórz ten sam adres w Chrome i wpisz to samo w Ustawieniach.
4. Ikona na ekranie iPhone'a: w Chrome stuknij **Udostępnij** (kwadrat ze strzałką obok paska adresu) → **Dodaj do ekranu początkowego**.

## Bezpieczeństwo

- Token ma dostęp tylko do repozytorium `polisy-dane` i tylko do plików. Nie ma dostępu do innych repozytoriów ani ustawień konta.
- Jeśli strona wykryje, że `polisy-dane` jest publiczne, pokaże czerwone ostrzeżenie.
- Nie wpisuj kluczy na cudzym ani wspólnym komputerze. Zgubiony telefon: unieważnij token na GitHub i klucz na console.anthropic.com, potem wygeneruj nowe.
- Dokumenty wysyłane do odczytu trafiają do Anthropic (Claude API) i do Twojego prywatnego repozytorium. Nigdzie indziej.

## Ograniczenia

- Aplikacja nie wie, czy rata naprawdę wpłynęła do ubezpieczyciela. Po zapłacie zaznacz ratę jako zapłaconą.
- Odczytane kwoty i daty trzeba raz porównać z dokumentem (aplikacja prosi o to przed zapisem).
- Kontakt do zgłoszenia szkody pochodzi tylko z dokumentów. Jeśli go tam nie ma, aplikacja to pokaże i możesz dopisać go ręcznie w **Edytuj**.
- Po zmianie danych na jednym urządzeniu odśwież stronę na drugim.

## Zmiana kodu

Po każdej zmianie w `styles.css` albo `app.js` podnieś numer `?v=` w `index.html`, żeby przeglądarki pobrały nową wersję.
