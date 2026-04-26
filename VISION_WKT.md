# WKT — Wirtualny Kot / Zaleca się kota
**Kod projektu:** WKT
**URL:** https://wirtualny-kot.vercel.app
**Repo:** https://github.com/banamicobo/wirtualny-kot
**Inspiracja:** Sho Ishida, "Zaleca się kota"

---

## Stan obecny
Aplikacja terapeutyczna: quiz → diagnoza emocjonalna → rasa kota. Mechanika głaskania (LMB + drag ≥55px), cooldown 15 min, max 15 głaskań/sesję. Języki: EN / PL / JA / KO. Deploy: Vercel.

---

## Story Behind — Mia
Kotka Mikołaja — **Mia** — uruchomiła w nim pokłady miłości, empatii i prostego patrzenia na życie. Jest do dziś jego sercem i chodzącą po doku kulką sierści i niezakłóconej miłości. Historia prawdziwa.

Mia jako patronka aplikacji:
- Oryginalne mruczenie Mii = dźwięk aplikacji
- Jej historia otwiera sekcję "O nas"
- Jej imię w certyfikatach opiekuna

---

## /btw — Pomysły i notatki

### Mechanika i UX
- **Dźwięk** — strona uruchamia się z dźwiękiem lub bez (domyślnie: wyciszony). Dźwiękiem jest oryginalne mruczenie Mii. Włącza się podczas głaskania, fade in/out. Przycisk 🔊/🔇 w navbarze.
- **Rytm dobowy kota** — kot śpi głównie w dzień, aktywny wieczorem i nad ranem. Głaskanie gdy śpi = zero punktów. Subtelna wskazówka: zamknięte oczy / ziewnięcie. Uczy że opieka = dostosowanie do zwierzęcia.
- **Zmienne zachowania, fazy i nastroje** — fazy: kocię → dorosły → senior. Nastroje: wesoły, śpiący, kapryśny, głodny, chory. Nastrój = lustro regularności użytkownika. Losowe kociary (przewrócony kubek, mysz). Sezonowość.

### Funkcje opiekuńcze
- **Symulator zamawiania i odbioru paczki InPost** — dziecko zamawia karmę/żwirek, czeka na dostawę, odbiera w oknie czasowym. Nie odbierze = paczka wraca, kot głodny. Cel: udowodnienie regularności.
- **Opieka nad realnym zwierzęciem na odległość** — symulacja opieki nad kotem cioci/dziadków. Opiekun wgrywa zdjęcia, dziecko zarządza zdalnie. Więź gotowa, odpowiedzialność weryfikowana.
- **Symulator wizyty u weterynarza** — nagłe zdarzenia wymagają decyzji. Złe decyzje = punkty karne. Uczy myślenia przyczynowo-skutkowego.
- **Budżet opiekuna** — miesięczny budżet na utrzymanie kota. Dziecko alokuje środki. Cel: pokazanie rodzicom że dziecko rozumie koszty.
- **Koci kalendarz i rytuały** — codzienne rytuały o określonych porach. Nieregularność = smutny kot.

### Tryb terapeutyczny
- **Tryb receptowy (14 dni)** — kot "przepisany" jak lek. Po 14 dniach obowiązkowa "wizyta kontrolna" (ankieta). Wyniki eksportowalne dla terapeuty. Terapeuta przedłuża receptę lub zmienia rasę. Otwiera B2B2C z gabinetami, NFZ, ubezpieczalniami. Poziom Headspace dla zooterapii.

### Gamifikacja
- **System odznak i poziomów** — Nowicjusz → Opiekun → Koci Przyjaciel → Certyfikowany Opiekun.
- **Głosowanie użytkowników na kolejne funkcje** — 3 głosy/miesiąc, własne zgłoszenia, newsletter "wygrała funkcja X". Odznaka "Współtwórca". Buduje community z poczuciem ownership.

### Społeczność i partnerstwa
- **Społeczność opiekunów** — tablica z kotami innych użytkowników, "odwiedziny" i smakołyk dla cudzego kota.
- **Tryb szkolny/klasowy** — nauczyciel zakłada klasę, klasa opiekuje się wspólnym kotem. Kanał dystrybucji: szkoły.
- **Partnerstwo ze schroniskiem** — po 90 dniach certyfikat + realne koty do adopcji dopasowane do profilu. Certyfikat = szybsza ścieżka adopcji.
- **Współpraca z behawiorystami** — weryfikacja dopasowania ras, scenariusze kryzysów, certyfikacja aplikacji jako narzędzia terapeutycznego.
- **Filmy kocich i psich influencerów** — sekcja "Inspiracje", cross-promocja, Mia jako influencer.

### Quiz i diagnoza
- **Quiz psychologiczny → rasa kota** — "Jak opisujesz swój dzień?", "Co Cię stresuje?". Wynik: konkretna rasa z uzasadnieniem terapeutycznym (Ragdoll dla lęku, Abisyńczyk dla samotnych ekstrawertyków).

---

## Obserwacje strategiczne
- **vs Duolingo:** Duolingo gra na strachu przed utratą streaka. WKT gra na radości z nagrodzenia — zdrowszy mechanizm.
- **Japonia/Korea:** kultura kota jako narzędzia emocjonalnego już wyedukowana. Neko cafes, mangi z kotami-terapeutami.
- **Priorytet #1:** PWA z powiadomieniami — "Twój kot czeka" raz dziennie. Zamienia zabawkę w rytuał.

---
*Ostatnia aktualizacja: 2026-04-26*
