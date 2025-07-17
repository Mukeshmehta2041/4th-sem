# Unit 5: Advanced Data Structures, Search Techniques, and NP-Completeness - Comprehensive Study Guide

## Table of Contents
1. Binary Search Trees (BST)
2. Height Balanced Trees (AVL Trees)
3. 2-3 Trees
4. B-Trees
5. Tree Traversal Techniques
6. Graph Search and Traversal Techniques
7. NP-Completeness Theory
8. Comparison of Data Structures
9. Practice Problems and Solutions

---

## 1. Binary Search Trees (BST) - Detailed Analysis

### What is a Binary Search Tree?
A Binary Search Tree is a binary tree data structure where for each node:
- All values in the left subtree are less than the node's value
- All values in the right subtree are greater than the node's value
- Both left and right subtrees are also BSTs

### BST Properties
1. **Ordering Property**: In-order traversal gives sorted sequence
2. **Unique Path**: Each value has a unique path from root
3. **Recursive Structure**: Each subtree is also a BST
4. **Dynamic**: Supports efficient insertion and deletion

### BST Node Structure
```python
class BSTNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.parent = None  # Optional: for easier deletion
    
    def __str__(self):
        return str(self.data)
```

### Complete BST Implementation

```python
class BinarySearchTree:
    def __init__(self):
        self.root = None
        self.size = 0
    
    def insert(self, data):
        """Insert a new value into BST"""
        if self.root is None:
            self.root = BSTNode(data)
            self.size += 1
            return
        
        self._insert_recursive(self.root, data)
    
    def _insert_recursive(self, node, data):
        """Recursive helper for insertion"""
        if data < node.data:
            if node.left is None:
                node.left = BSTNode(data)
                node.left.parent = node
                self.size += 1
            else:
                self._insert_recursive(node.left, data)
        elif data > node.data:
            if node.right is None:
                node.right = BSTNode(data)
                node.right.parent = node
                self.size += 1
            else:
                self._insert_recursive(node.right, data)
        # If data == node.data, do nothing (no duplicates)
    
    def search(self, data):
        """Search for a value in BST"""
        return self._search_recursive(self.root, data)
    
    def _search_recursive(self, node, data):
        """Recursive helper for search"""
        if node is None:
            return False
        
        if data == node.data:
            return True
        elif data < node.data:
            return self._search_recursive(node.left, data)
        else:
            return self._search_recursive(node.right, data)
    
    def find_min(self, node=None):
        """Find minimum value in BST or subtree"""
        if node is None:
            node = self.root
        
        if node is None:
            return None
        
        while node.left is not None:
            node = node.left
        return node
    
    def find_max(self, node=None):
        """Find maximum value in BST or subtree"""
        if node is None:
            node = self.root
        
        if node is None:
            return None
        
        while node.right is not None:
            node = node.right
        return node
    
    def delete(self, data):
        """Delete a value from BST"""
        self.root = self._delete_recursive(self.root, data)
    
    def _delete_recursive(self, node, data):
        """Recursive helper for deletion"""
        if node is None:
            return node
        
        if data < node.data:
            node.left = self._delete_recursive(node.left, data)
        elif data > node.data:
            node.right = self._delete_recursive(node.right, data)
        else:
            # Node to be deleted found
            self.size -= 1
            
            # Case 1: Node has no children (leaf)
            if node.left is None and node.right is None:
                return None
            
            # Case 2: Node has one child
            elif node.left is None:
                return node.right
            elif node.right is None:
                return node.left
            
            # Case 3: Node has two children
            else:
                # Find inorder successor (smallest in right subtree)
                successor = self.find_min(node.right)
                
                # Replace node's data with successor's data
                node.data = successor.data
                
                # Delete the successor
                node.right = self._delete_recursive(node.right, successor.data)
        
        return node
```

### BST Traversal Methods

```python
def inorder_traversal(self, node=None, result=None):
    """In-order traversal: Left -> Root -> Right"""
    if result is None:
        result = []
    if node is None:
        node = self.root
    
    if node is not None:
        self.inorder_traversal(node.left, result)
        result.append(node.data)
        self.inorder_traversal(node.right, result)
    
    return result

def preorder_traversal(self, node=None, result=None):
    """Pre-order traversal: Root -> Left -> Right"""
    if result is None:
        result = []
    if node is None:
        node = self.root
    
    if node is not None:
        result.append(node.data)
        self.preorder_traversal(node.left, result)
        self.preorder_traversal(node.right, result)
    
    return result

def postorder_traversal(self, node=None, result=None):
    """Post-order traversal: Left -> Right -> Root"""
    if result is None:
        result = []
    if node is None:
        node = self.root
    
    if node is not None:
        self.postorder_traversal(node.left, result)
        self.postorder_traversal(node.right, result)
        result.append(node.data)
    
    return result
```

### Complete Example: BST Operations

```python
# Create BST and insert values
bst = BinarySearchTree()
values = [50, 30, 70, 20, 40, 60, 80]

print("Inserting values:", values)
for val in values:
    bst.insert(val)

print("BST structure:")
print("Root:", bst.root.data)
print("Size:", bst.size)

# Tree structure:
#       50
#      /  \
#    30    70
#   / \   / \
#  20 40 60 80

print("\nTraversals:")
print("In-order:", bst.inorder_traversal())     # [20, 30, 40, 50, 60, 70, 80]
print("Pre-order:", bst.preorder_traversal())   # [50, 30, 20, 40, 70, 60, 80]
print("Post-order:", bst.postorder_traversal()) # [20, 40, 30, 60, 80, 70, 50]

print("\nSearch operations:")
print("Search 40:", bst.search(40))  # True
print("Search 90:", bst.search(90))  # False

print("\nMin and Max:")
print("Minimum:", bst.find_min().data)  # 20
print("Maximum:", bst.find_max().data)  # 80

print("\nDeletion:")
print("Delete 30 (node with two children)")
bst.delete(30)
print("In-order after deletion:", bst.inorder_traversal())  # [20, 40, 50, 60, 70, 80]
```

### BST Complexity Analysis

| Operation | Average Case | Worst Case | Best Case |
|-----------|--------------|------------|-----------|
| Search | O(log n) | O(n) | O(1) |
| Insert | O(log n) | O(n) | O(1) |
| Delete | O(log n) | O(n) | O(1) |
| Traversal | O(n) | O(n) | O(n) |

### BST Problems and Limitations

#### 1. Skewed Trees
```python
def demonstrate_skewed_bst():
    """Show how BST can become skewed (worst case)"""
    bst = BinarySearchTree()
    
    # Insert in sorted order - creates right-skewed tree
    for i in range(1, 8):
        bst.insert(i)
    
    # Tree becomes: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7
    # Height = n-1, operations become O(n)
    
    print("Skewed BST height:", calculate_height(bst.root))  # 6
    print("Balanced BST height would be:", math.log2(7))     # ~2.8

def calculate_height(node):
    """Calculate height of BST"""
    if node is None:
        return -1
    return 1 + max(calculate_height(node.left), calculate_height(node.right))
```

#### 2. BST Validation
```python
def is_valid_bst(node, min_val=float('-inf'), max_val=float('inf')):
    """Check if binary tree is valid BST"""
    if node is None:
        return True
    
    if node.data <= min_val or node.data >= max_val:
        return False
    
    return (is_valid_bst(node.left, min_val, node.data) and
            is_valid_bst(node.right, node.data, max_val))
```

### BST Applications
1. **Database Indexing**: B-trees (extension of BST)
2. **Expression Parsing**: Parse trees for mathematical expressions
3. **File Systems**: Directory structures
4. **Priority Queues**: When frequent insertions/deletions needed
5. **Symbol Tables**: Compiler design

---

## 2. Height Balanced Trees (AVL Trees) - Detailed Analysis

### What are AVL Trees?
AVL (Adelson-Velsky and Landis) trees are self-balancing binary search trees where the height difference between left and right subtrees of any node is at most 1.

### AVL Tree Properties
1. **Balance Factor**: For each node, |height(left) - height(right)| ≤ 1
2. **Self-Balancing**: Automatically maintains balance through rotations
3. **Height Guarantee**: Height is always O(log n)
4. **BST Property**: Maintains BST ordering

### Balance Factor Calculation
```python
def get_balance_factor(node):
    """Calculate balance factor of a node"""
    if node is None:
        return 0
    
    left_height = get_height(node.left)
    right_height = get_height(node.right)
    
    return left_height - right_height

def get_height(node):
    """Get height of a node"""
    if node is None:
        return 0
    return node.height
```

### AVL Node Structure
```python
class AVLNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.height = 1  # Height of node (leaf = 1)
    
    def update_height(self):
        """Update height based on children"""
        left_height = self.left.height if self.left else 0
        right_height = self.right.height if self.right else 0
        self.height = 1 + max(left_height, right_height)
```

### AVL Rotations

#### 1. Right Rotation (LL Case)
```python
def right_rotate(y):
    """
    Right rotation for LL imbalance
    
        y               x
       / \             / \
      x   T3    =>    T1  y
     / \                 / \
    T1  T2              T2  T3
    """
    x = y.left
    T2 = x.right
    
    # Perform rotation
    x.right = y
    y.left = T2
    
    # Update heights
    y.update_height()
    x.update_height()
    
    return x  # New root
```

#### 2. Left Rotation (RR Case)
```python
def left_rotate(x):
    """
    Left rotation for RR imbalance
    
      x                 y
     / \               / \
    T1  y      =>     x   T3
       / \           / \
      T2  T3        T1  T2
    """
    y = x.right
    T2 = y.left
    
    # Perform rotation
    y.left = x
    x.right = T2
    
    # Update heights
    x.update_height()
    y.update_height()
    
    return y  # New root
```

### Complete AVL Tree Implementation

