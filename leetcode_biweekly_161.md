

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




