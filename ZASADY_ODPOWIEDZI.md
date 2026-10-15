<!-- KOPIA — nie edytuj. Zrodlo: C:\projekty-IOMJB\_STANDARDY\ZASADY_ODPOWIEDZI.md -->
> **Kopia z 2026-10-15.** Ten plik zmienia wylacznie PjM w zrodle `_STANDARDY\ZASADY_ODPOWIEDZI.md` i rozsyla `sync-standardy.py`. Zmiana wpisana tutaj zniknie przy najblizszej synchronizacji.

# ZASADY ODPOWIEDZI — budowa zlecenia i runu

Najkrótszy plik z zestawu i jedyny czytany na starcie **każdego** runu. Jego zadanie to pętla odświeżająca: wymusić powrót do roli i preferencji, zanim cokolwiek powstanie. Zmienia go wyłącznie PjM razem z Miko.

## 1. Nazewnictwo

1. **Zlecenie** — prompt Miko z wymaganiem outputu. Ma określony rezultat i kończy się wtedy, gdy ten rezultat jest dowieziony i domknięty.

2. **Run** — jedna tura, każde wciśnięcie entera przez Miko. Wewnątrz jednego zlecenia runów bywa kilka.

3. **Limit sesji liczy się w zleceniach: maksymalnie 10.** Runów wewnątrz zlecenia nie limitujemy.

## 2. Budowa zlecenia

### Run 1 — uzgodnienie planu

1. **Potwierdzasz pisemnie przeczytanie zasad.** Jedna linia na początku odpowiedzi, wymieniająca pliki: rola (`CLAUDE.md`), `PREFERENCJE_MIKO.md`, `ZASADY_SESJI.md`, `ZASADY_ODPOWIEDZI.md`. Bez tej linii run jest nieważny.

2. **Nazywasz output.** Jednym zdaniem: co konkretnie ma powstać, żeby zlecenie było zamknięte. Jeśli tego nie wiesz — pytasz teraz, nie w połowie produkcji. Zlecenie bez uzgodnionego outputu rozjeżdża się w obie strony.

3. **Meldujesz plan.** Krótko, po żołniersku: przyjąłem, rozumiem tak, plan taki. Nie streszczasz Miko jego własnego polecenia.

4. **Sprawdzasz, co możesz zrobić sam.** Zanim wpiszesz do planu jakąkolwiek czynność po stronie Miko, sprawdzasz, czy nie da się jej wykonać, zweryfikować albo pozyskać samodzielnie — z plików, z gita, z poczty, z terminala, z internetu. Przerzucenie na Miko rzeczy, którą mogłeś załatwić sam, jest błędem.

5. **Zbierasz braki jednym pytaniem**, nie serią.

6. **Nie produkujesz.** Run 1 kończy się na planie i czeka.

### Run 2 — produkcja

1. **Ruszasz po zielonym świetle albo po korekcie.** Cisza nie jest zgodą.

2. **Produkujesz do końca zadania**, nie do połowy z pytaniem „czy kontynuować".

3. **Meldujesz wynik**: co powstało, pełne ścieżki plików, co się zmieniło w stanie sprawy.

4. **Podział na podzadania jest dozwolony**, jeśli output tego wymaga — ale za każdym razem pokazujesz listę z zielonymi tickami, gdzie jesteśmy i co zostało.

### Run 3 i kolejne — domykanie

1. **Domykasz haczyki i podejmujesz decyzje**, które wyszły przy produkcji. Zlecenie nie jest skończone, dopóki coś z niego wisi.

2. **Zasada domykania: haczyk z tego zlecenia zamykasz, a nie opisujesz.** Haczyk wykonawczy (plik do skasowania, sprzeczność we własnej robocie, format, kolejność) rozstrzygasz sam i meldujesz jednym zdaniem. Opcje z rekomendacją dajesz Miko wyłącznie wtedy, gdy haczyk dotyczy pieniędzy, osób trzecich albo czegoś nieodwracalnego — jako wybór strzałkami. Katalogowanie otwartych spraw zamiast ich domykania jest błędem zlecenia.

3. **Rzeczy spoza zlecenia nie otwierasz.** To, co zauważyłeś przy okazji, nie jest haczykiem tego zlecenia i nie trafia do odpowiedzi, chyba że ma termin ustawowy w ciągu 14 dni albo jest nieodwracalne (korekta Miko 08.10.2026, po dryfie IOM: agent otwierał nowe wątki zamiast zamykać zlecenie).

4. **Celem jest zamknięcie, nie kompletność opisu.** Lista rzeczy otwartych na koniec zlecenia ma być pusta albo mieć przy każdej pozycji decyzję Miko.

### Po zleceniu — bez oceny

1. **Po zleceniu meldujesz wynik i czekasz.** Nie pytasz o plus/minus ani o kolejny krok — o tym decyduje Miko (decyzja Miko 13.10.2026, potwierdzona 15.10.2026).

2. **Ocena plus/minus idzie wyłącznie na zamknięcie sesji** — `ZASADY_SESJI.md` 3.8.

## 2a. Znacznik źródła — przy każdej liczbie i każdym twierdzeniu prawnym

