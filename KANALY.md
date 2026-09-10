<!-- KOPIA — nie edytuj. Zrodlo: C:\projekty-IOMJB\_STANDARDY\KANALY.md -->
> **Kopia z 2026-09-10.** Ten plik zmienia wylacznie PjM w zrodle `_STANDARDY\KANALY.md` i rozsyla `sync-standardy.py`. Zmiana wpisana tutaj zniknie przy najblizszej synchronizacji.

# KANAŁY — tablica, telefon, kalendarz

Trzy miejsca, w których żyje robota Miko. Agent prowadzi swoje wiersze na tablicy, PjM zarządza priorytetem, zależnościami i porządkiem całości, a kalendarz i telefon nadążają za tablicą **automatycznie** (od 01.09.2026). Zmienia ten plik wyłącznie PjM razem z Miko.

Podział ról w jednym zdaniu: **tablica** to przegląd wszystkiego, **telefon** to lista na dziś, **kalendarz** to daty pewne.

## 1. Tablica — `PjM\tablica-zadan.xlsx`

Podgląd w przeglądarce: `PjM\tablica.html` (`narzedzia\tablica-html.py`), edycja ręczna przez `narzedzia\tablica-serwer.py` na `127.0.0.1:8765`. Agent pisze przez `narzedzia\tablica.py` (`pokaz`, `ustaw`, `dodaj`).

### 1.1 Format wpisu — obowiązkowy

Pozycja ma **dwie osobne kolumny**: nazwę i opis. Lista ma się czytać jednym rzutem oka, a szczegóły być pod ręką bez rozpychania wiersza.

1. **`Zadanie` — `[KOD] HEADLINE`.** Kod projektu w nawiasie **kwadratowym, na początku**, potem nazwa wielkimi literami. Nazwa mówi, co to za rzecz — nie czynność w toku.

2. **`Opis` — JEDNO zdanie w formie dokonanej.** Forma dokonana wymusza deliverable: opisujesz stan po zakończeniu, nie to, czym się zajmujesz. Z tego zdania ma być widać, po czym poznać, że zadanie jest zrobione.

Wzory:

> `[PRV] PROTEST PRZECIWKO FERMIE ŚWIŃ` · opis: `Podpisy pod wnioskiem o zmianę MPZP zebrane i złożone w gminie.`
>
> `[4EN] SUMMARY DECK DLA SPONSORA` · opis: `Deck pptx stworzony i prezentacja przygotowana dla Bartka.`

**Kontekst, powody i historia idą do notatki, nie do opisu.** Opis to jedno zdanie; wiersz rozpisany na trzy zdania z uzasadnieniem zamienia tablicę w tekst do czytania.

Czego nie wpisujemy jako nazwy: „prace nad deckiem", „temat prezentacji", „ogarnąć deck" — to opisy zajęcia, nie rezultatu. Zadania bez deliverable nie da się odhaczyć, bo nikt nie wie, kiedy się skończyło.

**Prefiks idzie za projektem.** Przepięcie pozycji do innego projektu zmienia ID i prefiks nazwy razem — narzędzie robi to samo.

### 1.1a Nazwa i opis — para, nie powtórzenie

Nazwa i opis odpowiadają na dwa różne pytania. Mieszanie ich sprawia, że lista czyta się jak dziennik rzeczy zrobionych, choć żadna z nich nie jest jeszcze zrobiona.

1. **Nazwa nazywa RZECZ, bez czasownika.** `DWA MAILE DO WSPÓLNICZKI`, `RAPORT FINDINGS DLA GRUPY WB`, `HOTEL DLA MIESZKAŃCÓW KOŚCIELNEJ`. WIELKIMI LITERAMI, bo to nagłówek, a nie zdanie.

2. **Opis mówi, co ma być dowiezione — z czasownikiem WIELKIMI LITERAMI.** `Oba maile WYSŁANE i odbiór POTWIERDZONY.`, `Raport STWORZONY i PRZEKAZANY grupie WB.` Czasownik jest najważniejszym słowem opisu, bo to on wyznacza warunek zamknięcia pozycji — dlatego rzuca się w oczy.

3. **Źle:** `DWA MAILE DO WSPÓLNICZKI WYSŁANE` w nazwie. Czasownik w nazwie zabiera opisowi jego jedyną robotę i sugeruje, że rzecz jest już za nami.

4. **Narzędzia podpowiadają, nie blokują.** `tablica.py` i okno „dodaj zadanie" wypisują uwagę, gdy nazwa wygląda na zdanie z czasownikiem albo gdy opis nie ma słowa pisanego wielkimi literami. Reguła jest heurystyczna — ostatnie słowo należy do człowieka.

### 1.2 Kolumny

