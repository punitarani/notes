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