```python
class AVLTree:
    def __init__(self):
        self.root = None
    
    def insert(self, data):
        """Insert value and maintain AVL property"""
        self.root = self._insert_recursive(self.root, data)
    
    def _insert_recursive(self, node, data):
        """Recursive insertion with balancing"""
        # Step 1: Perform normal BST insertion
        if node is None:
            return AVLNode(data)
        
        if data < node.data:
            node.left = self._insert_recursive(node.left, data)
        elif data > node.data:
            node.right = self._insert_recursive(node.right, data)
        else:
            return node  # No duplicates
        
        # Step 2: Update height
        node.update_height()
        
        # Step 3: Get balance factor
        balance = get_balance_factor(node)
        
        # Step 4: Perform rotations if unbalanced
        
        # Left Left Case
        if balance > 1 and data < node.left.data:
            return right_rotate(node)
        
        # Right Right Case
        if balance < -1 and data > node.right.data:
            return left_rotate(node)
        
        # Left Right Case
        if balance > 1 and data > node.left.data:
            node.left = left_rotate(node.left)
            return right_rotate(node)
        
        # Right Left Case
        if balance < -1 and data < node.right.data:
            node.right = right_rotate(node.right)
            return left_rotate(node)
        
        return node
    
    def delete(self, data):
        """Delete value and maintain AVL property"""
        self.root = self._delete_recursive(self.root, data)
    
    def _delete_recursive(self, node, data):
        """Recursive deletion with balancing"""
        # Step 1: Perform normal BST deletion
        if node is None:
            return node
        
        if data < node.data:
            node.left = self._delete_recursive(node.left, data)
        elif data > node.data:
            node.right = self._delete_recursive(node.right, data)
        else:
            # Node to be deleted
            if node.left is None:
                return node.right
            elif node.right is None:
                return node.left
            else:
                # Node with two children
                successor = self._find_min(node.right)
                node.data = successor.data
                node.right = self._delete_recursive(node.right, successor.data)
        
        # Step 2: Update height
        node.update_height()
        
        # Step 3: Get balance factor
        balance = get_balance_factor(node)
        
        # Step 4: Perform rotations if unbalanced
        
        # Left Left Case
        if balance > 1 and get_balance_factor(node.left) >= 0:
            return right_rotate(node)
        
        # Left Right Case
        if balance > 1 and get_balance_factor(node.left) < 0:
            node.left = left_rotate(node.left)
            return right_rotate(node)
        
        # Right Right Case
        if balance < -1 and get_balance_factor(node.right) <= 0:
            return left_rotate(node)
        
        # Right Left Case
        if balance < -1 and get_balance_factor(node.right) > 0:
            node.right = right_rotate(node.right)
            return left_rotate(node)
        
        return node
    
    def _find_min(self, node):
        """Find minimum node in subtree"""
        while node.left is not None:
            node = node.left
        return node
```

### Complete AVL Example

```python
# Create AVL tree and demonstrate balancing
avl = AVLTree()
values = [10, 20, 30, 40, 50, 25]

print("Inserting values:", values)
for val in values:
    avl.insert(val)
    print(f"After inserting {val}:")
    print_tree_structure(avl.root)
    print()

# Insertion trace:
# Insert 10: Tree = [10]
# Insert 20: Tree = [10, None, 20]  
# Insert 30: Tree becomes unbalanced, left rotation needed
#   Before: 10 -> 20 -> 30 (right skewed)
#   After:     20
#            /    \
#          10      30

# Insert 40: Tree = [20, 10, 30, None, None, None, 40]
# Insert 50: Right subtree becomes unbalanced
#   Before:    20           After:     20
#            /    \                  /    \
#          10      30              10      40
#                    \                   /  \
#                     40               30    50
#                       \
#                        50

# Insert 25: Causes LR rotation in right subtree
```

### AVL vs Regular BST Comparison

```python
def compare_avl_vs_bst():
    """Compare AVL tree with regular BST"""
    
    # Worst case for BST: sorted input
    sorted_values = list(range(1, 16))
    
    # Regular BST
    bst = BinarySearchTree()
    for val in sorted_values:
        bst.insert(val)
    
    # AVL Tree
    avl = AVLTree()
    for val in sorted_values:
        avl.insert(val)
    
    print("Comparison for sorted input [1, 2, ..., 15]:")
    print(f"BST height: {calculate_height(bst.root)}")      # 14 (skewed)
    print(f"AVL height: {calculate_height(avl.root)}")      # 3 (balanced)
    print(f"Optimal height: {math.ceil(math.log2(16))}")    # 4
```

### AVL Tree Complexity

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Search | O(log n) | O(1) |
| Insert | O(log n) | O(log n) recursion |
| Delete | O(log n) | O(log n) recursion |
| Height | Always O(log n) | - |

### AVL Tree Applications
1. **Database Systems**: When frequent lookups needed
2. **Memory Management**: Balanced allocation trees
3. **Graphics**: Spatial data structures
4. **Compilers**: Symbol table management---

##
 3. 2-3 Trees - Detailed Analysis

### What are 2-3 Trees?
A 2-3 tree is a balanced search tree where:
- Each internal node has either 2 or 3 children
- All leaves are at the same level
- A 2-node contains 1 key and has 2 children
- A 3-node contains 2 keys and has 3 children

### 2-3 Tree Properties
1. **Perfect Balance**: All leaves at same level
2. **Flexible Node Size**: Nodes can have 2 or 3 children
3. **Ordered Keys**: Keys in each node are sorted
4. **Search Property**: For 2-node with key k: left < k < right
5. **Search Property**: For 3-node with keys k₁ < k₂: left < k₁ < middle < k₂ < right

### Node Structure for 2-3 Trees

```python
class Node23:
    def __init__(self):
        self.keys = []          # 1 or 2 keys
        self.children = []      # 2 or 3 children (empty for leaves)
        self.is_leaf = True
    
    def is_2_node(self):
        return len(self.keys) == 1
    
    def is_3_node(self):
        return len(self.keys) == 2
    
    def is_full(self):
        return len(self.keys) == 2
    
    def add_key(self, key):
        """Add key maintaining sorted order"""
        self.keys.append(key)
        self.keys.sort()
    
    def add_child(self, child):
        """Add child at appropriate position"""
        self.children.append(child)
        if not self.is_leaf:
            # Sort children based on their minimum keys
            self.children.sort(key=lambda x: min(x.keys) if x.keys else float('inf'))
```

### 2-3 Tree Implementation

```python
class Tree23:
    def __init__(self):
        self.root = Node23()
    
    def search(self, key):
        """Search for a key in 2-3 tree"""
        return self._search_recursive(self.root, key)
    
    def _search_recursive(self, node, key):
        """Recursive search helper"""
        if node.is_leaf:
            return key in node.keys
        
        # Determine which child to search
        if node.is_2_node():
            if key < node.keys[0]:
                return self._search_recursive(node.children[0], key)
            elif key == node.keys[0]:
                return True
            else:
                return self._search_recursive(node.children[1], key)
        
        else:  # 3-node
            if key < node.keys[0]:
                return self._search_recursive(node.children[0], key)
            elif key == node.keys[0]:
                return True
            elif key < node.keys[1]:
                return self._search_recursive(node.children[1], key)
            elif key == node.keys[1]:
                return True
            else:
                return self._search_recursive(node.children[2], key)
    
    def insert(self, key):
        """Insert key into 2-3 tree"""
        result = self._insert_recursive(self.root, key)
        
        # If root split, create new root
        if isinstance(result, tuple):
            new_root = Node23()
            new_root.keys = [result[1]]
            new_root.children = [result[0], result[2]]
            new_root.is_leaf = False
            self.root = new_root
    
    def _insert_recursive(self, node, key):
        """
        Recursive insertion helper
        Returns: Node if no split, (left_node, middle_key, right_node) if split
        """
        
        if node.is_leaf:
            if key in node.keys:
                return node  # Duplicate key
            
            node.add_key(key)
            
            if len(node.keys) <= 2:
                return node
            else:
                # Split leaf node (has 3 keys)
                return self._split_node(node)
        
        else:
            # Internal node - find correct child
            child_index = self._find_child_index(node, key)
            result = self._insert_recursive(node.children[child_index], key)
            
            if isinstance(result, tuple):
                # Child split - need to handle promotion
                left_child, promoted_key, right_child = result
                
                # Replace old child with left_child
                node.children[child_index] = left_child
                
                # Insert promoted key and right child
                node.add_key(promoted_key)
                node.children.insert(child_index + 1, right_child)
                
                if len(node.keys) <= 2:
                    return node
                else:
                    # This node also needs to split
                    return self._split_node(node)
            
            return node
    
    def _find_child_index(self, node, key):
        """Find which child should contain the key"""
        if node.is_2_node():
            return 0 if key < node.keys[0] else 1
        else:  # 3-node
            if key < node.keys[0]:
                return 0
            elif key < node.keys[1]:
                return 1
            else:
                return 2
    
    def _split_node(self, node):
        """
        Split a node with 3 keys into two nodes with 1 key each
        Returns: (left_node, middle_key, right_node)
        """
        keys = sorted(node.keys)
        left_node = Node23()
        right_node = Node23()
        
        # Distribute keys
        left_node.keys = [keys[0]]
        middle_key = keys[1]
        right_node.keys = [keys[2]]
        
        # Set leaf status
        left_node.is_leaf = node.is_leaf
        right_node.is_leaf = node.is_leaf
        
        # Distribute children if internal node
        if not node.is_leaf:
            left_node.children = node.children[:2]
            right_node.children = node.children[2:]
        
        return (left_node, middle_key, right_node)
```

### Complete 2-3 Tree Example

```python
def demonstrate_23_tree():
    """Demonstrate 2-3 tree operations"""
    tree = Tree23()
    values = [10, 20, 30, 40, 50, 60, 70]
    
    print("Inserting values into 2-3 tree:", values)
    
    for val in values:
        print(f"\nInserting {val}:")
        tree.insert(val)
        print_23_tree(tree.root, 0)
    
    # Insertion trace:
    # Insert 10: [10]
    # Insert 20: [10, 20]
    # Insert 30: [10, 20, 30] -> Split -> 
    #            20
    #           /  \
    #         [10] [30]
    
    # Insert 40: 
    #            20
    #           /  \
    #         [10] [30, 40]
    
    # Insert 50: [30, 40, 50] splits ->
    #              20
    #           /      \
    #         [10]   [40]
    #               /    \
    #            [30]   [50]
    # But this violates 2-3 property, so we get:
    #           20, 40
    #          /   |   \
    #       [10] [30] [50]
    
    print("\nFinal tree structure:")
    print_23_tree(tree.root, 0)
    
    print("\nSearch operations:")
    for val in [25, 30, 45]:
        result = tree.search(val)
        print(f"Search {val}: {result}")

def print_23_tree(node, level):
    """Print 2-3 tree structure"""
    if node is None:
        return
    
    indent = "  " * level
    print(f"{indent}Keys: {node.keys}")
    
    if not node.is_leaf:
        for i, child in enumerate(node.children):
            print(f"{indent}Child {i}:")
            print_23_tree(child, level + 1)
```

### 2-3 Tree Deletion