`ID` · `Projekt` · `Zadanie` · `Opis` · `Do kiedy` · `Status` · `Notatka` · `Blokuje` · `Zablokowane przez` · `Notatka USER` · `Zrodlo` · `Godziny` · `Link` · `Od`

**Kolumna terminu nazywa się `Do kiedy`** (`by when` w wersji angielskiej) — jedno słowo znaczy termin wszędzie: na tablicy, w podglądzie i na liście partnera. W kodzie klucz nadal brzmi `deadline`; `kanaly_lib` rozwija aliasy nagłówków, więc napis w arkuszu można zmienić bez ruszania narzędzi.

W podglądzie kolumna `Notatka` ma nagłówek **Notatka agenta** — dla odróżnienia od `Notatka USER`.

**Kolumn `Pilne` i `Ważne` nie ma.** Pilność wynika z deadline'u: coś ma termin albo go nie ma.

**`Notatka USER` to jedyna kolumna, której agent nie pisze** (nagłówek zmieniony z `Notatka Miko` 25.08.2026; klucz w kodzie nadal brzmi `notatka miko`, alias rozwija `kanaly_lib`). Miko dopisuje tam swoje uwagi z podglądu w przeglądarce, przyciskiem ✎. Agent ją **czyta na otwarciu sesji** razem z resztą wiersza i traktuje jak polecenie albo kontekst od człowieka — nie kasuje jej i nie poprawia. Swoje ustalenia agent wpisuje do kolumny `Notatka`.

### 1.3 Do kiedy (termin)

1. **Data w formacie `DD-MMM-RRRR` albo pusto** — `12-STY-2026` po polsku, `12-JAN-2026` po angielsku. Miesiąc słownie znosi dwuznaczność `DD/MM` kontra `MM/DD` — `03-04-2026` znaczyło dwie różne rzeczy dla dwóch czytelników. Żadnych „koniec sierpnia”, „przed pierwszą fakturą”, „~02.09”. Nie znasz dokładnej daty — wybierz najbliższą sensowną i wpisz ją jako datę; przybliżenie w notatce, nie w kolumnie. Narzędzia przyjmują też starsze zapisy (kropki, ukośniki) i przeliczają je same, a jedynym miejscem, gdzie format żyje, jest `kanaly_lib.sformatuj_date`.

2. **Przy statusie `waiting for 3rd party` termin to data ponaglenia**, nie termin wykonania. Bez daty szarpnięcia sprawa leży miesiącami — wniosek do ZUK z 15 lipca ruszył dopiero po wezwaniu z 18 sierpnia.

3. **Brak daty jest dozwolony** i znaczy: robota bez zegara. Taki wiersz nie dostaje koloru i nie wchodzi na listę dnia.

### 1.4 Dwa kolory — projekt i termin

Tablica niesie **dwa niezależne kolory** i nigdy nie mieszają się one w jednej komórce:

1. **Kolor projektu** — na `ID` i na kodzie w kolumnie `Projekt`. Paleta jest jedna dla całego systemu i siedzi w `kanaly_lib.KOLORY_PROJEKTOW`: PjM stalowy, WZS szałwiowy, IOM błękitny, 4EN bursztynowy, CMI wrzosowy, TAX terakota, ODS morski, PRV różowy, KOS oliwkowy. Ten sam kolor dostaje pas projektu na osi czasu, a najechanie myszą pokazuje pełną nazwę projektu (`kanaly_lib.NAZWY_PROJEKTOW`).

2. **Kolor terminu** — na komórce z **nazwą zadania**. Maluje ją `tablica.py` przy każdym zapisie i `kolory-tablicy.py` przy sprzątaniu.

| Ile dni do terminu | Kolor |
|---|---|
| poniżej 7 | **czerwony** |
| 7–14 | **pomarańczowy** |
| 14–21 | **żółty** |
| powyżej 21 albo brak daty | bez koloru |

Po terminie: czerwony, jak przedział poniżej 7 dni.

### 1.5 Statusy — sześć i tylko sześć

1. **`in progress`** — piłka po naszej stronie, robota trwa.
2. **`waiting for 3rd party`** — sprawa żyje, ale czekamy na kogoś **spoza tablicy**: organ, gestora, kontrahenta, sąd, klienta. Nazwę wpisujemy do kolumny **`Zablokowane przez`** jako `3rd party: ENEA Operator`. Bez nazwy status jest bezużyteczny.
3. **`blocked`** — zadanie nie może ruszyć, bo czeka na **inną pozycję z tej tablicy**. ID blokerów wpisujemy do kolumny **`Zablokowane przez`** (sekcja 1.6). Narzędzie odmawia zapisu tego statusu bez ID.
4. **`waiting`** — może poczekać, nikt na nic nie czeka, odkładamy świadomie.
5. **`parked`** — zawieszone, wróci później.
6. **`done`** — zamknięte.

