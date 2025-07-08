

---

## 🧩 Problem Statement: Insert Delete GetRandom O(1)

Design a data structure that supports all of the following operations in **average O(1) time**:

- `insert(val)`: Inserts an item `val` into the set if it is not already present. Returns `true` if the item was inserted, `false` otherwise.
- `remove(val)`: Removes an item `val` from the set if it is present. Returns `true` if the item was removed, `false` otherwise.
- `getRandom()`: Returns a random element from the current set of elements. Each element must have the same probability of being returned.

### ✨ Constraints:
- The value of `val` lies in the range \([-2^{31}, 2^{31} - 1]\).
- At most \(2 \times 10^5\) calls will be made to `insert`, `remove`, and `getRandom`.
- It is guaranteed that at least one element exists in the set when `getRandom()` is called.

### 🧪 Example:

```plaintext
Input:
["RandomizedSet", "insert", "remove", "insert", "getRandom", "remove", "insert", "getRandom"]
[[], [1], [2], [2], [], [1], [2], []]

Output:
[null, true, false, true, 2, true, false, 2]
```

**Explanation:**
```java
RandomizedSet randomizedSet = new RandomizedSet();
randomizedSet.insert(1);     // Returns true
randomizedSet.remove(2);     // Returns false
randomizedSet.insert(2);     // Returns true
randomizedSet.getRandom();   // Returns 1 or 2 randomly
randomizedSet.remove(1);     // Returns true
randomizedSet.insert(2);     // Returns false (already present)
randomizedSet.getRandom();   // Returns 2
```

---


# Intuition

### 💡 First Thoughts (Intuition)

To achieve **O(1)** average time complexity for all operations (`insert`, `remove`, and `getRandom`), we need to use a combination of data structures that allow:

- **Fast lookup** to check if an element exists → use a **HashMap**
- **Fast insertion and deletion** from the end → use a **List**
- **Random access by index** → again, a **List** is ideal

The key insight is to **simulate a set using a list and a map**:
- The **list** stores the actual values.
- The **map** stores each value’s index in the list.

This way:
- `insert(val)` adds to the end of the list and maps the value to its index.
- `remove(val)` swaps the value with the last element, updates the map, and removes the last element.
- `getRandom()` simply picks a random index from the list.

This hybrid approach ensures that all operations run in **amortized O(1)** time.

?
# Approach
### 🧭 Approach to Solving the Problem

To design a data structure that supports `insert`, `remove`, and `getRandom` in average **O(1)** time, we use a combination of:

#### 🔧 Data Structures:
- **HashMap<Integer, Integer> valToIndex**: Maps each value to its index in the list.
- **ArrayList<Integer> values**: Stores the actual elements.
- **Random rand**: For generating random indices.

#### 🛠️ Operations:

- **Insert(val)**:
  - Check if `val` exists in `valToIndex`.
  - If not, append `val` to `values` and record its index in `valToIndex`.
  - Return `true` if inserted, `false` otherwise.

- **Remove(val)**:
  - If `val` is not in `valToIndex`, return `false`.
  - Otherwise:
    - Get the index of `val`.
    - Swap it with the last element in `values`.
    - Update the index of the swapped element in `valToIndex`.
    - Remove the last element from `values` and delete `val` from `valToIndex`.
  - Return `true`.

- **getRandom()**:
  - Use `rand.nextInt(values.size())` to get a random index.
  - Return the element at that index from `values`.

This approach ensures that all operations are done in **amortized O(1)** time.



# Complexity
- Time complexity:


# Code
```java []
class RandomizedSet {
    private Map<Integer, Integer> valToIndex;
    private List<Integer> values;
    private Random rand;

    public RandomizedSet() {
        valToIndex = new HashMap<>();
        values = new ArrayList<>();
        rand = new Random();
    }
    
    public boolean insert(int val) {
        if (valToIndex.containsKey(val)) {
            return false;
        }

        valToIndex.put(val, values.size());
        values.add(val);
        return true;
    }
    
    public boolean remove(int val) {
        if (!valToIndex.containsKey(val)) {
            return false;
        }

        int index = valToIndex.get(val);
        int lastVal = values.get(values.size() - 1);
        values.set(index, lastVal);
        valToIndex.put(lastVal, index);
        values.remove(values.size() - 1);
        valToIndex.remove(val);
        return true; 
    }
    
    public int getRandom() {
        return values.get(rand.nextInt(values.size()));
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
