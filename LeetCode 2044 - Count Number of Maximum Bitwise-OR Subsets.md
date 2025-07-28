
---

## 🔢 LeetCode 2044 - Count Number of Maximum Bitwise-OR Subsets

### 💡 Problem Statement (Hinglish Mein)

Aapko ek integer array `nums[]` diya gaya hai.

**Goal:** Array ke sabhi non-empty subsets mein se count karo kitne subsets ka **bitwise OR** value maximum possible OR ke barabar hai.

---

### 📘 Definitions

- **Subset:** Array ka koi bhi portion (elements delete kar sakte ho), order same rahe.  
  Eg: `[3,1]` ke subsets ho sakte hain → `[3]`, `[1]`, `[3,1]`

- **Bitwise OR (`|`)**: Binary level pe comparison hota hai.  
  Agar dono bits mein koi bhi `1` hai, toh result `1` hota hai.  
  Example:  
  ```
  3 | 1 = 3
  (011) | (001) = (011) = 3
  ```

---

### 🧠 Solution Insight

- Pura array ka OR sabse zyada hoga.
- Har subset explore karo (via DFS), agar uska OR max OR ke barabar hai → count badhao!

---

### 🧪 Example

```java
Input: nums = [3, 2, 1, 5]
```

Step 1:  
```
totalOr = 3 | 2 | 1 | 5 = 7
```

Step 2: Subsets jinka OR == 7:
- [3,5]
- [2,5]
- [3,2,5]
- [3,1,5]
- [2,1,5]
- [3,2,1,5]

✅ Output: `6`

---

### 🚀 Java Code with Hinglish Comments

```java
class Solution {
    private int ans = 0; // Final answer store hoga

    public int countMaxOrSubsets(int[] nums) {
        int totalOr = 0;

        // Step 1: Poore array ka OR nikalo
        for (int x : nums) {
            totalOr |= x;
        }

        // Step 2: DFS start karo to explore all subsets
        dfs(0, 0, nums, totalOr);
        return ans;
    }

    private void dfs(int i, int subsetOr, int[] nums, int totalOr) {
        // Base case: agar array end tak pahunch gaye
        if (i == nums.length) {
            if (subsetOr == totalOr) {
                ans++; // Valid subset mila → count karo
            }
            return;
        }

        // Case 1: current element ko ignore karo
        dfs(i + 1, subsetOr, nums, totalOr);

        // Case 2: current element ko include karo
        dfs(i + 1, subsetOr | nums[i], nums, totalOr);
    }
}
```

---

### 🔍 Dry Run for `nums = [3, 2, 1, 5]`

1. `dfs(0, 0)` → two choices:
   - exclude `3` → `dfs(1, 0)`
   - include `3` → `dfs(1, 3)`

2. Each level gives two further choices (include/exclude).

Base case hits when `i == nums.length`, and we check `subsetOr == 7`.

✅ Valid hits:  
- `[3,5]` → OR = 7  
- `[2,5]` → OR = 7  
- `[3,2,5]` → OR = 7  
- `[3,1,5]` → OR = 7  
- `[2,1,5]` → OR = 7  
- `[3,2,1,5]` → OR = 7

Final count = `6`

---

### ⏱️ Complexity

- **Time:** O(2ⁿ) → brute-force subsets
- **Space:** O(n) recursion depth

---

