---
{"dg-publish":true,"permalink":"/szkola/informatyka/drzewo-przedzialowe/"}
---

## Cel i motywacja

Drzewo przedziałowe to jedna z najbardziej wszechstronnych struktur w informatyce, służąca do efektywnego zarządzania danymi rozłożonymi na liniowej osi. Rozwiązuje ono fundamentalny problem: jak pogodzić częste aktualizacje danych z częstymi zapytaniami o wyniki operacji na ich podzbiorach.

W przypadku zwykłej tablicy mamy do czynienia z kompromisem:

- **Aktualizacja punktowa:** $O(1)$.
- **Zapytanie o przedział:** wymaga przejścia pętlą przez elementy, co zajmuje $O(n)$.

Drzewo przedziałowe dzięki swojej hierarchicznej budowie sprowadza obie te operacje do złożoności logarytmicznej $O(\log n)$.


## Struktura i budowa

Drzewo przedziałowe jest pełnym drzewem binarnym. Każdy jego poziom reprezentuje coraz większe rozdrobnienie danych:

1. **Korzeń:** Reprezentuje cały zakres tablicy, od indeksu $0$ do $n-1$.
2. **Węzły wewnętrzne:** Każdy taki węzeł dzieli zakres swojego rodzica na dwie, niemal równe części. Jeśli rodzic obsługuje zakres $[L, R]$, to jego lewe dziecko obsłuży $[L, mid]$, a prawe $[mid + 1, R]$, gdzie $mid = (L+R)/2$.
3. **Liście:** To najniższy poziom drzewa. Każdy liść odpowiada dokładnie jednemu elementowi oryginalnej tablicy.
    

### Ile pamięci potrzeba?

Dla tablicy o rozmiarze $n$, która nie jest potęgą liczby 2, drzewo może posiadać puste węzły na ostatnim poziomie. Standardowo przyjmuje się bezpieczny rozmiar tablicy drzewa jako $4n$. Pozwala to uniknąć wyjścia poza zakres przy implementacji opartej na tablicy.


## Podstawowe warianty drzew

W zależności od tego, jaką funkcję agregującą przechowujemy w węzłach, drzewo zmienia swoje przeznaczenie.

### 1. Drzewo typu SUM (Suma na przedziale)

W każdym węźle przechowujemy sumę wartości jego dzieci.

- **Zastosowanie:** Obliczanie sumy elementów w zakresie $[L, R]$.
- **Węzeł rodzica:** `tree[v] = tree[2*v] + tree[2*v+1]`.
- **Neutralny element:** Dla operacji sumowania elementem neutralnym jest $0$ (zwracane, gdy zapytanie nie pokrywa się z zakresem węzła).
    

### 2. Drzewo typu MIN (Minimum na przedziale)

W każdym węźle przechowujemy najmniejszą wartość znalezioną w jego poddrzewie.

- **Zastosowanie:** Rozwiązywanie problemu RMQ (Range Minimum Query). Pozwala błyskawicznie sprawdzić, jaka jest najmniejsza wartość na danym odcinku.
- **Węzeł rodzica:** `tree[v] = min(tree[2*v], tree[2*v+1])`.
- **Neutralny element:** Nieskończoność (infinity), ponieważ każda inna liczba będzie od niej mniejsza.
    

### 3. Drzewo typu MAX (Maksimum na przedziale)

Działa analogicznie do drzewa typu MIN, ale przechowuje wartości największe.

- **Zastosowanie:** Szukanie najwyższego punktu, największego zysku lub limitów w danym zakresie.
- **Węzeł rodzica:** `tree[v] = max(tree[2*v], tree[2*v+1])`.
- **Neutralny element:** Minus nieskończoność lub $0$ (jeśli operujemy tylko na liczbach dodatnich).
    

## Operacje podstawowe krok po kroku

### Budowa (Build)

Proces budowy zaczynamy od liści (wartości tablicy) i idziemy w górę. Jest to proces rekurencyjny. Najpierw budujemy lewe poddrzewo, potem prawe, a na końcu obliczamy wartość dla bieżącego węzła na podstawie wyników jego dzieci. Złożoność wynosi $O(n)$.

```cpp
void build(vector<int> arr, int v, int tl, int tr) {
    if (tl == tr) {
        // Dotarliśmy do liścia
        tree[v] = arr[tl];
    } else {
        int tm = (tl + tr) / 2;
        // Budujemy lewe i prawe poddrzewo
        build(arr, 2 * v, tl, tm);
        build(arr, 2 * v + 1, tm + 1, tr);
        
        // Sumujemy wartości dzieci (dla MIN użyj: min, dla MAX: max)
        tree[v] = tree[2 * v] + tree[2 * v + 1];
    }
}
```

### Aktualizacja punktowa (Update)

Kiedy zmienia się wartość $arr[i]$, musimy:

1. Znaleźć liść odpowiadający indeksowi $i$.
2. Zmienić jego wartość.
3. Cofnąć się wzdłuż ścieżki do korzenia i przeliczyć wartości we wszystkich węzłach znajdujących się nad tym liściem.
    
    Ponieważ wysokość drzewa to $\log n$, wykonujemy tylko tyle operacji przeliczenia.

```cpp
// arr - tablica wejściowa, tree - tablica drzewa
// v - aktualny węzeł, tl/tr - lewy i prawy brzeg zakresu węzła
void build(int arr[], int v, int tl, int tr) {
    if (tl == tr) {
        tree[v] = arr[tl];
    } else {
        int tm = (tl + tr) / 2;
        build(arr, 2 * v, tl, tm);
        build(arr, 2 * v + 1, tm + 1, tr);
        
        tree[v] = tree[2 * v] + tree[2 * v + 1];
    }
}
```


### Zapytanie o przedział (Query)

To najbardziej wyrafinowana część. Zapytanie o zakres $[L, R]$ może trafić na węzeł, który:

- **Całkowicie mieści się w $[L, R]$:** Zwracamy gotową wartość z tego węzła.
- **Całkowicie leży poza $[L, R]$:** Zwracamy element neutralny (np. 0 lub nieskończoność).
- **Częściowo nachodzi na $[L, R]$:** Dzielimy zapytanie i wysyłamy je do obojga dzieci, a następnie łączymy wyniki.

Nawet jeśli przedział jest bardzo szeroki, zostanie on rozbity na najwyżej $2 \cdot \log n$ węzłów.

```cpp
// l, r - zakres zapytania użytkownika
int query(int v, int tl, int tr, int l, int r) {
    if (l > r) {
        return 0; //Element neutralny
    }
    if (l == tl && r == tr) {
        return tree[v];
    }
    int tm = (tl + tr) / 2;

    return query(2 * v, tl, tm, l, min(r, tm))
         + query(2 * v + 1, tm + 1, tr, max(l, tm + 1), r);
}
```

## Dalsze sposoby użycia drzew przedziałowych
To, co zostało omówione powyżej to dopiero wierzchołek góry lodowej, jeżeli chodzi o drzewa przedziałowe. [TODO]