**Odblokowanie dzieje się samo.** Gdy **ostatni** z blokerów przechodzi na `done`, pozycja czekająca na nie wraca na `in progress` — robi to `tablica.py` i serwer podglądu, w tym samym zapisie. Nie trzeba tego pamiętać ani obchodzić ręcznie.

**Kiedy `blocked`, a kiedy `waiting for 3rd party`:** jeśli potrafisz wskazać ID pozycji, która musi się skończyć pierwsza — `blocked`. Jeśli czekasz na człowieka albo instytucję, których na tablicy nie ma — `waiting for 3rd party`. Przykład: umowa WB Electronics blokuje przeniesienie udziałów i umowę zlecenie Mikołaja; te dwie pozycje nie są otwarte, tylko `blocked` z ID umowy.

### 1.6 Dwa kierunki blokady — dwie osobne kolumny

Blokada ma dwie strony i **każda ma własną kolumnę**. Trzymanie obu w jednym miejscu zaciera, czy pozycja blokuje, czy jest blokowana.

1. **`Blokuje`** — kierunek **wychodzący**: ID pozycji, które ta sprawa wstrzymuje. **Bez trzeciej strony** — my nikogo z zewnątrz nie blokujemy. Wiersz z wypełnioną kolumną „Blokuje" wchodzi na listę dnia niezależnie od daty; blokada jest pilnością nawet bez zegara.

2. **`Zablokowane przez`** — kierunek **przychodzący**: co wstrzymuje tę pozycję. Dwie dopuszczalne treści, mogą wystąpić razem:
   - **ID pozycji** z tablicy, po przecinku: `IOM-002, IOM-011`
   - **`3rd party: nazwa`** — gdy czeka się na kogoś spoza tablicy: `3rd party: ENEA Operator`

   Zapis łączony wygląda tak: `3rd party: UP Grodzisk | IOM-002`. Narzędzie odrzuca wpis, w którym nie ma ani ID, ani trzeciej strony.

Przykład: `IOM-002` (przeniesienie udziałów) i `IOM-011` (umowa zlecenie) mają w „Blokuje" ID pozycji z pierwszą fakturą. Ta pozycja ma w „Zablokowane przez" wpisane `IOM-002, IOM-011`. Ten sam fakt z dwóch stron — i dopiero druga strona pozwala odblokować sprawę automatycznie.

4. **W podglądzie obie kolumny wypełnia się z listy**, nie z ręki. Przycisk ✎ otwiera okno z pozycjami do zaznaczenia — **najpierw z tego samego projektu**, potem reszta, z filtrem po ID i nazwie. W „Zablokowane przez" pierwsza pozycja okna to `3rd party` z polem na nazwę.

5. **Status `blocked` czyta kolumnę „Zablokowane przez"**. Bez ID w tej kolumnie narzędzie odmawia ustawienia tego statusu.

6. **Odblokowanie czeka na wszystkie blokery.** Pozycja wymieniająca trzy ID wraca na `in progress` dopiero, gdy wszystkie trzy są zamknięte — zamknięcie pierwszego z nich niczego nie uruchamia.

### 1.7 Archiwum

Wiersze `done` i `parked` przenosimy do arkusza **ARCHIWUM** w tym samym pliku. Aktywna tablica pokazuje tylko sprawy żywe; historia zostaje pod ręką.

### 1.8 Kto prowadzi

Swoje wiersze prowadzi agent swojego projektu — on zna deliverable. PjM prowadzi wiersze `PjM` i `PRV`, a nad resztą ma zarząd: priorytet, zależności, porządek. **Notatka jest podpisana autorem** (`[TAX 01-SEP-2026]`) — podpis stawia narzędzie samo, bo od 01.09.2026 tablica jest kanałem komunikacji między agentem, PjM i Miko, a kanał bez nadawcy nie działa.

**Jeden wyjątek:** sprawę, która wyszła u Ciebie, a należy do innego projektu, **zakładasz jako nowy wiersz z kodem tamtego projektu**. W notatce piszesz, skąd się wzięła i kto ją zgłosił. Istniejących cudzych wierszy nadal nie ruszasz. Szczegóły: `REFERENCJA_SESJI.md` 5.7.

### 1.9 Stałe ID pozycji — jedyny sposób adresowania

**Każda pozycja ma stałe ID w formacie `KOD-NNN`** — `PJM-014`, `WZS-003`, `IOM-025`. Nadawane przy zakładaniu wiersza, nigdy nie zmieniane. Kolumna `ID` jest pierwsza w arkuszu.

