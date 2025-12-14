---
title: "Trie"
---

```cpp
struct TrieNode {
    TrieNode* links[26];
    bool isLeaf;

    TrieNode() {
        for (int i=0; i < 26; i++)
            links[i] = nullptr;

        isLeaf = false;
    }

    bool containsKey(char key) {
        return links[key - 'a'] != nullptr;
    }

    void put(char key) {
        links[key - 'a'] = new TrieNode();
    }

    TrieNode* get(char key) {
        return links[key - 'a'];
    }

    void setEnd() {
        isLeaf = true;
    }

    bool isEnd() {
        return isLeaf;
    }
};


class Trie {
private:
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    void insert(string data) {
        TrieNode* node = root;

        for (char ch: data) {
            if (!node->containsKey(ch))
                node->put(ch);

            node = node->get(ch);
        }

        node->setEnd();
    }

    bool search(string data) {
        TrieNode* node = root;

        for (char ch: data) {
            if (!node->containsKey(ch))
                return false;

            node = node->get(ch);
        }

        return node->isEnd();
    }

    bool startsWith(string prefix) {
        TrieNode* node = root;

        for (char ch: prefix) {
            if (!node->containsKey(ch))
                return false;

            node = node->get(ch);
        }

        return true;
    }
};
```
