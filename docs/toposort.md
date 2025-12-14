---
title: Toposort (Kahn's Algorithm)
---

```cpp
vector<int> toposort(int n, vector<vector<int>> adj) {
    vector<int> sorted;
    vector<int> indegree(n);

    for (int i=0; i < n; i++) {
        for (int nextNode: adj[i]) {
            indegree[nextNode]++;
        }
    }

    queue<int> q;

    for (int i=0; i < n; i++) {
        if (indegree[i] == 0)
            q.push(i);
    }

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        sorted.push_back(node);

        for (int nextNode: adj[node]) {
            indegree[nextNode]--;
            if (indegree[nextNode] == 0)
                q.push(nextNode);
        }
    }

    return sorted;
}
```
