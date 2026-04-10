# Wykrywanie Oszustw Finansowych – Klasyfikacja Niezbalansowanych Danych

> Projekt Laboratoryjny nr 1 | Uczenie Maszynowe 2026  
> Uniwersytet VIZJA w Warszawie

## Cel projektu

Zaprojektowanie, implementacja i porównanie modeli uczenia maszynowego do wykrywania transakcji fraudowych w warunkach ekstremalnej nierównowagi klas (0.1–1% fraudów).

## Zadania

- Zrozumienie problemu klasy niezbalansowanej
- Analiza wpływu różnych strategii balansowania danych
- Porównanie modeli klasycznych i zespołowych
- Ocena modeli z wykorzystaniem właściwych metryk (nie tylko accuracy)
- Przeprowadzenie analizy kosztów błędnych decyzji

## Zbiór danych

Wybrany z Kaggle / UCI Repository:

- **Credit Card Fraud Detection** (Kaggle) – 284 807 transakcji, ~492 fraudy (~0.17%)
- Alternatywnie: IEEE-CIS Fraud Detection (bardziej złożony, wymagający feature engineering)

## Kontekst i motywacja

W realnych systemach finansowych klasa fraud stanowi często mniej niż 1% danych.
Model może osiągnąć 99% accuracy, klasyfikując wszystkie obserwacje jako klasę normalną –
co jest wynikiem pozornie dobrym, lecz praktycznie bezużytecznym.

Jednocześnie koszt błędu **False Negative** (niewykryty fraud) jest zwykle znacznie większy
niż koszt **False Positive** (fałszywy alarm).

Dlatego projekt koncentruje się na:
- analizie metryk w warunkach niezbalansowania,
- strategiach radzenia sobie z nierównowagą klas,
- analizie kosztowej klasyfikacji.

## Modele

| Typ | Model |
|-----|-------|
| Liniowy | Logistic Regression (baseline) |
| Drzewiasty | Decision Tree, Random Forest |
| Zespołowy/Boosting | XGBoost, LightGBM |

## Strategie radzenia sobie z nierównowagą klas

- Brak modyfikacji (baseline)
- Class weighting
- Random undersampling / oversampling
- SMOTE
- ADASYN
- Threshold moving

## Metryki ewaluacyjne

- ROC-AUC
- PR-AUC *(metryka kluczowa)*
- Recall (klasa fraud)
- Precision, F1-score
- Confusion matrix
- Expected cost (macierz kosztów)

## Struktura projektu
```
fraud-detection/
├── data/               # Surowe i przetworzone dane
├── notebooks/          # Notatniki EDA i eksperymentów
├── src/                # Kod źródłowy / pipeline
├── reports/            # Raporty 1, 2, 3 (PDF)
└── README.md
```

## Raporty

| Raport | Zakres | Maks. punkty |
|--------|--------|-------------|
| Raport 1 | Podstawy teoretyczne, EDA, opis danych | 25 pkt |
| Raport 2 | Implementacja, metryki, kod (zip) | 35 pkt |
| Raport 3 | Analiza wyników, wnioski | 40 pkt |

### Raport 1 – Aspekty teoretyczne i opis danych

| Kryterium | 3.0 (15–17 pkt) | 3.5 (18–19 pkt) | 4.0 (20–21 pkt) | 4.5 (22–23 pkt) | 5.0 (24–25 pkt) |
|-----------|----------------|----------------|----------------|----------------|----------------|
| Opis problemu i nierównowagi klas | ogólny opis | poprawne wskazanie % fraud | analiza rozkładu klas | pogłębiona analiza + wizualizacje | analiza problemu jako cost-sensitive |
| EDA i opis danych | podstawowe informacje | rozkłady cech | analiza korelacji | analiza outlierów i braków danych | identyfikacja ryzyk (data leakage) |
| Uzasadnienie wyboru modeli | brak uzasadnienia | krótkie uzasadnienie | poprawne uzasadnienie | porównanie metod | sformułowane hipotezy badawcze |

### Raport 2 – Implementacja metody i miary

| Ocena | Min. modeli | Wymagania techniczne | Elementy metodologiczne |
|-------|------------|---------------------|------------------------|
| 3.0 (21–23 pkt) | 3 | 1 metoda balansowania, podstawowe metryki | Train/test split |
| 3.5 (24–26 pkt) | 3 | 2 metody balansowania, ROC i PR curves | Porównanie wyników w tabeli |
| 4.0 (27–29 pkt) | 3–4 (min. 1 boosting) | ≥2 metody balansowania | k-fold CV, analiza wariancji |
| 4.5 (30–32 pkt) | 4 | ≥3 metody balansowania | CV + threshold tuning |
| 5.0 (33–35 pkt) | 4+ (min. 2 zespołowe) | ≥3 metody + cost-sensitive | Automatyzacja, analiza hiperparametrów |

### Raport 3 – Analiza wyników i wnioski

| Ocena | Zakres analizy | Elementy obowiązkowe | Poziom interpretacji |
|-------|---------------|---------------------|---------------------|
| 3.0 (24–26 pkt) | Proste porównanie modeli | Tabela wyników, confusion matrix | Opis typu „model A lepszy niż B" |
| 3.5 (27–29 pkt) | Porównanie kilku metryk | Analiza ROC lub PR-AUC | Wskazanie różnic między modelami |
| 4.0 (30–33 pkt) | Analiza wpływu balansowania | Recall klasy fraud, CV results | Interpretacja kompromisu precision–recall |
| 4.5 (34–37 pkt) | Analiza threshold tuning + stabilność | Analiza wariancji, overfitting | Dyskusja kompromisów i ryzyka błędów |
| 5.0 (38–40 pkt) | Pogłębiona analiza kosztowa | Expected cost, analiza trade-off | Interpretacja w kontekście realnych systemów |

## Skala ocen końcowych

| Suma punktów (R1+R2+R3) | Ocena |
|------------------------|-------|
| 0–59 | 2.0 |
| 60–67 | 3.0 |
| 68–74 | 3.5 |
| 75–82 | 4.0 |
| 83–90 | 4.5 |
| 91–100 | 5.0 |

## Zespół
- [Adam Unrath](https://github.com/AdamUnrath)

## Uruchomienie projektu

> **Wymagany plik danych – nie jest commitowany do repozytorium!**
>
> Przed uruchomieniem projektu pobierz plik `creditcard.csv` (150.83 MB) ze strony Kaggle:
> [https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
>
> Następnie umieść pobrany plik `creditcard.csv` w głównym katalogu projektu (obok pliku `project.ipynb`).

## Środowisko
```bash
pip install -r requirements.txt
```
