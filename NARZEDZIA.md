<!-- KOPIA — nie edytuj. Zrodlo: C:\projekty-IOMJB\_STANDARDY\NARZEDZIA.md -->
> **Kopia z 2026-11-15.** Ten plik zmienia wylacznie PjM w zrodle `_STANDARDY\NARZEDZIA.md` i rozsyla `sync-standardy.py`. Zmiana wpisana tutaj zniknie przy najblizszej synchronizacji.

# NARZĘDZIA — czym co robimy

Mapa narzędzi IOMJB. Odpowiada na jedno pytanie: **mam do zrobienia X, czym to zrobić i jaka jest pułapka**. Zasady stojące za tymi narzędziami: `KANALY.md` (tablica, kalendarz, telefon), `POCZTA-IMAP.md` (skrzynki), `ZASADY_SESJI.md` (przebieg sesji). Zmienia ten plik wyłącznie PjM.

Wszystkie ścieżki są bezwzględne — narzędzia działają z dowolnego katalogu.

## 1. Tablica zadań

| Chcę | Komenda |
|---|---|
| zobaczyć swoje wiersze | `python C:\projekty-IOMJB\PjM\narzedzia\tablica.py pokaz --projekt KOD` |
| zobaczyć też zamknięte | `... pokaz --projekt KOD --wszystko` |
| zobaczyć notatki i blokady | `... pokaz --projekt KOD --pelne` |
| zmienić pozycję | `... ustaw --id KOD-NNN --status ... --deadline ... --zadanie "..." --notatka "..."` |
| dopisać do notatki, nie nadpisać | `... ustaw --id KOD-NNN --dopisz --notatka "..."` |
| dodać pozycję | `... dodaj --projekt KOD --zadanie "HEADLINE (KOD) — opis dokonany" --deadline DD.MM.RRRR` |
| przenieść zamknięte do archiwum | `... archiwizuj` (`--podglad` = tylko raport) |
| przemalować kolory po zmianach dat | `python ...\narzedzia\kolory-tablicy.py` (`--podglad`) |
| zobaczyć tablicę w przeglądarce | `python ...\narzedzia\tablica-html.py` → `PjM\tablica.html` |
| pozwolić Miko klikać zmiany | `python ...\narzedzia\tablica-serwer.py` → `127.0.0.1:8765` |

**Pułapki:**

1. **Excel trzyma plik na wyłączność.** Otwarty `tablica-zadan.xlsx` blokuje zapis — narzędzie zgłosi błąd, ale zdarzało się, że commit szedł dalej i wyglądał na udany. Po zapisie sprawdzaj plik, nie log konsoli.

2. **Adresuj po stałym ID, nie po numerze wiersza** (`KANALY.md` 1.9). Numery pływają przy każdym dodaniu i archiwizacji; `ustaw --id` odmawia zapisu, gdy ID nie istnieje, i wypisuje `PRZED: ID | projekt | treść` do kontroli.

3. **Konsola Windows chodzi na cp1252.** Bez `PYTHONIOENCODING=utf-8` polski znak w nazwie wiersza urywa listę w połowie, a wygląda ona na kompletną.

## 1b. Karty zadań (instrukcje wykonania)

| chcesz | komenda |
|---|---|
| zobaczyć kartę pozycji | dwuklik w ID na podglądzie tablicy (wymaga `tablica-serwer.py`) |
| przeczytać kartę w konsoli | `python ...\narzedzia\karty.py pokaz --id WZS-011` |
| założyć kartę z szablonu | `python ...\narzedzia\karty.py zaloz --id WZS-011` |
| sprawdzić, które pozycje mają kartę | `python ...\narzedzia\karty.py lista` |

**Pułapki:**

1. **Karta bez serwera się nie otworzy** — plik `tablica.html` jest statyczny, kartę składa `tablica-serwer.py` na żądanie.

2. **Nazwa pliku to ID i nic innego** — `PjM\karty\WZS-011.md`. Zmiana nazwy pliku odcina kartę od wiersza.

3. **PII do `-dane`** — w karcie wpisujesz ścieżkę do skanu, nie jego treść.

4. Zasada i podział ról: `KANALY.md` 1.14.

## 1a. Listy zewnętrzne (arkusze partnerów)

| Chcę | Komenda |
|---|---|
| zobaczyć wpięte listy | `python C:\projekty-IOMJB\PjM\narzedzia\listy_zewnetrzne.py listy` |
| zobaczyć pozycje partnera | `... listy_zewnetrzne.py pokaz --lista 4EN-AP --moje` |
| sprawdzić, co jest już na tablicy | `... dopasuj --lista 4EN-AP` |
| powiązać istniejący wiersz | `... powiaz --lista 4EN-AP --id 4EN-011 --nr 6` |
| przenieść termin i status na tablicę | `... sync --lista 4EN-AP` (`--zapisz`) |

