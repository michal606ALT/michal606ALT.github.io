---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/test-pierwszosci/"}
---


# Cel
Sprawdzenie czy liczba jest pierwsza

# Idea działania
Liczba jest pierwsza jeżeli jej dzielnikami są tylko 1 i ona sama. Możemy sprawdzić wszystkie liczby w przedziale $[2, \sqrt{n}]$. Jest to **metoda naiwna**.

Zamiast tego możemy wygenerować liczby pierwsze za pomocą [[Szkoła/Informatyka/Algorytmy/Sito Erastotenesa\|sita Eratostenesa]] i sprawdzić tylko je.

Zaczniemy od generowania liczb pierwszych w przedziale $[0, \sqrt{n_{max}}]$. Potem aby sprawdzić czy dana liczba jest pierwsza przejdziemy przez liczby pierwsze po kolei i sprawdzimy czy zachodzi podzielność.

# Kiedy użyć?
Jeżeli mamy mało liczb, ale mogą być duże (np. $10^{14}$), to lepiej użyć metody naiwnej.

Jeżeli mamy dużo, ale stosunkowo małych liczb, to lepiej użyć sita.

# Implementacja

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPrime(vector<int> &primes, int& n){
	for(auto& p: primes){
		if(p * p > n) break;
		
		if(n % p == 0) return false;
	}
	return true;
}

```

# Złożoność
Czasowa: $O(\frac{\sqrt{n}}{\ln{\sqrt{n}}})$ (Jeżeli mamy listę liczb pierwszych)
Pamięciowa: $O(\sqrt{n_{max}}$