```python
def delete(self, key):
    """Delete key from 2-3 tree"""
    self.root = self._delete_recursive(self.root, key)
    
    # If root becomes empty, replace with its only child
    if not self.root.keys and self.root.children:
        self.root = self.root.children[0]

def _delete_recursive(self, node, key):
    """Recursive deletion helper"""
    if node.is_leaf:
        if key in node.keys:
            node.keys.remove(key)
        return node
    
    # Find child that should contain key
    child_index = self._find_child_index(node, key)
    
    # Check if key is in current node
    if key in node.keys:
        # Replace with predecessor/successor from leaf
        key_index = node.keys.index(key)
        
        # Find predecessor in left subtree
        predecessor = self._find_max_in_subtree(node.children[key_index])
        node.keys[key_index] = predecessor
        
        # Delete predecessor from leaf
        self._delete_recursive(node.children[key_index], predecessor)
    else:
        # Key not in current node, recurse to child
        child = self._delete_recursive(node.children[child_index], key)
        
        # Check if child became empty (underflow)
        if not child.keys:
            self._handle_underflow(node, child_index)
    
    return node

def _handle_underflow(self, parent, child_index):
    """Handle underflow when child has no keys"""
    child = parent.children[child_index]
    
    # Try to borrow from left sibling
    if child_index > 0:
        left_sibling = parent.children[child_index - 1]
        if len(left_sibling.keys) > 1:
            self._borrow_from_left(parent, child_index)
            return
    
    # Try to borrow from right sibling
    if child_index < len(parent.children) - 1:
        right_sibling = parent.children[child_index + 1]
        if len(right_sibling.keys) > 1:
            self._borrow_from_right(parent, child_index)
            return
    
    # Cannot borrow, must merge
    if child_index > 0:
        self._merge_with_left(parent, child_index)
    else:
        self._merge_with_right(parent, child_index)
```

### 2-3 Tree Complexity Analysis

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Search | O(log n) | O(log n) recursion |
| Insert | O(log n) | O(log n) recursion |
| Delete | O(log n) | O(log n) recursion |
| Height | Always O(log n) | - |

### 2-3 Tree Advantages
1. **Perfect Balance**: All operations guaranteed O(log n)
2. **No Rotations**: Uses splitting/merging instead
3. **Conceptual Simplicity**: Easier to understand than AVL
4. **Foundation for B-trees**: Direct generalization

### 2-3 Tree Disadvantages
1. **Implementation Complexity**: More complex than BST
2. **Memory Overhead**: Variable node sizes
3. **Cache Performance**: Less predictable memory access

---

## 4. B-Trees - Comprehensive Analysis

### What are B-Trees?
B-trees are self-balancing search trees designed for systems that read and write large blocks of data. They generalize 2-3 trees to allow nodes with many more keys and children.

### B-Tree Properties
For a B-tree of order m (minimum degree t = ⌈m/2⌉):
1. **Root**: Has at least 1 key (unless tree is empty)
2. **Internal Nodes**: Have at least t-1 keys and at most 2t-1 keys
3. **Leaf Nodes**: All at same level
4. **Children**: Internal node with k keys has k+1 children
5. **Sorted Keys**: Keys in each node are sorted
6. **Search Property**: For key k at position i, all keys in child i are < k, all keys in child i+1 are > k

### B-Tree Node Structure

```python
class BTreeNode:
    def __init__(self, is_leaf=True):
        self.keys = []              # List of keys
        self.children = []          # List of child pointers
        self.is_leaf = is_leaf      # True if leaf node
        self.num_keys = 0           # Number of keys currently stored
    
    def is_full(self, max_keys):
        """Check if node is full"""
        return self.num_keys == max_keys
    
    def search_key(self, key):
        """Find position where key should be"""
        i = 0
        while i < self.num_keys and key > self.keys[i]:
            i += 1
        return i
```

### Complete B-Tree Implementation

```python
class BTree:
    def __init__(self, min_degree):
        """
        Initialize B-tree with minimum degree t
        - Each node has at most 2t-1 keys
        - Each node has at least t-1 keys (except root)
        - Each internal node has at most 2t children
        """
        self.root = BTreeNode(is_leaf=True)
        self.min_degree = min_degree  # Minimum degree t
        self.max_keys = 2 * min_degree - 1
        self.min_keys = min_degree - 1
    
    def search(self, key):
        """Search for key in B-tree"""
        return self._search_recursive(self.root, key)
    
    def _search_recursive(self, node, key):
        """Recursive search helper"""
        i = 0
        
        # Find the first key greater than or equal to key
        while i < node.num_keys and key > node.keys[i]:
            i += 1
        
        # If key found
        if i < node.num_keys and key == node.keys[i]:
            return True
        
        # If leaf node and key not found
        if node.is_leaf:
            return False
        
        # Recurse to appropriate child
        return self._search_recursive(node.children[i], key)
    
    def insert(self, key):
        """Insert key into B-tree"""
        root = self.root
        
        # If root is full, split it
        if root.is_full(self.max_keys):
            new_root = BTreeNode(is_leaf=False)
            new_root.children.append(self.root)
            self._split_child(new_root, 0)
            self.root = new_root
        
        self._insert_non_full(self.root, key)
    
    def _insert_non_full(self, node, key):
        """Insert key into non-full node"""
        i = node.num_keys - 1
        
        if node.is_leaf:
            # Insert key into leaf node
            node.keys.append(0)  # Make space
            
            # Shift keys to make room for new key
            while i >= 0 and key < node.keys[i]:
                node.keys[i + 1] = node.keys[i]
                i -= 1
            
            node.keys[i + 1] = key
            node.num_keys += 1
        
        else:
            # Find child where key should be inserted
            while i >= 0 and key < node.keys[i]:
                i -= 1
            i += 1
            
            # If child is full, split it
            if node.children[i].is_full(self.max_keys):
                self._split_child(node, i)
                
                # After split, decide which child to recurse to
                if key > node.keys[i]:
                    i += 1
            
            self._insert_non_full(node.children[i], key)
    
    def _split_child(self, parent, index):
        """Split full child at given index"""
        full_child = parent.children[index]
        new_child = BTreeNode(is_leaf=full_child.is_leaf)
        
        # Move half the keys to new child
        mid_index = self.min_keys
        new_child.keys = full_child.keys[mid_index + 1:]
        new_child.num_keys = len(new_child.keys)
        
        # Move half the children to new child (if not leaf)
        if not full_child.is_leaf:
            new_child.children = full_child.children[mid_index + 1:]
        
        # Reduce keys in original child
        full_child.keys = full_child.keys[:mid_index]
        full_child.num_keys = len(full_child.keys)
        
        if not full_child.is_leaf:
            full_child.children = full_child.children[:mid_index + 1]
        
        # Insert new child into parent
        parent.children.insert(index + 1, new_child)
        
        # Move middle key up to parent
        middle_key = full_child.keys[mid_index] if mid_index < len(full_child.keys) else new_child.keys[0]
        parent.keys.insert(index, middle_key)
        parent.num_keys += 1
    
    def delete(self, key):
        """Delete key from B-tree"""
        self._delete_recursive(self.root, key)
        
        # If root becomes empty, make its only child the new root
        if self.root.num_keys == 0 and not self.root.is_leaf:
            self.root = self.root.children[0]
    
    def _delete_recursive(self, node, key):
        """Recursive deletion helper"""
        i = node.search_key(key)
        
        if i < node.num_keys and node.keys[i] == key:
            # Key found in current node
            if node.is_leaf:
                # Case 1: Key in leaf node
                node.keys.pop(i)
                node.num_keys -= 1
            else:
                # Case 2: Key in internal node
                self._delete_from_internal_node(node, i)
        
        elif not node.is_leaf:
            # Key not in current node, recurse to child
            
            # Check if child has minimum number of keys
            if node.children[i].num_keys == self.min_keys:
                self._ensure_child_has_enough_keys(node, i)
                
                # After rebalancing, key position might change
                if i > node.num_keys:
                    i = node.num_keys
            
            self._delete_recursive(node.children[i], key)
    
    def _delete_from_internal_node(self, node, index):
        """Delete key from internal node"""
        key = node.keys[index]
        
        # Case 2a: Left child has at least min_degree keys
        if node.children[index].num_keys >= self.min_degree:
            predecessor = self._get_predecessor(node, index)
            node.keys[index] = predecessor
            self._delete_recursive(node.children[index], predecessor)
        
        # Case 2b: Right child has at least min_degree keys
        elif node.children[index + 1].num_keys >= self.min_degree:
            successor = self._get_successor(node, index)
            node.keys[index] = successor
            self._delete_recursive(node.children[index + 1], successor)
        
        # Case 2c: Both children have min_degree-1 keys
        else:
            self._merge_children(node, index)
            self._delete_recursive(node.children[index], key)
    
    def _get_predecessor(self, node, index):
        """Get predecessor of key at index"""
        current = node.children[index]
        while not current.is_leaf:
            current = current.children[current.num_keys]
        return current.keys[current.num_keys - 1]
    
    def _get_successor(self, node, index):
        """Get successor of key at index"""
        current = node.children[index + 1]
        while not current.is_leaf:
            current = current.children[0]
        return current.keys[0]
    
    def _merge_children(self, parent, index):
        """Merge child at index with its right sibling"""
        left_child = parent.children[index]
        right_child = parent.children[index + 1]
        
        # Move key from parent to left child
        left_child.keys.append(parent.keys[index])
        left_child.num_keys += 1
        
        # Move all keys from right child to left child
        left_child.keys.extend(right_child.keys)
        left_child.num_keys += right_child.num_keys
        
        # Move all children from right child to left child
        if not left_child.is_leaf:
            left_child.children.extend(right_child.children)
        
        # Remove key and child from parent
        parent.keys.pop(index)
        parent.children.pop(index + 1)
        parent.num_keys -= 1
```

### B-Tree Example with Detailed Operations

```python
def demonstrate_btree():
    """Demonstrate B-tree operations"""
    # Create B-tree with minimum degree 3 (max 5 keys per node)
    btree = BTree(min_degree=3)
    
    # Insert values
    values = [10, 20, 5, 6, 12, 30, 7, 17]
    print("Inserting values:", values)
    
    for val in values:
        print(f"\nInserting {val}:")
        btree.insert(val)
        print_btree(btree.root, 0)
    
    # Insertion trace for min_degree=3:
    # Insert 10: [10]
    # Insert 20: [10, 20]
    # Insert 5: [5, 10, 20]
    # Insert 6: [5, 6, 10, 20]
    # Insert 12: [5, 6, 10, 12, 20] (full, max_keys = 5)
    # Insert 30: Node splits ->
    #           [10]
    #          /    \
    #      [5, 6]  [12, 20, 30]
    
    print("\nSearch operations:")
    for val in [6, 15, 20]:
        result = btree.search(val)
        print(f"Search {val}: {result}")
    
    print("\nDeleting 6:")
    btree.delete(6)
    print_btree(btree.root, 0)

def print_btree(node, level):
    """Print B-tree structure"""
    if node is None:
        return
    
    indent = "  " * level
    print(f"{indent}Keys: {node.keys[:node.num_keys]}")
    
    if not node.is_leaf:
        for i, child in enumerate(node.children):
            if child:
                print(f"{indent}Child {i}:")
                print_btree(child, level + 1)
```

