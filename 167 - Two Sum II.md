Problem Explanation (Hinglish)
Aapko ek sorted integer array diya hua hai, jisme numbers already non-decreasing order mein hain. Aapko do aise numbers dhoondhne hain jinki sum ek given target ke barabar ho.

Array 1-indexed hai, matlab indices 1 se count karne hain. Aapko un do numbers ke indices (1-based) return karne hain jinhe jodke target ban raha hai.

Constraints:

Array size minimum 2, max 30,000

Exactly one solution guaranteed hai.

Same element do baar use nahi kar sakte.

Approach
Two Pointer Technique (Efficient)
Start with two pointers: left=0 (start), right=n-1 (end) of array.

Sum karo numbers[left] + numbers[right].

Agar sum target se chhota hai, toh left++ karke sum bada karo.

Agar sum target se bada hai, toh right-- karke sum chhota karo.

Sum agar target ke barabar ho toh wahi answer hai aur return karo.

Time complexity is O(n), and space complexity O(1).

Brute Force Approach (Naive)
Two nested for loops iterate karke sab pairs check karo.

Time complexity O(n²), space O(1).

Simple but inefficient for large n.

Code (Java)
Two Pointers Solution
java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                // 1-based indexing
                return new int[] {left + 1, right + 1};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        // problem statement guarantees solution, so never reached
        return new int[] {-1, -1};
    }
}
Optional: Brute Force Two For Loop Solution
java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length;

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (numbers[i] + numbers[j] == target) {
                    return new int[] {i + 1, j + 1};
                }
            }
        }
        return new int[] {-1, -1};
    }
}
Dry Run Example (Hinglish)
Input:

text
numbers = [2, 7, 11, 15]
target = 9
Start: left=0 (points to 2), right=3 (points to 15)
Sum = 2 + 15 = 17 > 9 → right-- → right=2 (points to 11)

Sum = 2 + 11 = 13 > 9 → right-- → right=1 (points to 7)

Sum = 2 + 7 = 9 == target → return [1,

Output: [1,[2]

Summary
Sorted array hone ki wajah se two-pointer technique best suited hai.

Brute force simple hai lekin inefficient hai.

Two pointers se O(n) solution milta hai with constant extra space.

Problem ke according exactly one solution hai, toh early return possible hai.
