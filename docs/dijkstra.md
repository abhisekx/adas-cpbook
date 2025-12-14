---
title: Dijkstra's Algorithm
---

```cpp
vector<int> dijkstra(int n, vector<vector<pair<int,int>>> adj, int start) {
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> q;
    vector<int> dist(n, int(1e9));
    dist[start] = 0;
    q.push({dist[start], start});

    while (!q.empty()) {
        int u = q.top().second;
        q.pop();

        for (auto& item: adj[u]) {
            int v = item.first;
            int d = item.second;

            if (dist[u] + d < dist[v]) {
                dist[v] = dist[u] + d;
                q.push({dist[v], v});
            }
        }
    }

    return dist;
}
```
