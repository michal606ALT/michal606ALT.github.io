---
{"dg-publish":true,"permalink":"/szkola/informatyka/techniki/suma-prefiksowa/"}
---

## Cel

Technika ta pozwala na błyskawiczne (w czasie stałym) obliczanie sumy dowolnego spójnego fragmentu tablicy.

## Idea działania

Polega na przygotowaniu dodatkowej tablicy $P$, w której pod indeksem $i$ przechowujemy sumę wszystkich elementów oryginalnej tablicy od początku aż do pozycji $i-1$. Dzięki temu suma dowolnego przedziału staje się różnicą dwóch wartości.

Wzór na element tablicy prefiksowej:

$$P[i] = \sum_{k=0}^{i-1} arr[k]$$

Przyjmujemy, że $P[0] = 0$.

## Kiedy użyć?

Głównym zastosowaniem jest obliczanie sum na przedziałach $[L, R]$. Zamiast każdorazowo sumować elementy pętlą (co zajmuje czas $O(n)$), korzystamy z gotowych wyników:

$$\text{Suma}(L, R) = P[R + 1] - P[L]$$

Gdzie:

- **L**: indeks początku przedziału,
- **R**: indeks końca przedziału,
- **P**: pomocnicza tablica sum prefiksowych.

To podejście jest niezastąpione w zadaniach optymalizacyjnych, gdzie musimy wielokrotnie pytać o sumy różnych podtablic.

---

## Sumy Postfiksowe

Możemy również stworzyć tablicę sum od końca (od prawej do lewej). Jest to przydatne, gdy potrzebujemy informacji o "reszcie" tablicy z prawej strony.

$$Post[i] = \sum_{k=i}^{n-1} arr[k]$$

## Implementacja (C++)

Budowa tablicy prefiksowej zajmuje czas $O(n)$ i wymaga $O(n)$ dodatkowej pamięci.

```cpp
// Zakładamy, że n to rozmiar tablicy arr
vector<int> prefixSum(n + 1, 0);

for(int i = 0; i < n; i++) {
    prefixSum[i + 1] = prefixSum[i] + arr[i];
}
```

## Zadania do poćwiczenia

Technika ta pojawia się w ogromnej liczbie problemów. Warto zacząć od:

- **LeetCode:** [Zbiór zadań Prefix Sum](https://leetcode.com/problem-list/prefix-sum/)
- **USACO Guide:** [Srebrny poziom - Sumy prefiksowe - zadania](https://usaco.guide/silver/prefix-sums#problems)