---
{"dg-publish":true,"permalink":"/szkola/informatyka/techniki/rekurencja/"}
---

Funkcja rekurencyjna to taka, która woła samą siebie pośrednio lub bezpośrednio. 

Algorytm rekurencyjny za każdym wywołaniem funkcji powinien znajdować się o krok bliżej do wyniku.


# Przypadek bazowy
Ponieważ funkcja może wołać się w nieskończoność, konieczne jest ustanowienie sytuacji bazowej (np. Jeżeli a == 1 to zwróć 1).

# Argumenty

Za każdym razem, gdy wywołujemy funkcję rekurencyjnie, musimy zmodyfikować jej argumenty. W przeciwnym razie funkcja będzie przetwarzać te same dane w kółko, co doprowadzi do tzw. **przepełnienia stosu** (stack overflow). Zazwyczaj dążymy do tego, aby argument przybliżał nas do przypadku bazowego (np. zmniejszamy liczbę $n$ o 1 lub dzielimy zbiór danych na pół).

# Jak zaimplementować?

1. **Zdefiniuj przypadek bazowy**: To taki, gdzie wynik funkcji jest trywialny i nie wymaga dalszych wywołań.
2. **Zdefiniuj przypadek rekurencyjny**: Podziel problem na mniejsze podproblemy i rozwiąż je oddzielnie, wołając tę samą funkcję.
3. **Upewnij się, że funkcja ma koniec**: Funkcja musi zawsze trafić na jakiś przypadek bazowy. Wartość przekazywana niższemu pokoleniu funkcji powinna być mniejsza lub prostsza.
4. **Połącz wyniki funkcji po ich zawołaniu**: Zsumuj, pomnóż lub zestaw ze sobą rezultaty otrzymane z głębszych poziomów rekurencji.

# Kiedy używać

Rekurencji często używa się przy pracy z **drzewami** i grafami. Jeżeli jakiś program ma złożoność wykładniczą, to prawdopodobnie używa rekurencji.

Rekurencja jest przydatna, gdy w danej sytuacji musimy się „rozdzielić” na kilka przypadków. Silniki szachowe opierają się na rekurencji, ponieważ różne ruchy można przedstawić w formie drzewa. Warto jednak pamiętać o **memoizacji** (zapamiętywaniu wyników), aby nie obliczać tego samego kilka razy.

# Przykłady

### 1. Silnia (klasyka gatunku)

Silnia z liczby $n$ (zapisywana jako $n!$) to iloczyn wszystkich liczb naturalnych od 1 do $n$.

- **Przypadek bazowy**: $0! = 1$.
- **Krok rekurencyjny**: $n! = n \cdot (n-1)!$.

### 2. Ciąg Fibonacciego

Każda liczba w ciągu jest sumą dwóch poprzednich. To idealny przykład na to, jak funkcja „rozgałęzia się” na dwa kolejne wywołania.

- **Przypadek bazowy**: Dla $n=0$ zwróć 0, dla $n=1$ zwróć 1.
- **Krok rekurencyjny**: $F(n) = F(n-1) + F(n-2)$.