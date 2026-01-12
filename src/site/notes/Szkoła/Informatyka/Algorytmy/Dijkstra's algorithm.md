---
{"dg-publish":true,"permalink":"/szkola/informatyka/algorytmy/dijkstra-s-algorithm/"}
---


# Cel
Znaleźć najkrótszą drogę od źródła do każdego z wierzchołków na [[Graf\|grafie]].

# Plan działania
1. Tworzymy tablicę $dystans$ i ustawiamy wartość wszystkich elementów na $\infty$. Źródło powinno mieć wartość 0.
2. Tworzymy [[Heap\|kolejkę priorytetową]] i na początku wrzucamy do niej parę $(\text{0; źródło})$ kolejką będzie przetrzymywała pary $(dystans, wierzchołek)$.
3. Weź pierwszy element ($u$) z kolejki i dla każdego jego sąsiada ($v$): Jeżeli$$dystans[v] > dystans[u] + waga$$ to$$dystans[v] = dystans[u] + waga$$ i dodaj nową parę do kolejki
4. Jeżeli `d_z_kolejki > dystans[u]`, to znaczy, że w międzyczasie znaleźliśmy już lepszą trasę do wierzchołka $u$ i ten wpis w kolejce jest "przeterminowany". Wtedy robimy `continue`.
5. Bierzemy nowe elementy, tak długo aż kolejka nie będzie pusta.

# Kod

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

const long long INF = 1e18;

struct Edge {
    int to;
    int weight;
};

void dijkstra(int start, const vector<vector<Edge>>& graph) {
    int n = graph.size();
    
    vector<long long> dist(n, INF);
    dist[start] = 0;

    // 2. Kolejka priorytetowa przechowująca pary {dystans, wierzchołek}
    // std::greater sprawia, że najmniejsze wartości są na górze (min-heap)
    priority_queue<pair<long long, int>, vector<pair<long long, int>>, greater<pair<long long, int>>> pq;
    
    pq.push({0, start});

    while (!pq.empty()) {
        long long d = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        // 4. Sprawdzenie, czy to "stara" wartość
        if (d > dist[u]) continue;
        
        for (const auto& edge : graph[u]) {
            int v = edge.to;
            int weight = edge.weight;

            if (dist[v] > dist[u] + weight) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }

    cout << "Najkrótsze dystanse od wierzchołka " << start << ":" << endl;
    for (int i = 0; i < n; i++) {
        if (dist[i] == INF) cout << i << ": nieosiągalny" << endl;
        else cout << i << ": " << dist[i] << endl;
    }
}

int main() {
    int nodes = 5;
    vector<vector<Edge>> graph(nodes);

    // Przykładowy graf
    graph[0].push_back({1, 4});
    graph[0].push_back({2, 1});
    graph[2].push_back({1, 2});
    graph[1].push_back({3, 1});
    graph[2].push_back({3, 5});
    graph[3].push_back({4, 3});

    dijkstra(0, graph);

    return 0;
}
```

# Wersja z wieloma źródłami
Możemy chcieć użyć więcej niż 1 źródła. Wtedy będziemy szukać najmniejszego dystansu od jakiegokolwiek z źródeł.

Wtedy dla każdego źródła ustawimy $dystans[u] = 0$ i wszystkie źródła trafią początkowo do kolejki priorytetowej.
