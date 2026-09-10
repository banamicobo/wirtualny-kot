<!-- KOPIA — nie edytuj. Zrodlo: C:\projekty-IOMJB\_STANDARDY\REFERENCJA_SESJI.md -->
> **Kopia z 2026-09-10.** Ten plik zmienia wylacznie PjM w zrodle `_STANDARDY\REFERENCJA_SESJI.md` i rozsyla `sync-standardy.py`. Zmiana wpisana tutaj zniknie przy najblizszej synchronizacji.

# REFERENCJA SESJI — mapa skrzynek, akta, układ plików

Materiał **doczytywany**, nie czytany na starcie każdego runu. Wydzielony z `ZASADY_SESJI.md` 24.08.2026, bo checklista otwarcia i zamknięcia musi być krótka, a mapa skrzynek, zasady akt i układ katalogów są potrzebne raz na jakiś czas.

Otwierasz ten plik, gdy: odbierasz pocztę i nie wiesz, która skrzynka jest Twoja · trafiasz na sprawę cudzego projektu · Twój projekt ma akta · dostajesz wpis ze skrzynki mobilnej · porządkujesz katalog projektu.

Zmienia go wyłącznie PjM razem z Miko.

## 5. Kto co prowadzi

Każdy agent prowadzi swoje sprawy sam. PjM planuje, sprawdza kompletność i utrzymuje zasady — nie przepisuje cudzych statusów, nie zakłada cudzych terminów i nie obrabia cudzej poczty. Przepisywanie przez jedną osobę gubiło pozycje i było podwójną robotą.

**Jeden wyjątek: PjM przegląda wszystkie skrzynki, ale ich nie obrabia** (decyzja Miko 22.08.2026, sekcja 5.8). Bez tego mail do projektu, którego sesji nikt tego dnia nie otworzył, leżałby nieodebrany do czasu, aż ktoś sobie o nim przypomni.

1. **Tablica** — swoje wiersze prowadzi agent projektu.

2. **Kalendarz** — swoje terminy wpisuje agent projektu.

3. **Telefon** — po zmianie priorytetów agent odświeża listę dnia.

4. **Poczta** — agent odbiera skrzynki swojego projektu:

| Skrzynka | Projekt |
|---|---|
| `mj.banas@outlook.com` | WZS — gestorzy, klienci, Mariusz |
| `IOMJB@proton.me` | IOM — KRS, e-Doręczenia, Nest Bank, Fakturomania |
| `IOMJB_Jadwiga@proton.me` | IOM — korespondencja Prezes Zarządu |
| `IOMJB_consultant@proton.me` | 4EN |
| `IOMJB_Mikolaj@pm.me` | ODS **i** TAX — czytają obaj, każdy swoje wątki (podział niżej) |
| `banamicobo@icloud.com` | PRV i KOS — sprawy prywatne |
| `mikolajbanas@gmail.com`, `banamicobo@gmail.com`, `IOMJB@pm.me` | PjM — reszta, w większości szum |

5. **Skrzynka dzielona `IOMJB_Mikolaj@pm.me`** — jedyna czytana przez dwóch agentów, bo obsługuje dwie niepowiązane sprawy. Podział wątków jest sztywny:

   - **ODS** bierze wszystko wokół szukania pracy: aplikacje, odpowiedzi rekrutacyjne, potwierdzenia zgłoszeń, korespondencję z kancelarią w sprawie 271/26.
   - **TAX** bierze urzędy i instytucje niemieckie: Bundesagentur für Arbeit, Finanzamt, ELSTER, Commerzbank, sprawy rezydencji i ALG.
   - **Wiadomość, która nie pasuje do żadnego wątku**, obrabia ten, kto zobaczył ją pierwszy, i wpisuje do logu sesji, że ją wziął. Bez tego wpisu druga sesja obrobi ją drugi raz.

6. **Wiadomość spoza swojego zakresu** zostawiasz nietkniętą i nie odpowiadasz w cudzej sprawie.

7. **Sprawa, która wyszła u Ciebie, a należy do innego projektu, idzie OD RAZU NA TABLICĘ** jako nowy wiersz z kodem tamtego projektu (`tablica.py dodaj --projekt KOD`). W notatce piszesz, skąd sprawa się wzięła i kto ją zgłosił. Do logu sesji wpisujesz to samo w punkcie „co dotyczy innych projektów" — jako ślad, nie jako kanał przekazania.

   **To jedyny przypadek, w którym zakładasz wiersz cudzego projektu.** Istniejących cudzych wierszy nadal nie ruszasz — ani treści, ani statusu, ani deadline'u. Zakładasz nowy i zostawiasz go agentowi tamtego projektu.

   Powód: przekazywanie przez plik pośredni wymagało, żeby ktoś go przeczytał i przeniósł — zgłoszenia leżały tygodniami.

