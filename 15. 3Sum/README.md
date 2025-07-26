=

---

### 📝 Problem: 3Sum (LeetCode #15)

Given an integer array `nums`, return **all unique triplets** `[nums[i], nums[j], nums[k]]` such that:

- `i != j`, `j != k`, and `i != k`
- `nums[i] + nums[j] + nums[k] == 0`

You must return the solution **without duplicates**, and in any order.

---

### 🧪 Test Case

**Input:**
```
nums = [-1, 0, 1, 2, -1, -4]
```

**Output:**
```
[[-1, -1, 2], [-1, 0, 1]]
```

Explanation:  
- `-1 + -1 + 2 = 0`  
- `-1 + 0 + 1 = 0`  
No other combination gives zero sum without repeating triplets.

---

### 🧑‍💻 Java Code — Two Pointer Approach

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Sort the array

        for (int i = 0; i < nums.length - 2; i++) {
            // Skip duplicates
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));

                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;

                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }
}
```

---

### 🧠 Dry Run (Hinglish)

Array: `[-1, 0, 1, 2, -1, -4]`  
➡️ Step 1: Sort karo → `[-4, -1, -1, 0, 1, 2]`  

Now fix `i = 0` (i.e., `-4`)  
- Left = `1`, Right = `5`  
- `-4 + (-1) + 2 = -3` → sum chhota hai → left++  
- Try next pairs → koi valid triplet nahi mila  

Fix `i = 1` (i.e., `-1`)  
- `-1 + (-1) + 2 = 0` ✅  
- `-1 + 0 + 1 = 0` ✅  
- Triplets: `[-1,-1,2]` and `[-1,0,1]`

Duplicates ko skip karte hue final result compile ho gaya.

---