1. **Adresujesz po ID, nigdy po numerze wiersza.** `tablica.py ustaw --id WZS-012 --status done`. Numery wierszy w Excelu pływają przy każdym dodaniu, usunięciu i archiwizacji; zapis po numerze sprzed kilku minut trafia w cudzy wiersz.

2. **Kod projektu w ID mówi, czyja to pozycja.** Nie ruszasz wiersza, którego ID zaczyna się cudzym kodem — ani treści, ani statusu, ani deadline'u. Jedyny wyjątek: zakładanie **nowej** pozycji dla innego projektu (sekcja 1.8).

3. **ID nie wraca do obiegu.** Numer liczy się z maksimum w obu arkuszach, także w ARCHIWUM — zarchiwizowana sprawa zachowuje swój identyfikator na zawsze. Dzięki temu ID w logu sesji sprzed miesiąca nadal wskazuje tę samą sprawę.

4. **Swoje ID znajdujesz komendą `tablica.py pokaz --projekt KOD`** — pierwsza kolumna wypisu. Podgląd w przeglądarce pokazuje je w kolorowym znaczniku przy każdym wierszu.

5. **Po zapisie sprawdź plik, nie log konsoli.** Excel otwarty na pliku blokuje zapis, `openpyxl` kończy błędem, a commit i tak wygląda na udany.

6. **Podgląd w przeglądarce filtruje wielokrotnie.** Kolumny Projekt i Status mają panele z checkboxami — można zostawić na widoku kilka projektów naraz, nie tylko jeden albo wszystkie. Filtry łączą się warunkiem AND między kolumnami, OR w obrębie jednej. Wybór przeżywa odświeżenie strony.

7. **Treść zadania zmienia się przyciskiem ✎ i oknem edycji**, nie klikiem w komórkę — to zdanie, które ma trzymać format, więc wymaga świadomego otwarcia. Okno pokazuje wzór i ostrzega, gdy nazwa nie trzyma formatu `HEADLINE (KOD) — opis`.

8. **Przepięcie pozycji do innego projektu robi Miko** z listy wyboru w podglądzie przeglądarkowym (`tablica-serwer.py`). Serwer nadaje wtedy **nowe ID z kodem nowego projektu** i zostawia ślad po starym w notatce — bo to po kodzie w ID agent poznaje, która pozycja jest jego. Agent sam nie przepina cudzych spraw do siebie ani swoich do kogoś innego; zgłasza to Miko.

### 1.10 Ręczne zmiany Miko — czytasz je na otwarciu sesji

Miko steruje tablicą sam, z podglądu w przeglądarce (`tablica-serwer.py` na `127.0.0.1:8765`). Zmienia tam **status, deadline i przypisanie do projektu**. To jest normalna droga, nie wyjątek — tablica ma być sterowalna ręcznie.

1. **Każda taka zmiana ląduje w `PjM\zmiany-miko.md`** — data, ID pozycji, projekt, nazwa zadania, pole oraz wartość przed i po.

2. **Czytasz ten plik na otwarciu sesji**, zaraz po przejrzeniu swoich wierszy. Wpis dotyczący Twojego kodu w ID znaczy, że człowiek przestawił coś w Twojej sprawie między sesjami — i że stan, który pamiętasz z ostatniego razu, jest nieaktualny.

3. **Nie cofasz zmian Miko** i nie „poprawiasz" ich pod swoją wersję stanu. Jeśli zmiana wygląda na pomyłkę albo kłóci się z tym, co wiesz o sprawie, mówisz mu to — decyzja jest jego.

4. **Zmiana przypisania do projektu przenosi pozycję razem z ID.** Wiersz, który wczoraj był `WZS-003`, dziś może być `IOM-026` — ślad po starym identyfikatorze zostaje w notatce. Dlatego pozycja, której nie znajdujesz pod znanym ID, mogła zostać przepięta, a nie zniknąć.

5. **Log jest dopisywany, nigdy nadpisywany.** Przy przeglądzie czytasz wpisy od daty ostatniej swojej sesji, nie cały plik.

### 1.11 Kamień milowy — punkt, po którym projekt jest w innym stanie

Zwykły termin mówi „to ma być zrobione do". Kamień milowy mówi „od tego dnia projekt jest gdzie indziej": pierwsza faktura, wpis do rejestru, rozprawa, koniec zatrudnienia, zamknięcie roku. Na osi czasu w tablicy jedno rysuje się kropką, drugie rombem — dlatego potrzebują rozróżnienia w zapisie, a nie w pamięci agenta.

