# Model Zachowania Kota — Wirtualny Kot

> Podstawa behawioralna dla symulacji wirtualnego kota. Oparty na literaturze International Cat Care, pracach Jacksona Galaxy, badaniach ASPCA oraz ekspertyzach behawiorystów kocich (Pam Johnson-Bennett, Sarah Ellis).

---

## Schemat modelu

Każdy kot opisany jest przez 8 wymiarów zachowania, zróżnicowanych według rasy i płci:

### 1. Sen
- **Łączny czas snu** (h/dobę)
- **Preferowane pory** (godziny)
- **Charakter snu** (lekki/głęboki, solo/przy człowieku)

### 2. Aktywność
- **Okna aktywności** (godziny)
- **Typ aktywności** (eksploracja, polowanie, zabawa, patrolowanie)
- **Szczyt energii** (rano / wieczór / noc)

### 3. Polowanie
- **Sesje łowieckie** (liczba/dobę)
- **Godziny polowania**
- **Intensywność** (1–5)

### 4. Zabawa z człowiekiem
- **Sesje/dobę**
- **Czas trwania sesji** (min)
- **Preferowany typ** (wędka / laser / fetch / solo)

### 5. Interakcja z człowiekiem
- **Częstotliwość potrzeby kontaktu** (razy/dobę)
- **Typ** (bliskość / dotyk / wokalizacja)
- **Inicjator** (kot / człowiek / obojętne)

### 6. Jedzenie
- **Posiłki/dobę**
- **Preferowane pory**
- **Styl jedzenia** (zachłanny / powolny / wybredny)

### 7. Wypróżnianie
- **Częstotliwość** (razy/dobę)
- **Pory**

### 8. Potrzeba przestrzeni
- **Terytorialność** (1–5)
- **Reakcja na obcych** (przyjazna / neutralna / agresywna)

---

## Różnice płciowe (ogólne zasady)

| Cecha | Samiec (niekastrowany) | Samica (niesterylizowana) | Po kastracji/sterylizacji |
|-------|----------------------|--------------------------|--------------------------|
| Terytorialność | Wysoka | Średnia | Spada o 30–40% |
| Wokalizacja | Markowanie głosem | Ruja (głośna) | Normalizuje się |
| Aktywność | Wyższa | Zmienna (cykl rui) | Stabilizuje się |
| Interakcja z człowiekiem | Mniej szukana | Bardziej szukana | Wyrównuje się |
| Agresja | Wyższa (między samcami) | Niższa | Znacząco spada |

> **Uwaga:** Model zakłada koty kastrowane/sterylizowane jako standard domowy. Różnice płciowe po zabiegu są subtelniejsze, ale nadal mierzalne behawioralnie.

---

## Dobowy cykl kota (ogólny)

```
00:00–04:00  Głęboki sen (większość ras)
04:00–06:00  Pierwsza aktywność (polowanie o świcie) — szczyt u Bengalów i Syjamów
06:00–08:00  Jedzenie + krótka aktywność
08:00–12:00  Sen / drzemki
12:00–14:00  Krótka aktywność, poszukiwanie kontaktu
14:00–17:00  Sen (sjesta)
17:00–20:00  Szczyt aktywności wieczornej — zabawa, interakcja, jedzenie
20:00–22:00  Bliskość z człowiekiem, wyciszenie
22:00–00:00  Sen lub nocna aktywność (zależnie od rasy)
```

---

## Źródła

- Johnson-Bennett, P. *Think Like a Cat* (2011)
- Ellis, S. et al. *AAFP and ISFM Feline Environmental Needs Guidelines* (2013)
- Vitale Shreve, K. & Udell, M. *What's inside your cat's head?* Animal Cognition (2015)
- International Cat Care — *Cat Behaviour* series
- Galaxy, J. *Cat Daddy* + *Total Cat Mojo* (2012, 2017)
- Bradshaw, J. *Cat Sense* (2013)
