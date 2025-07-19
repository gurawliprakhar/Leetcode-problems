

---

### 🎬 ** Split Array by Prime Indices | Leetcode Biweekly Contest 161 Q1**

---



---

#### 📄 **\[Problem Statement - ]**

```
🎤 "You are given an integer array called `nums`. We need to split this array into two new arrays — A and B — based on a simple rule:

- All elements at **prime indices** go into array A.
- All other elements go into array B.

Once split, we return the **absolute difference** between the sums of arrays A and B.

That is: return |sum(A) - sum(B)|"
```

---

#### 🧠 **\[Understanding with Example - ]**

```
🎤 "Let’s understand with an example:

Input: nums = [2, 3, 4]

The indices are: 0 → 2, 1 → 3, 2 → 4

Index 2 is prime → goes to A → A = [4]
Indices 0 and 1 are not prime → go to B → B = [2, 3]

Sum(A) = 4, Sum(B) = 5 → Output = |4 - 5| = 1"
```

---

#### 🔎 **\[Prime Index Logic ]**

```
🎤 "Now the main challenge is identifying whether an index is prime. Remember, a prime number is greater than 1 and only divisible by 1 and itself.

So we’ll write a helper function `isPrime(i)` to check if an index is prime."
```

---

#### 💻 **\[Java Code Explanation ]**

```java
public class Solution {
    public long splitArray(int[] nums) {
        long sumA = 0, sumB = 0;

        for (int i = 0; i < nums.length; i++) {
            if (isPrime(i)) {
                sumA += nums[i]; // Prime index → array A
            } else {
                sumB += nums[i]; // Non-prime index → array B
            }
        }

        return Math.abs(sumA - sumB);
    }

    private boolean isPrime(int num) {
        if (num < 2) return false;
        if (num == 2) return true;
        if (num % 2 == 0) return false;
        for (int i = 3; i * i <= num; i += 2) {
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

---

#### 🧪 **\[Sample Test Cases - ]**

```
🎤 "Let’s look at a few sample test cases."

Test Case 1:
Input: [2, 3, 4]
Prime Index: 2 → A = [4], B = [2, 3] → Output: 1

Test Case 2:
Input: [-1, 5, 7, 0]
Prime Indices: 2, 3 → A = [7, 0], B = [-1, 5] → Output: 3
```

---

#### ✅ **\[Summary ]**

```
🎤 "To summarize:
- Prime index detection is key.
- Just add elements accordingly to A or B.
- Then return the absolute difference of their sums.

This solution runs in O(n√n) worst-case due to prime checks but is fast enough for contest constraints."
```

---


---
! Let's now move to **Problem 2: Count Islands With Total Value Divisible by K** from Leetcode Biweekly Contest 161.

---

## 🎬 ** Count Islands With Total Value Divisible by K | Biweekly 161 Q2**

---



---

### 📄 **\[Problem Statement -]**

```
🎤 "We are given a grid of integers and a number `k`.

Each group of **4-directionally connected positive integers** in the grid forms an island.

We have to count how many such islands have their **total value divisible by k**.

So, we need to:
1. Identify islands
2. Sum values of each island
3. Count only those where sum % k == 0
```

---

### 🧠 **\[Understanding with Example - ]**

#### Example 1:

```
Input: 
grid = [
  [0,2,1,0,0],
  [0,5,0,0,5],
  [0,0,1,0,0],
  [0,1,4,7,0],
  [0,2,0,0,8]
]
k = 5

🎤 "There are 4 islands. Out of them, 2 have total value divisible by 5, so the output is 2."
```

---

### 💻 **\[Code Walkthrough ]**

```java
class Solution {
    private int m, n;
    private boolean[][] visited;
    private int[][] grid;
    private int k;
    private int[] dx = {-1, 1, 0, 0}; // up, down
    private int[] dy = {0, 0, -1, 1}; // left, right

    public int countIslands(int[][] grid, int k) {
        this.grid = grid;
        this.k = k;
        this.m = grid.length;
        this.n = grid[0].length;
        this.visited = new boolean[m][n];
        int count = 0;

        // Loop through each cell in the grid
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // Start DFS if cell is unvisited land
                if (grid[i][j] > 0 && !visited[i][j]) {
                    int[] sum = new int[1];
                    dfs(i, j, sum);
                    if (sum[0] % k == 0) {
                        count++;
                    }
                }
            }
        }

        return count;
    }

    private void dfs(int x, int y, int[] sum) {
        visited[x][y] = true;
        sum[0] += grid[x][y];

        // Explore 4 directions
        for (int d = 0; d < 4; d++) {
            int nx = x + dx[d];
            int ny = y + dy[d];

            if (nx >= 0 && nx < m && ny >= 0 && ny < n &&
                grid[nx][ny] > 0 && !visited[nx][ny]) {
                dfs(nx, ny, sum);
            }
        }
    }
}
```

---

### 🔍 **\[Code Explanation ]**

```
🎤 "Let’s break it down:

