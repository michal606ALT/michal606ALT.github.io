---
{"dg-publish":true,"permalink":"/szkola/informatyka/techniki/suma-prefiksowa/"}
---

Jest to technika która polega na stworzeniu [[Tablica\|tablicy]] przechowywującej sumę pierwszych $i$ elementów.
$$a[i] = \sum_{n=1}^{i} t[n - 1]$$
Czasem $a[0]$ = 0, a czasem $a[0] = n[0]$. Zmienia to trochę sposób numerowania pól (pierwsza metoda przesuwa całą tablicę o 1 index w przód). 

# Kiedy użyć?
Ta metoda jest przydatna, kiedy chcemy znaleźć sumę jakiegoś przedziału w tablicy. Zamiast liczyć taką sumę liniowo, możemy zrobić to w czasie stałym.

$$\text{Suma}(L, R) = P[R + 1] - P[L]$$
L - początek przedziału
R - koniec przedziału
P - tablica z sumą prefiksową

Takie zastosowanie często występuje w problemach z [[Szkoła/Informatyka/Podtablica\|podtablicami]].

Możemy także obliczyć sumo postfiksową, czyli taką liczącą sumę od końca
$$
Post(k) = P[N] - P(N - k)
$$

# Implementacja

```cpp
vector<int> prefixSum (n + 1, 0);
for(int i = 0; i < n; i++){
	prefixSum[i + 1] = prefixSum[i] + arr[i];
}
```

# Zadania
## Leetcode
https://leetcode.com/problem-list/prefix-sum/