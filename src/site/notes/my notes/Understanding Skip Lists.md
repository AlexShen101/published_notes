---
{"dg-publish":true,"permalink":"/my-notes/understanding-skip-lists/","created":"2024-07-06T20:41:57.136-04:00","updated":"2024-07-06T20:42:29.562-04:00"}
---


In the world of computer science and data management, there are numerous ways to organize and access data efficiently. One such innovative data structure is the **skip list**. This blog aims to provide a comprehensive yet engaging primer on skip lists, covering their structure, operations, and analysis. By the end of this read, you'll have a solid understanding of skip lists and their significance in computer science.

## What is a Skip List?
A skip list is an advanced data structure that allows fast search, insertion, and deletion operations. It is essentially a hierarchy of linked lists where each level is a subset of the level below it. This hierarchical organization enables higher-level linked lists to "skip" many elements, making search operations more efficient.

### Structure of a Skip List
- **Levels and Sentinels**: Each skip list contains multiple levels, starting from the bottom level (L0) that includes all elements. Each higher level contains a subset of elements from the level below. Notably, each level contains two sentinel nodes: $-\infty $ and $+\infty $, which represent the negative and positive infinity bounds.
- **Nodes and Towers**: Each non-sentinel element in a skip list is a node. Nodes can be part of multiple levels, forming a structure known as a tower. Every node points to the node below it and the node after it.

## Operations on a Skip List
Skip lists support three primary operations: search, insertion, and deletion. Let's delve into each of these operations with a step-by-step breakdown.

### 1. Search
The search operation in a skip list begins at the topmost level and progresses downwards until the desired element is found or confirmed absent.

**Algorithm:**
```cpp
skipList::search(int k) {
    // Get the list of predecessors of key k
    std::stack<Node*> P = getPredecessors(k);

    // Get the predecessor of k in the bottom-level list (L0)
    Node* p0 = P.top();

    // Check if the key after p0 is k
    if (p0->after->key == k) {
        // If found, return the key-value pair at p0->after
        return p0->after->kvp;
    } else {
        // If not found, return "not found"
        return "not found";
    }
}
```
- **Step 1**: Start at the highest level and move right until the key is found or the next key is larger than the target.
- **Step 2**: Move down one level and repeat the process.
- **Step 3**: Continue until reaching the bottom level (L0). If the key is found, return it; otherwise, indicate its absence.

### Get Predecessors:
Get predecessors takes in a node with key k, and returns a stack containing every predecessor of the given node on each list of the skip list.
```cpp
std::stack<Node*> skipList::getPredecessors(int k) {
    // Start at the root node
    Node* p = root;

    // Initialize a stack of nodes, initially containing p
    std::stack<Node*> P;
    P.push(p);

    // Traverse downwards until reaching the bottom level
    while (p->below != NULL) {
        // Move to the node below
        p = p->below;
        // Traverse rightwards until the key after p is not less than k
        while (p->after->key < k) {
            p = p->after;
        }
        // Push the current node onto the stack
        P.push(p);
    }

    // Return the stack of predecessors
    return P;
}
```

### 2. Insertion
Inserting an element involves determining a random height for the node and then placing it appropriately across different levels.

**Algorithm:**
```cpp
void skipList::insert(int k, int v) {
    // Determine the random tower height
    int i;
    for (i = 0; random(2) == 1; i++);

    // Ensure the skip list has enough levels
    int h = 0;
    Node* p = root.below;
    while (p != NULL) {
        // Check if we need to increase the skip list height
        while (i >= h) {
            // Step 4: Create a new sentinel-only list and link it in below the topmost list
            createNewSentinelList();
            h++;
        }
        // Move to the node below
        p = p->below;
        h++;
    }

    // Get the list of predecessors for key k
    std::stack<Node*> P = getPredecessors(k);

    // Insert (k, v) in the bottom-level list (L0)
    Node* p = P.top();
    P.pop();
    Node* zbelow = new Node(k, v);
    zbelow->after = p->after;
    p->after = zbelow;

    // Insert k in levels L1 to Li
    while (i > 0) {
        p = P.top();
        P.pop();
        Node* z = new Node(k);
        z->after = p->after;
        p->after = z;
        z->below = zbelow;
        zbelow = z;
        i--;
    }
}
```
- **Step 1**: Determine a random height for the new node.
- **Step 2**: If necessary, create new levels to accommodate the height of the new node.
- **Step 3**: Identify the predecessors for the new node across all relevant levels.
- **Step 4**: Insert the new node at each level, linking it appropriately to maintain the skip list structure.

### 3. Deletion
Deletion involves finding all instances of the node across different levels and removing them.

**Algorithm:**
```cpp
skipList::delete(k)
1. P ← get-predecessors(k)
2. while P is non-empty
3. p ← P.pop() // predecessor of k in some list
4. if p.after.key = k
5. p.after ← p.after.after
6. else break // no more copies of k
```
- **Step 1**: Identify all predecessors of the node to be deleted.
- **Step 2**: Remove the node from each level where it appears.

## Analysis of Skip Lists
Since a skiplist is randomly generated from the insert method, we analyze the expected space and height from the skip list (the worst case is that insert doesn't terminate due to creating a node with infinite height).
- **Expected Space Usage**: $O(n)$, where $n$ is the number of elements in the skip list. This space complexity ensures that skip lists are space-efficient.
- **Expected Height**: $O(\log n)$. The height of a skip list grows logarithmically with the number of elements due to the probabilistic nature of node heights.
- **Time Complexity**: All operations (search, insert, delete) have an expected time complexity of $O(\log n)$. This is because each level of the skip list contains fewer nodes, making it faster to traverse the list.
