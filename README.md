# Projekt: Klasyfikacja Chorób Serca z Wykorzystaniem Metod Uczenia Maszynowego
## Cel Projektu
Celem projektu jest zbudowanie i porównanie różnych modeli uczenia maszynowego do klasyfikacji (przewidywania) występowania chorób serca na podstawie dostępnego zbioru danych medycznych. Projekt obejmuje kompleksowe etapy, od wstępnego przetwarzania danych, poprzez implementację klasycznych algorytmów i sieci neuronowych, aż po optymalizację i szczegółową analizę wyników.

## Źródło Danych
Dane wykorzystane w projekcie pochodzą z [pliku heart.csv](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction). Zbiór ten zawiera szereg atrybutów medycznych pacjentów, takich jak:
- wiek
- płeć
- typ bólu w klatce piersiowej
- wyniki badań (np. poziom cholesterolu, ciśnienie krwi w spoczynku)
- zmienną docelową HeartDisease, wskazującą na obecność choroby serca.

## Dotychczasowe Kroki Realizacji Projektu
### 1. Wstępne Przetwarzanie Danych (Preprocessing)
W tej fazie wykonano następujące kroki:
- Załadowanie danych: Zbiór danych heart.csv został wczytany przy użyciu biblioteki pandas.
- Analiza wstępna: Przeprowadzono podstawową eksplorację danych, wyświetlając pierwsze wiersze (df.head()) oraz ogólne informacje o strukturze zbioru (df.info()).
- Kodowanie zmiennych kategorycznych: Zmienne kategoryczne (Sex, ChestPainType, RestingECG, ExerciseAngina, ST_Slope) zostały przekształcone na format numeryczny za pomocą kodowania zero-jedynkowego (pd.get_dummies) z usunięciem pierwszej kategorii (drop_first=True) w celu uniknięcia współliniowości.
- Przygotowanie zmiennych X i y: Wydzielono cechy (X) oraz zmienną docelową (y - HeartDisease).
- Obsługa brakujących/błędnych danych: Rekordy, w których wartość Cholesterol wynosiła 0 (uznane za brakujące lub błędne), zostały usunięte ze zbioru danych.
- Skalowanie danych numerycznych: Cechy numeryczne (Age, RestingBP, Cholesterol, MaxHR, Oldpeak) zostały przeskalowane przy użyciu StandardScaler ze sklearn.preprocessing, aby zapewnić jednolity zakres wartości.
- Podział danych: Zbiór danych został podzielony na zbiór treningowy (80%) i testowy (20%) za pomocą funkcji train_test_split ze sklearn.model_selection. Zastosowano stratyfikację (stratify=y) w celu zachowania podobnego rozkładu klas w obu zbiorach.

### 2. Implementacja i Ocena Modeli Klasycznych
Zaimplementowano i wstępnie oceniono następujące modele:
- Regresja Logistyczna (LogisticRegression):
  - Model został wytrenowany na danych treningowych.
  - Dokonano predykcji na zbiorze testowym.
Oceniono model za pomocą metryk: dokładność (accuracy), raport klasyfikacji (precision, recall, F1-score) dla każdej klasy oraz macierz pomyłek.

- K-Najbliższych Sąsiadów (KNeighborsClassifier):
  - Przeprowadzono prostą optymalizację hiperparametru k (liczby sąsiadów) poprzez testowanie wartości w zakresie 1-20 i wybór tej, która dała najwyższą dokładność na zbiorze testowym.
  - Model z najlepszym k został wytrenowany i oceniony analogicznie do Regresji Logistycznej.

### 3. Implementacja Algorytmu Sieci Neuronowych (TensorFlow Keras)
Zbudowano i oceniono model sieci neuronowej:
- Model Podstawowy (Przed Optymalizacją KerasTuner):
- Zbudowano prosty model sieci neuronowej (perceptron wielowarstwowy - MLP) przy użyciu tensorflow.keras.Sequential.
- Architektura obejmowała warstwy gęste (Dense) z funkcjami aktywacji relu oraz warstwę wyjściową z aktywacją sigmoid (dla klasyfikacji binarnej). Zastosowano również warstwy Dropout w celu regularyzacji.
- Model został skompilowany z optymalizatorem adam i funkcją straty binary_crossentropy.
- Do trenowania wykorzystano mechanizm EarlyStopping w celu zapobiegania przeuczeniu.
- Model został oceniony na zbiorze testowym.
 
### 4. Optymalizacja Rozwiązań
Przeprowadzono optymalizację wybranych modeli:
- K-NN: Dokonano prostej optymalizacji liczby sąsiadów k.

### 5. Zestawienie Porównawcze Wyników
Po każdym etapie implementacji i optymalizacji modelu, wyniki (dokładność, precyzja, czułość, F1-score) były zbierane i prezentowane w formie tabeli porównawczej (pandas.DataFrame). Pozwala to na bieżąco śledzić wydajność poszczególnych podejść.
Ostatnia tabela porównawcza zawiera wyniki dla:
- Regresji Logistycznej
- K-NN (z najlepszym k)
- Sieci Neuronowej przed optymalizacją KerasTuner
- Sieci Neuronowej po optymalizacji KerasTuner