1. **Zapis:** `[KOD] M: HEADLINE` — po prefiksie projektu litera `M`, dwukropek, spacja i nazwa. Wzór: `[IOM] M: PIERWSZA FAKTURA WYSTAWIONA`.
2. **Kamień milowy zawsze ma deadline.** Bez daty nie jest kamieniem milowym, tylko życzeniem — i nie pojawi się na osi.
3. **Każdy agent odpowiada za to, żeby kamienie milowe z jego `VISION_*.md` miały pozycję na tablicy z datą.** Wizja bez odbicia na tablicy jest niewidoczna dla wszystkich pozostałych.
4. **Nie mnożymy ich.** Kamień milowy to zdarzenie, po którym zmienia się stan projektu — kilka na projekt, nie kilkanaście. Reszta to zwykłe pozycje z terminem.

### 1.11a Spotkanie — pozycja, która ma godziny

Termin mówi „do kiedy", kamień milowy mówi „od tego dnia jest inaczej", a spotkanie zajmuje **konkretny kawałek dnia** i ma miejsce, do którego się wchodzi. Dlatego dostało dwie własne kolumny, a nie kolejny prefiks w nazwie: po godzinach da się sortować i liczyć długość, po prefiksie nie.

1. **`Godziny` decydują.** Wypełniona kolumna robi z pozycji spotkanie; pusta zostawia zwykły termin. Format `HH:MM-HH:MM` (`10:00-11:30`); sama godzina początku dostaje domyślną godzinę długości. Kropka zamiast dwukropka i myślnik długi też przechodzą — narzędzie je prostuje.

2. **`Link` to adres połączenia** — Teams, Zoom, Meet. Na karcie zadania staje się przyciskiem **dołącz do spotkania**. Adres bez `http` wyświetla się jako tekst, więc numer sali albo telefon też można tu wpisać.

3. **`Do kiedy` zostaje datą spotkania.** Kolumna terminu nie zmienia znaczenia — godziny ją tylko doprecyzowują.

4. **Na osi czasu spotkanie jest paskiem o długości slotu**, nie kropką. Przy zakresie kilku miesięcy pasek schodzi do minimalnej szerokości; realny wymiar czasu widać po zawężeniu zakresu.

5. **Dwuklik w pasek otwiera kartę spotkania** — z godzinami, przyciskiem dołączenia i sekcją `Notatki ze spotkania` na górze, w której pisze się w trakcie rozmowy. Karta spotkania ma inny szablon niż karta zadania: notatki, po co to spotkanie, do przejścia, ustalenia, co z tego wychodzi.

6. **Warstwa `spotkania` na osi** pokazuje wyłącznie je. Na liście działa filtr `spotkania`.

### 1.11b Sprint — okres, nie punkt

Termin, kamień milowy i spotkanie są punktami na osi. Sprint jest **odcinkiem**: okresem, w którym skupiamy się na jednej rzeczy — albo świadomie nie robimy nic — wolne też jest sprintem, reenergetyzującym.

1. **`Od` decyduje.** Wypełniona kolumna razem z `Do kiedy` robi z pozycji sprint: okres od daty początku do dnia terminu włącznie. Format daty ten sam co w `Do kiedy` (1.3).

2. **`Od` późniejsze niż `Do kiedy` nie jest sprintem.** Odwrotnie wpisane daty dałyby pasek o ujemnej długości, więc narzędzie traktuje taki wiersz jak zwykły termin — bez cichego znikania z osi.

3. **Na osi sprint jest paskiem od początku okresu do terminu.** Początek sprzed zakresu osi przycina się do lewej krawędzi, żeby długość paska nie kłamała.

4. **Wolne też zakładamy jako sprint.** Urlop, przerwa, tydzień bez spotkań — to okres, w którym Miko czegoś nie robi, i ma być widoczny na osi tak samo jak okres pracy.

### 1.11c Cztery kształty na osi

Kształt niesie rodzaj pozycji, kolor niesie termin (1.4). Legenda pod osią pokazuje te same kształty, nie ich nazwy.

| kształt | rodzaj | co go robi |
|---|---|---|
| ▽ trójkąt w dół | termin | wybór `termin` — domyślny |
| ◆ romb | kamień milowy | wybór `kamień`, dawniej `M:` w nazwie (1.11) |
| ■ kwadrat | spotkanie | wybór `spotkanie`, dawniej wypełnione `Godziny` (1.11a) |
| ▬ pasek | sprint | wybór `sprint` plus data w `Od` (1.11b) |

**Rodzaj wskazuje się z listy w kolumnie `Rodzaj`** (1.11d, decyzja Miko 25.08.2026). Pozycja należy do dokładnie jednej warstwy — inaczej znikałaby z filtra, w którym Miko jej szuka.

