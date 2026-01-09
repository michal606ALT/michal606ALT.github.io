---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/algorytm-euklidesa/","tags":["informatyka","matematyka"]}
---

# Cel
Znajduje [[Największy Wspólny Dzielnik\|Największy Wspólny Dzielnik]] (GCD lub NWD) dwóch liczb.

# Idea działania
Dla dwóch liczb całkowitych dodatnich $a$ i $b$ zachodzi równość:

$$\text{NWD}(a, b) = \text{NWD}(b, a \pmod b)$$

Algorytm powtarzamy tak długo, aż reszta z dzielenia wyniesie **0**. Wtedy ostatnia niezerowa reszta (lub liczba, przez którą dzieliliśmy w ostatnim kroku) jest szukanym NWD.

Stworzymy dodatkową zmienną tymczasową, i tak długo jak $b$ nie będzie 0, będziemy powtarzać
$$c =a\mod{b}$$
$$a = b$$
$$b = c$$

# Kiedy użyć?
W przypadku tego algorytmu proste jest zauważenie potrzeby jego użycia, gdy taka jest obecna.

# Implementacja

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int NWD(int & a, int & b) {
    int c;
    while(b != 0){
        c = a%b;
        a = b;
        b = c;
    }
    return a;
}
```


# Złożoność
Czasowa: $O(n)$
Pamięciowa: O(log n)