---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/sito-erastotenesa/"}
---

# Cel
Wyznaczenie wszystkich liczb pierwszych mniejszych od danej

# Idea działania
Jeżeli wykreślimy wielokrotności wszystkich mniejszych liczb pierwszych, to mamy pewność, że następna niewykreślona liczba też jest pierwsza.

Z przedziału $[2,n]$ bierzemy liczbę najmniejszą (2), i wykreślamy wszystkie jesj wielokrotności.

Z pozostałych wybieramy najmniejszą (3) i wykreślamy także jej wielokrotności.

Powtarzamy to do momentu, gdy kolejna wybrana liczba $i$ będzie większa niż $\sqrt{n}$

# Kiedy użyć?
W przypadku tego algorytmu proste jest zauważenie potrzeby jego użycia, gdy taka jest obecna.

# Implementacja

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> sieve(int & n) {
    if(n < 2) return {};
    vector<bool> prime (n+1, true);
	prime[0] = false;
	prime[1] = false;
	
	for(int i = 0; i*i <= n; i++){
		if(prime[i]){
			for(int j = i * i; t <= n; t+= i){
				prime[t] = false;
			}
		}
	}
	
	vector<int> res;
	for(int i = 2; i < prime.size(); i++){
		if(prime[i]) res.push_back(i);
	}
	return res;
}
```

# Złożoność
Czasowa: $O(n \log{\log{n}})$