**Pusta kolumna `Rodzaj` nie jest błędem** — wtedy rodzaj wyprowadza się z danych jak przed 25.08: sprint przed spotkaniem, spotkanie przed kamieniem, reszta to termin. Zapas jest po to, żeby wiersz wpięty z cudzej listy albo dopisany komendą trafił na oś bez ręcznego uzupełniania.

### 1.11d Kolumna `Rodzaj` i filtr rodzaju na liście

Do 25.08.2026 rodzaj widać było wyłącznie na osi czasu, jako kształt. Lista pokazywała wszystko jednakowo, więc żeby zobaczyć, czy pozycja jest kamieniem, trzeba było włączyć oś.

1. **`Rodzaj` jest kolumną listy** — kształt plus nazwa, ten sam kształt co na osi. W podglądzie z serwerem komórka jest listą wyboru: `termin`, `termin pewny`, `kamień`, `spotkanie`, `sprint`.

2. **Wybór `sprint` otwiera kolumnę `Od`** — datę początku okresu wpisuje się w niej z kalendarza. Przy pozostałych rodzajach kolumna stoi pusta, a gdy na widoku nie ma ani jednego sprintu, chowa się w całości.

3. **Zejście ze sprintu na inny rodzaj kasuje `Od`.** Data zostawiona w arkuszu wróciłaby przy następnym wyborze `sprint` jako cudza, stara.

4. **Początek po terminie jest odrzucany przy zapisie**, z komunikatem. Sprint to okres, więc daty muszą iść w jedną stronę (1.11b p. 2).

5. **Filtr rodzaju działa jak warstwy osi** (1.12 p. 5): niezależne przełączniki, `wszystkie` zapala się samo po włączeniu ostatniego, `żaden` po zgaszeniu wszystkich — pusta lista jest wtedy stanem celowym. Wybór trzyma się między odświeżeniami.

6. **Ta sama kontrolka stoi w dwóch miejscach:** przyciski w pasku nad listą i ptaszki w wierszu filtrów pod nagłówkiem `Rodzaj`. Przycisk przestawia ten sam ptaszek, więc nie da się ich rozjechać. Przyciski są do jednego kliknięcia, ptaszki do wyboru kilku rodzajów naraz.

### 1.12 Oś czasu — wizualizacja terminów

Tablica ma przycisk **kalendarz** obok suwaka wysokości wiersza. Włączony dzieli ekran poziomo: lista zadań na górze, oś czasu na dole.

1. **Zakres domyślny to trzy miesiące**, suwak zoom zmienia go od jednego do dwunastu. Oś zaczyna się pierwszego dnia bieżącego miesiąca.
2. **Każdy projekt ma własny pas** i własny przycisk włączania — projekt wyłączony znika z osi, ale zostaje na liście. Wybór trzyma się między odświeżeniami strony.
3. **Kolor punktu to ten sam kolor co na liście** — liczony z terminu (1.4). **Kolor pasa po lewej to kolor projektu** — jedyne miejsce na osi, gdzie pojawia się barwa projektu, żeby punkty terminów nie konkurowały z tłem. Pozycje po terminie zbierają się na lewym skraju osi ze strzałką.
4. **Oś czyta tablicę, nie kalendarz Outlooka.** Termin, który ma się na niej pojawić, musi być pozycją tablicy z deadline'em — to samo źródło, z którego liczy się kolor i pilność. Dotyczy też spotkań (1.11a): warstwa spotkań bierze się z kolumny `Godziny`, nie z konta `mj.banas@outlook.com`.

5. **Warstwy osi:** `wszystkie` · `żaden` · `kamienie` · `terminy` · `spotkania` · `sprinty`. **Warstwy są niezależne** — włączasz jedną, dwie, trzy albo cztery. `wszystkie` zapala się samo po włączeniu ostatniej, `żaden` po zgaszeniu wszystkich; pusta oś jest wtedy stanem celowym. Wybór trzyma się między odświeżeniami, tak samo jak wyłączone projekty.

### 1.12a Język systemu — PL i EN

1. **Podgląd tablicy ma dwie wersje językowe**, przełączane przyciskiem `EN`/`PL` w pasku. Wybór zapamiętuje przeglądarka.

2. **Tłumaczy się wyłącznie obudowa**: nagłówki kolumn, przyciski, liczniki, dymki, nazwy miesięcy i skrót daty. **Treści pól nie tłumaczymy** — nazwa zadania, opis i notatki zostają dokładnie tak, jak je napisał agent albo partner. Tłumaczenie treści zmieniałoby dane, a tablica ma je pokazywać, nie interpretować.

3. **Słownik żyje w jednym miejscu** — `SLOWNIK` w `tablica-html.py`. Nowa etykieta bez wpisu w słowniku pokaże swój klucz, więc braku nie da się przeoczyć.

