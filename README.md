# DSA-PROJECT-HASH-TABLE-IMPLEMENTATION
class Node:
    """Node for storing key-value pairs in a linked list (for chaining)."""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None

class HashTable:
    """Custom Hash Table with Chaining and Dynamic Resizing."""
    def __init__(self, size=10):
        self.size = size
        self.table = [None] * self.size
        self.count = 0  # Track number of elements
        self.load_factor_threshold = 0.7  # Resize if exceeded

    def _hash(self, key):
        """Hash function using modulo operation."""
        return hash(key) % self.size

    def _resize(self):
        """Doubles the table size and rehashes all elements."""
        new_size = self.size * 2
        new_table = [None] * new_size
        old_table = self.table
        self.table = new_table
        self.size = new_size
        self.count = 0  # Reset count and reinsert

        for node in old_table:
            while node:
                self.insert(node.key, node.value)
                node = node.next

    def insert(self, key, value):
        """Inserts a key-value pair into the hash table."""
        index = self._hash(key)
        node = self.table[index]

        while node:
            if node.key == key:
                node.value = value  # Update existing key
                return
            node = node.next

        # Insert new node at the head (chaining)
        new_node = Node(key, value)
        new_node.next = self.table[index]
        self.table[index] = new_node
        self.count += 1

        # Check if resizing is needed
        if self.count / self.size > self.load_factor_threshold:
            self._resize()

    def search(self, key):
        """Searches for a key in the hash table."""
        index = self._hash(key)
        node = self.table[index]

        while node:
            if node.key == key:
                return node.value
            node = node.next

        return None  # Key not found

    def delete(self, key):
        """Deletes a key-value pair from the hash table."""
        index = self._hash(key)
        node = self.table[index]
        prev = None

        while node:
            if node.key == key:
                if prev:
                    prev.next = node.next
                else:
                    self.table[index] = node.next
                self.count -= 1
                return True  # Key deleted
            prev = node
            node = node.next

        return False  # Key not found

    def display(self):
        """Displays the hash table contents."""
        for i, node in enumerate(self.table):
            print(f"Index {i}: ", end="")
            while node:
                print(f"({node.key}: {node.value}) -> ", end="")
                node = node.next
            print("None")

# Example Usage
ht = HashTable()
ht.insert("apple", 100)
ht.insert("banana", 200)
ht.insert("orange", 300)
ht.insert("grape", 400)
ht.display()

print("Search for 'banana':", ht.search("banana"))  # Output: 200
ht.delete("banana")
ht.display()
