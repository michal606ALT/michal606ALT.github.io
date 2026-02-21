---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/quicksort/"}
---

## Cel

Quicksort to jeden z najszybszych i najczęściej stosowanych algorytmów sortowania. Jego głównym celem jest uporządkowanie elementów tablicy w czasie średnim $O(n \log n)$ przy wykorzystaniu strategii „dziel i zwyciężaj”.

## Idea działania

Algorytm opiera się na wyborze tzw. **pivotu** (elementu osiowego). Wszystkie elementy mniejsze od pivotu trafiają na jego lewą stronę, a większe na prawą. Po takim podziale pivot znajduje się na swojej docelowej, ostatecznej pozycji. Proces ten powtarzamy rekurencyjnie dla powstałych podtablic.

Kluczowe kroki:

1. **Wybór pivotu:** Może to być pierwszy, ostatni, środkowy lub losowy element.
2. **Partycjonowanie:** Przegrupowanie tablicy wokół pivotu.
3. **Rekurencja:** Sortowanie lewej i prawej części.
    

Wzór na złożoność czasową (przypadek średni):

$$T(n) = 2T(n/2) + \Theta(n) \implies O(n \log n)$$

# Partycjonowanie
>Istnieje wiele metod partycjonowania, które przeważnie są sobie równe pod względem wydajności.

Wykorzystujemy dwa wskaźniki, które przeszukują tablicę w jednym kierunku:

1. **Wskaźnik wolny (i):** Wyznacza granicę strefy elementów mniejszych. Wszystko na lewo od niego zostało już zweryfikowane jako mniejsze od pivotu.
2. **Wskaźnik szybki (j):** Przeszukuje kolejne komórki tablicy w poszukiwaniu wartości, które powinny trafić do lewej części.

**Przebieg operacji:**

- Jeśli wskaźnik szybki napotka wartość mniejszą od pivotu, zwiększamy wskaźnik wolny i zamieniamy miejscami elementy pod tymi dwoma indeksami.
- Jeśli wskaźnik szybki napotka wartość większą, po prostu przechodzi do następnej pozycji.
- Po sprawdzeniu wszystkich elementów, pivot zostaje zamieniony z elementem znajdującym się bezpośrednio za granicą strefy mniejszej.

> **Ważna uwaga:** Elementy wewnątrz lewej i prawej części nie muszą być jeszcze posortowane względem siebie. Istotne jest jedynie to, że znajdują się po właściwej stronie elementu osiowego.

## Kiedy użyć?

Quicksort jest wyborem domyślnym w większości bibliotek standardowych np. `std::sort` w C++ często używa jego hybrydowej wersji.

- **Zaleta:** Sortuje „w miejscu” (in-place), co oznacza bardzo małe zapotrzebowanie na dodatkową pamięć w porównaniu do Merge Sort.
- **Wada:** W najgorszym przypadku (np. przy fatalnym doborze pivotu na już posortowanej tablicy) złożoność może spaść do $O(n^2)$.


To podejście jest niezastąpione, gdy zależy nam na szybkości procesora i efektywnym wykorzystaniu pamięci cache.


## Wybór Pivotu

Strategia wyboru pivotu ma kluczowe znaczenie dla wydajności. Najczęstsze techniki to:

- **Median-of-three:** Wybieramy medianę z pierwszego, środkowego i ostatniego elementu.
- **Randomizacja:** Wybór losowego indeksu niemal całkowicie eliminuje ryzyko trafienia na przypadek $O(n^2)$.

## Implementacja


```cpp
int partition(vector<int>& arr, int low, int high) {
    int pivot = arr[high]; // Wybieramy ostatni element jako pivot
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(vector<int>& arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```