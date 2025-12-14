---
title: Depth First Search
---

```cpp
vector<int> dfs(int start, vector<vector<int>> adj, vector<int> visited) {
    vector<int> traversal;
    visited[start] = 1;
    traversal.push_back(start);

    for (auto next: adj[start]) {
        if (!visited[next]) {
            dfs(next, adj, visited);
        }
    }

    return traversal;
}
```