- We use Depth-First Search (DFS) to explore connected land (positive cells).
- While visiting each cell in an island, we keep adding its value to `sum[0]`.
- After completing one island, we check if `sum % k == 0`. If yes, we count it.

We use a visited[][] matrix to make sure we don't revisit the same cell."
```

---

### 🧪 **\[Test Cases -]**

#### Test Case 1:

```java
grid = [
  [0,2,1,0,0],
  [0,5,0,0,5],
  [0,0,1,0,0],
  [0,1,4,7,0],
  [0,2,0,0,8]
]
k = 5

🎤 Output = 2
```

#### Test Case 2:

```java
grid = [
  [3,0,3,0],
  [0,3,0,3],
  [3,0,3,0]
]
k = 3

🎤 Output = 6 (Each individual 3 is an island)
```

---

### ⏱️ **\[Time & Space Complexity ]**

```
🎤 "Time Complexity is O(m * n) — we visit each cell once.

Space Complexity is also O(m * n) due to the visited array."
```

---

### ✅ **\[Conclusion ]**

```
🎤 "So the key concepts in this problem:
- Island DFS traversal
- Keeping track of sum
- Divisibility check

If you’ve done 'Number of Islands' before, this will feel familiar with a twist!"
```

---

= **Problem 3: Minimum Number of Operations to Make Array XOR Equal to K** from **Leetcode Biweekly Contest 161**.

---

## 🎬 **Minimum Operations to Make XOR Equal to K | Biweekly 161 Q3**

---

### 🎙️ **\[Intro - 0:00]**

```
 "Leetcode Biweekly 161 - Question 3"

🎤 "Hey everyone! Welcome back t. In this we’ll solve Leetcode Biweekly 161 Question 3 — *Minimum Number of Operations to Make Array XOR Equal to K*.

This problem blends bitwise XOR, frequency counting, and clever DP — let’s break it down!"
```

---

### 📄 **\[Problem Statement - ]**

```
🎤 "You’re given an array `nums` and an integer `k`.

In **one operation**, you can **replace any element in the array** with **any non-negative integer**.

Your goal: make the XOR of the entire array equal to `k`.

Return the minimum number of operations needed."
```

---

### 🧠 **\[Example - ]**

#### Example:

```
Input: nums = [2,1,3], k = 1

Current XOR = 2 ^ 1 ^ 3 = 0

We want XOR = 1 → So change one element (e.g., change 3 to 1)

New XOR = 2 ^ 1 ^ 1 = 2

Try changing 2 to 2 → no use.

Eventually, change two elements → XOR becomes 1.

So output = 2.
```

---

### 💡 **\[Approach ]**

```
🎤 "Let’s analyze the idea:

1. Let `x` be the XOR of all numbers in the array.
2. If x == k → no changes needed → return 0.
3. Else, try to replace minimum elements to get XOR = k.

We can use the bitwise property:

    a ^ b = c  →  b = a ^ c

So if x != k, the difference = x ^ k

We count how many bits are set in (x ^ k) → that’s how many places we need to flip to fix the XOR.

But since we can change **any element**, and we can pick any value, we can do it optimally."
```

---

### 💻 **\[Code Walkthrough ]**

```java
class Solution {
    public int minimumOperations(int[] nums, int k) {
        int xor = 0;
        for (int num : nums) {
            xor ^= num;
        }
        
        // If XOR is already equal to k, no ops needed
        if (xor == k) return 0;

        // Otherwise, need to make xor == k → change some elements
        return 1;
    }
}
```

---

### 🔍 **\[Why Return 1? - ]**

```
🎤 "Here’s the trick — You can **replace any number** with **any value**. That means, you can **force any XOR output in 1 operation**.

Why?

Let’s say:
- Current XOR = x
- We want XOR = k

Then change 1 element `nums[i]` to `nums[i] ^ (x ^ k)`.

This will flip the current XOR to k.

✅ So in 1 operation, we can force it.

Only when x == k, we need 0 ops.

So the final logic is:
- If x == k → return 0
- Else → return 1
```

---

### 🧪 **\[Test Cases - ]**

#### Test Case 1:

```java
nums = [2,1,3], k = 1
XOR = 2^1^3 = 0 → 0 != 1 → output = 1
```

#### Test Case 2:

```java
nums = [5,5], k = 0
XOR = 5^5 = 0 → 0 == 0 → output = 0
```

---

### ⏱️ **\[Time & Space Complexity ]**

```
🎤 "Time Complexity: O(n) to compute XOR

Space Complexity: O(1)

Very efficient solution!"
```

---

### ✅ **\[Conclusion -]**

```
🎤 "This was a nice problem testing our understanding of XOR properties.

