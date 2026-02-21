---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/merge-sort/"}
---

## Cel

Merge Sort (sortowanie przez scalanie) to stabilny algorytm sortowania, który gwarantuje stałą złożoność czasową $O(n \log n)$ niezależnie od początkowego układu danych. Wykorzystuje on paradygmat dziel i zwyciężaj.

## Idea działania

Algorytm opiera się na rekurencyjnym dzieleniu tablicy na coraz mniejsze fragmenty, aż osiągniemy pojedyncze elementy. Następnie wykonujemy proces scalania tych fragmentów w taki sposób, aby wynikowa struktura była posortowana.

Kluczowe kroki:

1. **Podział:** Znajdujemy środek tablicy i dzielimy ją na dwie połowy.
2. **Rekurencja:** Wywołujemy Merge Sort dla lewej i prawej części.
3. **Scalanie:** Łączymy dwie posortowane podtablice w jedną większą, zachowując porządek.

Złożoność czasowa w każdym przypadku (najlepszym, średnim i najgorszym):

$$T(n) = 2T(n/2) + n \implies O(n \log n)$$

## Kiedy użyć?

Merge Sort jest niezastąpiony, gdy wymagana jest stabilność (zachowanie kolejności elementów o tej samej wartości) oraz przewidywalny czas działania.

- **Zaleta:** Gwarantowana wydajność $O(n \log n)$ nawet dla skrajnie niekorzystnych danych.
- **Wada:** Wymaga $O(n)$ dodatkowej pamięci na pomocniczą tablicę podczas scalania.

To podejście jest szczególnie efektywne przy sortowaniu struktur danych, które nie oferują swobodnego dostępu do elementów, takich jak listy jednokierunkowe.


## Proces Scalania (Merge)

To najważniejszy etap algorytmu. Zakładamy, że mamy dwie posortowane podtablice i chcemy połączyć je w jedną.

**Przebieg operacji:**

1. Ustawiamy dwa wskaźniki na początku obu podtablic.
2. Porównujemy elementy wskazywane przez wskaźniki.
3. Mniejszy z nich trafia do tablicy wynikowej, a odpowiadający mu wskaźnik przesuwa się o jedną pozycję.
4. Powtarzamy czynność, aż jedna z podtablic zostanie opróżniona.
5. Pozostałe elementy z drugiej podtablicy kopiujemy bezpośrednio na koniec wyniku.

Dzięki temu, że wejściowe części są już posortowane, scalanie odbywa się w czasie liniowym $O(n)$.

## Implementacja

Poniżej znajduje się klasyczna implementacja wykorzystująca dodatkowy wektor pomocniczy.


```cpp
void merge(vector<int>& arr, int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```