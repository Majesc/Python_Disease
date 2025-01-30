Wprowadzenie -m
Celem projektu było stworzenie modelu klasyfikacyjnego, który przewiduje diagnozę chorób na podstawie symptomów. Zastosowano podejście uczenia maszynowego, wykorzystując różne modele klasyfikacyjne, takie jak Random Forest, Support Vector Machine (SVM) oraz Gradient Boosting. Projekt obejmował także przetwarzanie danych, w tym normalizację tekstu, usuwanie zbędnych cech, a także wizualizację zależności między symptomami a chorobami.

1️⃣ Importowanie bibliotek
Zaimportowano niezbędne biblioteki do analizy danych (pandas, numpy), wizualizacji (matplotlib, seaborn), przetwarzania języka naturalnego (nltk), oraz uczenia maszynowego (sklearn). Wykorzystane zasoby jak stopwords i wordnet z NLTK umożliwiają obróbkę tekstu, a narzędzia z sklearn służą do tworzenia modeli klasyfikacyjnych i oceny wyników.

2️⃣ Wczytanie danych
Funkcja wczytuje dane z plików CSV, usuwa zbędną kolumnę "Unnamed: 133" oraz kolumnę "fluid_overload", jeśli występuje. Oczyszczone dane są zwracane jako dwa DataFrame: train_df i test_df.

3️⃣ Normalizacja tekstu
Funkcja przetwarza tekst, wykonując następujące kroki:

Zamiana na małe litery i usunięcie zbędnych spacji.
Usunięcie znaków specjalnych i cyfr.
Usunięcie stop words (często występujących, ale mało znaczących słów).
Lematyzacja słów do ich podstawowej formy.
Usunięcie duplikatów słów.
Na koniec tekst jest formatowany, tak aby każde słowo zaczynało się wielką literą.

4️⃣ Przetwarzanie danych
Funkcja przeprowadza kilka operacji na danych:

Normalizacja tekstu w kolumnie 'prognosis' dla obu zbiorów (treningowego i testowego).
Podział danych na cechy (X) i etykiety (y), gdzie etykiety to kolumna 'prognosis'.
Kodowanie etykiet za pomocą LabelEncoder.
Skalowanie cech przy użyciu StandardScaler.
Podział danych na zbiór treningowy i walidacyjny.
Funkcja zwraca przetworzone dane oraz obiekty przydatne do dalszego modelowania (label_encoder, scaler).

5️⃣ Macierz korelacji
Funkcja tworzy macierz korelacji między cechami w zbiorze danych:

Kodowanie celu: Tymczasowo koduje etykiety w kolumnie 'prognosis' za pomocą LabelEncoder.
Obliczenie korelacji: Oblicza korelacje między wszystkimi cechami za pomocą metody .corr().
Wizualizacja: Tworzy wykres ciepła (heatmap) z użyciem biblioteki seaborn dla macierzy korelacji, z odpowiednią kolorystyką i etykietami.
Funkcja umożliwia wizualną analizę zależności między cechami, co może pomóc w zrozumieniu struktury danych.

6️⃣ Gęstościowa mapa cieplna (symptomy vs choroby)
Funkcja tworzy mapę cieplną ilustrującą zależność między symptomami a chorobami:

Obliczanie średnich symptomów: Oblicza średnie wystąpienie symptomów dla każdej choroby w zbiorze danych.
Normalizacja: Normalizuje średnie wartości symptomów, dzieląc przez średnią wartość symptomów w całym zbiorze.
Wizualizacja: Rysuje mapę cieplną, gdzie kolory reprezentują znormalizowane wartości występowania symptomów w różnych chorobach.
Mapa cieplna pomaga w analizie, które symptomy są istotne dla poszczególnych chorób.

7️⃣ Trenowanie modelu
Funkcja służy do trenowania modelu klasyfikacyjnego:

Wybór modelu: Funkcja umożliwia wybór spośród trzech modeli: RandomForestClassifier, SVC (Support Vector Machine) oraz GradientBoostingClassifier.
Hiperparametry: Dla każdego modelu definiowana jest siatka hiperparametrów do optymalizacji.
Optymalizacja: Zastosowanie GridSearchCV do przeszukiwania najlepszych hiperparametrów za pomocą walidacji krzyżowej (cross-validation).
Zwrócenie najlepszego modelu: Po przeprowadzeniu przeszukiwania, funkcja zwraca najlepszy model.

