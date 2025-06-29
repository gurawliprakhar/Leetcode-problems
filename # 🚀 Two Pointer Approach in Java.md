

---

# 🚀 Two Pointer Approach in Java

The **Two Pointer Technique** is a powerful and commonly used algorithmic approach for solving problems involving arrays, strings, or linked lists in **linear time** with **constant space**.

---

## 📌 What is the Two Pointer Approach?

In the **Two Pointer approach**, we use **two separate variables (pointers)** to iterate over the data structure.

These two pointers can:

* **Start at both ends and move towards each other** (opposite ends)
* **Start together and move in the same direction** (same direction)
* Or even **move independently based on logic**

---

## ✅ When to Use Two Pointers?

| Scenario                    | Example Problems                   |
| --------------------------- | ---------------------------------- |
| Sorted Arrays               | Pair Sum, Removing Duplicates      |
| Subarray/Substring problems | Longest Substring Without Repeats  |
| Linked Lists                | Detect Cycles, Reverse, Merge Sort |
| Searching / Pair Matching   | Two Sum, Three Sum                 |
| Sliding Window Problems     | Maximum Subarray, Longest Window   |

---

## 🛠️ Types of Two Pointer Approaches

1. **Opposite Ends**
   Start one pointer at the beginning (`left`) and the other at the end (`right`).
   → Useful for **pair problems in sorted arrays**.

2. **Same Direction**
   Both pointers start at the same position and move forward.
   → Useful for **sliding window, duplicate removal**, etc.

---

## ✨ Example 1: Find Pair with Target Sum (Opposite Ends)

Given a **sorted array**, find if there is a pair with a given target sum.

```java
public class TwoPointerExample {
    public static boolean hasPairWithSum(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            int sum = arr[left] + arr[right];

            if (sum == target) {
                System.out.println("Pair found: " + arr[left] + ", " + arr[right]);
                return true;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 6, 8, 9};
        int target = 10;

        boolean result = hasPairWithSum(arr, target);
        if (!result) {
            System.out.println("No pair found.");
        }
    }
}
```

🧑‍💻 **Output:**

```
Pair found: 2, 8
```

---

## ✨ Example 2: Remove Duplicates from Sorted Array (Same Direction)

Given a **sorted array**, remove duplicates **in-place**.

```java
public class RemoveDuplicates {
    public static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int i = 0;

        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2, 2, 3, 4, 4};
        int newLength = removeDuplicates(nums);

        System.out.print("Array after removing duplicates: ");
        for (int i = 0; i < newLength; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```

🧑‍💻 **Output:**

```
Array after removing duplicates: 1 2 3 4
```

---

## ✅ Benefits of Two Pointer Approach

* **Time Complexity:** Usually **O(n)**
* **Space Complexity:** Usually **O(1)**
* **Readable Logic:** Clean and simple code
* **Performance Boost:** Avoids unnecessary nested loops

---

## ✅ Quick Summary

| Property        | Details                       |
| --------------- | ----------------------------- |
| Movement        | Towards each other / Forward  |
| Used On         | Arrays, Strings, Linked Lists |
| Common Problems | Pair Sum, Duplicates, Windows |

---

## ✅ Further Practice Problems 📚

* Two Sum (sorted array)
* Three Sum Problem
* Container With Most Water
* Longest Substring Without Repeating Characters
* Move Zeroes to End
* Merge Two Sorted Arrays

---


### ✅ 1. Two Sum (Sorted Array) – Two Pointers from Opposite Ends

```java
public class TwoSumSorted {
    public static int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                return new int[] {left, right};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[] {-1, -1};  // Not found
    }

    public static void main(String[] args) {
        int[] arr = {2, 7, 11, 15};
        int target = 9;
        int[] result = twoSum(arr, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```

---

### ✅ 2. Three Sum Problem – Nested Two Pointer after Sorting

```java
import java.util.*;

public class ThreeSum {
    public static List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();

        for (int i = 0; i < nums.length - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++;
                    right--;

                    while (left < right && nums[left] == nums[left - 1]) left++;
                    while (left < right && nums[right] == nums[right + 1]) right--;

                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {-1, 0, 1, 2, -1, -4};
        System.out.println(threeSum(nums));
    }
}
```

---

### ✅ 3. Container With Most Water – Two Pointers from Ends Moving Inward

```java
public class ContainerWithMostWater {
    public static int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int maxArea = 0;

        while (left < right) {
            int area = Math.min(height[left], height[right]) * (right - left);
            maxArea = Math.max(maxArea, area);

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        return maxArea;
    }

    public static void main(String[] args) {
        int[] height = {1,8,6,2,5,4,8,3,7};
        System.out.println("Max Area: " + maxArea(height));
    }
}
```

---

### ✅ 4. Longest Substring Without Repeating Characters – Pure Sliding Window (Two Pointers without Set)

Since the problem naturally requires uniqueness checking, here’s the **Two Pointer with manual duplicate check (O(n^2))** instead of Set:

```java
public class LongestSubstringNoRepeat {
    public static int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        int left = 0;

        for (int right = 0; right < s.length(); right++) {
            for (int i = left; i < right; i++) {
                if (s.charAt(i) == s.charAt(right)) {
                    left = i + 1;  // Move left to avoid duplicate
                    break;
                }
            }
            maxLength = Math.max(maxLength, right - left + 1);
        }
        return maxLength;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Longest substring length: " + lengthOfLongestSubstring(s));
    }
}
```

> ✅ **Note:** This is not the most optimized solution (best would need HashSet or Map), but it’s pure **two-pointer based**.