If you can freely change values, then you can force any XOR in just one operation!"
```

---
Perfect! Let’s now work on the * for Problem 4 from **Leetcode Biweekly Contest 161**:

---

## 🎬 ** Number of Integers With Popcount-Depth Equal to K | Biweekly 161 Q4**

---

### 🎙️ **\[Intro - 0:00]**

```
 "Leetcode Biweekly 161 - Question 4"

🎤 "Hey everyone, welcome back  In this we’ll solve the final problem from Leetcode Biweekly 161 — *Number of Integers With Popcount-Depth Equal to K*.

This is a hard-level bit manipulation + DP problem — so let’s walk through it step by step!"
```

---

### 📄 **\[Problem Statement - ]**

```
🎤 "You are given two integers `n` and `k`.

A number x has a *popcount-depth* defined as follows:

- Create a sequence:
    - p0 = x
    - pi+1 = popcount(pi), where popcount = number of set bits in binary

- Stop when you reach 1. The number of steps taken is called the popcount-depth.

👉 Your task: count how many numbers from 1 to n have popcount-depth exactly equal to k."
```

---

### 🧠 **\[Understanding Through Example - ]**

#### Example:

```
Input: n = 7, k = 2

Check numbers from 1 to 7:

x = 3 (11) → 3 → 2 → 1 → depth = 2 ✅

x = 5 (101) → 5 → 2 → 1 → depth = 2 ✅

x = 6 (110) → 6 → 2 → 1 → depth = 2 ✅

Answer: 3
```

---

### 🔬 **\[Approach - Intuition First ]**

```
🎤 "We observe two things:

1. Final popcount-depth depends on how many 1s the number has, and how many 1s that number’s popcount has... until we reach 1.
2. If we could precompute the depth for each popcount, we can count how many numbers up to n have exactly that number of 1s.

→ This calls for: 
    - Bit counting logic
    - Dynamic Programming
    - Digit DP to count numbers up to n with a specific number of 1s"
```

---

### 🛠️ **\[Code Walkthrough ]**

```java
class Solution {
    int[] dpDepth = new int[1001];
    Long[][][] memo;

    public int countExcellentNumbers(long n, int k) {
        if (k == 0) return 0;
        // Precompute popcount-depths
        Arrays.fill(dpDepth, -1);
        dpDepth[0] = 0;
        dpDepth[1] = 0;
        for (int i = 2; i <= 1000; i++) {
            dpDepth[i] = 1 + dpDepth[Integer.bitCount(i)];
        }

        // Convert n to binary digits (MSB to LSB)
        List<Integer> bin = new ArrayList<>();
        while (n > 0) {
            bin.add((int)(n % 2));
            n /= 2;
        }
        Collections.reverse(bin);

        // Memoization for digit DP
        memo = new Long[bin.size() + 1][bin.size() + 1][2];
        long ans = 0;

        // Try all popcount values i with depth k
        for (int i = 1; i <= bin.size(); i++) {
            if (dpDepth[i] == k) {
                ans += dfs(0, 0, 1, i, bin);
            }
        }
        return (int) ans;
    }

    private long dfs(int pos, int count, int tight, int target, List<Integer> bin) {
        if (count > target) return 0;
        if (pos == bin.size()) return count == target ? 1 : 0;

        if (memo[pos][count][tight] != null) return memo[pos][count][tight];

        int limit = tight == 1 ? bin.get(pos) : 1;
        long res = 0;
        for (int d = 0; d <= limit; d++) {
            res += dfs(pos + 1, count + d, tight == 1 && d == limit ? 1 : 0, target, bin);
        }
        return memo[pos][count][tight] = res;
    }
}
```

---

### 🔍 **\[Code Explanation ]**

```
🎤 "Let’s break it down:

1. Precompute popcount-depths for all possible popcounts (up to 1000)
2. For each number of 1s `i`, check if its popcount-depth == k
3. If yes, count how many numbers ≤ n have exactly `i` bits set
   → Use digit-DP to count binary numbers with exactly i 1s, ≤ n

So it's:
- Outer loop for possible popcounts
- Inner digit-DP using DFS with memoization"
```

---

### 🧪 **\[Test Cases -]**

#### Test Case 1:

```java
n = 4, k = 1
Numbers: 2 (10) → 2→1 ✅, 4 (100) → 4→1 ✅
Output: 2
```

#### Test Case 2:

```java
n = 7, k = 2
Numbers: 3, 5, 6 → depth = 2
Output: 3
```

---

### ⏱️ **\[Time & Space Complexity ]**

```
🎤 "Time: O(#bits * #bits * 2) = around O(100 * 100)

Space: O(bits * ones * tight) for DP memo

Super efficient even for n up to 10^15"
```

---

### ✅ **\[Conclusion - ]**

```
🎤 "This was a classic case of combining number theory with digit DP.

We precompute popcount depths, then count matching numbers efficiently using binary digit logic."

📌 "You’ll see this trick often in hard problems with large n ranges!"
```

---







