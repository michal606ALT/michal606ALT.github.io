---
{"dg-publish":true,"permalink":"/szkola/informatyka/zadania/mnozenie/"}
---


# Cel
Mamy pomnożyć przez siebie 2 liczby, jednak są one za duże na liczbowe typy danych.

# Omówienie
Wczytamy te liczby początkowo [[String\|jako tekst]], a potem zamienimy na [[Tablica\|tablice]] cyfr. Przy okazji musimy obsłużyć możliwy minus.

Tablice powinny być odwrócone (ostatnia cyfra powinna być na początku).

Dalej stworzymy tablicę wynikową o rozmiarze $a.size() + b.size() - 1$.

Za pomocą 2 pętli zagnieżdżonych przechodzimy przez każdą parę cyfr $(a[i], b[j])$.

Pierwsza pętla powinna przechodzić przez cyfry $a$, a druga przez cyfry $b$. 

Teraz zapiszemy w tablicy wynikowej iloczyn tych dwóch cyfr, zwiększając wartość na pozycji $i + j$.
$$c[i + j] = a[i] + b[I]$$

Przechodzimy przez tablicę wynikową i jeżeli wartość jest większa niż 10, to przepisujemy "nadwyżkę" do kolejnego pola (możliwe jest że nam zabraknie pól, trzeba wtedy dodać nowy element na koniec tablicy).

Jeżeli wcześniej wyszło nam, że wynik będzie ujemny, to wypisujemy '-'. 

Idziemy od końca tablicy wynikowej, musimy pominąć wszystkie zera na początku liczby (np. 005 nie jest prawidłowym wynikiem).
