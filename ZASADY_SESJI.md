<!-- KOPIA — nie edytuj. Zrodlo: C:\projekty-IOMJB\_STANDARDY\ZASADY_SESJI.md -->
> **Kopia z 2026-10-15.** Ten plik zmienia wylacznie PjM w zrodle `_STANDARDY\ZASADY_SESJI.md` i rozsyla `sync-standardy.py`. Zmiana wpisana tutaj zniknie przy najblizszej synchronizacji.

# ZASADY SESJI — otwarcie, przebieg, zamknięcie

Obowiązuje każdego agenta IOMJB. Zastępuje `PROCEDURA_SESJI.md` od 2026-08-22. Zmienia ten plik wyłącznie PjM razem z Miko.

Sesja to jeden projekt i jedno okno piszące. Ma początek, limit i domknięcie — nie kończy się wtedy, gdy skończy się materiał, tylko wtedy, gdy wyczerpie się limit albo zadanie.

## 1. Otwarcie

1. **Wstajesz z roli.** Czytasz `CLAUDE.md` swojego projektu, potem `PREFERENCJE_MIKO.md`, `ZASADY_ODPOWIEDZI.md` i ten plik. Meldujesz jedną linią, że je przeczytałeś.

2. **Odtwarzasz pamięć z logów.** Ostatni plik w `sessions/` — co było zrobione, co zostało otwarte, gdzie utknęliśmy. Jeśli poprzednia sesja nie ma logu albo nie ma commita, domykasz ją, zanim ruszysz dalej.

3. **Odbierasz swoją pocztę** (sekcja 5). Merytoryczne wiadomości czytasz w całości razem z załącznikami; skany bez warstwy tekstowej renderujesz do PNG (`pymupdf`, `get_pixmap(dpi=150)`) i czytasz wzrokiem. Załączniki zapisujesz do `C:\projekty-IOMJB-dane\{projekt}\`, nigdy do repo. Streszczasz Miko numerowaną listą **z licznikiem** — ile przyszło, ile merytorycznych.

4. **Przeglądasz swoje wiersze na tablicy** — `python C:\projekty-IOMJB\PjM\narzedzia\tablica.py pokaz --projekt KOD`. Rozjazd między tablicą a stanem sprawy prostujesz od razu, przed pracą.

4a. **Czytasz `PjM\zmiany-miko.md` od daty swojej ostatniej sesji** — to, co Miko przestawił ręcznie w podglądzie: statusy, terminy, przypisania do projektów. Wpis z Twoim kodem w ID znaczy, że stan Twojej sprawy zmienił człowiek, a nie narzędzie (`KANALY.md` 1.10).

5. **Przeglądasz swoje terminy w kalendarzu** — czy to, co ma datę, w kalendarzu jest, i czy data nadal jest aktualna.

5a. **Odświeżasz akta sprawy, jeśli Twój projekt je ma.** Czytasz `FAKTY.md` (rejestr ustaleń z odsyłaczami do dokumentów) i sprawdzasz, że wiesz, gdzie leżą same akta — ścieżki są w sekcji **`## ZRODLA`** Twojego `CLAUDE.md`. Kontekst poprzedniej sesji **nie przenosi się**: to, że wczoraj czytałeś akta, dziś nie znaczy nic.

6. **Wykonujesz własne kroki otwarcia** — te, które ma tylko Twój projekt. Żyją w sekcji **`## OTWARCIE`** Twojego `CLAUDE.md`; jeśli tej sekcji nie ma, znaczy, że własnych kroków nie masz.

   Przykłady: WZS ciągnie zgłoszenia z formularza MP Inwestycje, IOM odpala `nest-sweep.ps1` na korespondencję bankową. Standard nie wymienia tych kroków po nazwie, bo zna je projekt, nie wspólny plik — ale **wie, że istnieją i że robi się je tutaj**, po krokach wspólnych, a przed meldunkiem.

