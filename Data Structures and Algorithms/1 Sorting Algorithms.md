# Sorting Algorithms

| Algorithm      | Best               | Average            | Worst              |
|----------------|--------------------|--------------------|--------------------|
| Insertion Sort | $\Theta(n)$        | $\Theta(n^2)$      | $\Theta(n^2)$      |
| Merge Sort     | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n \log n)$ |
| Quick Sort     | $\Theta(n \log n)$ | $\Theta(n \log n)$ | $\Theta(n^2)$      |

## Insertion Sort

```c
void insertion_sort(int A[], int n)
    int i, j, key;      // i is right ptr, j is left ptr
    for (i = 1; i < n; i++)
        key = A[i];         // Store A[i]
        for(j=i-1; j>=0 && A[j]>key; j--)
            A[j+1] = A[j];  // Shift A[j] to the right
        A[j+1] = key;       // Insert A[i] in right place
```

---

## Merge Sort

```c
void merge_sort(int A[], int l, int r)
    if (l < r)                      // Until only 1 element
        int m = (l + r) / 2;        // Find the middle
        merge_sort(A, l, m);        // Sort the left half
        merge_sort(A, m + 1, r);    // Sort the right half
        merge(A, l, m, r);          // Merge the halves
```

```c
void merge(int A[], int l, int m, int r)
    int n1 = m - l + 1;             // Size of the left half
    int n2 = r - m;                 // Size of the right half
    int L[n1], R[n2];               // Create temp arrays
    for (int i = 0; i < n1; i++)    // Copy left half to L
        L[i] = A[l + i];
    for (int j = 0; j < n2; j++)    // Copy right half to R
        R[j] = A[m + 1 + j];
    int i = 0, j = 0, k = l;        
    while (i < n1 && j < n2)        // Merge while sorting
        if (L[i] <= R[j])           // COMPARE L[i] <= R[j]
            A[k] = L[i];            // Copy L[i] to A[k]
            i++;
        else
            A[k] = R[j];            // Copy R[j] to A[k]
            j++;
        k++;
    while (i < n1)                  // Copy remaining elements
        A[k] = L[i];
        i++;
        k++;
    while (j < n2)
        A[k] = R[j];
        j++;
        k++;
```

---

## Quick Sort

```c
void quick_sort(int A[], int l, int r)
    if (l < r)                      // Until only 1 element
        int p = partition(A, l, r); // Partition and get pivot
        quick_sort(A, l, p - 1);    // Sort the left half
        quick_sort(A, p + 1, r);    // Sort the right half
```

```c
void partition(int A[], int l, int r)
    int pivot = A[r];               // Pick the last element as the pivot
    int i = l - 1;                  // Set left pointer to l-1
    for (int j = l; j < r; j++)     // Set right pointer to l and go to r-1
        if (A[j] <= pivot)          // COMPARE A[j] <= Pivot
            i++;                    // Move the left pointer to the right
            swap(A[i], A[j]);       // Swap the left and right elements

    swap(A[i + 1], A[r]);           // Swap the pivot with the element at i+1
    return i + 1;                   
```

---

**Stable** if the relative order of equal elements is preserved.
**Insertion Sort** and **Merge Sort** are stable. **Quick Sort** is unstable.
