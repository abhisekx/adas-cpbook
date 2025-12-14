---
title: "Count Distinct Substrings"
---

```cpp
struct TrieNode {
    TrieNode* links[26];

    TrieNode() {
        for (int i = 0; i < 26; i++)
            links[i] = nullptr;
    }

    bool containsKey(char ch) {
        return links[ch - 'a'] != nullptr;
    }

    void put(char ch) {
        links[ch - 'a'] = new TrieNode();
    }

    TrieNode* get(char ch) {
        return links[ch - 'a'];
    }
};


int countDistinctSubstrings(string word) {
    TrieNode* root = new TrieNode();
    int count = 0;

    for (int i = 0; i < word.size(); i++) {
        TrieNode* node = root;

        for (int j = i; j < word.size(); j++) {
            if (!node->containsKey(word[j])) {
                node->put(word[j]);
                count++;
            }
            node = node->get(word[j]);
        }
    }

    return count + 1;
}
```
