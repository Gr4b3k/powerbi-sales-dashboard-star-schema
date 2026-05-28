# E‑commerce Sales Dashboard — Power BI (Star Schema + KPI)

## Cel projektu
Celem projektu było stworzenie interaktywnego dashboardu sprzedażowego dla danych e‑commerce, umożliwiającego analizę:
- przychodów,
- liczby zamówień,
- średniej wartości koszyka (AOV),
- wyników platform sprzedażowych,
- top produktów i kategorii,
- sezonowości sprzedaży.

---

## Dashboard
![Dashboard](https://github.com/Gr4b3k/powerbi-sales-dashboard-star-schema/blob/0563be1d6ff4f90fcfdf56fda39a32fd06c2c737/powerbi/dashboard.png?raw=true)

Dashboard prezentuje:
- KPI: Całkowity przychód, Liczba zamówień, Średnia wartość zamówienia (AOV), Średnia liczba produktów na zamówienie  
- Trend miesięczny: analiza sezonowości sprzedaży  
- Top produkty: ranking wg przychodu  
- Sprzedaż wg kategorii  
- Wyniki platform sprzedażowych (np. Amazon, Allegro, Shopify)  
- Filtry: data, platforma, kategoria, produkt  

---

## Model danych (Star Schema)
![Model](https://github.com/Gr4b3k/powerbi-sales-dashboard-star-schema/blob/0563be1d6ff4f90fcfdf56fda39a32fd06c2c737/powerbi/model.png?raw=true)

Model danych został zbudowany w architekturze **star schema**, co zapewnia:
- wysoką wydajność,
- prostotę relacji,
- czytelność modelu,
- łatwość tworzenia miar DAX.

### Tabela faktów
**FactSales** — zawiera transakcje: przychód, ilość, cena, data, produkt, platforma, miasto

### Tabele wymiarów
- **dim_products** — nazwa produktu, kategoria, marka  
- **dim_categories** — kategorie produktów  
- **dim_brand** — marki  
- **dim_platforms** — platformy sprzedażowe  
- **dim_city** — miasta  
- **dim_date** — pełny kalendarz dat  

### Relacje
- Każdy wymiar → **1 : \*** → FactSales  
- Filtracja jednokierunkowa  
- Klucze główne po stronie wymiarów  

---

## Proces przygotowania danych (Power Query)
W Power Query wykonano:
- typowanie kolumn (daty, liczby, tekst),
- usunięcie błędów i duplikatów,
- podstawowe czyszczenie danych,
- normalizację nazw i kategorii,
- podział danych na tabele wymiarów i faktów.

Transformacje nie były optymalizowane pod pełny query folding — celem było przygotowanie danych do modelu analitycznego, a nie budowa produkcyjnego pipeline’u.

---

## Parametr FilePath (dynamiczna ścieżka do danych)
Aby zapewnić poprawne działanie odświeżania danych w Power Query na dowolnym komputerze, zastosowano parametr **FilePath**, który wskazuje na lokalizację folderu projektu.

---

## Struktura repozytorium
/powerbi

dashboard.pbix

dashboard.png

model.png


/raw_data

ecommerce_23000_2024_2025_extended_v2.csv


README.md

---

## Najważniejsze miary DAX

### KPI sprzedażowe
- Przychód (Revenue)  
- Liczba Zamówień (Orders)  
- Sprzedane Sztuki (Units Sold)  
- Średnia Cena Produktu (Avg Price)  
- Śr. liczba produktów / zamówienie (Units per Order)  

### AOV — Average Order Value
- AOV  
- AOV PP  
- AOV vs PP %  
- Kolor AOV vs PP  

### Porównania okresowe (PP / LY / % zmiany)
- Przychód PP  
- Przychód LY  
- Wzrost %  
- Liczba zamówień PP  
- Liczba zamówień vs PP %  
- Kolor Przychód vs PP  
- Kolor Liczba zamówień vs PP  

### Produktywność i struktura zamówień
- Produkty / zamówienie PP  
- Produkty / zamówienie vs PP %  
- Kolor Produkty/zamówienie vs PP  

### Miary jakości (rating)
- Ocena  
- Ocena MAX  
- Ocena MIN  
- Ocena Target