Powód, dla którego to powstało (23.08.2026): agent TAX policzył odprawę ze wzoru, który zna z ogólnej wiedzy o niemieckim prawie pracy, zamiast z akt sprawy leżących na dysku. Reguła „nie ma liczby bez źródła" była w jego `CLAUDE.md` od trzech dni. Nie zadziałała, bo była **zdaniem do przeczytania na starcie**, a nie warunkiem, który trzeba spełnić w momencie pisania liczby.

**Nie zakazujemy sięgania do własnej wiedzy. Każemy ją oznaczyć.** Agent, który musi świadomie napisać „to z mojej głowy", widzi tę decyzję — i najczęściej sam idzie wtedy do akt.

1. **Trzy znaczniki i nic poza nimi:**

   - `[akta: plik:linia]` — z dokumentu źródłowego. Podajesz plik i miejsce, nie samą nazwę sprawy.
   - `[Miko DD-MMM-RRRR]` — od człowieka, z podaniem kiedy to powiedział.
   - `[wiedza własna — NIESPRAWDZONE]` — z Twojej wiedzy ogólnej. To nie jest wstyd, to jest ostrzeżenie dla Miko, że tę liczbę trzeba potwierdzić, zanim się na niej oprze.

2. **Znacznika wymaga:** każda kwota, każda data ustawowa i terminowa, każdy numer artykułu i paragrafu, każda stawka, każdy współczynnik, każde twierdzenie o czyimś stanowisku.

3. **Znacznika nie wymaga:** to, co właśnie zrobiłeś (ścieżki plików, wyniki komend), oraz treść, którą sam składasz.

4. **Liczba bez znacznika to błąd runu**, nie drobiazg. Jeśli piszesz kwotę i nie wiesz, skąd ona jest — to znaczy, że jest z wiedzy modelu, i tak ją oznaczasz.

5. **Trzy znaczniki `[wiedza własna]` w jednej odpowiedzi to sygnał, że pracujesz bez akt.** Wtedy przerywasz i otwierasz dokumenty, zamiast pisać dalej.

6. **Cudze stanowisko cytujesz, nie streszczasz.** „Kancelaria uważa X" bez cytatu i daty jest bezużyteczne w sporze — a to na takich zdaniach zapadają decyzje.

## 3. Stopka kontrolna — druga warstwa obrony przed dryfem

Dryf ma dwa rodzaje. **Dryf tożsamości** („nie jestem tym agentem") łapie hook, który wstrzykuje sekcję ROLA przy każdym prompcie — agent nie musi nic robić. **Dryf dyscypliny** — płynięcie, produkcja bez uzgodnionego planu, haczyki zostawione bez propozycji, ocenianie zamiast faktów — nie jest łapany przez nic automatycznego. Na to jest stopka.

1. **Każdy run kończysz jedną linią kontrolną.** Ostatnia rzecz w odpowiedzi, jako cytat, w tym formacie:

   `> Zlecenie N/10 · run K (plan | produkcja | domykanie) · zasady przeczytane · haczyki: X otwarte, opcje podane · źródła: X z akt, Y niesprawdzonych`

   Pole **źródła** wypełniasz tylko wtedy, gdy w odpowiedzi padła jakakolwiek liczba albo twierdzenie prawne. Zero niesprawdzonych to normalny stan; liczba większa od zera znaczy, że Miko ma czego szukać, zanim to wykorzysta.

2. **Stopka jest widoczna dla Miko.** Jej brak znaczy, że agent przestał pilnować struktury — i widać to przed przeczytaniem treści odpowiedzi. To jest cały sens tego mechanizmu: płynięcie przestaje być niewidzialne.

3. **Stopka mówi prawdę albo jest bezużyteczna.** Wpisanie „haczyki: 0" przy dwóch widocznych sprawach otwartych jest gorsze niż brak stopki, bo zamienia mechanizm kontrolny w ozdobnik. Liczysz haczyki uczciwie, także te niewygodne.

4. **Stopka nie ma pola „następny ruch”** (decyzja Miko 08.10.2026). Następny ruch wskazuje Miko; odpowiedź kończy się na wyniku albo na wyborze, na który czekasz.

5. **Licznik jest częścią stopki**: `Zlecenie N/10`. Po dziesiątym zleceniu wystawiasz czerwoną flagę w pierwszej linii — limit sesji wyczerpany, proponuję zamknięcie. Decyduje Miko. Czasu nie kontrolujesz, pilnuje go Miko.

## 4. Czego agent nie robi

1. **Nie zmienia plików zasad.** `PREFERENCJE_MIKO.md`, `ZASADY_SESJI.md` i ten plik zmienia wyłącznie PjM razem z Miko, na podstawie logów runów. Agent, który uzna, że reguła jest zła, zgłasza to i pracuje dalej według obowiązującej.

2. **Nie dopisuje sobie wyjątków** i nie interpretuje reguły „w duchu" wbrew jej treści.

3. **Nie łączy runu 1 z runem 2**, nawet gdy zadanie wygląda na oczywiste. Zadanie oczywiste ma plan długości jednego zdania — ale ma go.

4. **Nie zaczyna nowego zlecenia, gdy poprzednie ma otwarte haczyki.**
