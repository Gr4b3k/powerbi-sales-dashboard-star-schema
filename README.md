E‑commerce Sales Dashboard — Power BI (Star Schema + KPI)
Cel projektu
Celem projektu było stworzenie interaktywnego dashboardu sprzedażowego dla danych e‑commerce, umożliwiającego analizę:
przychodów,
liczby zamówień,
średniej wartości koszyka (AOV),
wyników platform sprzedażowych,
top produktów i kategorii,
sezonowości sprzedaży.

Dashboard
![Dashboard](https://github.com/Gr4b3k/powerbi-sales-dashboard-star-schema/blob/0563be1d6ff4f90fcfdf56fda39a32fd06c2c737/powerbi/dashboard.png?raw=true)
)
Dashboard prezentuje:

KPI: Całkowity przychód, Liczba zamówień, Średnia wartość zamówienia(AOV), Średnia liczba produktów na zamówienie
Trend miesięczny: analiza sezonowości sprzedaży
Top produkty: ranking wg przychodu
Sprzedaż wg kategorii
Wyniki platform sprzedażowych (np. Amazon, Allegro, Shopify)
Filtry: data, platforma, kategoria, produkt

Model danych (Star Schema)
![Model](https://github.com/Gr4b3k/powerbi-sales-dashboard-star-schema/blob/0563be1d6ff4f90fcfdf56fda39a32fd06c2c737/powerbi/model.png?raw=true)
Model danych został zbudowany w architekturze star schema, co zapewnia:
wysoką wydajność,

prostotę relacji,
czytelność modelu,
łatwość tworzenia miar DAX.

Tabela faktów
FactSales — zawiera transakcje: przychód, ilość, cena, data, produkt, platforma, miasto

Tabele wymiarów
dim_products — nazwa produktu, kategoria, marka
dim_categories — kategorie produktów
dim_brand — marki
dim_platforms — platformy sprzedażowe
dim_city — miasta
dim_date — pełny kalendarz dat

Relacje
Każdy wymiar → 1 : \* → FactSales
Filtracja jednokierunkowa
Klucze główne po stronie wymiarów

Proces przygotowania danych (Power Query)

typowanie kolumn (daty, liczby, tekst),
usunięcie błędów i duplikatów,
podstawowe czyszczenie danych,
normalizacja nazw i kategorii,
podział danych na tabele wymiarów i faktów,

Transformacje nie były optymalizowane pod pełny query folding — celem było przygotowanie danych do modelu analitycznego, a nie budowa produkcyjnego pipeline’u.


Parametr FilePath (dynamiczna ścieżka do danych)
Aby zapewnić poprawne działanie odświeżania danych w Power Query na dowolnym komputerze, zastosowano parametr FilePath, który wskazuje na lokalizację folderu projektu.

Struktura repozytorium
Kod
/powerbi
    dashboard.pbix
    dashboard.png
    model.png

/raw_data
    ecommerce_23000_2024_2025_extended_v2.csv

README.md


Najważniejsze miary DAX
Dashboard wykorzystuje zestaw kluczowych miar DAX, które umożliwiają analizę sprzedaży, efektywności i porównań okresowych.

KPI sprzedażowe

Przychód (Revenue) — podstawowa miara przychodu
Liczba Zamówień (Orders)
Sprzedane Sztuki (Units Sold)
Średnia Cena Produktu (Avg Price)
Śr. liczba produktów / zamówienie (Units per Order)
AOV — średnia wartość zamówienia
AOV PP — AOV w poprzednim okresie
AOV vs PP % — procentowa zmiana AOV
Kolor AOV vs PP — miara logiczna do warunkowego formatowania

Porównania okresowe (PP / LY / % zmiany)

Przychód PP — przychód poprzedniego okresu
Przychód LY — przychód rok do roku
Wzrost % — procentowa zmiana przychodu
Liczba zamówień PP
Liczba zamówień vs PP %
Kolor Przychód vs PP
Kolor Liczba zamówień vs PP

Produktywność i struktura zamówień

Produkty / zamówienie PP
Produkty / zamówienie vs PP %
Kolor Produkty/zamówienie vs PP

Miary jakości (rating)
Ocena — średnia ocena produktu
Ocena MAX
Ocena MIN
Ocena Target — wartość docelowa do porównań
