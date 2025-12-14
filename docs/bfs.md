---
title: Breadth First Search
---

```cpp
vector<int> bfs(int n, vector<vector<int>> adj, vector<int> visited) {
    vector<int> traversal;
    queue<int> q;
    q.push(0);
    visited[0] = 1;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        traversal.push_back(node);

        for (auto nextNode: adj[node]) {
            if (!visited[nextNode]) {
                q.push(nextNode);
                visited[nextNode] = 1;
            }
        }
    }

    return traversal;
}
```