8. **Narzędzie do odczytu:** `pwsh -File C:\projekty-IOMJB\PjM\narzedzia\poczta-przeglad.ps1 -Od RRRR-MM-DD -Skrzynka fraza`. Pojedyncze wiadomości i szkice: `_STANDARDY\poczta-czytaj.py` i `poczta-wyslij.py`. Szczegóły kont i pułapki: `POCZTA-IMAP.md`.

### 5.9 Zadania zlecane przez PjM — jednorazowe polecenia dla agenta

Z pracy PjM z Miko wychodzą czasem jednorazowe polecenia dla konkretnego agenta: przejrzyj coś u siebie, dostosuj się do zmienionego standardu, sprawdź swoje wiersze. To nie są sprawy projektu, tylko akcje na jego repo albo pozycjach.

1. **PjM zakłada je jako normalny wiersz z kodem tamtego projektu** (`tablica.py dodaj --projekt KOD`). Nie ma osobnego kanału ani pliku pośredniego.

2. **Notatka zaczyna się od `ZLECENIE PjM DD-MMM-RRRR:`** i zawiera całą instrukcję: co zrobić, na czym, po czym poznać, że skończone. Agent nie ma dopytywać, co autor miał na myśli.

3. **Agent widzi je na otwarciu sesji**, przy przeglądzie swoich wierszy (punkt 1.4). Melduje je Miko razem z resztą i **Miko decyduje, czy robimy to na początek, czy na koniec sesji.**

4. **Po wykonaniu wiersz idzie na `done` i wylatuje do archiwum** przy najbliższym sprzątaniu. Ślad z tego, co faktycznie zrobione, zostaje **w logu sesji** — tam, gdzie reszta pamięci projektu.

5. **Zlecenie nie jest sprawą projektu.** Nie dorabiamy do niego kamieni milowych ani osobnych terminów w kalendarzu; ma deadline tylko wtedy, gdy Miko go wskazał.

### 5.8 PjM jako czujka pocztowa — wykrywa, nie obrabia

Problem, który to rozwiązuje: agent odbiera swoją skrzynkę **na swojej sesji**. Jeśli Miko nie otworzy tej sesji przez kilka dni, pismo z terminem leży nieodebrane i nikt o tym nie wie.

1. **PjM przegląda wszystkie skrzynki na każdym swoim otwarciu** — od daty ostatniej swojej sesji, jednym przebiegiem `poczta-przeglad.ps1`.

2. **Czyta płytko: nadawca, temat, data, do której skrzynki przyszło.** Nie otwiera załączników w cudzych sprawach, nie renderuje skanów, nie streszcza treści.

3. **Nie zakłada wierszy, nie zmienia statusów, nie odpowiada.** To nie jest rozdzielanie poczty — tamten tryb zniesiono 22.08.2026 jako podwójną robotę.

4. **Jedyne, co robi: mówi Miko, którego agenta odpalić i dlaczego.** Jednym zdaniem na projekt: „przyszły dwie wiadomości od ZUK na skrzynkę WZS — odpal WZ-STUDIO". Jeśli z tematu widać, że coś się odblokowało albo pojawił się nowy termin, mówi i to.

5. **Sprawa własnego projektu (PjM, PRV, KOS) to normalna robota PjM** — tę obrabia do końca, tak jak każdy agent swoją.

6. **Milczenie też jest informacją.** Przy zerze merytorycznych wiadomości PjM podaje licznik: „61 wiadomości, wszystkie to szum, żadnej sesji nie trzeba otwierać".

## 5.10 Akta sprawy — projekty, które mają dokumenty źródłowe

Część projektów prowadzi sprawy oparte na dokumentach: pisma, umowy, protokoły, akta procesowe. Tam każda liczba i każde twierdzenie prawne ma swoje miejsce w papierze — i tylko stamtąd wolno je brać.

1. **Sekcja `## ZRODLA` w `CLAUDE.md` projektu** wymienia dokumenty źródłowe pełnymi ścieżkami, z jednym zdaniem o tym, co każdy zawiera. Nagłówek brzmi dokładnie `## ZRODLA` — tak samo u wszystkich, żeby dało się to sprawdzić jednym grepem. Hook czyta tę sekcję i **przypomina o niej przy każdym prompcie**, więc lista jest przed oczami zawsze, a nie tylko na starcie.