---

### ✅ 5. Move Zeroes to End – Two Pointer Overwriting Approach

```java
public class MoveZeroes {
    public static void moveZeroes(int[] nums) {
        int left = 0;

        for (int right = 0; right < nums.length; right++) {
            if (nums[right] != 0) {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
            }
        }
    }

    public static void main(String[] args) {
        int[] nums = {0, 1, 0, 3, 12};
        moveZeroes(nums);
        System.out.print("After moving zeroes: ");
        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

### ✅ 6. Merge Two Sorted Arrays – Two Pointers from End to Start (In-place Merge)

```java
public class MergeSortedArrays {
    public static void merge(int[] nums1, int m, int[] nums2, int n) {
        int p1 = m - 1;
        int p2 = n - 1;
        int p = m + n - 1;

        while (p1 >= 0 && p2 >= 0) {
            if (nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1];
                p1--;
            } else {
                nums1[p] = nums2[p2];
                p2--;
            }
            p--;
        }

        while (p2 >= 0) {
            nums1[p] = nums2[p2];
            p2--;
            p--;
        }
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 3, 0, 0, 0};
        int[] nums2 = {2, 5, 6};
        merge(nums1, 3, nums2, 3);
        System.out.print("Merged array: ");
        for (int num : nums1) {
            System.out.print(num + " ");
        }
    }
}
```

---

# ✅ ✅ ✅ ✅ Summary Table:

| Problem                         | Two Pointer Type                |
| ------------------------------- | ------------------------------- |
| Two Sum                         | Start-End (Opposite Direction)  |
| Three Sum                       | Fixed + Two Pointers (Nested)   |
| Container With Most Water       | Start-End (Opposite Direction)  |
| Longest Substring (without Set) | Sliding Window (Same Direction) |
| Move Zeroes                     | Same Direction                  |
| Merge Two Sorted Arrays         | Backward Two Pointers           |

---


---

# ✅ More Classic Two Pointer Problems with Java Solutions

---

## 7. ✅ **Remove Duplicates from Sorted Array (Leetcode 26)**

**Problem:** Given a **sorted array**, remove duplicates in-place.

```java
public class RemoveDuplicates {
    public static int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;

        int left = 0;
        for (int right = 1; right < nums.length; right++) {
            if (nums[right] != nums[left]) {
                left++;
                nums[left] = nums[right];
            }
        }
        return left + 1;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2, 3, 3, 4};
        int length = removeDuplicates(nums);
        System.out.print("After removing duplicates: ");
        for (int i = 0; i < length; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```

---

## 8. ✅ **Sorted Squares of a Sorted Array (Leetcode 977)**

**Problem:** Return squares of a sorted array in sorted order.

```java
import java.util.*;

public class SortedSquares {
    public static int[] sortedSquares(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        int left = 0, right = n - 1, pos = n - 1;

        while (left <= right) {
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                result[pos--] = nums[left] * nums[left];
                left++;
            } else {
                result[pos--] = nums[right] * nums[right];
                right--;
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {-7, -3, 2, 3, 11};
        int[] res = sortedSquares(nums);
        System.out.println(Arrays.toString(res));
    }
}
```

---

## 9. ✅ **Reverse a String In-Place (Leetcode 344)**

```java
public class ReverseString {
    public static void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }

    public static void main(String[] args) {
        char[] s = {'h', 'e', 'l', 'l', 'o'};
        reverseString(s);
        System.out.println(s);
    }
}
```

---

## 10. ✅ **Palindrome Check (Valid Palindrome) (Leetcode 125)**

```java
public class ValidPalindrome {
    public static boolean isPalindrome(String s) {
        s = s.toLowerCase();
        int left = 0, right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;

            if (s.charAt(left) != s.charAt(right)) return false;

            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "A man, a plan, a canal: Panama";
        System.out.println(isPalindrome(s));  // true
    }
}
```

---

## 11. ✅ **Remove Element (Leetcode 27)**

**Problem:** Remove all instances of a given value `val` from the array in-place.

```java
public class RemoveElement {
    public static int removeElement(int[] nums, int val) {
        int left = 0;

        for (int right = 0; right < nums.length; right++) {
            if (nums[right] != val) {
                nums[left++] = nums[right];
            }
        }
        return left;
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 2, 3};
        int length = removeElement(nums, 3);
        System.out.print("After removal: ");
        for (int i = 0; i < length; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```

---

## 12. ✅ **Find Maximum Number of Consecutive 1s (Leetcode 485)**

```java
public class MaxConsecutiveOnes {
    public static int findMaxConsecutiveOnes(int[] nums) {
        int maxCount = 0;
        int left = 0;

        for (int right = 0; right < nums.length; right++) {
            if (nums[right] == 1) {
                maxCount = Math.max(maxCount, right - left + 1);
            } else {
                left = right + 1;
            }
        }
        return maxCount;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 0, 1, 1, 1};
        System.out.println(findMaxConsecutiveOnes(nums));  // Output: 3
    }
}
```

---

## ✅ Summary of Additional Two Pointer Problems:

| Problem            | Two Pointer Type                     |
| ------------------ | ------------------------------------ |
| Remove Duplicates  | Slow & Fast pointer (same direction) |
| Sorted Squares     | Two Ends moving inward               |
| Reverse String     | Start-End swap                       |
| Valid Palindrome   | Two Ends skipping non-alphanumeric   |
| Remove Element     | Slow & Fast pointer                  |
| Max Consecutive 1s | Sliding Window (Two Pointers)        |

---



---



