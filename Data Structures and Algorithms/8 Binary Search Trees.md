# Binary Search Trees

## Traversal Patterns

- **Inorder**: left - print - right
- **Preorder**: print - left - right
- **postorder**: left - right - print

## Functions

```text
Tree-Search(x, data)
    if x = NIL or data = x.key
        return x
    if data < x.key
        return Tree-Search(x.left, data)
    else
        return Tree-Search(x.right, data)
```

```text
Iterative-Tree-Search(x, data)
    while x ≠ NIL and data ≠ x.key
        if data < x.key
            x = x.left
        else
            x = x.right
    return x
```

```text
Tree-Minimum(x)
    while x.left ≠ NIL
        x = x.left
    return x
```

```text
Tree-Maximum(x)
    while x.right ≠ NIL
        x = x.right
    return x
```

```text
Successor(x)
    if x.right ≠ NIL
        return Tree-Minimum(x.right)
    y = x.π
    while y ≠ NIL and x = y.right
        x = y
        y = y.π
    return y
```

Successor is the next node in the inorder traversal.

```text
Tree-Insert(T, z)
    y = NIL
    x = T.root
    while x ≠ NIL
        y = x
        if z.key < x.key
            x = x.left
        else
            x = x.right
    z.π = y
    if y = NIL
        T.root = z
    else if z.key < y.key
        y.left = z
    else
        y.right = z
```

```text
Transplant(T, u, v)
    if u.π = NIL
        T.root = v
    else if u = u.π.left
        u.π.left = v
    else
        u.π.right = v
    if v ≠ NIL
        v.π = u.π
```

```text
Tree-Delete(T, z)
    if z.left == NIL then
        Transplant(T, z, z.right)
    else if z.right == NIL then
        Transplant(T, z, z.left)
    else
        y = Tree-Minimum(z.right)
        if y.π ≠ z then
            Transplant(T, y, y.right)
            y.right = z.right
            y.right.π = y
        Transplant(T, z, y)
        y.left = z.left
        y.left.π = y
```

Time complexity is $O(h)$, where $h$ is the height of the tree.

## Red-Black Trees

1. Each node is either red or black.
2. [*] The root is black.
3. Every leaf (NIL) is black.
4. [*] Red nodes have black children.
5. [*] Every path from a node to a descendant leaf contains the same number of black nodes.

```text
Left-Rotate(T, x)
    y = x.right
    x.right = y.left
    if y.left ≠ NIL
        y.left.π = x
    y.π = x.π
    if x.π = NIL
        T.root = y
    else if x = x.π.left
        x.π.left = y
    else
        x.π.right = y
    y.left = x
    x.π = y
```

### Insertion

1. X, Parent and Uncle are all RED.
   - Grandparent becomes reREDd, parent and uncle become BLACK (resolved or propagated)
2. X and Parent are RED, Uncle is BLACK, and X is near Uncle.
   - Rotate with X and Parent as backbones (propagated to case 3).
3. X and Parent are RED, Uncle is BLACK, and X is far from Uncle.
   - Rotate with Parent and Grandparent as backbones (resolved).

```text
RB-Insert(T, x)
    Tree-Insert(T, x)
    x.color = RED
    while x.parent and x.parent.color  == RED
        if x.parent == x.parent.parent.left
            y = x.parent.parent.right
            if y.color == RED                   // case 1
                x.parent.color = BLACK
                y.color = BLACK
                x.parent.parent.color = RED
                x = x.parent.parent
            else if x == x.parent.right         // case 2
                x = x.parent
                Left-Rotate(T, x)
            x.parent.color = BLACK              // case 3
            x.parent.parent.color = RED
            Right-Rotate(T, x.parent.parent)
        else
            Reverse the above with left and right swapped
    T.root.color = BLACK
```

### Deletion

1. W is RED.
    - Rotate(W, Parent) (propagated to case 2, 3, 4)
2. W is BLACK and has 2 BLACK children.
    - W becomes RED (resolved or propagated)
3. W is BLACK and has 1 RED near child and 1 BLACK far child.
    - Rotate(W, near child) (propagated to case 4)
4. W is BLACK and has RED far child.
    - Rotate(W, Parent) and transfer extra BLACK  of X to far child of W (resolved)

Individual time complexity $O(1)$ and combined worst case $O(\log n)$.
