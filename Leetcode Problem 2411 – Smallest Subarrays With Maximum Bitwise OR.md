
---

```markdown
# Leetcode 2411 - Smallest Subarrays With Maximum Bitwise OR

## 🧠 Problem Statement (Hinglish Style)

Aapko ek array `nums[]` diya gaya hai jisme non-negative integers hain. Har index `i` se aapko ek subarray `[i...j]` choose karni hai jo:

- `i` se start ho,
- Bitwise OR kare maximum possible value (jitna ho sake future mein),
- Aur us OR value ke liye sabse chhoti subarray ho.

Aapko ek array `answer[]` return karna hai jisme `answer[i]` batata hai ki index `i` se start hone wali sabse chhoti subarray ki length kya hai jo maximum OR produce kare.

---

## 🔢 Example

### Input:
```txt
nums = [1, 0, 2, 1, 3]
```

### Output:
```txt
[3, 3, 2, 2, 1]
```

### Explanation:
- Index 0 → subarray `[1, 0, 2]` gives OR = 3 (length 3)
- Index 1 → subarray `[0, 2, 1]` gives OR = 3 (length 3)
- Index 2 → subarray `[2, 1]` gives OR = 3 (length 2)
- Index 3 → subarray `[1, 3]` gives OR = 3 (length 2)
- Index 4 → subarray `[3]` gives OR = 3 (length 1)

---

## ✅ Optimized Java Solution

```java
class Solution {
    public int[] smallestSubarrays(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];

        for (int i = 0; i < n; i++) {
            int x = nums[i];      // current OR seed
            ans[i] = 1;           // minimum subarray length is 1

            for (int j = i - 1; j >= 0; j--) {
                if ((nums[j] | x) != nums[j]) {
                    nums[j] |= x;             // boost OR value
                    ans[j] = i - j + 1;       // update subarray length
                } else {
                    break; // OR didn't increase anymore, break karo
                }
            }
        }

        return ans;
    }
}
```

---

## 🧪 Dry Run (Step-by-Step in Hinglish)

Let’s trace the input: `nums = [1, 0, 2, 1, 3]`

- `i = 0`: OR seed = 1  
  → no previous, `ans[0] = 1`

- `i = 1`: OR seed = 0  
  → no boost, `ans[1] = 1`

- `i = 2`: OR seed = 2  
  - j = 1: nums[1] = 0 → OR = 2 ⇒ update `nums[1] = 2`, `ans[1] = 2`  
  - j = 0: nums[0] = 1 → OR = 3 ⇒ update `nums[0] = 3`, `ans[0] = 3`

- `i = 3`: OR seed = 1  
  - j = 2: nums[2] = 2 → OR = 3 ⇒ update `nums[2] = 3`, `ans[2] = 2`

- `i = 4`: OR seed = 3  
  - j = 3: nums[3] = 1 → OR = 3 ⇒ update `nums[3] = 3`, `ans[3] = 2`

Final answer: `[3, 3, 2, 2, 1]`

---

## 🧮 Time Complexity

- **O(n × log U)**, where U = 10^9 ⇒ ~30 bits
- Efficient for `n` up to `10^5`

---

```
