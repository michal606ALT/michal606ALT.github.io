---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/kmp/"}
---

To bardzo efektywny algorytm szukania fragmentów tekstu. Używa przedprocesowania fragmentu, aby mądrze obsługiwać niezgodności, przez co osiąga złożoność liniową.

# Idea
Jak można szukać tekstu w tekście? Wbrew pozorom jest to istotna funkcja, potrzebna w wielu dziedzinach informatyki (i nie tylko).

W dalszych podpunktach będziemy odnosić się do fragmentu szukanego jako $v$ i do tekstu w którym szukamy jako $a$
## Algorytm naiwny
Możemy iść po $a$ i zaczynając od każdego indeksu $i$ sprawdzać dla każdego miejsca $s$w $v$ czy $a[i + s] = v[s]$. Jak możemy zauważyć jest to bardzo nieefektywne, ponieważ gdy natrafimy na niezgodność, to musimy się cofać do samego początku w $v$.

## KMP
Zaczniemy od stworzenia tablicy $lps$. Longest prefix suffix to najdłuższy fragment na początku danego tekstu, który występuje też na końcu. Warto dodać, że prefix i suffix nie powinny się na siebie nakładać.

Na przykład dla fragmentu aabcdcdaab, najdłuższym takim jest aab.

Teraz jeżeli weźmiemy pierwsze $s$ znaków naszego $v$ to możemy wpisać najdłuższy prefix-suffix do $lps[s - 1]$ (tak, że nie bierzemy pod uwagę fragmentu 0 znakowego).

### Przykładowa konstrukcja lps
**Wzorzec: "aabaaac"**
- **Indeks 0: "a"** → Brak właściwego prefiksu/sufiksu → `lps[0] = 0`
- **Indeks 1: "aa"** → "a" jest zarówno prefiksem, jak i sufiksem → `lps[1] = 1`
- **Indeks 2: "aab"** → Żaden prefiks nie pasuje do sufiksu → `lps[2] = 0`
- **Indeks 3: "aaba"** → "a" jest prefiksem i sufiksem → `lps[3] = 1`
- **Indeks 4: "aabaa"** → "aa" jest prefiksem i sufiksem → `lps[4] = 2`
- **Indeks 5: "aabaaa"** → "aa" jest prefiksem i sufiksem (tutaj najdłuższym dopasowaniem jest "aa") → `lps[5] = 2`
- **Indeks 6: "aabaaac"** → Brak dopasowania (mismatch), następuje reset → `lps[6] = 0`
### Jak sprawnie obliczyć lps
Ponieważ tablica 1-elementowa nie ma poprawnych prefixów, które są suffixami, wpisujemy $lps[0] = 0$. Tworzymy zmienną $len$, która przetrzymuje jak długi jest poprzedni prefix suffix.

Idziemy przez $v$ od indexu 1, i porównujemy z $v[len]$. Mamy 3 przypadki.

Przypadek 1: $v[i] == v[len]$
To oznacza, że nowy znak kontynuuje istniejące dopasowanie.
- Zwiększamy $lps$ o 1
- $lps[i] = len$
- idziemy do kolejnego indeksu


Przypadek 2: $v[i] != v[len]$ i $len == 0$
Nie ma żadnego pasującego prefixu, więc nie możemy wrócić do poprzedniego spasowania.
- $lps[i] = 0$
- idziemy do kolejnego indeksu


Przypadek 3: $v[i] != v[len]$ i $len \neq 0$
Nie możemy kontynuować istniejącego ciągu, jednak może istnieć krótszy ciąg, który zadziała. Ponieważ $v[0...len -1]$ = $v[i - len...i-1]$, to możemy wrócić do $lps[len - 1]$.
- $len = lps[len - 1]$
- nie zmieniamy i

#### Kod
```cpp
vector<int> computeLPSArray(string &pattern) {
    int n = pattern.size();
    vector<int> lps(n, 0);
        
    int len = 0;  
    int i = 1;

    while (i < n) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) { 
                // wracamy do starego wzoru
                len = lps[len - 1];  
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }

    return lps;
}
```

## Dlaczego LPS jest takie ważne?

Tablica LPS (Longest Prefix Suffix) pozwala nam uniknąć bezcelowego sprawdzania tych samych znaków po raz drugi. W algorytmie naiwnym, po wykryciu niezgodności, cofamy się do początku wzorca. W KMP, dzięki LPS, wiemy dokładnie, o ile pozycji możemy bezpiecznie przesunąć nasz wzorzec, nie tracąc przy tym szansy na znalezienie dopasowania.

Wykorzystujemy fakt, że jeśli doszło do niezgodności na pozycji $j$, to znaki we wzorcu od $0$ do $j-1$ pasowały do tekstu. Tablica LPS mówi nam, jak duża część tego dopasowanego fragmentu jest jednocześnie swoim własnym początkiem. Dzięki temu „skaczemy” wzorcem do przodu, zamiast cofać się w tekście.


## Działanie Algorytmu KMP

Mając przygotowaną tablicę LPS, możemy przystąpić do przeszukiwania tekstu $a$ w poszukiwaniu wzorca $v$.

**Przebieg wyszukiwania:**

1. Używamy dwóch wskaźników: $i$ dla tekstu $a$ oraz $j$ dla wzorca $v$.
2. Jeśli znaki $a[i]$ oraz $v[j]$ są zgodne, zwiększamy oba wskaźniki.
3. Jeśli $j$ osiągnie długość wzorca, oznacza to znalezienie dopasowania. Wtedy $j$ przeskakuje do wartości $lps[j-1]$, aby szukać kolejnych wystąpień.
4. W przypadku niezgodności ($a[i] \neq v[j]$):
    - Jeśli $j \neq 0$, zmieniamy $j$ na $lps[j-1]$ (nie cofamy wskaźnika $i$!).
    - Jeśli $j = 0$, po prostu zwiększamy $i$, przechodząc do kolejnego znaku w tekście

Złożoność czasowa wyszukiwania wynosi $O(n)$, gdzie $n$ to długość tekstu $a$. Całkowita złożoność algorytmu (wraz z budową LPS) to $O(n + m)$, co czyni go niezwykle wydajnym.

```cpp

vector<int> computeLPSArray(string &pattern) {
    int n = pattern.size();
    vector<int> lps(n, 0);
        
    int len = 0;  
    int i = 1;

    while (i < n) {
        if (pattern[i] == pattern[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) { 
                // wracamy do starego wzoru
                len = lps[len - 1];  
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }

    return lps;
}

void KMPSearch(string text, string pattern) {
    int n = text.size();
    int m = pattern.size();

    // Przygotowanie tablicy pomocniczej
    vector<int> lps = computeLPSArray(pattern);

    int i = 0; // wskaźnik dla tekstu (text)
    int j = 0; // wskaźnik dla wzorca (pattern)

    while (i < n) {
        if (pattern[j] == text[i]) {
            i++;
            j++;
        }

        if (j == m) {
            cout << "Wzorzec znaleziony na indeksie: " << i - j << endl;
            
            // Przygotowanie do szukania kolejnych wystąpień
            j = lps[j - 1];
        } 
        else if (i < n && pattern[j] != text[i]) {
            if (j != 0) {
                // Dzięki LPS nie cofamy się w tekście (i zostaje w miejscu)
                j = lps[j - 1];
            } else {
                // Jeśli j jest na początku, po prostu przesuwamy się w tekście
                i++;
            }
        }
    }
}

```