### 1.13 Listy zewnętrzne — cudze arkusze wpięte do tablicy

Partner prowadzi własną listę zadań (4EN: action plan Bartka) i to jego arkusz jest źródłem prawdy dla swoich pozycji. Tablica trzyma z niej **lustro**, żeby nasze sprawy z cudzej listy miały termin, kolor i miejsce na osi czasu — bez przepisywania ręką.

1. **Kolumna `Zrodlo`** na tablicy trzyma odnośnik w formacie `KODLISTY:NR` (np. `4EN-AP:6`). Pozycja z odnośnikiem dostaje w tablicy ikonę ogniwa przy ID.
2. **Lustrujemy tylko nasze pozycje** — te, w których właścicielem jesteśmy my. Cudze widać w panelu, na tablicy ich nie ma.
3. **Synchronizacja jest jednokierunkowa: arkusz partnera → tablica**, i tylko termin oraz status. Nazwy i opisu nie nadpisujemy — na tablicy trzymają nasz standard `[KOD] HEADLINE` i zdanie dokonane.
4. **Status idzie tylko do przodu.** Arkusz partnera bywa nieodświeżony; cofnięcie statusu kasowałoby naszą wiedzę o tym, że sprawa ruszyła. Cofnięcie jest raportowane jako **rozjazd** i zostaje decyzją człowieka.
5. **Pozycji zamkniętych u partnera nie wciągamy** na tablicę — zakładalibyśmy wiersz po to, żeby go zaraz zarchiwizować.
6. **Pracujemy w panelu, nie na lustrze.** Panel otwiera się przyciskiem z kodem listy i dzieli ekran w pionie; ma inną kolorystykę, bo zapis idzie **wprost do pliku partnera**. Przed pierwszym zapisem w danym dniu narzędzie odkłada kopię arkusza do podkatalogu `_kopie`.
7. **Nową listę wpina się konfiguracją**, nie kodem: `PjM
arzedzia\listy-zewnetrzne.json` — ścieżka pliku, arkusz, mapowanie kolumn, skala postępu na nasze statusy, właściciel lustra.

### 1.14 Karta zadania — instrukcja wykonania

Wiersz tablicy musi mieścić się w jednej linii, więc niesie headline, termin i status. Wszystko, co potrzebne **do wykonania** — kroki, warunki, numery pism, ścieżki do dokumentów, linki do portali — mieszka w karcie zadania.

1. **Jeden plik na pozycję: `PjM\karty\{ID}.md`.** Nazwa pliku to ID, więc karta nie gubi się przy przepięciu wiersza do innego projektu ani po archiwizacji.

2. **Otwiera się dwuklikiem w ID** na podglądzie tablicy, w osobnej zakładce przeglądarki. Działa tylko przy uruchomionym `tablica-serwer.py` — sam plik `tablica.html` nie ma skąd wziąć treści.

3. **Podział: tablica trzyma STAN, karta trzyma INSTRUKCJĘ.** Status, termin i blokady zmieniają się często i żyją w wierszu. Kroki i materiał zmieniają się rzadko i żyją w karcie. Nie dublujemy jednego w drugim.

4. **Kartę pisze agent projektu**, którego kod stoi w ID. Miko dopisuje z przeglądarki przyciskiem „edytuj kartę” (Ctrl+S zapisuje).

5. **Stałe sekcje:** po co to robimy · jak wykonać · warunki i pułapki · linki · załączniki · historia. Szablon zakłada się sam przy pierwszym otwarciu pustej karty.

5a. **Krok do odhaczenia pisze się `1. [ ] treść kroku`.** Nawias kwadratowy na początku pozycji listy robi z niej **klikalny kwadracik**, a kliknięcie zapisuje stan do pliku karty (`[x]`). Po to, żeby agent widział na otwarciu sesji, na którym kroku Miko utknął, bez pytania go o to — kroki urzędowe robi się na raty i między wizytami. Numeracja zostaje, bo o krokach mówi się po numerach. Działa w listach numerowanych i punktowanych. Składnia jest opcjonalna: pozycja bez nawiasu renderuje się normalnie, więc zdania opisowe zostawiamy bez kwadracika — kwadracik dostaje to, co Miko ma faktycznie wykonać.

6. **PII zostaje w `-dane`.** W karcie są **ścieżki** do skanów i formularzy, nigdy ich treść. Ścieżka `C:\...` renderuje się jako odnośnik otwierany jednym kliknięciem.

7. **Karta nie zastępuje notatki na tablicy.** Notatka mówi, co się stało (ślad dla PjM i dla następnej sesji); karta mówi, jak to wykonać.

## 2. Kalendarz — konto `mj.banas@outlook.com`