2. **`FAKTY.md` w repo projektu** to rejestr ustaleń: fakt, wartość, data, **odsyłacz do akt** (`plik:linia`). Krótki plik zamiast trzymania całych akt w kontekście — akta otwierasz wtedy, gdy ich potrzebujesz, a nie na wszelki wypadek.

3. **Fakt bez odsyłacza nie wchodzi do `FAKTY.md`.** Jeśli czegoś nie ma w aktach, a wiesz to od Miko — wpisujesz `[Miko DD-MMM-RRRR]`. Jeśli nie wiesz skąd, nie wpisujesz wcale.

4. **Przed policzeniem czegokolwiek otwierasz akta.** Kwota, staż, termin ustawowy, wysokość roszczenia — to wszystko czyta się z dokumentu w tej sesji, nie z pamięci poprzedniej.

5. **PII zostaje w `-dane`.** `FAKTY.md` żyje w repo i trzyma wartości oraz odsyłacze; same dokumenty leżą poza repo.

6. **Gdy akta należą do innego projektu, pytanie też do niego należy.** Sprawę prowadzi ten, kto ma jej akta i mandat — reszta bierze z niej wynik, nie prowadzi jej równolegle.

## 5.11 Skrzynka mobilna — co Miko podyktował w terenie

Miko wpada na coś poza sesją — w samochodzie, u klienta, w kolejce. Skrzynka przyjmuje wpis natychmiast i **rozdaje go na otwarciach sesji, wszystkim naraz**, żeby rzecz nie czekała na sesję właściwego projektu.

1. **Gdzie leży:** `C:\projekty-IOMJB\PjM\skrzynka\`, jeden plik na wpis, nazwa `RRRR-MM-DD-HHMM-slug.md`. Nagłówek `data` / `zrodlo` / `projekt` / `status`, treść **dokładnie jak podyktowana**, na końcu sekcja `## Ślad`. Pełny opis formatu: `PjM\skrzynka\README.md`.

2. **Czytają wszyscy agenci, na każdym otwarciu** (punkt 4b). Kanał z jednym czytelnikiem zawsze czeka, aż ten otworzy sesję — dlatego skrzynkę czytają wszyscy.

3. **Puste pole `projekt` znaczy „PjM rozstrzygnie", a nie „niczyje".** Agent, który widzi wpis bez przypisania i rozpoznaje w nim swoją sprawę, bierze go i dopisuje swój kod. Nie rozpoznaje — zostawia; PjM przypisze na swoim otwarciu.

4. **Routing — trzy tory, wybierasz jeden:**

   - **Deliverable** (coś ma powstać, ktoś ma odpowiedzieć, jest termin) → **na tablicę**, `tablica.py dodaj --projekt KOD`. Notatka zaczyna się od `ZE SKRZYNKI DD-MMM-RRRR:` i zawiera treść wpisu. Prefiks jest po to, żeby przy odtwarzaniu pamięci było widać, że pozycja przyszła z terenu, a nie z sesji.
   - **Drobiazg bez daty** (poprawka w narzędziu, notatka do sprawdzenia przy okazji) → **`zadania.md` Twojego projektu**. Na tablicę tego nie wnosimy — tablica jest listą Miko, nie listą Twoich sprzątań.
   - **PII** (dane osobowe, numery, skany) → **osobny plik w `C:\projekty-IOMJB-dane\{projekt}\`**, a w skrzynce zostaje **sama ścieżka**. Repo idzie na GitHub; bramka 3 z `CLAUDE.md` obowiązuje też tutaj.

5. **Po zroutowaniu oznaczasz wpis i zapisujesz ślad:** `skrzynka.py podjety --wpis FRAGMENT --slad "tablica WZS-014"`. Ślad jest obowiązkowy — wpis, który zniknął z listy bez informacji dokąd poszedł, jest gorszy niż wpis nieprzeczytany. Gdy sprawa jest domknięta w tej samej sesji: `skrzynka.py zrobiony`, który przenosi plik do `skrzynka\_archiwum\`.

6. **Wpisu nie kasujesz i nie przepisujesz jego treści.** Treść jest dyktowana i zostaje słowo w słowo — Twoja interpretacja idzie do notatki na tablicy, nie do wpisu.

7. **Leżakujący wpis meldujesz Miko.** `skrzynka.py nowe` oznacza `[ZALEG]` powyżej 2 dni i `[PILNE]` powyżej 7. Jeśli coś Twojego leży z takim znacznikiem, mówisz o tym w meldunku otwarcia (punkt 1.7), zanim przejdziesz do pracy.

8. **Skrzynka nie jest kanałem PjM → agent.** Jednorazowe polecenia PjM idą na tablicę (sekcja 5.9). Skrzynka przyjmuje wyłącznie to, co pochodzi od Miko z terenu.

## 6. Układ plików projektu

Katalog projektu widać w explorerze i to jest pierwsza rzecz, którą Miko ma przed oczami. Ma się czytać bez tłumaczenia. **Standard ustala PjM, porządek robi agent u siebie** — bo tylko on wie, który plik jeszcze żyje.

### 6.1 Co leży w korzeniu

1. **Zestaw agenta** — `CLAUDE.md`, `PREFERENCJE_MIKO.md`, `ZASADY_SESJI.md`, `ZASADY_ODPOWIEDZI.md`, `KANALY.md`, `NARZEDZIA.md`, `LOG_RUNOW.md`, `LOG_STYLU_KOMUNIKACJI.md`, katalog `sessions\`. Do tego `DZIENNIK_MIKO.md` i `VISION_{KOD}.md`.

2. **Żywa specyfika projektu** — proces, wiedza dziedzinowa, rejestry, otwarte punkty. To, co agent faktycznie otwiera w trakcie pracy.

3. **Nic więcej.** Każdy plik w korzeniu musi mieć odpowiedź na pytanie „kiedy go ostatnio otwierałem i po co".

4. **Sekcja `## OTWARCIE` w `CLAUDE.md`** — jeśli projekt ma własne kroki otwarcia sesji (pull danych, skrypt na skrzynkę, sprawdzenie zewnętrznego systemu), opisujesz je tam: co uruchomić, czym i po co. Agent wykonuje je po krokach wspólnych, jako punkt 6 sekcji 1. **Nagłówek brzmi dokładnie `## OTWARCIE`** — jednakowy u wszystkich, żeby dało się jednym grepem sprawdzić, który projekt ma własne kroki. Opis pod nagłówkiem jest już Twój.