Zasady: `KANALY.md` 1.13. Panel w przeglądarce (przycisk z kodem listy obok „kalendarz") dzieli ekran w pionie i pisze **wprost do pliku partnera** — przed pierwszym zapisem dnia powstaje kopia w podkatalogu `_kopie`. Nową listę wpina się wpisem w `listy-zewnetrzne.json`, bez zmian w kodzie.

**Pułapki:** dopasowanie po nazwie jest propozycją, nie faktem — headline partnera i nasza nazwa dokonana to dwa różne zdania o tej samej sprawie; wiązanie zatwierdza człowiek komendą `powiaz`. Status z arkusza partnera idzie tylko do przodu — cofnięcie wraca jako rozjazd do decyzji, nie jako zapis.

## 1c. Przeglądarka — Edge dla agenta, Opera dla Miko

Dwie przeglądarki, dwa światy. Dzięki temu karty, sesje i logowania się nie mieszają: agent może siedzieć zalogowany w Fakturomanii i KSeF, a okno Miko zostaje nietknięte.

1. **Wszystko, co robisz w przeglądarce sam, robisz w Edge.** Fakturomania, KSeF, e-Doręczenia, portale urzędowe, bankowość, logowania, sprawdzanie czegoś na stronie. Profil zostaje zalogowany między sesjami, więc nie logujesz się od nowa za każdym razem.

   `& "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" "URL"` albo z Pythona `kanaly_lib.otworz_dla_agenta(url)`.

2. **Wszystko, co pokazujesz Miko, otwierasz w Operze Air.** Podgląd tablicy, karta zadania, świeży deploy projektu webowego — tam Miko ma swoje karty i tam patrzy.

   `kanaly_lib.otworz_dla_miko(url)`.

1d. **Oddanie pliku Miko: `kanaly_lib.pokaz_plik(sciezka)`** — otwiera Explorer z **zaznaczonym** plikiem; katalog otwiera bez zaznaczania, nieistniejąca ścieżka nie otwiera niczego. To jest znaczenie słowa „zrobione" przy każdym dokumencie (`PREFERENCJE_MIKO.md` 7.6). Przed nadpisaniem pliku otwartego w PowerPoincie, Excelu albo Wordzie: `kanaly_lib.zamknij_dokument(sciezka)`; `pokaz_plik` sam zamyka okna Explorera otwarte już na tym folderze (jedna wersja naraz, `PREFERENCJE_MIKO.md` 10.5). Siatka bezpieczeństwa: hook `pokaz-plik.ps1` (Stop) robi to samo po odpowiedzi, gdy zapomnisz — dla dokumentów z ostatnich 6 godzin, raz na plik w sesji.

3. **Nie używaj `webbrowser.open`, `os.startfile` ani `start URL` do pokazywania czegoś Miko.** Domyślna przeglądarka systemu to **Edge**, czyli okno agenta — trafisz do siebie, nie do niego.

4. **Chrome nie istnieje na tej maszynie.** Komenda z `chrome` kończy się po cichu błędem i nic się nie otwiera — jeśli gdzieś ją znajdziesz, jest do poprawienia.

5. **Ścieżki obu przeglądarek żyją w `kanaly_lib`** (`PRZEGLADARKA_MIKO`, `PRZEGLADARKA_AGENTA`) — zmiana wersji albo instalacja w innym miejscu to poprawka w jednym pliku.

## 2. Co pali się teraz

```
python C:\projekty-IOMJB\PjM\narzedzia\pilne.py                # blokery, po terminie, ten tydzień, 7-14 dni
python ...\pilne.py --wszystko --projekt WZS --data 2026-09-01
```

Kubełki liczone z deadline'u, blokery wchodzą zawsze. **Listę pilnych generuje narzędzie, nie pamięć** — ręczne streszczenie 17.08 zgubiło wnioski do gestorów sieci. Skracasz w rozmowie → podaj licznik i nazwij pominięte.

## 3. Telefon

```
python C:\projekty-IOMJB\PjM\narzedzia\na-telefon.py --podglad   # co by poszło
python ...\na-telefon.py                                          # synchronizuje Google Tasks
python ...\na-telefon.py --dni 7 --max 15
```

Dwie listy: `Mikołaj's list` (dziś) i `PjM przeglad` (reszta). **Od 01.09.2026 nie odpalasz tego ręcznie** — `kanaly_lib.zapisz_tablice` robi to samo po każdym zapisie tablicy, w tle. Ręcznie tylko `--podglad`, żeby zobaczyć, co poszłoby na listę. Warstwa niżej: `_STANDARDY\google-tasks.py` (`listy`, `pokaz`, `dodaj`, `partia`, `zrobione`).

## 3a. Kalendarz

```
python C:\projekty-IOMJB\PjM\narzedzia\na-kalendarz.py --podglad   # co by sie zmienilo
python ...\na-kalendarz.py                                         # synchronizuje kalendarz Outlook
```

Kalendarz `mj.banas@outlook.com` nadąża za tablicą **sam**, z tego samego automatu co telefon (decyzja Miko 01.09.2026). Wchodzą pozycje o rodzaju `termin pewny`, `kamien`, `spotkanie` — zwykły `termin` zostaje na tablicy, bo bywa datą ponaglenia. Wpisy automatu mają w treści znacznik `[tablica:ID]`; **wpisów bez znacznika skrypt nie dotyka**, więc ręczne wpisy Miko są bezpieczne. Zamknięcie pozycji zdejmuje wpis.

**Pułapka:** wpis powstaje na koncie `mj.banas@outlook.com`, bo tylko ono synchronizuje kalendarz z telefonem — kalendarze kont IMAP są plikami lokalnymi.

## 4. Poczta

```
pwsh -File C:\projekty-IOMJB\PjM\narzedzia\poczta-przeglad.ps1 -Od 2026-08-22 -Skrzynka fraza
python C:\projekty-IOMJB\_STANDARDY\poczta-czytaj.py --account proton-iomjb --count 15
python ...\poczta-czytaj.py --id 82                    # pełna treść po UID
python ...\poczta-wyslij.py --to a@x.pl --subject "T" --body-file tresc.txt --attach plik.pdf
```

**Bramka bez wyjątków: powstaje wyłącznie SZKIC do Drafts. „Wyślij" klika Miko — flagi `--send` nie używamy nigdy.**

**Pułapki:** Proton wymaga działającego Bridge'a (`127.0.0.1:1143`), a Bridge blokuje po dwóch nieudanych logowaniach — jedna próba, potem zmiana drogi na Outlook COM. Skany bez warstwy tekstowej renderuj przez `pymupdf` (`get_pixmap(dpi=150)`) i czytaj wzrokiem; `pypdf` zwraca na nich pustkę.

## 5. Kalendarz

Wpisy zakłada agent przez Outlook COM na koncie `mj.banas@outlook.com` (`Namespace.Stores` → `GetDefaultFolder(9)`). Bez uczestników, więc nic nie wychodzi mailem. Zasady treści i przypomnień: `KANALY.md` sekcja 2.

## 5a. Skrzynka mobilna — co Miko podyktował w terenie

Każdy agent czyta ją na otwarciu sesji (`ZASADY_SESJI.md` 4b); routing i format: `REFERENCJA_SESJI.md` 5.11 oraz `PjM\skrzynka\README.md`.

| chcę | polecenie |
|---|---|
| zobaczyć, co leży dla mnie | `python C:\projekty-IOMJB\PjM\narzedzia\skrzynka.py nowe --od RRRR-MM-DD --projekt KOD` |
| dodać wpis | `python ...\skrzynka.py dodaj --tresc "..." --zrodlo dispatch --projekt KOD` |
| oznaczyć zroutowany | `python ...\skrzynka.py podjety --wpis FRAGMENT --slad "tablica WZS-014"` |
| domknąć i zarchiwizować | `python ...\skrzynka.py zrobiony --wpis FRAGMENT --slad "co z tego wyszło"` |

1. **`git -C C:\projekty-IOMJB\PjM pull` przed odczytem.** Skrzynka żyje w repo PjM, a wpis mógł dojść z innej maszyny — bez pulla czytasz wczorajszy stan.

2. **Narzędzie jest wygodą, nie bramką.** Wpis to zwykły plik `.md` z nagłówkiem; dopisanie go ręcznie albo przez Dispatch zwykłym zapisem jest równie ważne. Parser uzupełnia braki (brak statusu = `nowy`, data z nazwy pliku), zamiast odmawiać.

3. **`--projekt KOD` pokazuje też wpisy bez przypisania.** To celowe — puste pole znaczy „PjM rozstrzygnie", a nie „niczyje". Bierzesz taki wpis tylko wtedy, gdy sprawa faktycznie jest Twoja.

4. **`--slad` jest wymagany przy `podjety`.** Wpis, który zniknął z listy bez informacji dokąd poszedł, jest gorszy niż wpis nieprzeczytany.

5. **`[ZALEG]` powyżej 2 dni, `[PILNE]` powyżej 7.** Leżakujący wpis meldujesz Miko w meldunku otwarcia.

## 5b. Pamięć projektu — wyciąg z logów sesji

`python C:\projekty-IOMJB\PjM\narzedzia\pamiec.py --projekt KOD` — jedyna droga do logów sesji. Bezpośredni odczyt `sessions\*.md` odmawia hook `PreToolUse` (`C:\Users\Miko\.claude\hooks\blokada-logow.ps1`). Przełączniki: `--wszystkie` (najnowszy log każdego projektu — przegląd PjM), `--ile 2` (dwa ostatnie logi).

1. **Skrypt tnie po nagłówkach `##`** i odcina sekcje o przebiegu: „Co zrobione", „Lessons learned", „Ocena", „Otwarcie". Pułapka: sekcja z faktami nazwana jednym z tych tytułów też wyleci — nazywaj sekcje po treści.

2. **Zapis logu działa normalnie.** Blokada łapie odczyt (`Read`, `Grep`, `Glob`, `cat`, `Get-Content`), nie zapis, nie listowanie katalogu i nie gita.

## 5d. Ocena sesji — wpis do LOG_RUNOW (tylko na zamknięciu)

| chcę | komenda |
|---|---|
| zapisać minus ze słowami Miko | `python ...\narzedzia\ocena.py --projekt KOD --zlecenie "..." --notatka "..."` |
| minus bez notatki | `... ocena.py --projekt KOD --zlecenie "..." --bez-notatki` |
| zobaczyć, ile minusów ma każdy agent | `python ...\narzedzia\ocena.py --stan` |

Plusów nie logujemy. Narzędzie odmawia zapisu bez `--notatka` albo `--bez-notatki` — notatki nie wymyślamy, idzie dosłownie to, co powiedział Miko.

## 5c. Formatka zlecenia — INPUT / ZLECENIE / OUTPUT

`python C:\projekty-IOMJB\PjM\narzedzia\zlecenie.py --projekt KOD` — otwiera Miko trzypolową formatkę w Operze Air i czeka. Strzałki góra/dół na skraju pola przechodzą dalej, Ctrl+Enter zapisuje, Esc anuluje. Wynik: plik w `PjM\zlecenia\` i treść na stdout, którą czytasz jako zlecenie.

1. **To jest narzędzie do bramki wejścia** (`ZASADY_ODPOWIEDZI.md` 1a), nie do każdego promptu. Odpalasz je wtedy, gdy zadanie ma coś stworzyć albo zmienić, a output nie jest jasny.

2. **Nie odpalasz go po „leć"** ani przy czynnościach odczytowych. Miko powiedział „leć" — ruszasz i bierzesz odpowiedzialność za interpretację.

3. **Serwer czeka 15 minut i kończy.** Brak zapisu = brak zlecenia; nie produkujesz wtedy niczego, tylko pytasz Miko.

## 6. Wejścia spoza sesji (PjM)

```
python C:\projekty-IOMJB\PjM\narzedzia\stan-sesji.py zapisz      # na zamknięciu
python ...\stan-sesji.py porownaj                                 # na otwarciu
```

Migawka kalendarza, Google Tasks, tablicy i backlogu do `PjM\stan\ostatnie-zamkniecie.json`. Pokazuje, co Miko dorzucił z telefonu albo ręcznie w Excelu między sesjami.

## 7. Zasady i ich rozsyłka (PjM)

```
python C:\projekty-IOMJB\_STANDARDY\sync-standardy.py            # rozsyła do wszystkich
python ...\sync-standardy.py --projekt 4en --sprawdz              # co jest nieaktualne
```

Kopiuje pliki wspólne ze źródła w `_STANDARDY\` do katalogu każdego agenta i zakłada brakujące `LOG_RUNOW.md`. Idempotentny — porównuje treść bez nagłówka kopii.

## 8. Warstwa wspólna

`PjM\narzedzia\kanaly_lib.py` — reguła koloru z deadline'u, parsowanie dat, kanoniczne kody projektów, lista statusów. **Zmiana reguły idzie tutaj, nie do pięciu skryptów osobno.** Macierz kolorów skopiowana do dwóch plików zawsze zostawia jedną kopię w tyle.

## 9. Specyficzne dla projektu

1. **WZ-STUDIO** — `narzedzia\nowe_zgloszenia.py`: porównuje teczki w `klienci\` z wierszami na tablicy i katalogami w `sprawy\`, wypisuje zgłoszenia bez śladu. Kończy kodem 1, gdy coś wisi. Uruchamiane na otwarciu sesji po `git pull`.

2. **iomjb-firma** — `narzedzia\nest-sweep.ps1`: przenosi korespondencję Nest Banku do folderu `Nest Bank` i wypisuje nieprzeczytane. Uruchamiane na otwarciu sesji.

Narzędzie własne projektu opisujesz w sekcji `## OTWARCIE` swojego `CLAUDE.md`, jeśli należy do otwarcia sesji.