7. **Meldujesz gotowość — i na tym kończysz.** Otwarcie sesji to odzyskanie świadomości przez agenta, nie praca (decyzja Miko 25.08.2026). Meldunek ma **dwie części i nic poza nimi**:

   **✅ ZROBIONE** — jedna linia na krok, sam fakt wykonania. „Pamięć z logu odtworzona", „tablica przejrzana", „poczta: 53 wiadomości, 0 merytorycznych". Bez treści kroku, bez szczegółów, bez wniosków. Miko poprosi o zawartość, jeśli będzie jej chciał.

   **BRIEF** — co ma zegar. Terminy bijące dziś i w tym tygodniu, każdy jako fakt z datą. Nagłówek brzmi dokładnie `BRIEF`, żeby Miko wiedział bez czytania, gdzie zaczyna się jedyna część wymagająca uwagi.

   **Czego w meldunku otwarcia NIE MA — żadnego wyjątku:**

   - sekcji **„ℹ️ DECYZJE, KTÓRE PODJĄŁEM SAM"** — agent jeszcze nie zaczął pracować, więc nie ma czego decydować. Decyzja wykonawcza podjęta przed pierwszym zleceniem jest błędem, nie inicjatywą,
   - haczyków, spraw otwartych i rozjazdów do wyjaśnienia,
   - propozycji, listy wariantów, pytania „od czego zaczynamy",
   - **informacji na zapas** — wszystkiego, co agent wie i wyświetla, choć nikt o to nie pytał.

   **Powód:** Miko otwiera agenta z zadaniem w głowie i to on nadaje tempo. Każde zdanie ponad te dwie części każe mu najpierw przeczytać cudzą pracę, zanim powie własną — a to koszt zamiast oszczędności.

## 2. Przebieg — zlecenia i runy

1. **Zlecenie** to prompt Miko z wymaganiem outputu; **run** to jedna tura. Wewnątrz zlecenia runów bywa kilka. Budowa zlecenia — `ZASADY_ODPOWIEDZI.md`: run 1 plan, run 2 produkcja, run 3 i kolejne domykanie. Po zleceniu nie ma pytania o ocenę — ocena jest jedna, na zamknięcie sesji (3.8).

2. **Podajesz licznik** w każdym meldunku: `Zlecenie N/10`.

3. **Limit sesji: 1 godzina 15 minut pracy i maksymalnie 10 zleceń.** Do tego 15 minut na zamknięcie — zamknięcie zawsze trwa i musi się zmieścić w czasie, a nie po nim.

4. **Po dziesiątym zleceniu wystawiasz czerwoną flagę w pierwszej linii**: limit wyczerpany, proponuję zamknięcie. Czas pilnuje Miko, Ty pilnujesz zleceń.

5. **Nie zaczynasz nowego zlecenia pod koniec limitu** ani wtedy, gdy poprzednie ma otwarte haczyki. Zostało mniej niż dwa zlecenia — meldujesz to i pytasz, czy zaczynamy, czy domykamy.

## 3. Zamknięcie

Wszystkie kroki, bez pomijania. Krok już zrobiony weryfikujesz i raportujesz ✅ zamiast powtarzać.

1. **Log sesji** — `{projekt}/sessions/YYYY-MM-DD.md`, według sekcji 4.

2. **Swoje wiersze na tablicy** — każda pozycja, która ruszyła: `tablica.py ustaw --wiersz N --status ... --notatka "..."`; nowe sprawy `tablica.py dodaj --projekt KOD ...`.

3. **Rodzaj przy pozycjach z datą pewną** — rozprawa, termin ustawowy, umówione spotkanie dostają w kolumnie `Rodzaj` wartość `termin pewny` (albo `kamien`, `spotkanie`). Kalendarz zaciąga je sam; pozycja bez tego oznaczenia zostaje wyłącznie na tablicy.

4. **Kalendarza i telefonu nie odpalasz ręcznie** — pilnuje ich automat po zapisie tablicy (sekcja 5.2 i 5.3). Stan sprawdzisz przez `na-telefon.py --podglad` i `na-kalendarz.py --podglad`.

5. **Commit i push** wszystkich edytowanych repo.

6. **Dziennik Miko** — pytasz jednym zdaniem, czy chce coś dopisać do `DZIENNIK_MIKO.md`. Jeśli tak, zapisujesz jego słowa bez przeróbek. Jeśli nie, pomijasz. Sam tam nie piszesz nic.

7. **„Gdzie byłem"** — dopisujesz do logu miejsce i sytuację Miko. To test pamięci na start kolejnej sesji.

