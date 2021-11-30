# Python biblical cheatsheet

### Lists

- Lists are dynamically resized: a `tuple` differs from a list from the fact that it is **immutable**
- You can `append(el)`, `remove(value)`, `insert(index, value)`
- `A in array` checks for presence of `A` with complexity `O(n)`
- `B=A` copies the reference, `B=list(A)` copies the array, `copy.deepcopy(A)` does a deep copy
- `min(A)` and `max(A)` are nice to use
- For binary search, you can use `bisect.bisect(array, element)` which returns the `i` for which we can split the array and have everything that's less than `element` to the left
- You can use slicing to rotate a list: `A[k:]+A[k:]`
- Slicing can shallow-copy too: `B =A[:]`
- List comprehension is multi-level too: `[(x,y) for x in A for y in B]` works
- 