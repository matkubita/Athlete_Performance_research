# Raport z projektu: Predykcja efektywności biegaczy

**Autorzy:** Jan Zubalewicz & Mateusz Kubita  
**Data:** Grudzień 2025  

---

## 1. Cel projektu
Głównym celem naszego projektu było zbudowanie modelu regresyjnego do przewidywania wskaźnika efektywności biegacza (**efficiency_score**). Analiza opierała się na danych fizjologicznych oraz biomechanicznych. Chcieliśmy sprawdzić, które algorytmy uczenia maszynowego najlepiej radzą sobie ze złożonością danych sportowych oraz jakie cechy (np. $VO_2$ max czy kadencja) mają kluczowy wpływ na końcowy wynik.

## 2. Opis danych i preprocessing
Analizę przeprowadziliśmy na zbiorze danych obejmującym **1158 rekordów** dotyczących biegaczy. Przed przystąpieniem do modelowania wykonaliśmy niezbędne kroki przygotowawcze:
* **Usuwanie zbędnych cech:** Odrzuciliśmy kolumny `athlete_id` oraz `sport`, ponieważ nie wnosiły wartości predykcyjnej dla modelu regresji.
* **Czyszczenie danych:** Kolumna `power_output` została usunięta ze względu na całkowity brak danych (same wartości null).
* **Wybrane cechy:** Ostatecznie model skupił się na takich parametrach jak: wiek, płeć (zakodowana numerycznie), $VO_2$ max, zmienność tętna (HRV), próg mleczanowy, tętno spoczynkowe/maksymalne oraz długość kroku i kadencja.

## 3. Problem przeuczenia (Overfitting)
Podczas prac nad projektem kluczowym wyzwaniem okazał się **overfitting**. Nasze pierwsze podejście z użyciem drzewa decyzyjnego zakończyło się błędem MSE wynoszącym 0.00 na zbiorze treningowym, co oznaczało, że model "nauczył się danych na pamięć" i nie potrafił generalizować wiedzy.



Aby rozwiązać ten problem, zastosowaliśmy **GridSearchCV** do optymalizacji modelu **Gradient Boosting**. Poprzez wprowadzenie parametrów takich jak `max_depth`, `min_samples_leaf` oraz `learning_rate`, udało nam się znacznie zmniejszyć różnicę między błędem treningowym a testowym.

## 4. Porównanie modeli i wyniki
Przetestowaliśmy cztery różne podejścia. Poniżej przedstawiamy zestawienie wyników błędu średniokwadratowego (MSE) oraz współczynnika determinacji ($R^2$):

| Model | Test MSE | Training MSE | Test R² | Status |
| :--- | :--- | :--- | :--- | :--- |
| **Zoptymalizowany GBR** | **218.85** | **199.74** | **-0.02** | **Najlepsza stabilność** |
| **Regresja Liniowa** | 219.63 | 211.35 | -0.02 | Stabilna, ale prosta |
| **Random Forest** | 235.63 | 31.16 | -0.10 | Lekkie przeuczenie |
| **Drzewo Decyzyjne** | 409.68 | 0.00 | -0.91 | Silne przeuczenie |



## 5. Wnioski i podsumowanie
1. **Fizjologia to nie wszystko:** Choć $VO_2$ max i próg mleczanowy są istotne, niski wskaźnik $R^2$ sugeruje, że efektywność biegowa zależy od czynników, których nie ma w tym zbiorze (np. staż treningowy, technika czy warunki pogodowe).
2. **Kluczowa rola regularyzacji:** Projekt pokazał, że bez odpowiedniego ograniczenia złożoności modeli (jak w przypadku Gradient Boosting), algorytmy bardzo łatwo dopasowują się do szumu w danych.
3. **Najlepszy model:** Za najbardziej wiarygodny uznaliśmy model **Gradient Boosting**, ponieważ mimo trudnego zbioru danych, wykazał się najmniejszą luką między błędem na danych znanych i nieznanych.

---