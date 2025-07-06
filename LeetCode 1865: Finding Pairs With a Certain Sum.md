---

### 🧠 Problem: Finding Pairs With a Certain Sum

You are given two arrays of numbers: `nums1` and `nums2`.

You need to build a special class that can do two things:

---

### 1. **Add a number to an element in `nums2`**
You can pick any index in `nums2` and add a number to it.

Example:  
If `nums2 = [1, 2, 3]` and you do `add(1, 5)`,  
then `nums2` becomes `[1, 7, 3]` because `2 + 5 = 7`.

---

### 2. **Count how many pairs add up to a target number**
You need to count how many pairs `(i, j)` exist such that:
```
nums1[i] + nums2[j] == target
```

Example:  
If `nums1 = [1, 2]` and `nums2 = [3, 4]`, and the target is `5`,  
then the valid pairs are:
- (0, 1) → 1 + 4 = 5  
- (1, 0) → 2 + 3 = 5  
So the answer is `2`.

---

### 🧪 Your Task

You will implement a class with:
- A constructor to store the two arrays.
- A method to update `nums2`.
- A method to count how many pairs add up to a given number.

---


# Intuition
### 💡 First Thoughts on How to Solve the Problem

When I first looked at this problem, I noticed two key things:

1. **`nums1` is small (≤ 1000)**  
2. **`nums2` can be large (≤ 10⁵)**

This immediately suggested that we should **optimize for fast lookups in `nums2`**, especially during the `count()` operation.

---

### 🧠 Intuition

- Since we need to count how many times `nums1[i] + nums2[j] == tot`, we can fix each element in `nums1` and look for `tot - nums1[i]` in `nums2`.
- To do this efficiently, we can **store the frequency of each number in `nums2` using a HashMap**.
- This way, for each `nums1[i]`, we can instantly know how many `nums2[j]` values will form a valid pair.

---

### 🛠️ Strategy

- **Use a HashMap** to store the frequency of elements in `nums2`.
- **Update the map** whenever `add(index, val)` is called.
- **Loop through `nums1`** during `count(tot)` and for each value, check how many times `tot - nums1[i]` appears in `nums2` using the map.

This approach gives us:
- `add()` in **O(1)**
- `count()` in **O(n)** where `n = nums1.length`

---



# Approach
### ✅ Approach to Solving the Problem

To solve the **Finding Pairs With a Certain Sum** problem efficiently, we take advantage of the fact that `nums1` is small and `nums2` can be large. Here's a breakdown of the approach:

---

### 🔍 Key Observations

- `nums1.length` is small (≤ 1000), so we can afford to loop through it frequently.
- `nums2.length` is large (≤ 10⁵), so we should avoid looping through it repeatedly.
- We need to support two operations efficiently: `add(index, val)` and `count(tot)`.

---

### 🧠 Strategy

1. **Use a HashMap to store frequencies of elements in `nums2`**  
   This allows us to quickly find how many times a number appears in `nums2`.

2. **For `add(index, val)`**:
   - Update the value at `nums2[index]`.
   - Update the frequency map: decrease the count of the old value and increase the count of the new value.

3. **For `count(tot)`**:
   - Loop through each element `num` in `nums1`.
   - For each `num`, calculate `complement = tot - num`.
   - Add the frequency of `complement` from the map to the result.

---

### 🧮 Time and Space Complexity

| Operation     | Time Complexity | Space Complexity |
|---------------|------------------|------------------|
| Constructor   | O(m)             | O(m)             |
| `add()`       | O(1)             | O(1)             |
| `count()`     | O(n)             | O(1)             |

Where `n = nums1.length` and `m = nums2.length`.

---

This approach is both **efficient** and **scalable**, especially when `count()` is called many times.



# Complexity
Here’s how you can describe the **time and space complexity** for the optimized solution using a frequency map:

---

### ⏱️ Time Complexity

- **Constructor**:  
  $$O(m)$$ — where \( m = \text{nums2.length} \), to build the frequency map.

- **add(index, val)**:  
  $$O(1)$$ — direct update to the array and frequency map.

- **count(tot)**:  
  $$O(n)$$ — where \( n = \text{nums1.length} \), since we loop through `nums1` and do constant-time lookups in the map.

