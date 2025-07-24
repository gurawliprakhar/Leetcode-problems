
## Problem Statement (Hinglish)

Aapko ek **array** `nums` diya hai, aur ek integer `k`.  
Count karo kitne **contiguous subarrays** (lagatar elements ka group) aise hain jinka **product** `k` se strictly chhota hai.

Yani, aapko har aise subarray ki ginati karni hai jinke elements ka multiplication `k` se kam ho.

## Example Testcase

Input:
```
nums = [10, 5, 2, 6]
k = 100
```
Output:
```
8
```

#### Explanation:
Yeh 8 subarrays hain jinka product = k) {
                product /= nums[left];
                left++;
            }
            result += right - left + 1;
        }
        return result;
    }
}
```

## Dry Run (Hinglish)

Input:
```
nums = [10, 5, 2, 6], k = 100
```

1. right = 0 → 10 < 100  
   Window = , result = 1
2. right = 1 → 10*5 = 50 < 100  
   Window = , ; result += 2 (total 3)
3. right = 2 → 50*2 = 100 (not < 100)  
   Ab left = 1 (remove 10), product = 5*2 = 10 < 100  
   Window = , ; result += 2 (total 5)
4. right = 3 → 10*6 = 60 < 100  
   Window = , , ; result += 3 (total 8)

Output is **8**.

## Summary

- Problem: Count all contiguous subarrays with product less than `k`.
- Approach: Sliding window technique for product tracking and efficient counting.
- Complexity: O(n) time, O(1) space.
- Code and dry run steps included for clarity.

