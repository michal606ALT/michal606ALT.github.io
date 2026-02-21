---
{"dg-publish":true,"permalink":"/szkola/informatyka/zadania/mnozenie/"}
---


## Cel

Standardowe typy danych (jak `int` czy `long long`) mają swoje limity pamięciowe. Gdy musimy pomnożyć przez siebie liczby mające setki lub tysiące cyfr, musimy zrezygnować z gotowych rozwiązań i zaimplementować własną logikę mnożenia, opartą na metodzie, którą znamy ze szkoły – **mnożeniu pisemnym**.

## Omówienie algorytmu

### 1. Przygotowanie danych

Liczby wczytujemy jako **ciągi znaków (String)**, co pozwala na ich dowolną długość. Następnie konwertujemy je na **tablice liczb**, przechowujące poszczególne cyfry.

- **Obsługa znaku:** Należy sprawdzić, czy liczby są ujemne. Wynik będzie ujemny tylko wtedy, gdy dokładnie jedna z liczb posiada minus. 
- **Odwrócenie kolejności:** Tablice cyfr warto odwrócić tak, aby cyfra jedności znalazła się pod indeksem `0`. To znacznie ułatwia zarządzanie indeksami podczas mnożenia i przenoszenia nadwyżek.

### 2. Tablica wynikowa

Rozmiar tablicy wynikowej $c$ powinien wynosić maksymalnie $a.size() + b.size()$.

> _Uwaga: Suma liczby cyfr dwóch mnożonych liczb określa maksymalną długość wyniku._

### 3. Logika mnożenia (Splot)

W przeciwieństwie do zwykłego mnożenia pisemnego, gdzie mnożymy liczbę a przez każdą cyfrę b, tu będziemy mnożyć każdą cyfrę a przez każdą cyfrę b.

Zamiast przejmować się skomplikowanymi przeniesieniami, pozwolimy zapisać dowolną liczbę na miejscu cyfry. W [[#4. Normalizacja wyniku (Obsługa przeniesień)]] się zajmiemy tego konsekwencjami.

Używając dwóch zagnieżdżonych pętli, mnożymy każdą cyfrę pierwszej liczby przez każdą cyfrę drugiej. Wynik mnożenia pary cyfr na pozycjach $i$ oraz $j$ dodajemy do tablicy wynikowej pod indeksem $i + j$.


Zależność tę opisuje wzór:

$$c[i + j] += a[i] \cdot b[j]$$

### 4. Normalizacja wyniku (Obsługa przeniesień)

Po zakończeniu mnożenia wszystkich par, w polach tablicy $c$ mogą znajdować się liczby znacznie większe niż 10. Musimy "uporządkować" tablicę, idąc od początku:

- Wartość pod danym indeksem zostaje zastąpiona przez resztę z dzielenia przez 10.
- Nadwyżka (część całkowita z dzielenia) przechodzi do kolejnego pola.

### 5. Formatowanie wyjścia

Zanim wyświetlimy wynik, musimy wykonać dwa kroki:

1. **Usunięcie zer wiodących:** Podczas mnożenia (np. $0 \cdot 0$) na końcu tablicy wynikowej mogą pojawić się niepotrzebne zera (np. otrzymamy `500` zamiast `5`). Należy je pominąć, aż trafimy na pierwszą cyfrę znaczącą.
2. **Znak:** Jeśli z analizy na początku wynika, że liczba jest ujemna (a wynik nie jest zerem), wypisujemy znak `-`.
3. **Kolejność:** Ponieważ operowaliśmy na odwróconych tablicach, wynik wypisujemy od końca.
