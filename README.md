# Przygotowanie i walidacja danych – Zarys projektu
**Autor:** Daniel Faltynowski

## 1. Etap opisu danych
Wszystkie zebrane dane trzeba opisać, niezależnie czy będą dalej potrzebne do analizy, czy nie.

1.  **Brakujące dane:** Każdą zmienną zbiorów trzeba sprawdzić pod kątem brakujących danych. Najszybciej: `df['column'].isna().sum()` oraz `len(df)`. Jeśli w opisie zbioru danych jest taka informacja, podaj powód braku danych oraz sposób postępowania:
    * **Missing at Random (MAR)** – Interpolacja liniowa lub imputacja wielokrotna.
    * **Missing Completely at Random (MCAR)** – Średnia, mediana, moda.
    * **Missing Not at Random (MNAR)** – Wyszukiwanie wzorca, estymacja metodą największej wiarygodności.
    
    > **Uwaga:** Osoba nr 1 tylko daje instrukcje, a nie wstawia danych samodzielnie!

2.  **Typy zmiennych:** W opisie danych ważne jest określenie typu zmiennej:
    * **Zmienna dychotomiczna** – 0/1, tak/nie, prawda/fałsz (dwie etykiety $c_1, c_2$).
    * **Zmienna ilościowa dyskretna** – posiada skończony zbiór wartości.
    * **Zmienna ilościowa ciągła** – posiada nieskończony zbiór wartości.
    * **Zmienna jakościowa nominalna/kategoryczna** – elementy nieporównywalne.
    * **Zmienna jakościowa porządkowa** – elementy porównywalne.

    *W opisie zmiennej musi być podany zbiór wartości oraz informacja o typie brakujących wartości.*

3.  **Wizualizacja wstępna:**
    * **Zmienne dychotomiczne i jakościowe:** Najlepiej `countplot`. Dla porządkowych ustawić kolejność $c_1 < c_2 < c_3 < \dots$ i opisać ten porządek.
    * **Zmienne ilościowe:** Koniecznie **histogram**, opcjonalnie **boxplot**. Przy boxplocie warto zdefiniować zakres wąsów, np. $[Q_1 - 1.5IQR, Q_3 + 1.5IQR]$ lub od 5. do 95. percentyla.

4.  **Sugestie:** Dodać własne uwagi i propozycje dalszych kroków.

5.  **ISTOTNOŚĆ:** Wskazać, które zmienne są kluczowe, a które nieistotne (np. zmienna nie wnosi informacji o sprzedaży lub nie pozwala na segmentację klientów).

---

## 2. Etap przetwarzania danych
Krok realizowany po zakończeniu opisu danych.

1.  **Selekcja:** Wybór zmiennych z datasetu i uzasadnienie odrzucenia pozostałych.
2.  **Obsługa braków:** Wstawienie lub usunięcie brakujących wartości na podstawie wytycznych Osoby nr 1.
3.  **Zmienne jakościowe:** Sprawdzenie unikalnych wartości za pomocą `df['x'].value_counts(dropna=False)`. Korekta błędów (np. literówki) operacjami na stringach. Konwersja na typ kategoryczny: `df['x'] = df['x'].astype('category')`.
4.  **Outliery:** Weryfikacja wartości odstających (na podstawie boxplotów). Wykonanie testów statystycznych i opisanie podjętych działań.
5.  **Integracja:** Połączenie danych w jeden lub kilka kluczowych datasetów.
6.  **Feature Engineering:** Tworzenie nowych zmiennych (np. przedziały wiekowe, wielkość miejscowości).
7.  **Statystyki opisowe:** Obliczenie średniej, mediany, mody, kwartyli, wariancji, odchylenia, skośności i kurtozy.
    * Interpretacja: czy rozkład jest lepto-/platykurtyczny oraz kierunek skośności.

---

## 3. Etap eksploracyjnej analizy danych (EDA)
Po otrzymaniu gotowego zbioru danych.

1.  **Testy rozkładu:** Wykonanie testów statystycznych (Kołmogorowa-Smirnowa, Craméra-von Misesa, Andersona-Darlinga) oraz kryteriów AIC/BIC.
2.  **Korelacja i Regresja:** Obliczenie macierzy korelacji. Zastosowanie metody najmniejszych kwadratów (OLS).
3.  **Analiza pogłębiona:** Wykorzystanie tabel przestawnych i heatmap. Analiza grupowa (średnie, mediany).
4.  **Wizualizacja:** Proste wykresy pomocnicze, np. wykresy kołowe.

---

## 4. Etap wizualizacji danych
Finalna prezentacja wyników.

* **Spójność:** Jednolita kolorystyka.
* **Tytuły "z tezą":** Tytuł powinien sugerować wniosek (np. *"Sprzedaż produktu X jest najwyższa w przedziale 18-25"*).