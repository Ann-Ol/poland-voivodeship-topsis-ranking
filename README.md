[README.md](https://github.com/user-attachments/files/32299807/README.md)
# Ranking województw metodą TOPSIS – analiza zmian w latach 2019–2023

## Opis projektu

Projekt przedstawia wielokryterialny ranking **16 polskich województw** w latach **2019–2023** z wykorzystaniem metody **TOPSIS** (*Technique for Order Preference by Similarity to Ideal Solution*).

Głównym celem analizy było nie tylko utworzenie rankingów dla poszczególnych lat, ale przede wszystkim pokazanie zmian, których nie widać na podstawie samych miejsc `1, 2, 3, ...`.

Przykładowo województwo może pozostawać liderem przez kilka kolejnych lat, ale jego przewaga nad pozostałymi regionami może się zwiększać albo zmniejszać. Z tego powodu w projekcie zastosowano dwa uzupełniające podejścia:

- **ranking roczny TOPSIS** – pokazujący pozycję województwa względem innych regionów w konkretnym roku,
- **indeks globalny TOPSIS** – liczony na wspólnej skali dla całego okresu 2019–2023, umożliwiający analizę zmian w czasie.

## Cele projektu

Analiza obejmuje:

- utworzenie rankingów województw w R,
- wizualizację rankingu dla wybranego roku,
- przedstawienie wyników na mapie Polski w formie kartogramu,
- analizę zmian w czasie niewidocznych w samych miejscach rankingowych,
- analizę luki do lidera,
- porównanie pierwszego i ostatniego roku,
- analizę stabilności pozycji województw,
- analizę korelacji pomiędzy kryteriami,
- analizę wrażliwości rankingu.

## Dane

Plik wejściowy został przekazany przez prowadzącego w ramach zadania projektowego.

Zbiór zawiera:

- **80 obserwacji**,
- **16 województw**,
- dane z lat **2019–2023**,
- **7 kryteriów diagnostycznych**,
- 4 stymulanty,
- 3 destymulanty.

W analizowanym zbiorze nie występują braki danych.

Zmienne mają techniczne nazwy:

- `W1_stymulant`,
- `W2_destymulant`,
- `W3_stymulant`,
- `W4_destymulant`,
- `W5_stymulant`,
- `W6_destymulant`,
- `W7_stymulant`.

Nie udostępniono ich nazw merytorycznych ani jednostek. Z tego powodu projekt **nie interpretuje rankingu jako rankingu jakości życia, rozwoju gospodarczego ani innego konkretnego zjawiska społeczno-ekonomicznego**.

Wnioski dotyczą wyłącznie względnych wyników województw według zestawu kryteriów dostarczonych w pliku źródłowym oraz zachowania zastosowanej metody rankingowej.

> Plik danych został przekazany przez prowadzącego. Przed umieszczeniem surowego arkusza w publicznym repozytorium należy upewnić się, że jego publiczne udostępnienie jest dozwolone.

## Metoda TOPSIS

Do budowy rankingu zastosowano metodę **TOPSIS**.

Dla każdego kryterium przeprowadzana jest normalizacja min–max do przedziału `[0, 1]`.

Dla stymulant:

```text
z = (x - min(x)) / (max(x) - min(x))
```

Dla destymulant:

```text
z = (max(x) - x) / (max(x) - min(x))
```

Po normalizacji wyznaczana jest odległość każdego województwa od:

- rozwiązania idealnego,
- rozwiązania antyidealnego.

Indeks TOPSIS przyjmuje wartości od 0 do 1. Wyższa wartość oznacza wynik bliższy rozwiązaniu idealnemu.

## Wagi kryteriów

W treści zadania nie określono hierarchii ważności kryteriów, a zmienne mają anonimowy charakter.

Dlatego przyjęto **jednakowe wagi**:

```text
w = 1 / 7
```

dla każdego z siedmiu kryteriów.

Założenie to jest traktowane jako neutralne rozwiązanie techniczne, a nie stwierdzenie, że wszystkie kryteria powinny mieć taką samą wagę w rzeczywistym zastosowaniu.

## Ranking roczny

Ranking roczny jest liczony **oddzielnie dla każdego roku**.

Oznacza to, że wartości minimalne i maksymalne używane do normalizacji pochodzą wyłącznie z obserwacji danego roku.

Tak skonstruowany ranking odpowiada na pytanie:

> Które województwo wypada najlepiej względem pozostałych regionów w danym roku?

Nie służy natomiast do bezpośredniego mierzenia poprawy lub pogorszenia pomiędzy latami, ponieważ punkt odniesienia zmienia się każdego roku.

### Ranking w 2023 r.

Pierwsze trzy miejsca zajęły:

| Miejsce | Województwo | Indeks TOPSIS |
|---:|---|---:|
| 1 | Opolskie | 0,641 |
| 2 | Kujawsko-pomorskie | 0,559 |
| 3 | Zachodniopomorskie | 0,550 |

## Indeks globalny

Aby umożliwić analizę zmian w czasie, utworzono również **indeks globalny**.

W tym przypadku wartości minimalne i maksymalne dla każdego kryterium są wyznaczane na podstawie **całego okresu 2019–2023**.

Dzięki temu wszystkie obserwacje korzystają ze wspólnej skali odniesienia.

Indeks globalny umożliwia analizę:

- kierunku zmian syntetycznego wyniku województwa,
- skali poprawy lub pogorszenia,
- dystansu do lidera,
- zmian niewidocznych w samych pozycjach rankingowych.

## Luka do lidera

Dla każdego województwa obliczono różnicę pomiędzy jego indeksem globalnym a wynikiem najlepszego regionu w danym roku.

Spadek luki oznacza **zbliżanie się do lidera**, natomiast jej wzrost oznacza zwiększanie dystansu.

Jest to jeden z kluczowych elementów projektu, ponieważ pozwala analizować sytuację, w której lider pozostaje ten sam, ale relacje pomiędzy województwami zmieniają się w czasie.

## Najważniejsze wyniki

W latach 2019–2023 województwo **Opolskie zajmowało pierwsze miejsce we wszystkich pięciu analizowanych latach**.

Jednocześnie sam brak zmiany lidera nie oznacza braku zmian w danych.

Pomiędzy 2019 a 2023 r.:

- największą poprawę indeksu globalnego odnotowało **Zachodniopomorskie**: około **+0,044**,
- następne było **Dolnośląskie**: około **+0,037**,
- największy spadek odnotowało **Małopolskie**: około **−0,018**.

Wyniki pokazują, że sama zmiana miejsca w rankingu nie opisuje pełnej skali zmian pomiędzy regionami.

## Analiza stabilności i wrażliwości

W projekcie sprawdzono również stabilność otrzymanego rankingu.

Dla roku 2023 ranking został ponownie wyliczony siedem razy, za każdym razem po usunięciu jednego kryterium.

Korelacja rang Spearmana pomiędzy rankingiem bazowym i rankingami alternatywnymi wyniosła od około:

- **0,832** do
- **0,938**.

W zależności od pominiętego kryterium maksymalna zmiana pozycji pojedynczego województwa wynosiła od **3 do 6 miejsc**.

Oznacza to, że ogólny układ rankingu pozostaje dodatnio i dość silnie związany z rankingiem bazowym, ale dokładne pozycje części województw są wrażliwe na zestaw wykorzystanych kryteriów.

## Wizualizacje

Projekt zawiera:

- wykres słupkowy rankingu dla wybranego roku,
- kartogram Polski,
- wykres zmian indeksu globalnego,
- wykres luki do lidera,
- mapę cieplną pozycji rankingowych,
- porównanie wyników z 2019 i 2023 r.,
- tabelę stabilności miejsc,
- macierz korelacji kryteriów.

Granice województw do kartogramu są pobierane z bazy **GADM** za pomocą pakietu `geodata`.

Przy pierwszym generowaniu mapy wymagane jest połączenie z internetem.

## Technologie i biblioteki

Projekt został wykonany w **R / R Markdown**.

Wykorzystane pakiety:

- `readxl`,
- `dplyr`,
- `tidyr`,
- `stringr`,
- `ggplot2`,
- `scales`,
- `knitr`,
- `sf`,
- `geodata`,
- `terra`,
- `tibble`.

## Struktura repozytorium

```text
.
├── README.md
├── ranking_wojewodztw_TOPSIS.Rmd
├── ranking_wojewodztw_TOPSIS.html
└── dane_wojewodztwa_stabilne.xlsx
```

Plik HTML zawiera gotowy, wyrenderowany raport wraz z kodem, tabelami, wynikami i wizualizacjami.

## Jak uruchomić projekt

1. Pobierz lub sklonuj repozytorium.
2. Umieść plik `dane_wojewodztwa_stabilne.xlsx` w tym samym katalogu co plik `.Rmd`.
3. Upewnij się, że arkusz z danymi ma nazwę `DANE`.
4. Otwórz `ranking_wojewodztw_TOPSIS.Rmd` w RStudio.
5. Zainstaluj wymagane pakiety, jeżeli nie są dostępne.
6. Wybierz **Knit → Knit to HTML**.

Rok prezentowany na głównym wykresie oraz kartogramie można zmienić przez parametr `rok` w nagłówku dokumentu R Markdown.

## Ograniczenia

Najważniejsze ograniczenia projektu:

- kryteria `W1–W7` są anonimowe i nie mają udostępnionych jednostek,
- wszystkim kryteriom przypisano jednakowe wagi,
- wynik TOPSIS ma charakter względny,
- wynik zależy od zestawu analizowanych obiektów i zakresu danych,
- indeks globalny jest porównywalny tylko w ramach przyjętej bazy 2019–2023,
- dołączenie nowych lat wymaga ponownego przeliczenia wspólnej skali,
- analiza nie pozwala na wnioskowanie przyczynowe,
- dokładne miejsca części województw wykazują pewną wrażliwość na zestaw kryteriów.

## Autor

**Anna Oleszko**

Projekt wykonany w ramach zadania dotyczącego wielokryterialnego rankingu województw i wizualizacji zmian w czasie.