8. **Ocena sesji: plus albo minus** — jedyne miejsce, w którym pytasz o ocenę (decyzja Miko 13.10.2026). Wybór strzałkami, nie pytanie otwarte. Plus — nie logujesz nic. Minus — pytasz, czy chce dodać notatkę, i zapisujesz jego słowa bez przeróbek do `LOG_RUNOW.md` (`ocena.py`). Oceny nie komentujesz i nie dyskutujesz z nią.

9. **Raportujesz wykonanie każdego kroku** ✅.

## 4. Log sesji — treść

Log jest jednocześnie pamięcią projektu i raportem dla PjM. Osobnego `DO-PJM.md` nie prowadzimy od 2026-08-22 — PjM czyta logi sesji rodzeństwa.

Log zawiera:

1. **Co zrobione** — konkretnie, z pełnymi ścieżkami powstałych plików.

2. **Decyzje** — czyje, z jaką datą i z jakiego powodu. Decyzja bez powodu jest bezużyteczna przy odtwarzaniu pamięci.

3. **Zdobyta wiedza i ustalenia** — fakty, które wyszły w tej sesji i będą potrzebne później: numery pism, terminy, warunki, cudze stanowiska.

4. **Zmiany statusu spraw** — co domknięte, co przeszło w oczekiwanie, na kim leży piłka.

5. **Co otwarte na następną sesję**, z terminami.

6. **Co dotyczy innych projektów** — sprawa, która wyszła u Ciebie, a należy do kogoś innego. PjM to odbierze i przekaże.

7. **Lessons learned** — refleksje agenta idą tutaj, nie do dziennika Miko.

8. **„Gdzie byłem"**.

Bez PII: dane osobowe, skany i wypełnione formularze zostają w `-dane`, w logu jest tylko ścieżka.

## 5. Kto co prowadzi

**Agent jest egzekutorem razem z Miko, PjM zarządza i śledzi** (decyzja Miko 01.09.2026). Agent ma pełen dostęp do swoich wierszy: zakłada, opisuje, zmienia status, zamyka. PjM nie wykonuje zadań projektów — trzyma priorytety, zależności między pozycjami, spójność tablicy i rejestr, i odpowiada za to, żeby obraz całości się zgadzał.

**Tablica jest kanałem komunikacji, nie tylko rejestrem.** Piszą do niej wszyscy troje: agent melduje, co zrobił, PjM wstawia zlecenia i porządkuje zależności, Miko przestawia z przeglądarki. Dlatego **każdy wpis w notatce jest podpisany autorem** — `[TAX 01-SEP-2026]`, `[PjM 01-SEP-2026]` — a podpis stawia narzędzie samo, na podstawie katalogu, z którego zostało uruchomione (`kanaly_lib.z_podpisem`). Ręczne zmiany Miko mają swój ślad w `PjM\zmiany-miko.md`.

**Powód zmiany wobec ustroju z 22.08.2026:** Miko nie odpala wszystkich agentów codziennie, więc model „każdy prowadzi swoje w swojej sesji" zostawiał obraz całości bez gospodarza aż do następnego otwarcia. Agent nadal prowadzi swoje sprawy, ale zarząd nad nimi ma PjM, a kanały trzymają się razem same (punkty 2 i 3).

1. **Tablica** — swoje wiersze prowadzi agent projektu; PjM zarządza priorytetem, zależnościami i porządkiem całości. Cudzych wierszy nadal nie przepisujesz (5.7).

2. **Kalendarz — robi się sam.** Po każdym zapisie tablicy `na-kalendarz.py` odpala się w tle i dopisuje, przesuwa albo zdejmuje wpisy w kalendarzu `mj.banas@outlook.com`. Wchodzą tam **wyłącznie pozycje o rodzaju `termin pewny`, `kamien` albo `spotkanie`** — zwykły `termin` na tablicy bywa datą ponaglenia, a nie datą pewną. **Twoja robota to oznaczyć rodzaj**, nie wpisywać terminu ręcznie.

3. **Telefon — robi się sam.** `na-telefon.py` odpala się z tego samego automatu, więc lista dnia nadąża za tablicą niezależnie od tego, kto pisał: agent, PjM czy Miko w przeglądarce. Ręcznie odpalasz tylko po to, żeby zobaczyć stan (`--podglad`).

4. **Poczta** — agent odbiera skrzynki swojego projektu:

| Skrzynka | Projekt |
|---|---|
| `mj.banas@outlook.com` | WZS — gestorzy, klienci, Mariusz |
| `IOMJB@proton.me` | IOM — KRS, e-Doręczenia, Nest Bank, Fakturomania |
| `IOMJB_Jadwiga@proton.me` | IOM — korespondencja Prezes Zarządu |
| `IOMJB_consultant@proton.me` | 4EN |
| `IOMJB_Mikolaj@pm.me` | TAX — kancelaria 271/26, urzędy niemieckie, aplikacje o pracę |
| `banamicobo@icloud.com` | PRV i KOS — sprawy prywatne |
| `mikolajbanas@gmail.com`, `banamicobo@gmail.com`, `IOMJB@pm.me` | PjM — reszta, w większości szum |

5. **`IOMJB_Mikolaj@pm.me` czyta wyłącznie TAX** — od 01.09.2026, kiedy ODS (odprawa Sennheiser) został scalony z TAX w jeden projekt „finanse i podatki" (decyzja Miko). Skrzynka przestała być dzielona; podział wątków ODS/TAX zniesiony.

   - TAX bierze całość: kancelarię w sprawie 271/26, urzędy i instytucje niemieckie (Bundesagentur für Arbeit, Finanzamt, ELSTER, Commerzbank, rezydencja, ALG) oraz odpowiedzi rekrutacyjne i potwierdzenia zgłoszeń.
   - **Dziennik aplikacji o pracę prowadzi CMI** (`CMI\aplikacje-o-prace.md`); TAX pilnuje rytmu wysyłek i trzyma je jako dowód do sprawy odprawy i do ALG.

6. **Wiadomość spoza swojego zakresu** zostawiasz nietkniętą i nie odpowiadasz w cudzej sprawie.

7. **Sprawa, która wyszła u Ciebie, a należy do innego projektu, idzie OD RAZU NA TABLICĘ** jako nowy wiersz z kodem tamtego projektu (`tablica.py dodaj --projekt KOD`). W notatce piszesz, skąd sprawa się wzięła i kto ją zgłosił. Do logu sesji wpisujesz to samo w punkcie „co dotyczy innych projektów" — jako ślad, nie jako kanał przekazania.

   **To jedyny przypadek, w którym zakładasz wiersz cudzego projektu.** Istniejących cudzych wierszy nadal nie ruszasz — ani treści, ani statusu, ani deadline'u. Zakładasz nowy i zostawiasz go agentowi tamtego projektu.

   Powód: `DO-PJM.md` zniesiony 22.08.2026. Przekazanie przez plik pośredni wymagało, żeby ktoś go przeczytał i przeniósł; przy siedmiu projektach zgłoszenia leżały tam tygodniami (IOM miał 41 nieodebranych pozycji).

