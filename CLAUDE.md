# CLAUDE.md — wirtualny-kot (WKT)

Ten plik czytasz na starcie sesji. Sekcja ROLA jest kotwicą — wstrzykuje ją hook przy każdym prompcie i do niej wracasz przy re-anchorze. Wspólne reguły: `..\CLAUDE.md` (Claude Code ładuje kaskadowo).

## ROLA

**Deweloper aplikacji WKT — budujesz, rozwijasz i deployujesz Wirtualnego Kota** (rola ustalona przez Miko 10.09.2026; do tego dnia projekt był stubem bez roli). Piszesz kod, stawiasz go na produkcji i pilnujesz, żeby to, co Miko zobaczy w przeglądarce, działało. Wizja produktu należy do Miko i mieszka w `VISION_WKT.md` — bierzesz z niej zakres, nie dokładasz do niej własnych pomysłów.

Prowadzisz swoje wiersze na tablicy pod kodem **WKT**: zakładasz, opisujesz, zmieniasz status, zamykasz. Priorytety i zależności między pozycjami trzyma PjM.

**Decyzje wykonawcze podejmujesz sam** — sposób implementacji, kolejność, struktura plików, refaktor. Pytasz wyłącznie o: dane spoza bazy, pieniądze i zobowiązania wobec osób trzecich, nieodwracalne kasowanie. Kreatywne decyzje i treść produktu należą do Miko.

## Zasady — czytasz na starcie każdego runu

Kopie ze źródła w `_STANDARDY\`, rozsyłane przez `sync-standardy.py`; zmienia je wyłącznie PjM razem z Miko.

1. `PREFERENCJE_MIKO.md` — jak współpracować z Miko.
2. `ZASADY_SESJI.md` — otwarcie, przebieg, zamknięcie sesji.
3. `ZASADY_ODPOWIEDZI.md` — budowa zlecenia i runu, ocena, licznik.
4. `KANALY.md`, `NARZEDZIA.md`, `REFERENCJA_SESJI.md`.

Własne: `LOG_RUNOW.md`, `LOG_STYLU_KOMUNIKACJI.md`, `sessions\RRRR-MM-DD.md`.

## Czym jest ta aplikacja

Aplikacja terapeutyczna „Zaleca się kota" (inspiracja: Sho Ishida). Quiz → diagnoza emocjonalna → rasa kota, plus mechanika głaskania. Wizja, historia Mii i backlog pomysłów: `VISION_WKT.md` — to jest plik Miko, nie Twój.

## Stack i deploy

1. **Front:** statyczny HTML z CSS i JS w plikach — bez frameworka i bez builda. Jedna strona = jeden `index.html` w swoim katalogu (`/`, `login`, `register`, `breeds`, `auth/callback`).
2. **Biblioteki z CDN:** `@supabase/supabase-js@2` (jsDelivr), Cloudflare Turnstile.
3. **Auth i baza:** Supabase. Magic link przez Resend jako custom SMTP, Google OAuth.
4. **Hosting:** Vercel, produkcja `https://wirtualny-kot.vercel.app`. Routing i przepisania: `vercel.json`. Deploy: `vercel --prod --yes`.
5. **Repo:** `https://github.com/banamicobo/wirtualny-kot`, branch `master`. To osobne repo — katalog jest wyłączony w `.gitignore` rodzica.
6. **Mapa narzędzi projektu:** `tools-map.html`.

Cykl przy zmianie widocznej dla człowieka: commit → push → deploy → otwarcie w przeglądarce **Miko** (Opera Air; `kanaly_lib.otworz_dla_miko`). Domyślna przeglądarka systemu to okno agenta, nie Miko.

## Stan aplikacji

Ostatni log sesji: `sessions\2026-05-08.md`. Stan stamtąd, niezweryfikowany w kodzie po tej dacie:

1. **Działa:** magic link end-to-end, Google OAuth, stan zalogowania w nav, callback obsługujący oba flow (PKCE i magic link).
2. **Otwarte:** Facebook OAuth, dashboard po zalogowaniu, podmiana testowego sitekey Cloudflare Turnstile na prawdziwy.
3. **Produkcja odpowiada** (sprawdzone 10.09.2026: HTTP 200).

Zanim cokolwiek dopiszesz — sprawdź stan w kodzie, nie w tym akapicie. Log z maja nie jest opisem dzisiejszego repo.

## Czego ten projekt nie ma

1. **Własnej skrzynki pocztowej** — `ZASADY_SESJI.md` 5.4 nie przypisuje WKT żadnego konta. Krok „odbierasz swoją pocztę" odpada; korespondencja w sprawie projektu trafia do PjM.
2. **Akt sprawy** — brak sekcji `## ZRODLA`, bo projekt nie stoi na dokumentach źródłowych. Liczby i twierdzenia i tak oznaczasz według `ZASADY_ODPOWIEDZI.md` 2a.
3. **Danych osobowych w repo.** Konta użytkowników żyją w Supabase; cokolwiek z PII zejdzie na dysk, idzie do `C:\projekty-IOMJB-dane\WKT\`, nigdy tutaj.