Jedyny kalendarz, jaki mamy. Powód techniczny: z dziewięciu skrzynek w Outlooku tylko ta jest kontem Microsoft, więc jej kalendarz żyje na serwerze i widać go na telefonie. Kalendarze kont IMAP są lokalnymi plikami i nie synchronizują się nigdzie; Proton Bridge wystawia wyłącznie pocztę.

1. **Kto pisze:** nikt ręcznie — `PjM\narzedzia\na-kalendarz.py`, odpalany automatycznie po każdym zapisie tablicy (decyzja Miko 01.09.2026: „jak zamknę zadanie z agentem, to nie chcę musieć odpalać PjM dla aktualizacji"). Skrypt idzie przez Outlook COM (`Namespace.Stores` → `GetDefaultFolder(9)`), bez uczestników, więc nic nie wychodzi mailem.

1a. **Co decyduje o wejściu do kalendarza:** kolumna `Rodzaj` w tablicy. Wchodzą `termin pewny`, `kamien` i `spotkanie`; zwykły `termin` zostaje na tablicy, bo „do kiedy" bywa datą ponaglenia, którą ustawiliśmy sami. Wpisy założone przez automat mają w treści znacznik `[tablica:ID]` — **wpisów bez tego znacznika skrypt nie rusza**, więc to, co Miko wpisał ręcznie, jest bezpieczne. Zamknięcie pozycji albo zdjęcie daty zdejmuje wpis z kalendarza.

2. **Co trafia:** terminy urzędowe i sądowe z datą pewną · terminy podatkowe spółki wraz z dniem ostatniej paczki wysyłkowej przed nimi · spotkania i telefony z klientami, kancelariami i urzędami · upływy terminów gestorów i organów jako przypomnienia całodniowe.

3. **Czego nie wpisujemy:** zadań roboczych bez daty pewnej — te żyją na tablicy.

4. **Treść wpisu:** temat zaczyna się kodem obszaru (`WZS:`, `4EN:`, `TERMIN:`, `ROZPRAWA`), w treści jedno zdanie „skąd ta data". Termin niepotwierdzony oznaczamy w temacie `[NIEPOTWIERDZONY]`.

5. **Przypomnienia:** 2 h przed spotkaniem, 1 dzień przed terminem, 2 dni przed końcem okna procedury, 7 dni przed rozprawą.

## 3. Telefon — Google Tasks, konto `mikolajbanas@gmail.com`

Dwie listy, obsługiwane przez `_STANDARDY\google-tasks.py`, synchronizowane przez `PjM\narzedzia\na-telefon.py`.

1. **`Mikołaj's list`** — robota na dziś: pozycje po terminie, z terminem dzisiejszym oraz wszystkie blokery.

2. **`PjM przeglad`** — reszta do wglądu.

3. **Kiedy synchronizujemy:** automatycznie, po każdym zapisie tablicy (od 01.09.2026 — `kanaly_lib.zapisz_tablice` odpala `na-telefon.py` w tle). Ręcznie odpalasz wyłącznie `--podglad`, żeby zobaczyć, co poszłoby na listę.

4. **Odhaczanie działa w obie strony** — Miko odhacza na telefonie, agent to widzi; agent odhacza to, co sam dowiózł.

5. **Zasady wpisu:** tytuł mówi, co zrobić, czasownik na początku · treść zawiera powód, źródło i skutek spóźnienia, bo Miko czyta zadanie bez dostępu do repo · termin dzienny obowiązkowy dla wszystkiego, co ma być zrobione danego dnia.

## 4. Zadania cykliczne — reguła 28 dni

Terminy powtarzalne (JPK, ZUS, deklaracje, opłaty) nie zaśmiecają tablicy przez cały rok.

1. **Powyżej 28 dni do terminu** — pozycja siedzi wyłącznie w kalendarzu.

2. **Gdy do terminu zostaje 28 dni lub mniej** — agent projektu dodaje ją na tablicę jako normalny wiersz z deadline'em. Kolor policzy się sam.

3. **Po wykonaniu** wiersz idzie na `done` i do archiwum; wpis cykliczny w kalendarzu zostaje na następny okres.

## 5. Co gdzie nie trafia

1. **Backlog bez daty i bez blokady** — `zadania.md` projektu, nie tablica.

2. **Prompty, materiał i notatki z dispatcha** — do właściwego pliku projektu albo do `-dane`, nigdy jako zadanie.

3. **Rozstrzygnięcia i decyzje** — do logu sesji. Decyzja nie jest zadaniem i nie ma deliverable.

4. **Dane osobowe** — w notatce wiersza podajemy ścieżkę do pliku w `-dane`, nigdy samą treść.