7a. **Zrobiłeś coś na cudzym podwórku — zostawiasz właścicielowi wpis w skrzynce** (decyzja Miko 18.09.2026; pierwszy przypadek: TAX przejmuje od CMI `aplikacje-o-prace.md`). Dotyczy każdej akcji na czyimś repo, pliku albo sprawie za decyzją Miko: zabranie pliku, przejęcie sprawy, zmiana rejestru. Trzy ruchy, wszystkie w tej samej sesji:

   - **Wpis skrzynki z nadawcą:** `skrzynka.py dodaj --zrodlo agent --od TWÓJ_KOD --projekt KOD_WŁAŚCICIELA --tresc "..."` (`--od` bierze się sam z katalogu roboczego). Treść ma stały szkielet: **co zrobiłem · na czym (pełna ścieżka źródła i celu) · decyzja Miko z datą · co właściciel ma u siebie zmienić.** Właściciel widzi wpis na swoim otwarciu (4b), PjM na swoim; leżakujący wpis krzyczy `[ZALEG]`.
   - **Stub w miejscu zabranego pliku:** jedna linia u właściciela — `Przeniesiony do {ścieżka} — decyzja Miko DD.MM.RRRR, wpis skrzynki {nazwa pliku}`. **To jedyna postać zapisu w cudzym repo, jaką wolno zrobić** — bez tego agent, który sięgnie po plik z pamięci, trafi na brak zamiast na wskazówkę.
   - **Sekcja 6 własnego logu** — ślad, tak jak w punkcie 7.

   **Rachuba właściciela to status wpisu.** Właściciel na swoim otwarciu robi `podjety` → `zrobiony --slad "..."` — dopiero to zamyka przekazanie, a plik w `skrzynka\_archiwum\` jest rejestrem: kto, kiedy, jaka decyzja, co zrobiono po stronie odbiorcy. Osobnego rejestru przekazań nie prowadzimy.

8. **Narzędzie do odczytu:** `pwsh -File C:\projekty-IOMJB\PjM\narzedzia\poczta-przeglad.ps1 -Od RRRR-MM-DD -Skrzynka fraza`. Pojedyncze wiadomości i szkice: `_STANDARDY\poczta-czytaj.py` i `poczta-wyslij.py`. Szczegóły kont i pułapki: `POCZTA-IMAP.md`.

### 5.9 Zadania zlecane przez PjM — jednorazowe polecenia dla agenta

Z pracy PjM z Miko wychodzą czasem polecenia dla konkretnego agenta: przejrzyj coś u siebie, dostosuj się do zmienionego standardu, sprawdź stan swoich wierszy. To nie są sprawy projektu — to jednorazowe akcje na jego repo albo na jego pozycjach (decyzja Miko 23.08.2026).

1. **PjM zakłada je jako normalny wiersz z kodem tamtego projektu** (`tablica.py dodaj --projekt KOD`). Nie ma osobnego kanału ani pliku pośredniego — przekazywanie przez plik już raz nie zadziałało (`DO-PJM.md`, zniesiony 22.08.2026).

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

Część projektów prowadzi sprawy oparte na dokumentach: pisma, umowy, protokoły, akta procesowe. Tam każda liczba i każde twierdzenie prawne ma swoje miejsce w papierze — i tylko stamtąd wolno je brać (zasada wprowadzona 23.08.2026 po tym, jak agent policzył odprawę ze wzoru znanego z ogólnej wiedzy zamiast z akt).

1. **Sekcja `## ZRODLA` w `CLAUDE.md` projektu** wymienia dokumenty źródłowe pełnymi ścieżkami, z jednym zdaniem o tym, co każdy zawiera. Nagłówek brzmi dokładnie `## ZRODLA` — tak samo u wszystkich, żeby dało się to sprawdzić jednym grepem. Hook czyta tę sekcję i **przypomina o niej przy każdym prompcie**, więc lista jest przed oczami zawsze, a nie tylko na starcie.

2. **`FAKTY.md` w repo projektu** to rejestr ustaleń: fakt, wartość, data, **odsyłacz do akt** (`plik:linia`). Krótki plik zamiast trzymania całych akt w kontekście — akta otwierasz wtedy, gdy ich potrzebujesz, a nie na wszelki wypadek.

3. **Fakt bez odsyłacza nie wchodzi do `FAKTY.md`.** Jeśli czegoś nie ma w aktach, a wiesz to od Miko — wpisujesz `[Miko DD-MMM-RRRR]`. Jeśli nie wiesz skąd, nie wpisujesz wcale.

4. **Przed policzeniem czegokolwiek otwierasz akta.** Kwota, staż, termin ustawowy, wysokość roszczenia — to wszystko czyta się z dokumentu w tej sesji, nie z pamięci poprzedniej.

5. **PII zostaje w `-dane`.** `FAKTY.md` żyje w repo i trzyma wartości oraz odsyłacze; same dokumenty leżą poza repo.

6. **Gdy akta należą do innego projektu, pytanie też do niego należy.** Sprawę prowadzi ten, kto ma jej akta i mandat — reszta bierze z niej wynik, nie prowadzi jej równolegle.

## 6. Układ plików projektu

Katalog projektu widać w explorerze i to jest pierwsza rzecz, którą Miko ma przed oczami. Ma się czytać bez tłumaczenia. **Standard ustala PjM, porządek robi agent u siebie** — bo tylko on wie, który plik jeszcze żyje.

### 6.1 Co leży w korzeniu

1. **Zestaw agenta** — `CLAUDE.md`, `PREFERENCJE_MIKO.md`, `ZASADY_SESJI.md`, `ZASADY_ODPOWIEDZI.md`, `KANALY.md`, `LOG_RUNOW.md`, katalog `sessions\`. Do tego `DZIENNIK_MIKO.md` i `VISION_{KOD}.md`.

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
