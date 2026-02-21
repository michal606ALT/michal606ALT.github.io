---
{"dg-publish":true,"permalink":"/szkola/informatyka/stos/"}
---


## Cel

Stos (ang. _stack_) to liniowa struktura danych działająca według zasady **LIFO** (Last In, First Out). Oznacza to, że ostatni element, który został dodany do kolekcji, jest pierwszym, który ją opuszcza.

## Idea działania

Działanie stosu można porównać do wieży ułożonej z talerzy – aby zdjąć ten, który znajduje się na spodzie, musimy najpierw usunąć wszystkie leżące nad nim. Wszystkie operacje (dodawanie i usuwanie) odbywają się wyłącznie na jednym końcu, nazywanym wierzchołkiem (ang. _top_).

Podstawowe operacje :

- **Push:** Wstawienie elementu na wierzchołek stosu.
- **Pop:** Usunięcie elementu z wierzchołka.
- **Top/Peek:** Podgląd wartości elementu na wierzchołku bez jego usuwania.
- **IsEmpty:** Sprawdzenie, czy stos zawiera jakiekolwiek dane.

Złożoność czasowa dla wszystkich powyższych operacji wynosi $O(1)$.

## W c++
W c++ możemy użyć struktury danych `stack<type>`