---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/dfs/"}
---

**D**epth **F**irst **S**earch
To metoda przejścia po [[Graf\|grafie]], która kompletnie przegląda jedną scieżkę, zanim cofa się do następnej.

# Idea
Gdybyśmy chcieli rozwiązać labirynt, to moglibyśmy iść daną ścieżką, tak długo aż nie trafimy na ścianę (ślepy zaułek), a potem się cofać do ostatniego rozwidlenia. Jeżeli labirynt ma rozwiązanie, a my nie zapętlamy się, to kiedyś znajdziemy wyjście. To jest właśnie DFS, ponieważ labirynt to swego rodzaju [[Graf\|graf]], gdzie rozwidlenia są wierzchołkami.

# Implementacja
Jeżeli nasz graf może mieć zapętlenia, to będziemy potrzebowali jakieś metody, aby zapisać gdzie już byliśmy. Jeżeli napotkamy wierzchołek który już odwiedziliśmy, to możemy go pominąć.
## [[Szkoła/Informatyka/Techniki/Rekurencja\|Rekurencyjna]]
DFS jest idealny do implementacji rekurencyjnej. Jeżeli mamy funkcję, która przegląda wszystkie wierzchołki zaczynając od danego $u$, to wystarczy że w niej zawołamy ją samą dla każdego sąsiada $u$. 

Przykładowy kod 
```cpp
vector<bool> visited(n, false);
vector<vector<int>> adj (n); //Lista sąsiedztwa, do przechowania grafu

void DFS(int node){
	for(auto & v: adj[node]){
		DFS(v); // wołamy tą funkcję dla każdego sąsiada
	}
}
```

Oczywiście normalnie chcemy, aby nasza funkcja coś robiła (na przykład zwracała największa wartość) wtedy zmieniamy typ funkcji na potrzebny. 