### B-Tree Complexity Analysis

| Operation | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Search | O(log n) | O(log n) recursion |
| Insert | O(log n) | O(log n) recursion |
| Delete | O(log n) | O(log n) recursion |
| Height | O(log_t n) where t is min degree | - |

### B-Tree Applications

#### 1. Database Systems
```python
class DatabaseIndex:
    """B-tree used for database indexing"""
    def __init__(self, page_size=4096):
        # Calculate optimal min_degree based on page size
        key_size = 8  # bytes
        pointer_size = 8  # bytes
        
        # Each node: keys + pointers + metadata
        max_keys = (page_size - 64) // (key_size + pointer_size)
        min_degree = max_keys // 2
        
        self.btree = BTree(min_degree)
        self.page_size = page_size
    
    def create_index(self, table_data):
        """Create index from table data"""
        for record_id, key_value in table_data:
            self.btree.insert((key_value, record_id))
```

#### 2. File Systems
```python
class FileSystemBTree:
    """B-tree for file system directory structure"""
    def __init__(self):
        self.btree = BTree(min_degree=100)  # Large degree for disk efficiency
    
    def add_file(self, filename, metadata):
        """Add file to directory"""
        self.btree.insert((filename, metadata))
    
    def find_file(self, filename):
        """Find file in directory"""
        return self.btree.search(filename)
```

### B-Tree Variants

#### 1. B+ Trees
- All data stored in leaves
- Internal nodes only store keys for navigation
- Leaves linked for range queries

#### 2. B* Trees
- Higher minimum fill factor (2/3 instead of 1/2)
- Delayed splitting using redistribution

### B-Tree vs Other Trees Comparison

| Tree Type | Height | Node Size | Use Case |
|-----------|--------|-----------|----------|
| BST | O(n) worst | Fixed (3 pointers) | Memory-based |
| AVL | O(log n) | Fixed (4 pointers) | Memory-based |
| 2-3 Tree | O(log n) | Variable (2-3 keys) | Educational |
| B-Tree | O(log_t n) | Variable (many keys) | Disk-based |---


## 5. Tree Traversal Techniques - Comprehensive Analysis

### Overview of Tree Traversals
Tree traversal is the process of visiting each node in a tree data structure exactly once in a systematic way. There are two main categories:
1. **Depth-First Traversals**: Go deep before going wide
2. **Breadth-First Traversals**: Visit all nodes at current level before next level

### Depth-First Traversal Methods

#### 1. In-Order Traversal (Left-Root-Right)

```python
def inorder_traversal_recursive(root, result=None):
    """
    In-order traversal: Left -> Root -> Right
    For BST: gives sorted order
    """
    if result is None:
        result = []
    
    if root is not None:
        inorder_traversal_recursive(root.left, result)
        result.append(root.data)
        inorder_traversal_recursive(root.right, result)
    
    return result

def inorder_traversal_iterative(root):
    """Iterative in-order traversal using stack"""
    result = []
    stack = []
    current = root
    
    while stack or current:
        # Go to leftmost node
        while current:
            stack.append(current)
            current = current.left
        
        # Current is None, pop from stack
        current = stack.pop()
        result.append(current.data)
        
        # Visit right subtree
        current = current.right
    
    return result

def inorder_morris_traversal(root):
    """
    Morris traversal: In-order without stack/recursion
    Uses threading technique, O(1) space
    """
    result = []
    current = root
    
    while current:
        if current.left is None:
            # No left subtree, visit current and go right
            result.append(current.data)
            current = current.right
        else:
            # Find inorder predecessor
            predecessor = current.left
            while predecessor.right and predecessor.right != current:
                predecessor = predecessor.right
            
            if predecessor.right is None:
                # Create thread
                predecessor.right = current
                current = current.left
            else:
                # Remove thread and visit current
                predecessor.right = None
                result.append(current.data)
                current = current.right
    
    return result
```

#### 2. Pre-Order Traversal (Root-Left-Right)

```python
def preorder_traversal_recursive(root, result=None):
    """
    Pre-order traversal: Root -> Left -> Right
    Used for: copying tree, prefix expressions
    """
    if result is None:
        result = []
    
    if root is not None:
        result.append(root.data)
        preorder_traversal_recursive(root.left, result)
        preorder_traversal_recursive(root.right, result)
    
    return result

def preorder_traversal_iterative(root):
    """Iterative pre-order traversal using stack"""
    if not root:
        return []
    
    result = []
    stack = [root]
    
    while stack:
        current = stack.pop()
        result.append(current.data)
        
        # Push right first, then left (stack is LIFO)
        if current.right:
            stack.append(current.right)
        if current.left:
            stack.append(current.left)
    
    return result
```

#### 3. Post-Order Traversal (Left-Right-Root)

```python
def postorder_traversal_recursive(root, result=None):
    """
    Post-order traversal: Left -> Right -> Root
    Used for: deleting tree, postfix expressions, calculating size
    """
    if result is None:
        result = []
    
    if root is not None:
        postorder_traversal_recursive(root.left, result)
        postorder_traversal_recursive(root.right, result)
        result.append(root.data)
    
    return result

def postorder_traversal_iterative(root):
    """Iterative post-order traversal using two stacks"""
    if not root:
        return []
    
    result = []
    stack1 = [root]
    stack2 = []
    
    # First stack for traversal, second for result order
    while stack1:
        current = stack1.pop()
        stack2.append(current)
        
        if current.left:
            stack1.append(current.left)
        if current.right:
            stack1.append(current.right)
    
    # Pop from second stack to get post-order
    while stack2:
        result.append(stack2.pop().data)
    
    return result

def postorder_traversal_single_stack(root):
    """Post-order with single stack using last visited tracking"""
    if not root:
        return []
    
    result = []
    stack = []
    last_visited = None
    current = root
    
    while stack or current:
        if current:
            stack.append(current)
            current = current.left
        else:
            peek_node = stack[-1]
            
            # If right child exists and hasn't been processed yet
            if peek_node.right and last_visited != peek_node.right:
                current = peek_node.right
            else:
                result.append(peek_node.data)
                last_visited = stack.pop()
    
    return result
```

### Breadth-First Traversal (Level-Order)

```python
from collections import deque

def level_order_traversal(root):
    """
    Level-order traversal: Visit nodes level by level
    Uses queue (FIFO) data structure
    """
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        current = queue.popleft()
        result.append(current.data)
        
        if current.left:
            queue.append(current.left)
        if current.right:
            queue.append(current.right)
    
    return result

def level_order_by_levels(root):
    """Level-order traversal returning nodes grouped by level"""
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level_size = len(queue)
        current_level = []
        
        for _ in range(level_size):
            node = queue.popleft()
            current_level.append(node.data)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(current_level)
    
    return result

def zigzag_level_order(root):
    """Zigzag level-order: alternate left-to-right and right-to-left"""
    if not root:
        return []
    
    result = []
    queue = deque([root])
    left_to_right = True
    
    while queue:
        level_size = len(queue)
        current_level = deque()
        
        for _ in range(level_size):
            node = queue.popleft()
            
            if left_to_right:
                current_level.append(node.data)
            else:
                current_level.appendleft(node.data)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        result.append(list(current_level))
        left_to_right = not left_to_right
    
    return result
```

### Complete Tree Traversal Example

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def create_sample_tree():
    """
    Create sample tree:
           1
         /   \
        2     3
       / \   / \
      4   5 6   7
    """
    root = TreeNode(1)
    root.left = TreeNode(2)
    root.right = TreeNode(3)
    root.left.left = TreeNode(4)
    root.left.right = TreeNode(5)
    root.right.left = TreeNode(6)
    root.right.right = TreeNode(7)
    return root

def demonstrate_all_traversals():
    """Demonstrate all traversal methods"""
    root = create_sample_tree()
    
    print("Tree structure:")
    print("       1")
    print("     /   \\")
    print("    2     3")
    print("   / \\   / \\")
    print("  4   5 6   7")
    print()
    
    print("Depth-First Traversals:")
    print("In-order (L-Root-R):", inorder_traversal_recursive(root))      # [4, 2, 5, 1, 6, 3, 7]
    print("Pre-order (Root-L-R):", preorder_traversal_recursive(root))    # [1, 2, 4, 5, 3, 6, 7]
    print("Post-order (L-R-Root):", postorder_traversal_recursive(root))  # [4, 5, 2, 6, 7, 3, 1]
    print()
    
    print("Breadth-First Traversals:")
    print("Level-order:", level_order_traversal(root))                    # [1, 2, 3, 4, 5, 6, 7]
    print("Level-by-level:", level_order_by_levels(root))                 # [[1], [2, 3], [4, 5, 6, 7]]
    print("Zigzag level-order:", zigzag_level_order(root))                # [[1], [3, 2], [4, 5, 6, 7]]
    print()
    
    print("Iterative vs Recursive comparison:")
    print("In-order recursive:", inorder_traversal_recursive(root))
    print("In-order iterative:", inorder_traversal_iterative(root))
    print("In-order Morris:", inorder_morris_traversal(root))
```

### Specialized Tree Traversals

#### 1. Boundary Traversal
```python
def boundary_traversal(root):
    """
    Boundary traversal: left boundary + leaves + right boundary
    """
    if not root:
        return []
    
    result = [root.data]
    
    # Left boundary (excluding leaf nodes)
    def add_left_boundary(node):
        if node and not is_leaf(node):
            result.append(node.data)
            if node.left:
                add_left_boundary(node.left)
            elif node.right:
                add_left_boundary(node.right)
    
    # Leaf nodes
    def add_leaves(node):
        if node:
            if is_leaf(node):
                result.append(node.data)
            else:
                add_leaves(node.left)
                add_leaves(node.right)
    
    # Right boundary (excluding leaf nodes, in reverse)
    def add_right_boundary(node):
        if node and not is_leaf(node):
            if node.right:
                add_right_boundary(node.right)
            elif node.left:
                add_right_boundary(node.left)
            result.append(node.data)
    
    def is_leaf(node):
        return node and not node.left and not node.right
    
    if root.left:
        add_left_boundary(root.left)
    
    add_leaves(root)
    
    if root.right:
        add_right_boundary(root.right)
    
    return result
