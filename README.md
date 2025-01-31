# DSA-PROJECT-HASH-TABLE-IMPLEMENTATION
1. Structure and Components Node Class: Represents each entry in the hash table, storing a key-value pair and a pointer to the next node (for chaining). HashTable Class: Manages the hash table, including its operations and resizing logic.
2. Hashing Mechanism
The _hash function uses Python’s built-in hash() function with modulo (%) operation to determine an index in the table. If two keys hash to the same index, separate chaining via a linked list is used to store multiple values at that index.

3. Key Operations
Insertion (insert): Computes the index using _hash, then adds a new node at the front of the linked list if necessary. If the key already exists, its value is updated.
Search (search): Traverses the linked list at the computed index to find and return the value for the given key.
Deletion (delete): Searches for the key in the linked list and removes the corresponding node, ensuring proper linking.
