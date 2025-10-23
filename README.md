# Analiza-zbioru-klientów

# Analiza Danych Sprzedażowych "Superstore" (2003-2005)

Projekt ten jest szczegółową, 4-wymiarową analizą klasycznego zbioru danych "Sample Superstore Sales". Celem analizy jest przekształcenie surowych danych transakcyjnych w strategiczne wnioski biznesowe.
Źródło: https://www.kaggle.com/datasets/kyanyoga/sample-sales-data
---

## 1. Cel Projektu

Głównym celem projektu było przeprowadzenie dogłębnej analizy eksploracyjnej (EDA) w celu zidentyfikowania kluczowych czynników napędzających sprzedaż i rentowność. Analiza odpowiada na cztery fundamentalne pytania biznesowe:

1.  **KIEDY?** (Analiza Czasowa): Jakie są ogólne trendy sprzedaży i wzorce sezonowe?
2.  **CO?** (Analiza Produktowa): Które produkty i kategorie generują największy przychód?
3.  **KOMU?** (Analiza Klientów): Kim są najważniejsi klienci?
4.  **GDZIE?** (Analiza Geograficzna): Z których rynków (krajów) pochodzi największa sprzedaż?

---

## 2. Proces Analityczny

Analiza została przeprowadzona w notatniku Jupyter, krok po kroku, obejmując następujące etapy:

1.  **Wczytanie i Czyszczenie Danych (ETL):**
    * Wczytanie pliku `sales_data_sample.csv` (z uwzględnieniem kodowania `latin1`).
    * Inspekcja danych (`.info()`, `.head()`) w celu identyfikacji typów danych, braków i 25 kolumn.
    * **Czyszczenie Danych:**
        * Konwersja kolumny `ORDERDATE` z typu `object` na poprawny format `datetime64`.
        * Usunięcie 7 zbędnych lub w większości pustych kolumn (np. `ADDRESSLINE2`, `STATE`, `TERRITORY`, `PHONE`), aby uprościć zbiór danych.

2.  **Inżynieria Cech (Feature Engineering):**
    * Stworzenie nowych kolumn czasowych na podstawie `ORDERDATE`:
        * `YEAR_MONTH` (format RRRR-MM) do analizy trendów.
        * `MONTH` (nazwa miesiąca) do analizy sezonowości.

3.  **Agregacja i Wizualizacja (Pandas & Altair):**
    * Zastosowanie operacji `groupby()` i `sum()` lub `value_counts()` do agregowania danych dla każdego z czterech głównych pytań (czas, produkt, klient, geografia).
    * Wygenerowanie interaktywnych wykresów `Altair` (liniowych i słupkowych) w celu wizualizacji wyników.
    * Zapisanie wszystkich wizualizacji jako plików `.html`.

---

## 3. Wnioski Analityczne i Wizualizacje

### Kiedy? - Analiza Trendów i Sezonowości

* **Trend:** Dane obejmują lata 2003-2005. Wykres liniowy wyraźnie pokazuje, że dane za 2005 rok są niekompletne i **urywają się w maju**. Jest to kluczowy wniosek dotyczący jakości danych, który uniemożliwia rzetelne porównanie roczne z 2005 rokiem.
* **Sezonowość:** Biznes jest **skrajnie sezonowy**. Analiza sumaryczna miesięcy pokazuje potężny szczyt sprzedaży w **październiku i listopadzie**, co jest typowe dla sprzedaży detalicznej przygotowującej się do świąt. Najsłabsze miesiące to styczeń i luty.

<img width="878" height="464" alt="sales_trend_over_time" src="https://github.com/user-attachments/assets/c7d919c7-33e5-46e6-9e6d-4a7f67bf3cea" />


<img width="877" height="403" alt="seasonal_sales_chart" src="https://github.com/user-attachments/assets/b99a1469-5528-4286-a67b-e70da573e545" />


### Co? - Analiza Produktów

* **Linie Produktowe:** Kategoria **"Classic Cars"** jest absolutnym liderem i generuje największy przychód dla firmy, znacząco wyprzedzając pozostałe.
* **Bestsellery:** Co ciekawe, najczęściej zamawianym *pojedynczym* produktem nie jest "Classic Car", ale model o kodzie `S18_3232` (należący do innej kategorii).

`<img width="877" height="434" alt="productline_sales" src="https://github.com/user-attachments/assets/874b5570-bde2-490e-8b5e-c04237be518b" />

<img width="844" height="400" alt="top_10_bestsellers" src="https://github.com/user-attachments/assets/23ee71d0-a099-4add-a565-70d4b65283e7" />


### Komu? - Analiza Klientów

* **Koncentracja:** Sprzedaż jest silnie skoncentrowana. Dwóch klientów – **"Euro Shopping Channel"** i **"Mini Gifts Distributors Ltd."** – odpowiada za nieproporcjonalnie dużą część całkowitego przychodu.
* **Wniosek:** Utrata któregokolwiek z tych dwóch klientów "VIP" stanowiłaby poważne zagrożenie dla stabilności finansowej firmy.

<img width="877" height="478" alt="top_10_customers" src="https://github.com/user-attachments/assets/2397982b-8455-49f9-ad75-f547d4c87b92" />


### Gdzie? - Analiza Geograficzna

* **Dominacja Rynku:** Rynek jest zdominowany przez **USA**.
* **Kluczowe Rynki:** Chociaż firma działa globalnie, 10 najlepszych krajów generuje zdecydowaną większość przychodów. Poza USA, kluczowe rynki europejskie to **Hiszpania** i **Francja**.

<img width="877" height="400" alt="top_10_countries" src="https://github.com/user-attachments/assets/b2875e26-1c93-43ac-94e2-fc7dcf5fed96" />


## 4. Wykorzystane Technologie

* **Język:** Python 3.x
* **Środowisko:** Jupyter Notebook
* **Analiza Danych:**
    * **Pandas:** Biblioteka do wczytywania (CSV), czyszczenia, transformacji (`groupby`, `drop`, `to_datetime`, `dt.to_period`) i agregacji danych.
* **Wizualizacja Danych:**
    * **Altair:** Użyta do stworzenia wszystkich interaktywnych wizualizacji (wykresy słupkowe i liniowe), umożliwiających sortowanie i wyświetlanie podpowiedzi (tooltips).
