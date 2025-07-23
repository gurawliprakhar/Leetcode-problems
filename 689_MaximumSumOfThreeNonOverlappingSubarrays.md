

Aapko ek array `nums` diya hai aur ek integer `k`. Mujhe 3 alag-alag (non-overlapping) subarrays nikalne hain jinme har subarray ka size exactly `k` ho. In teeno subarrays ka total sum maximum hona chahiye.

Agar do ya zyada answer possible hain, toh woh wala choose karo jiska indices ka combination sabse chhota ho — yani lexicographically smallest.

## Example with Dry Run

**Input:**  
```
nums = [1, 2, 1, 2, 6, 7, 5, 1]
k = 2
```

**Possible Subarray Sums (size k=2):**
| Start Index | Subarray   | Sum |
| ----------- | ---------- | --- |
| 0           |       | 3   |
| 1           |       | 3   |
| 2           |       | 3   |
| 3           |       | 8   |
| 4           |       | 13  |
| 5           |       | 12  |
| 6           |       | 6   |

**Best non-overlapping triple:**  
- Pick  (index 0),  (index 3),  (index 5)
- Total sum: 3 + 8 + 12 = 23

**Output:**  
```
[0, 3, 5]
```

## क्यों Sliding Window Approach?

- Sliding window se humein kisi bhi fixed-size subarray ka sum O(1) mein nikal sakte hain, sirf ek element hatao, ek add karo.
- Isse har subarray sum efficiently niklega.
- Fir left aur right se max sum subarrays nikalne ke liye DP arrays bana lete hain.
- Ye technique array ke overlapping calculations ko avoid karti hai aur easy tracking allow karti hai.

## Java Code with Hinglish Comments

```java
import java.util.Arrays;

public class MaxSumOf3Subarrays {

    // Main logic function
    public int[] maxSumOfThreeSubarrays(int[] nums, int k) {
        int n = nums.length;
        int[] sum = new int[n - k + 1]; // Har k-length subarray ka sum

        // Step 1: Sliding window for k-length sums
        int windowSum = 0;
        for (int i = 0; i = k)
                windowSum -= nums[i - k];
            if (i >= k - 1)
                sum[i - k + 1] = windowSum;
        }

        // Step 2: Left - Max sum ka index from start to i
        int[] left = new int[sum.length];
        int best = 0;
        for (int i = 0; i  sum[best]) best = i;
            left[i] = best;
        }

        // Step 3: Right - Max sum ka index from i to end
        int[] right = new int[sum.length];
        best = sum.length - 1;
        for (int i = sum.length - 1; i >= 0; i--) {
            if (sum[i] >= sum[best]) best = i;
            right[i] = best;
        }

        // Step 4: Middle subarray ko fix karke answer nikaalo
        int maxTotal = 0;
        int[] res = new int[3];
        for (int j = k; j  maxTotal) {
                maxTotal = total;
                res[0] = i;
                res[1] = j;
                res[2] = l;
            }
        }
        return res;
    }

    // ---- Dry Run Test Cases ----
    public static void main(String[] args) {
        MaxSumOf3Subarrays obj = new MaxSumOf3Subarrays();

        int[] nums = {1, 2, 1, 2, 6, 7, 5, 1};
        int k = 2;
        System.out.println("Input: " + Arrays.toString(nums) + ", k=" + k);
        int[] ans = obj.maxSumOfThreeSubarrays(nums, k);
        System.out.println("Output indices: " + Arrays.toString(ans)); // [0, 3, 5]
    }
}
```

## Dry Run (Step by Step)

1. **Sums by sliding window:**  
   sum = [3, 3, 3, 8, 13, 12, [0, 0, 0, 3,  
   (Har position tak sabse bada sum ka start index)
3. **right = [4, 4,  
   (Har position se end tak sabse bada sum ka start index)
4. **Middle subarray positions:** j = 2, 3, 4
   - Try har j par, total = sum[left[j-k]] + sum[j] + sum[right[j+k]]
   - max sum milta hai indices: 0 (left), 3 (middle), 5 (right)
5. **Final answer:** `[0,## TL;DR (Summary)

- Pehle sab k-length subarrays ka sum sliding window se nikalo.
- Fir left se max sum ka index aur right se bhi.
- Har possible middle window try karo aur best pao.
- Approach **fast** hai (O(n)) aur lexicographically smallest answer bhi yahi approach se milta hai.

