---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/sortowanie-babelkowe/"}
---


# Cel
Posortować [[Tablica\|tablicę]].

# Idea działania
Idziemy przez tablicę i jeżeli 2 kolejne elementy są w złej kolejności to je **zamieniamy ze sobą**. Przesuwamy iterator o 1 i sprawdzamy ponownie. Po 1 przejściu mamy gwarancje, że największy (lub najmniejszy element, zależy jak sortujemy) jest na końcu tablicy. Możemy iść od początku od nowa i powtarzać aż nie posortujemy całej tablicy.

# Lista kroków
1. Ustaw zmienną $i$ na 0. Będzie to nasz iterator.
2. Porównaj $tab[i]$ i $tab[i + 1]$, jeżeli są w złej kolejności zamień je.
3. Zwiększ $i$ o 1.
4. Powtarzaj kroki `2` i `3` aż $tab[i + 1]$ nie wyjdzie poza tablice
5. Powtarzaj kroki `1-4` aż cała tablica nie będzie posortowana (tab.size() - 1 razy) Za każdym razem możesz skrócić zakres iteratora i o 1, ponieważ końcowe elementu powinny już być posortowane.

# Złożoność
**Czasowa**: $O(n^2)$
**Pamięciowa**: O(1)

# Kiedy użyć
Prawie nigdy, to jest mało efektywny algorytm sortowania. Najczęściej używamy funkcji `sort()`. Jeżeli już musimy sami coś zaimplementować, to lepiej zrobić [[Merge sort\|Merge Sort]].

# Kod
```cpp
void bubbleSort(vector<int> & tab){
	for(int k = 0; k < tab.size() - 1; k++){
		bool changed = false; // Optymalizacja: sprawdzamy, czy tablica została już posortowana
		for(int i = 0; i < tab.size() - k - 1; i++){
			if(tab[i] > tab[i + 1]){
				swap(tab[i], tab[i + 1]);
				changed = true;
			}
		}
		if(!changed) break;
	}
}
```
