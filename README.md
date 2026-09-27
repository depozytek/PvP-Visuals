# Zdalna konfiguracja moda

Pliki w tym repozytorium są pobierane przez mod w tle. Zmiana JSON na GitHubie
nie wymaga nowego pliku JAR. Wartości `enabled` na poziomie pliku są głównymi
przełącznikami. Pliki muszą pozostać poprawnym JSON-em.

## `config.json` — serwery na liście Multiplayer

- `enabled: false` — nie dodaje nowych serwerów; już dodane pozostają.
- `enabled: true` — dodaje włączone wpisy z tablicy `servers` po otwarciu ekranu Multiplayer.
- `servers[].enabled` — włącza lub wyłącza dodawanie konkretnego wpisu. `false` pozostawia go osobom, które już go mają.
- `name` — nazwa widoczna na liście; `address` — adres serwera.
- `position` — `top` albo `bottom`.

Usunięcie wpisu z tablicy powoduje usunięcie tego adresu przy następnym
odświeżeniu u osób, którym mod wcześniej sam go dodał. Ręcznie dodane serwery
nie są oznaczane jako dodane przez mod. Wpis przykładowy
`play.twoj-serwer.pl` trzeba zmienić przed włączeniem pliku.

## `announcements.json` — reklama na HUD

- `enabled` — główny przełącznik całego pliku.
- `announcements` — lista reklam; każda może mieć własne `enabled`.
- `id` — stały, unikalny identyfikator reklamy.
- `title`, `description` — nagłówek i treść bannera.
- `mode` — `once` (raz dla danego ID), `session` (raz na uruchomienie gry)
  albo `repeat` (cyklicznie).
- `delayMinutes` — po ilu minutach gry na serwerze może pokazać się pierwszy raz.
- `intervalMinutes` — odstęp pomiędzy rozpoczęciami pokazów w trybie `repeat`.
- `durationSeconds` — czas jednego pokazu.
- Opcjonalne `expiresAt` — data końca w formacie ISO-8601, np. `2026-12-31T23:00:00Z`.

Gracz może wyłączyć reklamy w ustawieniach moda i przenieść banner w edytorze
HUD. Mod sprawdza ten plik mniej więcej co 5 minut.

## `updates.json` — wiadomości na czacie

- `enabled` — główny przełącznik. Aktualnie jest ustawiony na `false`.
- `updates` — lista wiadomości; każda ma własne `enabled`.
- `id` — unikalne ID. Dana wiadomość jest wyświetlana najwyżej raz na
  uruchomienie gry.
- `title`, `description` — tytuł i tekst wiadomości.
- `button` — podpis klikalnego odnośnika na czacie.
- `url` — pełny adres HTTPS otwierany po kliknięciu.

Gracz może osobno wyłączyć te powiadomienia w ustawieniach moda. Mod pobiera
plik mniej więcej co 5 minut. Przykładowy adres `https://modrinth.com/`
należy zamienić na stronę konkretnego moda przed włączeniem powiadomienia.

## `partners.json` — zakładki KlejTXT i Partner

W menu mogą istnieć maksymalnie **dwie** takie zakładki. Dozwolone ID to
`klejtxt` i `partner`; nie można przez ten plik dodawać innych elementów GUI.

- `enabled` — główny przełącznik obu zakładek.
- `slots[].enabled` — widoczność danej zakładki.
- `id` — `klejtxt` albo `partner`.
- `title` — tytuł strony; `description` — tablica maksymalnie pięciu
  krótkich linii opisu.
- `button` — napis na przycisku; `url` — jego adres HTTPS.
- `icon` — pełny adres do białego PNG w tym repozytorium, np.
  `https://raw.githubusercontent.com/depozytek/PvP-Visuals/main/assets/partner-white.png`.
  Zalecane 64×64 px, najwyżej 128 KiB i 2048×2048 px. Mod przygotowuje
  miniaturę 64×64 w tle. Pusty adres używa ikony zastępczej.
- `iconColor` — kolor **samej białej ikony**, np. `#E91E82`. Nie zmienia
  obramowania ani tła kafelka.

Gdy zastąpisz PNG pod tym samym adresem, dopisz lub zmień na końcu adresu
`?v=2`, aby klient pobrał nową wersję ikony. Mod sprawdza konfigurację
mniej więcej co 10 minut. Przy chwilowym braku połączenia zachowuje ostatni
stan w bieżącej sesji; przy świeżym uruchomieniu awaryjnie pokazuje KlejTXT.

Logo KlejTXT znajduje się w `assets/klejtxt-logo-white.png`. Drugi slot jest
domyślnie wyłączony — przed włączeniem podmień jego tytuł, opis, adres i ikonę.
