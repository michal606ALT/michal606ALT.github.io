---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/wyszukiwanie-binarne/"}
---


# ​Idea działania

​Algorytm działa na zasadzie dziel i zwyciężaj. Zamiast sprawdzać każdy element po kolei (co zajęłoby dużo czasu w dużych zbiorach), algorytm celuje w środek zakresu i decyduje, w którą stronę iść dalej.

​Wymaganie wstępne: **Tablica musi być posortowana** (rosnąco lub malejąco).

### ​Algorytm krok po kroku:

1. ​Definiujemy początek (left) i koniec (right) przeszukiwanego zakresu.
2. ​Wyznaczamy środek (mid).
3. ​Porównujemy element środkowy z szukaną wartością:
    - ​Jeżeli $tablica[mid] == szukana$: Znaleźliśmy element. Zwracamy indeks.
    - ​Jeżeli $tablica[mid] > szukana$: Element musi być "na lewo". Przesuwamy koniec zakresu $(right = mid - 1)$.
    - ​Jeżeli $tablica[mid] < szukana$: Element musi być "na prawo". Przesuwamy początek zakresu $(left = mid + 1)$.
4. ​Powtarzamy proces dopóki left nie minie się z right.

## ​Dlaczego jest to "efektywne"? (Złożoność)

​Różnica wydajności jest ogromna dla dużych danych.

**Złożoność czasowa**: 
$$O(\log_2{n})$$