```

#### 2. Vertical Order Traversal
```python
def vertical_order_traversal(root):
    """Traverse tree in vertical order (by column)"""
    if not root:
        return []
    
    from collections import defaultdict, deque
    
    column_map = defaultdict(list)
    queue = deque([(root, 0)])  # (node, column)
    
    while queue:
        node, col = queue.popleft()
        column_map[col].append(node.data)
        
        if node.left:
            queue.append((node.left, col - 1))
        if node.right:
            queue.append((node.right, col + 1))
    
    # Sort by column and return values
    result = []
    for col in sorted(column_map.keys()):
        result.extend(column_map[col])
    
    return result
```

### Tree Traversal Applications

#### 1. Expression Trees
```python
def evaluate_expression_tree(root):
    """Evaluate arithmetic expression tree using post-order"""
    if not root:
        return 0
    
    # Leaf node (operand)
    if not root.left and not root.right:
        return int(root.data)
    
    # Internal node (operator)
    left_val = evaluate_expression_tree(root.left)
    right_val = evaluate_expression_tree(root.right)
    
    if root.data == '+':
        return left_val + right_val
    elif root.data == '-':
        return left_val - right_val
    elif root.data == '*':
        return left_val * right_val
    elif root.data == '/':
        return left_val / right_val

def infix_from_expression_tree(root):
    """Generate infix expression using in-order traversal"""
    if not root:
        return ""
    
    # Leaf node
    if not root.left and not root.right:
        return str(root.data)
    
    # Internal node
    left_expr = infix_from_expression_tree(root.left)
    right_expr = infix_from_expression_tree(root.right)
    
    return f"({left_expr} {root.data} {right_expr})"
```

#### 2. Tree Serialization/Deserialization
```python
def serialize_tree(root):
    """Serialize tree using pre-order traversal"""
    def preorder(node):
        if not node:
            return "null,"
        return str(node.data) + "," + preorder(node.left) + preorder(node.right)
    
    return preorder(root)

def deserialize_tree(data):
    """Deserialize tree from pre-order string"""
    def build_tree():
        val = next(values)
        if val == "null":
            return None
        
        node = TreeNode(int(val))
        node.left = build_tree()
        node.right = build_tree()
        return node
    
    values = iter(data.split(','))
    return build_tree()
```

### Traversal Complexity Analysis

| Traversal Type | Time Complexity | Space Complexity |
|----------------|----------------|------------------|
| In-order (Recursive) | O(n) | O(h) where h is height |
| In-order (Iterative) | O(n) | O(h) for stack |
| In-order (Morris) | O(n) | O(1) |
| Pre-order | O(n) | O(h) |
| Post-order | O(n) | O(h) |
| Level-order | O(n) | O(w) where w is max width |

---

## 6. Graph Search and Traversal Techniques - Comprehensive Analysis

### Graph Representation

#### 1. Adjacency Matrix
```python
class GraphMatrix:
    def __init__(self, num_vertices):
        self.num_vertices = num_vertices
        self.matrix = [[0] * num_vertices for _ in range(num_vertices)]
    
    def add_edge(self, u, v, weight=1):
        """Add edge from u to v"""
        self.matrix[u][v] = weight
    
    def add_undirected_edge(self, u, v, weight=1):
        """Add undirected edge"""
        self.matrix[u][v] = weight
        self.matrix[v][u] = weight
    
    def has_edge(self, u, v):
        """Check if edge exists"""
        return self.matrix[u][v] != 0
    
    def get_neighbors(self, vertex):
        """Get all neighbors of vertex"""
        neighbors = []
        for i in range(self.num_vertices):
            if self.matrix[vertex][i] != 0:
                neighbors.append(i)
        return neighbors
```

#### 2. Adjacency List
```python
from collections import defaultdict

class GraphList:
    def __init__(self):
        self.graph = defaultdict(list)
        self.num_vertices = 0
    
    def add_edge(self, u, v, weight=1):
        """Add edge from u to v"""
        self.graph[u].append((v, weight))
        self.num_vertices = max(self.num_vertices, max(u, v) + 1)
    
    def add_undirected_edge(self, u, v, weight=1):
        """Add undirected edge"""
        self.graph[u].append((v, weight))
        self.graph[v].append((u, weight))
        self.num_vertices = max(self.num_vertices, max(u, v) + 1)
    
    def get_neighbors(self, vertex):
        """Get all neighbors of vertex"""
        return [neighbor for neighbor, weight in self.graph[vertex]]
    
    def get_weighted_neighbors(self, vertex):
        """Get neighbors with weights"""
        return self.graph[vertex]
```

### Depth-First Search (DFS)

#### 1. Recursive DFS
```python
def dfs_recursive(graph, start, visited=None, result=None):
    """
    Depth-First Search using recursion
    Time: O(V + E), Space: O(V)
    """
    if visited is None:
        visited = set()
    if result is None:
        result = []
    
    visited.add(start)
    result.append(start)
    
    # Visit all unvisited neighbors
    for neighbor in graph.get_neighbors(start):
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited, result)
    
    return result

def dfs_with_timestamps(graph, start):
    """DFS with discovery and finish times"""
    visited = set()
    discovery_time = {}
    finish_time = {}
    time = [0]  # Use list to make it mutable in nested function
    
    def dfs_visit(vertex):
        time[0] += 1
        discovery_time[vertex] = time[0]
        visited.add(vertex)
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in visited:
                dfs_visit(neighbor)
        
        time[0] += 1
        finish_time[vertex] = time[0]
    
    dfs_visit(start)
    return discovery_time, finish_time
```

#### 2. Iterative DFS
```python
def dfs_iterative(graph, start):
    """
    Depth-First Search using stack
    Time: O(V + E), Space: O(V)
    """
    visited = set()
    result = []
    stack = [start]
    
    while stack:
        vertex = stack.pop()
        
        if vertex not in visited:
            visited.add(vertex)
            result.append(vertex)
            
            # Add neighbors to stack (reverse order for consistent traversal)
            neighbors = graph.get_neighbors(vertex)
            for neighbor in reversed(neighbors):
                if neighbor not in visited:
                    stack.append(neighbor)
    
    return result
```

### Breadth-First Search (BFS)

#### 1. Standard BFS
```python
from collections import deque

def bfs(graph, start):
    """
    Breadth-First Search using queue
    Time: O(V + E), Space: O(V)
    """
    visited = set()
    result = []
    queue = deque([start])
    visited.add(start)
    
    while queue:
        vertex = queue.popleft()
        result.append(vertex)
        
        # Add all unvisited neighbors to queue
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    
    return result

def bfs_with_distances(graph, start):
    """BFS that also computes shortest distances"""
    visited = set()
    distances = {start: 0}
    queue = deque([start])
    visited.add(start)
    
    while queue:
        vertex = queue.popleft()
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in visited:
                visited.add(neighbor)
                distances[neighbor] = distances[vertex] + 1
                queue.append(neighbor)
    
    return distances
```

#### 2. BFS for Shortest Path
```python
def bfs_shortest_path(graph, start, end):
    """Find shortest path using BFS"""
    if start == end:
        return [start]
    
    visited = set()
    queue = deque([(start, [start])])
    visited.add(start)
    
    while queue:
        vertex, path = queue.popleft()
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor == end:
                return path + [neighbor]
            
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, path + [neighbor]))
    
    return None  # No path found

def bfs_all_shortest_paths(graph, start):
    """Find shortest paths to all reachable vertices"""
    distances = {start: 0}
    parents = {start: None}
    queue = deque([start])
    
    while queue:
        vertex = queue.popleft()
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in distances:
                distances[neighbor] = distances[vertex] + 1
                parents[neighbor] = vertex
                queue.append(neighbor)
    
    return distances, parents

def reconstruct_path(parents, start, end):
    """Reconstruct path from parent pointers"""
    if end not in parents:
        return None
    
    path = []
    current = end
    while current is not None:
        path.append(current)
        current = parents[current]
    
    return path[::-1]
```

### Complete Graph Traversal Example

```python
def demonstrate_graph_traversals():
    """Demonstrate DFS and BFS on sample graph"""
    
    # Create sample graph
    #   0 --- 1 --- 2
    #   |     |     |
    #   3 --- 4 --- 5
    
    graph = GraphList()
    edges = [(0, 1), (0, 3), (1, 2), (1, 4), (2, 5), (3, 4), (4, 5)]
    
    for u, v in edges:
        graph.add_undirected_edge(u, v)
    
    print("Graph edges:", edges)
    print()
    
    start_vertex = 0
    
    print("DFS Traversals:")
    print("DFS Recursive:", dfs_recursive(graph, start_vertex))
    print("DFS Iterative:", dfs_iterative(graph, start_vertex))
    print()
    
    print("BFS Traversals:")
    print("BFS:", bfs(graph, start_vertex))
    print("BFS Distances:", bfs_with_distances(graph, start_vertex))
    print()
    
    print("Shortest Paths:")
    distances, parents = bfs_all_shortest_paths(graph, start_vertex)
    for vertex in range(6):
        if vertex in distances:
            path = reconstruct_path(parents, start_vertex, vertex)
            print(f"Path to {vertex}: {path}, Distance: {distances[vertex]}")
```

### Advanced Graph Algorithms

#### 1. Connected Components
```python
def find_connected_components(graph):
    """Find all connected components using DFS"""
    visited = set()
    components = []
    
    for vertex in range(graph.num_vertices):
        if vertex not in visited:
            component = []
            dfs_component(graph, vertex, visited, component)
            components.append(component)
    
    return components

def dfs_component(graph, vertex, visited, component):
    """DFS helper for finding connected components"""
    visited.add(vertex)
    component.append(vertex)
    
    for neighbor in graph.get_neighbors(vertex):
        if neighbor not in visited:
            dfs_component(graph, neighbor, visited, component)
```

#### 2. Cycle Detection
```python
def has_cycle_undirected(graph):
    """Detect cycle in undirected graph using DFS"""
    visited = set()
    
    def dfs_cycle(vertex, parent):
        visited.add(vertex)
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in visited:
                if dfs_cycle(neighbor, vertex):
                    return True
            elif neighbor != parent:
                return True  # Back edge found
        
        return False
    
    for vertex in range(graph.num_vertices):
        if vertex not in visited:
            if dfs_cycle(vertex, -1):
                return True
    
    return False