8️⃣ Ocena modelu
Funkcja ocenia wydajność modelu:

Predykcja: Przewiduje etykiety dla danych walidacyjnych.
Dokładność: Oblicza dokładność modelu na podstawie porównania przewidywanych i rzeczywistych etykiet.
Raport klasyfikacji: Wyświetla raport z miarami jakości klasyfikacji, takimi jak precyzja, recall, F1-score.
Macierz konfuzji: Rysuje mapę cieplną macierzy konfuzji, pokazującą błędy modelu w przewidywaniach.

9️⃣ Testowanie na zbiorze testowym
Funkcja testuje model na nowych, nieznanych danych:

Przygotowanie danych: Usuwa kolumnę 'prognosis' z danych testowych i koduje etykiety za pomocą wcześniej nauczonego label_encoder.
Skalowanie cech: Zastosowanie wcześniej wytrenowanego skalera do przekształcenia cech.
Predykcja: Model przewiduje etykiety na podstawie danych testowych.
Ocena: Oblicza dokładność modelu na zbiorze testowym.
Funkcja zwraca dokładność modelu na danych testowych.

🔟 Testy jednostkowe
W tej części projektu zastosowano testy jednostkowe:

setUp: Przygotowanie danych, przetwarzanie i trenowanie modelu przed każdym testem.
Testy:
test_model_training: Sprawdza, czy model został poprawnie wytrenowany (nie jest None).
test_prediction_shape: Weryfikuje, czy liczba predykcji zgadza się z liczbą próbek w zbiorze walidacyjnym.
test_accuracy_threshold: Sprawdza, czy dokładność modelu na zbiorze testowym przekracza 70%.
Testy jednostkowe pomagają upewnić się, że proces trenowania, predykcji i oceny modelu działa zgodnie z oczekiwaniami.

🔟 Wykonanie kodu
Oto pełny przepływ pracy w projekcie:

Wczytanie danych: Załadowanie danych treningowych i testowych.
Przetwarzanie danych: Usunięcie zbędnych kolumn, przetworzenie danych oraz podział na zbiory treningowe, walidacyjne i testowe.
Wizualizacje: Utworzenie wykresów przedstawiających macierz korelacji oraz mapę cieplną symptomów vs choroby.
Trenowanie modelu: Wybranie modelu i jego trenowanie na danych treningowych.
Ocena modelu: Ocena wyników modelu na zbiorze walidacyjnym oraz wizualizacja wyników.
Testowanie modelu: Testowanie modelu na zbiorze testowym i sprawdzenie dokładności.
Cały proces przechodzi przez etapy od wczytania danych po finalną ocenę modelu, co zapewnia pełną ocenę jego efektywności.

Analiza wyników
Po przeprowadzeniu procesu trenowania i oceny modelu, uzyskano dokładność na poziomie powyżej 70% dla zbioru testowego, co jest wynikiem zadowalającym w kontekście problemu klasyfikacyjnego. Model został oceniony pod kątem dokładności, precyzji, recall i F1-score, co pozwoliło na dokładną analizę jego wydajności w różnych klasach. Zastosowanie macierzy korelacji i mapy cieplnej umożliwiło wizualizację zależności między symptomami a chorobami, co pozwoliło lepiej zrozumieć, które cechy są istotne.

Wnioski końcowe
Model Random Forest okazał się najbardziej efektywny w kontekście tego zadania, osiągając najlepsze wyniki. Optymalizacja hiperparametrów przyczyniła się do poprawy wyników klasyfikacji.
Przetwarzanie danych miało kluczowe znaczenie dla jakości modelu. Usunięcie zbędnych cech, normalizacja tekstu i skalowanie danych pozytywnie wpłynęły na efektywność modelu.
Wizualizacje dostarczyły cennych informacji o zależnościach między symptomami a diagnozami, co może pomóc w dalszym udoskonalaniu modelu.
Projekt wykazał, że odpowiednie przetwarzanie danych oraz wybór odpowiednich modeli klasyfikacyjnych mogą prowadzić do skutecznych predykcji, przy czym dalsza optymalizacja i testowanie nowych podejść może poprawić wyniki.