### 6.2 Co idzie z korzenia

1. **`_archiwum\`** — sprawy zamknięte, drogi porzucone, jednorazowe instrukcje po wykonaniu. Plik przenoszony dostaje na górze jedną linię: dlaczego zamknięty i z jaką datą.

2. **Podkatalog tematyczny** — gdy jednego rodzaju plików jest kilka (`sprawy\`, `szablony\`, `narzedzia\`, `skills\`).

3. **`-dane`** — cokolwiek zawiera PII.

### 6.3 Kiedy plik jest kandydatem do archiwum

Trzy warunki naraz, sprawdzane przez agenta projektu:

1. Nietknięty od **ponad 30 dni** (`git log -1 --format=%ad -- plik`).
2. **Żaden żywy plik go nie przywołuje** — sprawdzasz `grep`, nie pamięcią.
3. Opisuje **stan, który już nie obowiązuje** — zamkniętą sprawę, wykonaną wysyłkę, odwołaną regułę.

Spełnione wszystkie trzy: przenosisz i meldujesz. Spełnione dwa: zostawiasz i pytasz Miko przy okazji.

### 6.4 Zakaz duplikatów

1. **Dwa pliki o tej samej roli to błąd, nie wariant.** Jeden zostaje, drugi idzie do `_archiwum\` z adnotacją, co go zastąpiło.

2. **Jeden system logu sesji: `sessions\RRRR-MM-DD.md`, jeden plik na sesję.** Kumulatywne `SESJE.md` z poprzedniego ustroju zamyka się nagłówkiem „historia do RRRR-MM-DD" i zostaje jako archiwum; nowe wpisy idą już wyłącznie do `sessions\`.

3. **Nazwy plików standardowych: WIELKIE_LITERY z podkreślnikiem.** `LOG_RUNOW.md`, nie `LOG-RUNOW.md` — dywiz i podkreślnik w jednym katalogu dają dwa pliki, których nikt nie zauważy.

## 7. Higiena

1. **Jedna sesja = jeden projekt.** Przy próbie przeskoku przypominasz o zamknięciu bieżącej.

2. **Jeden projekt = jedno okno piszące.** Drugie okno czyta i analizuje, nie zapisuje.

3. **Logi sesji dopisujesz, nigdy nie nadpisujesz.**

4. **Sprawdzasz datę systemową przed pierwszym zapisem.** Lekcja 12.08.2026: laptop chodził dobę do przodu i doba weszła do commitów, nazw plików i rejestrów w pięciu projektach.

5. **Zapis do tablicy weryfikujesz po zapisie.** Excel otwarty na pliku blokuje zapis, `openpyxl` kończy błędem, a commit i tak wygląda na udany. Sprawdzasz, czy zmiana jest w pliku, nie w logu konsoli.