def has_cycle_directed(graph):
    """Detect cycle in directed graph using DFS with colors"""
    WHITE, GRAY, BLACK = 0, 1, 2
    colors = [WHITE] * graph.num_vertices
    
    def dfs_cycle(vertex):
        colors[vertex] = GRAY
        
        for neighbor in graph.get_neighbors(vertex):
            if colors[neighbor] == GRAY:
                return True  # Back edge to gray vertex
            elif colors[neighbor] == WHITE and dfs_cycle(neighbor):
                return True
        
        colors[vertex] = BLACK
        return False
    
    for vertex in range(graph.num_vertices):
        if colors[vertex] == WHITE:
            if dfs_cycle(vertex):
                return True
    
    return False
```

#### 3. Topological Sorting
```python
def topological_sort_dfs(graph):
    """Topological sort using DFS"""
    visited = set()
    stack = []
    
    def dfs_topological(vertex):
        visited.add(vertex)
        
        for neighbor in graph.get_neighbors(vertex):
            if neighbor not in visited:
                dfs_topological(neighbor)
        
        stack.append(vertex)
    
    for vertex in range(graph.num_vertices):
        if vertex not in visited:
            dfs_topological(vertex)
    
    return stack[::-1]  # Reverse to get topological order

def topological_sort_bfs(graph):
    """Topological sort using BFS (Kahn's algorithm)"""
    # Calculate in-degrees
    in_degree = [0] * graph.num_vertices
    for vertex in range(graph.num_vertices):
        for neighbor in graph.get_neighbors(vertex):
            in_degree[neighbor] += 1
    
    # Initialize queue with vertices having in-degree 0
    queue = deque()
    for vertex in range(graph.num_vertices):
        if in_degree[vertex] == 0:
            queue.append(vertex)
    
    result = []
    
    while queue:
        vertex = queue.popleft()
        result.append(vertex)
        
        # Reduce in-degree of neighbors
        for neighbor in graph.get_neighbors(vertex):
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    # Check if all vertices are included (no cycle)
    if len(result) != graph.num_vertices:
        return None  # Graph has cycle
    
    return result
```

### Graph Traversal Applications

#### 1. Maze Solving
```python
def solve_maze_dfs(maze, start, end):
    """Solve maze using DFS"""
    rows, cols = len(maze), len(maze[0])
    visited = set()
    
    def is_valid(r, c):
        return (0 <= r < rows and 0 <= c < cols and 
                maze[r][c] == 0 and (r, c) not in visited)
    
    def dfs_maze(r, c, path):
        if (r, c) == end:
            return path + [(r, c)]
        
        visited.add((r, c))
        
        # Try all 4 directions
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if is_valid(nr, nc):
                result = dfs_maze(nr, nc, path + [(r, c)])
                if result:
                    return result
        
        visited.remove((r, c))  # Backtrack
        return None
    
    return dfs_maze(start[0], start[1], [])
```

#### 2. Social Network Analysis
```python
def find_mutual_friends(graph, user1, user2):
    """Find mutual friends using graph traversal"""
    friends1 = set(graph.get_neighbors(user1))
    friends2 = set(graph.get_neighbors(user2))
    return list(friends1.intersection(friends2))

def degrees_of_separation(graph, user1, user2):
    """Find degrees of separation using BFS"""
    if user1 == user2:
        return 0
    
    distances = bfs_with_distances(graph, user1)
    return distances.get(user2, -1)  # -1 if not connected
```

### Graph Traversal Complexity Summary

| Algorithm | Time Complexity | Space Complexity | Use Case |
|-----------|----------------|------------------|----------|
| DFS | O(V + E) | O(V) | Cycle detection, topological sort |
| BFS | O(V + E) | O(V) | Shortest path, level-order |
| Connected Components | O(V + E) | O(V) | Graph connectivity |
| Topological Sort | O(V + E) | O(V) | Task scheduling |--
-

## 7. NP-Completeness Theory - Comprehensive Analysis

### Introduction to Computational Complexity

#### Complexity Classes Overview
Computational complexity theory classifies problems based on the resources (time, space) required to solve them.

```python
class ComplexityClass:
    """Representation of computational complexity classes"""
    
    def __init__(self, name, description, examples):
        self.name = name
        self.description = description
        self.examples = examples
    
    def __str__(self):
        return f"{self.name}: {self.description}"

# Define major complexity classes
complexity_classes = {
    'P': ComplexityClass(
        'P', 
        'Problems solvable in polynomial time by deterministic algorithm',
        ['Sorting', 'Shortest Path', 'Matrix Multiplication']
    ),
    'NP': ComplexityClass(
        'NP',
        'Problems verifiable in polynomial time by deterministic algorithm',
        ['SAT', 'Hamiltonian Cycle', 'Vertex Cover']
    ),
    'NP-Complete': ComplexityClass(
        'NP-Complete',
        'Hardest problems in NP; all NP problems reduce to these',
        ['SAT', '3-SAT', 'Clique', 'Independent Set']
    ),
    'NP-Hard': ComplexityClass(
        'NP-Hard',
        'At least as hard as NP-Complete problems',
        ['Halting Problem', 'Traveling Salesman Optimization']
    )
}
```

### Formal Definitions

#### 1. Decision Problems
```python
class DecisionProblem:
    """Abstract base class for decision problems"""
    
    def __init__(self, name, question):
        self.name = name
        self.question = question
    
    def solve(self, instance):
        """Return True/False for given instance"""
        raise NotImplementedError
    
    def verify(self, instance, certificate):
        """Verify certificate for given instance"""
        raise NotImplementedError

class SATDecisionProblem(DecisionProblem):
    """Boolean Satisfiability Decision Problem"""
    
    def __init__(self):
        super().__init__(
            "SAT",
            "Given a Boolean formula, is there an assignment that makes it true?"
        )
    
    def solve(self, formula):
        """Brute force SAT solver - exponential time"""
        variables = self.extract_variables(formula)
        n = len(variables)
        
        # Try all 2^n possible assignments
        for i in range(2**n):
            assignment = {}
            for j, var in enumerate(variables):
                assignment[var] = bool(i & (1 << j))
            
            if self.evaluate_formula(formula, assignment):
                return True
        
        return False
    
    def verify(self, formula, assignment):
        """Verify assignment in polynomial time"""
        return self.evaluate_formula(formula, assignment)
    
    def extract_variables(self, formula):
        """Extract variables from formula"""
        # Simplified implementation
        import re
        return list(set(re.findall(r'[a-zA-Z]\w*', formula)))
    
    def evaluate_formula(self, formula, assignment):
        """Evaluate Boolean formula with given assignment"""
        # Simplified evaluation - would need proper parser in practice
        try:
            # Replace variables with their values
            expr = formula
            for var, value in assignment.items():
                expr = expr.replace(var, str(value))
            
            # Evaluate the expression
            return eval(expr.replace('∧', ' and ').replace('∨', ' or ').replace('¬', ' not '))
        except:
            return False
```

#### 2. Class P (Polynomial Time)
```python
def is_in_P(problem_solver, max_input_size=1000):
    """
    Check if problem appears to be in P by measuring runtime growth
    This is a heuristic check, not a proof
    """
    import time
    import random
    
    times = []
    sizes = [10, 20, 50, 100, 200, 500]
    
    for size in sizes:
        if size > max_input_size:
            break
            
        # Generate random input of given size
        test_input = generate_random_input(size)
        
        start_time = time.time()
        problem_solver(test_input)
        end_time = time.time()
        
        times.append(end_time - start_time)
    
    # Check if growth appears polynomial
    # This is a simplified heuristic
    growth_ratios = []
    for i in range(1, len(times)):
        if times[i-1] > 0:
            ratio = times[i] / times[i-1]
            size_ratio = sizes[i] / sizes[i-1]
            growth_ratios.append(ratio / (size_ratio ** 3))  # Check against cubic growth
    
    # If all ratios are reasonable, likely polynomial
    return all(ratio < 10 for ratio in growth_ratios)

def generate_random_input(size):
    """Generate random input for testing"""
    import random
    return [random.randint(1, 1000) for _ in range(size)]
```

#### 3. Class NP (Nondeterministic Polynomial)
```python
class NPProblem:
    """Base class for NP problems"""
    
    def __init__(self, name):
        self.name = name
    
    def verify_certificate(self, instance, certificate):
        """
        Verify certificate in polynomial time
        This is what defines NP - polynomial verification
        """
        raise NotImplementedError
    
    def brute_force_solve(self, instance):
        """
        Brute force solution (usually exponential)
        Used to find certificate if one exists
        """
        raise NotImplementedError

class HamiltonianCycleNP(NPProblem):
    """Hamiltonian Cycle as NP problem"""
    
    def __init__(self):
        super().__init__("Hamiltonian Cycle")
    
    def verify_certificate(self, graph, cycle):
        """
        Verify that cycle is a valid Hamiltonian cycle
        Time: O(n) - polynomial
        """
        n = len(graph)
        
        # Check if cycle visits all vertices exactly once
        if len(cycle) != n + 1 or cycle[0] != cycle[-1]:
            return False
        
        if len(set(cycle[:-1])) != n:
            return False
        
        # Check if all edges in cycle exist in graph
        for i in range(n):
            u, v = cycle[i], cycle[i + 1]
            if not graph[u][v]:  # Assuming adjacency matrix
                return False
        
        return True
    
    def brute_force_solve(self, graph):
        """
        Find Hamiltonian cycle by trying all permutations
        Time: O(n!) - exponential
        """
        import itertools
        
        n = len(graph)
        vertices = list(range(n))
        
        # Try all permutations starting from vertex 0
        for perm in itertools.permutations(vertices[1:]):
            cycle = [0] + list(perm) + [0]
            if self.verify_certificate(graph, cycle):
                return cycle
        
        return None
