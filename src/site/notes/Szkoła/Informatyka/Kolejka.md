---
{"dg-publish":true,"permalink":"/szkola/informatyka/kolejka/"}
---

## Cel

Kolejka (ang. _queue_) to liniowa struktura danych działająca według zasady **FIFO** (First In, First Out). Oznacza to, że pierwszy element, który został dodany do kolekcji, będzie pierwszym, który ją opuści. Jest to dokładne przeciwieństwo stosu.

## Idea działania

Działanie kolejki można porównać do ogonika w sklepie – osoba, która przyszła jako pierwsza, jest obsługiwana jako pierwsza, a nowe osoby dołączają zawsze na samym końcu. Operacje odbywają się na dwóch różnych końcach: dodajemy z tyłu (ang. _back_), a usuwamy z przodu (ang. _front_).

Podstawowe operacje:

- **Push / Enqueue:** Wstawienie elementu na koniec kolejki.
- **Pop / Dequeue:** Usunięcie elementu z początku kolejki.
- **Front:** Podgląd wartości elementu znajdującego się na początku.
- **IsEmpty:** Sprawdzenie, czy kolejka jest pusta.

Złożoność czasowa dla wszystkich powyższych operacji wynosi $O(1)$.

## W c++
W c++ możemy użyć struktury danych `queue<type>`