
```markdown
# 🎯 Maximum Value of Attending Events (Java Solution)

This repository contains a Java solution to the classic dynamic programming problem: **Maximize the total value by attending at most `k` non-overlapping events**.

---

## 📖 Problem Statement

You are given a list of events, where each event is represented as:

```

\[startDay, endDay, value]

````

You are also given an integer `k`, which is the **maximum number of events** you can attend.

Each event:
- Requires full attention for its duration (no overlapping).
- Earns a certain value if attended.
- Can only be chosen **if it doesn’t overlap** with any already-attended event (even a single day overlap is not allowed).

---

## 🧪 Example

### Input:
```java
events = [[1,2,4], [3,4,3], [2,3,1]];
k = 2;
````

### Output:

```
7
```

### ✅ Explanation:

* Pick Event 0: `[1,2] → value = 4`
* Then pick Event 1: `[3,4] → value = 3`
* Total value = **4 + 3 = 7**

You **cannot** attend Event 2 `[2,3]` together with Event 0 or 1 due to overlap.

---

## 💡 Approach

We use:

* **Top-down Dynamic Programming** (`dfs(i, k)`) — where `i` is the current event index and `k` is the number of events left to attend.
* **Memoization** to avoid recomputation.
* **Binary Search** to quickly find the next event that can be attended after taking the current one.

---

## 🔁 Java Code

```java
import java.util.*;

class Solution {
    public int maxValue(int[][] events, int k) {
        Arrays.sort(events, Comparator.comparingInt(a -> a[0]));
        int n = events.length;
        int[][] dp = new int[n][k + 1];

        for (int[] row : dp) Arrays.fill(row, -1);

        return dfs(0, k, events, dp);
    }

    private int dfs(int i, int k, int[][] events, int[][] dp) {
        if (i == events.length || k == 0) return 0;
        if (dp[i][k] != -1) return dp[i][k];

        int skip = dfs(i + 1, k, events, dp);
        int next = binarySearch(events, events[i][1]);
        int take = events[i][2] + dfs(next, k - 1, events, dp);

        return dp[i][k] = Math.max(skip, take);
    }

    private int binarySearch(int[][] events, int endTime) {
        int l = 0, h = events.length;
        while (l < h) {
            int m = (l + h) / 2;
            if (events[m][0] > endTime) h = m;
            else l = m + 1;
        }
        return l;
    }
}
```

---

## 🧠 Dry Run Example

### Input:

```java
events = [[1,2,4], [2,3,1], [3,4,3]];
k = 2
```

Sorted by start day:

```
[1,2,4]
[2,3,1]
[3,4,3]
```

Start from index `0` with `k=2`:

### Step-by-Step:

* **Option 1: Skip Event 0** → DFS(1, 2)
* **Option 2: Take Event 0** (value = 4)

  * Find next non-overlapping event using binary search (event 2)
  * DFS(2, 1) → returns 3
  * Total value = 4 + 3 = **7**

Choose `max(7, DFS(1, 2))`

Eventually: `dp[0][2] = 7`

---

## 🕐 Time & Space Complexity

| Metric | Complexity         |
| ------ | ------------------ |
| Time   | `O(n * k * log n)` |
| Space  | `O(n * k)`         |

Where `n` is the number of events and `k` is the max number of events you can attend.

---

## 🧾 Summary

✅ You decide whether to **skip or take** an event.
✅ If taken, use **binary search** to jump to the next non-overlapping event.
✅ **Memoize** results to avoid repeated calculations.

---

## 📂 File Structure

```
├── src
│   └── Solution.java     # Main DP + Binary Search logic
├── README.md             # Explanation, dry run, and code walkthrough
```

---

## 📌 Tips for Interviews

* Always sort intervals if planning to apply binary search.
* Use memoization to reduce exponential recursive solutions.
* Carefully handle the "next valid choice" when events overlap.

---

## 🧠 Related Concepts

* Dynamic Programming (Top-Down)
* Interval Scheduling
* Binary Search on Time
* Memoization

---

## 📢 Author

Created with ❤️ by \[Your Name]
Feel free to fork, clone, or star ⭐ the repository!

```

---

```