```

### NP-Complete Problems

#### 1. Boolean Satisfiability (SAT)
```python
class SATSolver:
    """SAT solver with various algorithms"""
    
    def __init__(self):
        self.name = "Boolean Satisfiability"
    
    def dpll_solve(self, clauses, assignment=None):
        """
        DPLL algorithm for SAT solving
        More efficient than brute force but still exponential worst-case
        """
        if assignment is None:
            assignment = {}
        
        # Simplify clauses with current assignment
        simplified = self.simplify_clauses(clauses, assignment)
        
        # Check if all clauses satisfied
        if not simplified:
            return assignment
        
        # Check if any clause is empty (unsatisfiable)
        if any(not clause for clause in simplified):
            return None
        
        # Unit propagation
        unit_clauses = [clause for clause in simplified if len(clause) == 1]
        if unit_clauses:
            literal = unit_clauses[0][0]
            var = abs(literal)
            value = literal > 0
            new_assignment = assignment.copy()
            new_assignment[var] = value
            return self.dpll_solve(clauses, new_assignment)
        
        # Pure literal elimination
        pure_literal = self.find_pure_literal(simplified)
        if pure_literal:
            var = abs(pure_literal)
            value = pure_literal > 0
            new_assignment = assignment.copy()
            new_assignment[var] = value
            return self.dpll_solve(clauses, new_assignment)
        
        # Choose variable and branch
        var = self.choose_variable(simplified)
        
        # Try positive assignment
        new_assignment = assignment.copy()
        new_assignment[var] = True
        result = self.dpll_solve(clauses, new_assignment)
        if result is not None:
            return result
        
        # Try negative assignment
        new_assignment = assignment.copy()
        new_assignment[var] = False
        return self.dpll_solve(clauses, new_assignment)
    
    def simplify_clauses(self, clauses, assignment):
        """Simplify clauses based on current assignment"""
        simplified = []
        
        for clause in clauses:
            new_clause = []
            satisfied = False
            
            for literal in clause:
                var = abs(literal)
                if var in assignment:
                    if (literal > 0) == assignment[var]:
                        satisfied = True
                        break
                    # else: literal is false, don't add to new_clause
                else:
                    new_clause.append(literal)
            
            if not satisfied:
                simplified.append(new_clause)
        
        return simplified
    
    def find_pure_literal(self, clauses):
        """Find a pure literal (appears only positive or only negative)"""
        literal_count = {}
        
        for clause in clauses:
            for literal in clause:
                if literal not in literal_count:
                    literal_count[literal] = 0
                literal_count[literal] += 1
        
        for literal in literal_count:
            if -literal not in literal_count:
                return literal
        
        return None
    
    def choose_variable(self, clauses):
        """Choose variable for branching (heuristic)"""
        var_count = {}
        
        for clause in clauses:
            for literal in clause:
                var = abs(literal)
                if var not in var_count:
                    var_count[var] = 0
                var_count[var] += 1
        
        # Choose most frequent variable
        return max(var_count.keys(), key=lambda v: var_count[v])
```

#### 2. 3-SAT Problem
```python
class ThreeSAT:
    """3-SAT: SAT where each clause has exactly 3 literals"""
    
    def __init__(self):
        self.name = "3-SAT"
    
    def is_3sat_formula(self, clauses):
        """Check if formula is in 3-SAT form"""
        return all(len(clause) == 3 for clause in clauses)
    
    def random_3sat_generator(self, num_vars, num_clauses):
        """Generate random 3-SAT instance"""
        import random
        
        clauses = []
        for _ in range(num_clauses):
            clause = []
            variables = random.sample(range(1, num_vars + 1), 3)
            
            for var in variables:
                # Randomly negate literal
                literal = var if random.choice([True, False]) else -var
                clause.append(literal)
            
            clauses.append(clause)
        
        return clauses
    
    def solve_3sat_brute_force(self, clauses):
        """Solve 3-SAT by trying all assignments"""
        if not self.is_3sat_formula(clauses):
            raise ValueError("Not a 3-SAT formula")
        
        # Find all variables
        variables = set()
        for clause in clauses:
            for literal in clause:
                variables.add(abs(literal))
        
        variables = sorted(list(variables))
        n = len(variables)
        
        # Try all 2^n assignments
        for i in range(2**n):
            assignment = {}
            for j, var in enumerate(variables):
                assignment[var] = bool(i & (1 << j))
            
            if self.evaluate_3sat(clauses, assignment):
                return assignment
        
        return None
    
    def evaluate_3sat(self, clauses, assignment):
        """Evaluate 3-SAT formula with given assignment"""
        for clause in clauses:
            clause_satisfied = False
            
            for literal in clause:
                var = abs(literal)
                value = assignment.get(var, False)
                
                if (literal > 0 and value) or (literal < 0 and not value):
                    clause_satisfied = True
                    break
            
            if not clause_satisfied:
                return False
        
        return True
```

#### 3. Vertex Cover Problem
```python
class VertexCover:
    """Vertex Cover: Find minimum set of vertices covering all edges"""
    
    def __init__(self):
        self.name = "Vertex Cover"
    
    def verify_vertex_cover(self, graph, vertex_set, k):
        """
        Verify that vertex_set is a vertex cover of size ≤ k
        Time: O(E) - polynomial
        """
        if len(vertex_set) > k:
            return False
        
        # Check if all edges are covered
        for u in range(len(graph)):
            for v in range(len(graph[u])):
                if graph[u][v] and u not in vertex_set and v not in vertex_set:
                    return False
        
        return True
    
    def brute_force_vertex_cover(self, graph, k):
        """
        Find vertex cover of size ≤ k by trying all subsets
        Time: O(2^n * E) - exponential
        """
        import itertools
        
        n = len(graph)
        vertices = list(range(n))
        
        # Try all subsets of size ≤ k
        for size in range(k + 1):
            for vertex_set in itertools.combinations(vertices, size):
                if self.verify_vertex_cover(graph, set(vertex_set), k):
                    return set(vertex_set)
        
        return None
    
    def approximation_vertex_cover(self, graph):
        """
        2-approximation algorithm for vertex cover
        Time: O(E) - polynomial
        """
        vertex_cover = set()
        edges = []
        
        # Collect all edges
        for u in range(len(graph)):
            for v in range(u + 1, len(graph)):
                if graph[u][v]:
                    edges.append((u, v))
        
        # Greedy algorithm: pick edge, add both endpoints
        covered_edges = set()
        
        for u, v in edges:
            if (u, v) not in covered_edges and (v, u) not in covered_edges:
                vertex_cover.add(u)
                vertex_cover.add(v)
                
                # Mark all edges incident to u or v as covered
                for x in range(len(graph)):
                    if graph[u][x]:
                        covered_edges.add((min(u, x), max(u, x)))
                    if graph[v][x]:
                        covered_edges.add((min(v, x), max(v, x)))
        
        return vertex_cover
```

### Polynomial Reductions

#### 1. Reduction Framework
```python
class PolynomialReduction:
    """Framework for polynomial-time reductions"""
    
    def __init__(self, from_problem, to_problem):
        self.from_problem = from_problem
        self.to_problem = to_problem
    
    def reduce(self, instance):
        """
        Transform instance of from_problem to instance of to_problem
        Must run in polynomial time
        """
        raise NotImplementedError
    
    def verify_reduction(self, original_instance, reduced_instance):
        """
        Verify that reduction preserves the answer
        original_instance is YES iff reduced_instance is YES
        """
        raise NotImplementedError

class SATTo3SAT(PolynomialReduction):
    """Reduction from SAT to 3-SAT"""
    
    def __init__(self):
        super().__init__("SAT", "3-SAT")
    
    def reduce(self, sat_clauses):
        """
        Convert SAT formula to 3-SAT formula
        Time: O(n) where n is total number of literals
        """
        three_sat_clauses = []
        new_var_counter = self.get_max_variable(sat_clauses) + 1
        
        for clause in sat_clauses:
            if len(clause) == 1:
                # (a) -> (a ∨ y₁ ∨ y₂) ∧ (a ∨ y₁ ∨ ¬y₂) ∧ (a ∨ ¬y₁ ∨ y₂) ∧ (a ∨ ¬y₁ ∨ ¬y₂)
                a = clause[0]
                y1, y2 = new_var_counter, new_var_counter + 1
                new_var_counter += 2
                
                three_sat_clauses.extend([
                    [a, y1, y2],
                    [a, y1, -y2],
                    [a, -y1, y2],
                    [a, -y1, -y2]
                ])
            
            elif len(clause) == 2:
                # (a ∨ b) -> (a ∨ b ∨ y) ∧ (a ∨ b ∨ ¬y)
                a, b = clause[0], clause[1]
                y = new_var_counter
                new_var_counter += 1
                
                three_sat_clauses.extend([
                    [a, b, y],
                    [a, b, -y]
                ])
            
            elif len(clause) == 3:
                # Already in 3-SAT form
                three_sat_clauses.append(clause)
            
            else:
                # (a₁ ∨ a₂ ∨ ... ∨ aₖ) with k > 3
                # -> (a₁ ∨ a₂ ∨ y₁) ∧ (¬y₁ ∨ a₃ ∨ y₂) ∧ ... ∧ (¬yₖ₋₃ ∨ aₖ₋₁ ∨ aₖ)
                literals = clause[:]
                
                # First clause
                y1 = new_var_counter
                new_var_counter += 1
                three_sat_clauses.append([literals[0], literals[1], y1])
                
                # Middle clauses
                for i in range(2, len(literals) - 2):
                    y_prev = y1 if i == 2 else new_var_counter - 1
                    y_curr = new_var_counter
                    new_var_counter += 1
                    three_sat_clauses.append([-y_prev, literals[i], y_curr])
                
                # Last clause
                y_last = new_var_counter - 1
                three_sat_clauses.append([-y_last, literals[-2], literals[-1]])
        
        return three_sat_clauses
    
    def get_max_variable(self, clauses):
        """Find the maximum variable number in clauses"""
        max_var = 0
        for clause in clauses:
            for literal in clause:
                max_var = max(max_var, abs(literal))
        return max_var
```

#### 2. Classic Reductions
```python
class ClassicReductions:
    """Collection of classic NP-Complete reductions"""
    
    @staticmethod
    def independent_set_to_vertex_cover(graph, k):
        """
        Reduction: Independent Set ≤ₚ Vertex Cover
        G has independent set of size k iff G has vertex cover of size n-k
        """
        n = len(graph)
        return graph, n - k  # Same graph, different parameter
    
    @staticmethod
    def vertex_cover_to_set_cover(graph):
        """
        Reduction: Vertex Cover ≤ₚ Set Cover
        Transform graph to set cover instance
        """
        n = len(graph)
        
        # Universe: all edges
        universe = []
        for u in range(n):
            for v in range(u + 1, n):
                if graph[u][v]:
                    universe.append((u, v))
        
        # Sets: for each vertex, set of incident edges
        sets = {}
        for u in range(n):
            incident_edges = []
            for v in range(n):
                if u != v and graph[u][v]:
                    edge = (min(u, v), max(u, v))
                    if edge in universe:
                        incident_edges.append(edge)
            sets[u] = incident_edges
        
        return universe, sets
    
    @staticmethod
    def three_sat_to_clique(clauses):
        """
        Reduction: 3-SAT ≤ₚ Clique
        Create graph where clique of size m exists iff 3-SAT formula is satisfiable
        """
        m = len(clauses)  # Number of clauses
        
        # Vertices: one for each literal in each clause
        vertices = []
        vertex_map = {}
        vertex_id = 0
        
        for i, clause in enumerate(clauses):
            for literal in clause:
                vertex_info = (i, literal)  # (clause_index, literal)
                vertices.append(vertex_info)
                vertex_map[vertex_info] = vertex_id
                vertex_id += 1
        
        # Edges: connect vertices if they can be in same satisfying assignment
        n = len(vertices)
        graph = [[False] * n for _ in range(n)]
        
        for i in range(n):
            for j in range(i + 1, n):
                clause_i, literal_i = vertices[i]
                clause_j, literal_j = vertices[j]
                
                # Connect if:
                # 1. From different clauses, AND
                # 2. Not contradictory literals
                if (clause_i != clause_j and 
                    literal_i != -literal_j):
                    graph[i][j] = True
                    graph[j][i] = True
        
        return graph, m  # Graph and clique size
