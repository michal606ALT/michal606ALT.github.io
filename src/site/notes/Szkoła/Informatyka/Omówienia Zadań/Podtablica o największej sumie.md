---
{"dg-publish":true,"permalink":"/szkola/informatyka/omowienia-zadan/podtablica-o-najwiekszej-sumie/"}
---

# Cel
Znaleźć największą sumę [[Szkoła/Informatyka/Podtablica\|podtablicy]] w danej [[Szkoła/Informatyka/Tablica\|tablicy]].

# Metoda naiwna
Możemy przejść przez każdą możliwą podtablicę i iterując się przez jej elementy, obliczyć jej sumę.

**Złożoność czasowa**: $O(n^3)$
**Złożoność pamięciowa**: $O(1)$

# Lepsza metoda naiwna
Jeżeli znamy sumę elementów $[j,i]$ to możemy prosto obliczyć sumę $[j,i + 1]$, trzeba dodać wartość elementu $i + 1$.

**Złożoność czasowa**: $O(n^2)$
**Złożoność pamięciowa**: $O(1)$

# Metoda z użyciem [[Szkoła/Informatyka/Techniki/Suma prefiksowa\|sum prefiksowych]]
Wiemy że:
$$\text{Suma}(i, j) = P[j+1] - P[i]$$
Zauważmy, że aby suma były największa dla danego j, trzeba odjąć jak najmniejsze $P[i]$. Możemy zapamiętać, jaki był **najmniejszy element do tej pory** i go odjąć. To eliminuje złożoność kwadratową z naszego programu.

**Złożoność czasowa**: $O(n)$
**Złożoność pamięciowa**: $O(n)$

## Kod
```cpp
int maxSubArray(vector<int> & a){
	vector<int> prefix(a.size() + 1, 0);
	
	//Budujemy tablicę z sumami prefiksowymi
	for(int i = 0; i < a.size(); ++i){
		prefix[i + 1] = prefix[i] + a[i];
	}
	int res = INT_MIN; // Początkowo ustawiamy sumę na najmniejszą możliwą
	int minPrefix = 0;
	for(int j = 0; j < a.size(); j++){
		res = max(res, a[j] - minPrefix);
		minPrefix = min(minPrefix, a[j]);
	}
	return res;
}
```


# Najlepsza metoda
Zauważmy, że nigdy nie opłaca nam się zacząć podtablicy od fragmentu z sumą ujemną. 

Jeżeli napotkamy taki fragment, to lepiej od nowa zacząć liczyć tablicę, ponieważ zero jest większe niż jakakolwiek liczba ujemna (przeważnie).

Korzystając z tej zasady możemy znaleźć bardzo prostą metodę szukania takiej tablicy. Idziemy przez tablicę licząc teraźniejszą sumę i jeżeli jest mniejsza od 0, to ją ustawiamy na 0. W międzyczasie aktualizujemy największą sumę jaką spotkaliśmy.

## Dlaczego to działa?
**Szukamy najlepszego „początku” dla każdego końca.** Dla elementu na pozycji $i$, najlepszym początkiem jest albo on sam (jeśli to, co było wcześniej, dawało sumę ujemną), albo dołączenie do poprzedniej najlepszej grupy (jeśli ta była dodatnia).

**Złożoność czasowa**: $O(n)$
**Złożoność pamięciowa**: $O(1)$

# Kod
```cpp
int maxSubArray(vector<int>& nums) {
	int total = 0;
	int res = nums[0];
	for(int i = 0; i < nums.size(); i++){
		total += nums[i];
		res = max(res, total);
		
		total = max(total, 0); //Jeżeli suma jest ujemna, to ją pomijamy
	}
	return res;
}
```