---

### 🧠 Space Complexity

- $$O(m)$$ — for storing the frequency map of `nums2`.

---



# Code
```java []
import java.util.*;

class FindSumPairs {
    private int[] nums1;
    private int[] nums2;
    private Map<Integer, Integer> freqMap;

    public FindSumPairs(int[] nums1, int[] nums2) {
        this.nums1 = nums1;
        this.nums2 = nums2;
        this.freqMap = new HashMap<>();
        for (int num : nums2) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }
    }

    public void add(int index, int val) {
        int oldVal = nums2[index];
        int newVal = oldVal + val;
        nums2[index] = newVal;

        // Update frequency map
        freqMap.put(oldVal, freqMap.get(oldVal) - 1);
        if (freqMap.get(oldVal) == 0) {
            freqMap.remove(oldVal);
        }
        freqMap.put(newVal, freqMap.getOrDefault(newVal, 0) + 1);
    }

    public int count(int tot) {
        int count = 0;
        for (int num : nums1) {
            int complement = tot - num;
            count += freqMap.getOrDefault(complement, 0);
        }
        return count;
    }
}

```

you can solve this problem without using a `HashMap`, though it will be less efficient. Here's how you can do it using a brute-force approach:

---

### 🚫 No HashMap Approach

Instead of maintaining a frequency map for `nums2`, you can directly iterate through both arrays during the `count` operation.

### ✅ Java Implementation (Without HashMap)

```java
class FindSumPairs {
    private int[] nums1;
    private int[] nums2;

    public FindSumPairs(int[] nums1, int[] nums2) {
        this.nums1 = nums1;
        this.nums2 = nums2;
    }

    public void add(int index, int val) {
        nums2[index] += val;
    }

    public int count(int tot) {
        int count = 0;
        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums2.length; j++) {
                if (nums1[i] + nums2[j] == tot) {
                    count++;
                }
            }
        }
        return count;
    }
}
```

---

### 🧠 Time Complexity

- `add(index, val)` → **O(1)**
- `count(tot)` → **O(n * m)** where `n = nums1.length` and `m = nums2.length`

This is acceptable only because `nums1.length ≤ 1000` and the number of `count()` calls is also limited to 1000. But it will be significantly slower than the `HashMap` approach for large `nums2`.

---

### 📝 When to Use This

- For educational purposes or when constraints are small.
- If you want to avoid extra space usage.

Let’s walk through a **dry run** of the optimized **HashMap approach** using the example from the problem:

---

### 🧪 Input

```java
nums1 = [1, 1, 2, 2, 2, 3]
nums2 = [1, 4, 5, 2, 5, 4]
```

We initialize:

```java
FindSumPairs findSumPairs = new FindSumPairs(nums1, nums2);
```

Internally, we build a frequency map for `nums2`:

```java
freqMap = {
  1: 1,
  2: 1,
  4: 2,
  5: 2
}
```

---

### 🔢 Step 1: `findSumPairs.count(7)`

We loop through each `num` in `nums1` and look for `tot - num` in `freqMap`.

- For `num = 1`: need `6` → not in map
- For `num = 1`: need `6` → not in map
- For `num = 2`: need `5` → found 2 times → count += 2
- For `num = 2`: need `5` → count += 2
- For `num = 2`: need `5` → count += 2
- For `num = 3`: need `4` → found 2 times → count += 2

✅ Total count = **8**

---

### ➕ Step 2: `findSumPairs.add(3, 2)`

- `nums2[3] = 2` → becomes `4`
- Update `freqMap`:
  - Decrease count of `2`: now 0 → remove it
  - Increase count of `4`: now 3

Updated `freqMap`:

```java
{
  1: 1,
  4: 3,
  5: 2
}
```

---

### 🔢 Step 3: `findSumPairs.count(8)`

- For `num = 1`: need `7` → not in map
- For `num = 1`: need `7` → not in map
- For `num = 2`: need `6` → not in map
- For `num = 2`: need `6` → not in map
- For `num = 2`: need `6` → not in map
- For `num = 3`: need `5` → found 2 times → count += 2

✅ Total count = **2**

---

This dry run shows how the frequency map helps us avoid scanning all of `nums2` each time, making `count()` much faster.
