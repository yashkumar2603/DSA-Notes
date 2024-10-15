
```cpp
    multiset<int> my_multiset = {5, 3, 8, 1, 3};
    
    for(int val : my_multiset) {
        cout << val << " ";
    }
```

**Sort in Descending order ( Ascending by default ) -**
```cpp
multiset<int, greater<int>> my_multiset ;
```

| Operation  | Description                              |
| ---------- | ---------------------------------------- |
| `insert()` | Insert elements into a multiset.         |
| `erase()`  | Erase all instances of an element.       |
| `clear()`  | Remove all the elements from a multiset. |
| `empty()`  | Check if the multiset is empty.          |
| `size()`   | Returns the size of the multiset.        |

##### Size and empty check functions - 
```cpp
// check if the multiset is empty
    cout << "\nEmpty: " << my_multiset.empty() << endl;

    // check the size of the multiset
    cout << "Size: " << my_multiset.size() << endl;
```