```

### Cook-Levin Theorem

#### Proof Sketch Implementation
```python
class CookLevinTheorem:
    """
    Demonstration of Cook-Levin Theorem proof technique
    Shows how to reduce any NP problem to SAT
    """
    
    def __init__(self):
        self.name = "Cook-Levin Theorem"
    
    def reduce_np_to_sat(self, np_problem, instance, certificate_length, time_bound):
        """
        Generic reduction from NP problem to SAT
        This is a simplified demonstration of the proof technique
        """
        
        # Step 1: Create variables for Turing machine configuration
        variables = self.create_tm_variables(time_bound, certificate_length)
        
        # Step 2: Create clauses ensuring valid computation
        clauses = []
        
        # Initial configuration clauses
        clauses.extend(self.initial_configuration_clauses(instance))
        
        # Transition clauses (one step follows from previous)
        clauses.extend(self.transition_clauses(time_bound))
        
        # Final configuration clauses (accepting state reached)
        clauses.extend(self.accepting_configuration_clauses(time_bound))
        
        return clauses
    
    def create_tm_variables(self, time_bound, tape_bound):
        """Create Boolean variables for Turing machine simulation"""
        variables = {}
        
        # Variables for each time step, tape position, and possible symbol
        for t in range(time_bound):
            for pos in range(tape_bound):
                for symbol in ['0', '1', 'blank']:
                    var_name = f"tape_{t}_{pos}_{symbol}"
                    variables[var_name] = len(variables) + 1
        
        # Variables for machine state at each time
        for t in range(time_bound):
            for state in ['q0', 'q1', 'q_accept', 'q_reject']:
                var_name = f"state_{t}_{state}"
                variables[var_name] = len(variables) + 1
        
        # Variables for head position at each time
        for t in range(time_bound):
            for pos in range(tape_bound):
                var_name = f"head_{t}_{pos}"
                variables[var_name] = len(variables) + 1
        
        return variables
    
    def initial_configuration_clauses(self, instance):
        """Clauses ensuring correct initial configuration"""
        clauses = []
        
        # Initial state is q0
        clauses.append([self.get_var("state_0_q0")])
        
        # Initial tape contains input
        for i, bit in enumerate(str(instance)):
            if bit == '1':
                clauses.append([self.get_var(f"tape_0_{i}_1")])
            else:
                clauses.append([self.get_var(f"tape_0_{i}_0")])
        
        # Head initially at position 0
        clauses.append([self.get_var("head_0_0")])
        
        return clauses
    
    def transition_clauses(self, time_bound):
        """Clauses ensuring valid transitions between configurations"""
        clauses = []
        
        # For each time step, ensure valid transition
        for t in range(time_bound - 1):
            # Add clauses based on Turing machine transition function
            # This is problem-specific and would be quite complex
            pass
        
        return clauses
    
    def accepting_configuration_clauses(self, time_bound):
        """Clauses ensuring accepting state is reached"""
        clauses = []
        
        # At some time step, machine is in accepting state
        accepting_clause = []
        for t in range(time_bound):
            accepting_clause.append(self.get_var(f"state_{t}_q_accept"))
        
        clauses.append(accepting_clause)
        
        return clauses
    
    def get_var(self, var_name):
        """Get variable number for given variable name"""
        # Simplified - would maintain proper mapping
        return hash(var_name) % 10000 + 1
```

### NP-Completeness Applications

#### 1. Practical Implications
```python
class NPCompletenessImplications:
    """Practical implications of NP-Completeness"""
    
    def __init__(self):
        self.implications = {
            'optimization': 'Use approximation algorithms',
            'exact_solutions': 'Use exponential algorithms for small instances',
            'heuristics': 'Use problem-specific heuristics',
            'parameterized': 'Use parameterized complexity approach'
        }
    
    def approximation_strategy(self, problem_name):
        """Suggest approximation strategy for NP-Complete problem"""
        strategies = {
            'vertex_cover': '2-approximation using maximal matching',
            'tsp': '1.5-approximation using MST (metric TSP)',
            'set_cover': 'ln(n)-approximation using greedy algorithm',
            'knapsack': 'FPTAS using dynamic programming'
        }
        
        return strategies.get(problem_name, 'Problem-specific heuristics')
    
    def exact_algorithm_choice(self, problem_size):
        """Choose exact algorithm based on problem size"""
        if problem_size <= 20:
            return "Brute force enumeration"
        elif problem_size <= 50:
            return "Branch and bound with good heuristics"
        elif problem_size <= 100:
            return "Dynamic programming (if applicable)"
        else:
            return "Approximation or heuristic algorithms only"
```

#### 2. Modern Approaches
```python
class ModernNPApproaches:
    """Modern approaches to NP-Complete problems"""
    
    def __init__(self):
        self.approaches = [
            'Approximation Algorithms',
            'Parameterized Complexity',
            'Randomized Algorithms',
            'Local Search Heuristics',
            'Machine Learning Approaches'
        ]
    
    def sat_solver_techniques(self):
        """Modern SAT solver techniques"""
        return {
            'DPLL': 'Basic backtracking with unit propagation',
            'CDCL': 'Conflict-driven clause learning',
            'Preprocessing': 'Formula simplification techniques',
            'Restart': 'Periodic restart strategies',
            'Heuristics': 'Variable and value ordering heuristics'
        }
    
    def approximation_ratios(self):
        """Known approximation ratios for NP-Complete problems"""
        return {
            'vertex_cover': 2,
            'set_cover': 'ln(n)',
            'tsp_metric': 1.5,
            'max_cut': 1.138,
            'independent_set': 'n/log²(n)'
        }
```

### Summary and Exam Preparation

#### Key Concepts for NP-Completeness
```python
class NPCompletenessStudyGuide:
    """Study guide for NP-Completeness concepts"""
    
    def __init__(self):
        self.key_concepts = {
            'decision_problems': 'Problems with YES/NO answers',
            'class_P': 'Polynomial-time solvable problems',
            'class_NP': 'Polynomial-time verifiable problems',
            'np_complete': 'Hardest problems in NP',
            'polynomial_reduction': 'Efficient transformation between problems',
            'cook_levin': 'SAT is NP-Complete'
        }
    
    def prove_np_completeness(self, problem_name):
        """Steps to prove a problem is NP-Complete"""
        steps = [
            f"1. Show {problem_name} is in NP",
            "   - Give polynomial-time verification algorithm",
            f"2. Show {problem_name} is NP-Hard",
            "   - Reduce known NP-Complete problem to it",
            "   - Prove reduction is polynomial-time",
            "   - Prove reduction preserves YES/NO answers"
        ]
        return steps
    
    def common_reductions(self):
        """Common polynomial reductions to remember"""
        return {
            '3SAT → Clique': 'Create vertex for each literal, connect compatible ones',
            '3SAT → Independent Set': 'Same as clique in complement graph',
            'Independent Set → Vertex Cover': 'Complement relationship',
            'Vertex Cover → Set Cover': 'Edges as universe, vertices as sets',
            'SAT → 3SAT': 'Transform clauses to have exactly 3 literals'
        }
    
    def exam_tips(self):
        """Tips for NP-Completeness exam questions"""
        return [
            "Always verify polynomial time for reductions",
            "Show both directions of equivalence in reductions",
            "Remember standard NP-Complete problems",
            "Practice reduction constructions",
            "Understand difference between NP-Hard and NP-Complete",
            "Know approximation algorithms for common problems"
        ]
```

---

## 8. Comparison of Data Structures - Comprehensive Analysis

### Performance Comparison Table

| Data Structure | Search | Insert | Delete | Space | Best Use Case |
|----------------|--------|--------|--------|-------|---------------|
| BST (Average) | O(log n) | O(log n) | O(log n) | O(n) | Dynamic sets, moderate size |
| BST (Worst) | O(n) | O(n) | O(n) | O(n) | Avoid for sorted input |
| AVL Tree | O(log n) | O(log n) | O(log n) | O(n) | Frequent searches, balanced needed |
| 2-3 Tree | O(log n) | O(log n) | O(log n) | O(n) | Educational, conceptual understanding |
| B-Tree | O(log n) | O(log n) | O(log n) | O(n) | Database indexes, file systems |

### When to Use Each Structure

```python
class DataStructureSelector:
    """Helper to choose appropriate data structure"""
    
    def __init__(self):
        self.recommendations = {}
    
    def recommend_structure(self, requirements):
        """Recommend data structure based on requirements"""
        
        if requirements.get('disk_based', False):
            return "B-Tree - optimized for disk I/O"
        
        if requirements.get('worst_case_guarantee', False):
            return "AVL Tree - guaranteed O(log n) operations"
        
        if requirements.get('simple_implementation', False):
            return "BST - simple but can degrade to O(n)"
        
        if requirements.get('educational_purpose', False):
            return "2-3 Tree - good for understanding balance concepts"
        
        return "Choose based on specific performance requirements"
```

---

## 9. Practice Problems and Solutions

### Problem 1: Tree Traversal (Exam Style)
**Problem**: Given a binary tree, implement all traversal methods and show output for sample tree.

**Solution**: [Implemented in Section 5]

### Problem 2: NP-Completeness Proof
**Problem**: Prove that Vertex Cover is NP-Complete.

**Solution**:
1. **Show Vertex Cover ∈ NP**: Given graph G and vertex set S, verify in O(E) time that S covers all edges
2. **Show Vertex Cover is NP-Hard**: Reduce 3-SAT to Vertex Cover
   - For each variable, create variable gadget
   - For each clause, create clause gadget
   - Connect gadgets appropriately
   - Show 3-SAT formula satisfiable iff graph has vertex cover of required size

### Problem 3: B-Tree Operations
**Problem**: Insert sequence [10, 20, 5, 6, 12, 30, 7, 17] into B-tree with minimum degree 3.

**Solution**: [Detailed trace provided in Section 4]

---

*This comprehensive unit covers all advanced data structures, search techniques, and NP-completeness concepts tested in CS/SD-402 examinations, with detailed implementations, complexity analysis, and practical applications.*