---
{"dg-publish":true,"permalink":"/szkola/informatyka/kolejka-priorytetowa/","tags":["PQ"]}
---

## Cel
Kolejka priorytetowa (priority queue - **PQ**) to struktura danych, która zawsze zwraca **największy element z podanych**. Możemy na niej wykonywać podobne operacje jak na zwykłej [[Szkoła/Informatyka/Kolejka\|kolejce]], jednak na przodzie jest zawsze największy element.

## Kiedy się to przydaje
Ta struktura danych bardzo często występuje w zadaniach typu zachłannego, ponieważ pozwala nam wybrać zachłannie element. Istnieje także wiele algorytmów na grafach z użyciem PQ. Przykładem takiego jest [[Szkoła/Informatyka/Algorytmy/Dijkstra's algorithm\|Algorytm Dijkstry]].

>[!warning] Wariacje
> Poza PQ, które zwraca największy element możemy także zrobić takie, co zawsze zwraca najmniejszy element.

## Stosowanie w C++
Będzie nam potrzebna odpowiednia biblioteka, jednak zalecam do używania `<bits/stdc++.h>` które zastępuje importowanie wszystkich bibliotek std

### Syntax
`priority_queue<typ, kontener(zazwyczaj vector<typ>, funckja porównująca`

Przykład (funkcja greater \<int> sprawia, że zawsze dostaniemy minimalny element)

```cpp
priority_queue<int, vector<int>, greater<int>>
```

Podstawowe operacje:

- **Push / Enqueue:** Wstawienie elementu do kolejki.
- **Pop / Dequeue:** Usunięcie elementu z początku kolejki.
- **Top:** Podgląd największego elementu (lub najmniejszego).
- **IsEmpty:** Sprawdzenie, czy kolejka jest pusta.