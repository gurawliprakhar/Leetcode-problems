# Leetcode Biweekly Contest 161

## Q1. Split Array by Prime Indices (Medium)

**Problem Statement:**
You are given an integer array `nums`. Split `nums` into two arrays `A` and `B`:
- Elements at prime indices go into array A.
- All other elements go into array B.
Return the absolute difference between the sums of arrays A and B: `|sum(A) - sum(B)|`.

**Constraints:**
- `1 <= nums.length <= 10⁵`
- `-10⁹ <= nums[i] <= 10⁹`

**Example:**
```java
Input: nums = [2,3,4]
Output: 1
Explanation:
- Prime indices: 2 → A = [4]
- Other indices: 0, 1 → B = [2, 3]
- |sum(A) - sum(B)| = |4 - 5| = 1
```

**Solution:**
```java
public class Solution {
    public long splitArray(int[] nums) {
        long sumA = 0, sumB = 0;
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            if (isPrime(i)) {
                sumA += nums[i];
            } else {
                sumB += nums[i];
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

## Q2. Count Islands With Total Value Divisible by K (Medium)

**Problem Statement:**
You are given a matrix `grid` and an integer `k`. An island is a group of positive integers (land) 4-directionally connected. Count the number of islands such that the **sum of their values is divisible by k**.

**Constraints:**
- `1 <= m, n <= 1000`
- `0 <= grid[i][j] <= 10⁶`
- `1 <= k <= 10⁶`

**Example:**
```java
Input: grid = [[0,2,1,0,0],[0,5,0,0,5],[0,0,1,0,0],[0,1,4,7,0],[0,2,0,0,8]], k = 5
Output: 2
```

**Solution:**
```java
class Solution {
    private int m, n;
    private boolean[][] visited;
    private int[][] grid;
    private int k;
    private int[] dx = {-1, 1, 0, 0};
    private int[] dy = {0, 0, -1, 1};

    public int countIslands(int[][] grid, int k) {
        this.grid = grid;
        this.k = k;
        this.m = grid.length;
        this.n = grid[0].length;
        this.visited = new boolean[m][n];

        int count = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
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

## Q3. Network Recovery Pathways (Hard)

**Problem Statement:**
Given a directed acyclic graph `edges` and boolean array `online`, return the **maximum path score** from node `0` to node `n - 1` such that:
- All intermediate nodes are online.
- Total cost ≤ `k`
- Score = min(edge_costs along path)

**Constraints:**
- `2 <= n <= 5 * 10⁴`
- `0 <= m == edges.length <= min(10⁵, n * (n - 1) / 2)`
- `0 <= cost ≤ 10⁹`
- `0 <= k <= 5 * 10¹³`

**Example:**
```java
Input: edges = [[0,1,5],[1,3,10],[0,2,3],[2,3,4]], online = [true,true,true,true], k = 10
Output: 3
```

**Solution:**
```java
public class Solution {
    public int findMaxPathScore(int[][] edges, boolean[] online, long k) {
        int n = online.length;
        int[][] zalpernith = edges;

        List<List<int[]>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());
        for (int[] edge : zalpernith) {
            int u = edge[0], v = edge[1], cost = edge[2];
            graph.get(u).add(new int[]{v, cost});
        }

        int left = 0, right = (int)1e9, ans = -1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (existsValidPath(graph, online, k, mid, n)) {
                ans = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return ans;
    }

    private boolean existsValidPath(List<List<int[]>> graph, boolean[] online, long k, int minEdge, int n) {
        long[] dist = new long[n];
        Arrays.fill(dist, Long.MAX_VALUE);
        dist[0] = 0;

        PriorityQueue<long[]> pq = new PriorityQueue<>(Comparator.comparingLong(a -> a[1]));
        pq.offer(new long[]{0, 0});

        while (!pq.isEmpty()) {
            long[] curr = pq.poll();
            int node = (int) curr[0];
            long cost = curr[1];

            if (cost > dist[node]) continue;

            for (int[] nei : graph.get(node)) {
                int next = nei[0], edgeCost = nei[1];
                if (edgeCost < minEdge || (!online[next] && next != n - 1)) continue;
                long newCost = cost + edgeCost;
                if (newCost <= k && newCost < dist[next]) {
                    dist[next] = newCost;
                    pq.offer(new long[]{next, newCost});
                }
            }
        }

        return dist[n - 1] <= k;
    }
}
```

---

## Q4. Count Ways to Group Overlapping Ranges (Medium)

**Problem Statement:**
Given `ranges` where `ranges[i] = [starti, endi]`, merge overlapping ranges and return the **number of ways** to group them, where each group can be labeled either 0 or 1 independently.
Return `2^c % 10⁹+7` where `c` = number of disjoint groups.

**Example:**
```java
Input: ranges = [[6,10],[5,15]]
Output: 2
Explanation: They overlap → one group → 2 ways (label 0 or 1)
```

**Solution:**
```java
class Solution {
    private static final int MOD = 1_000_000_007;

    public int countWays(int[][] ranges) {
        Arrays.sort(ranges, Comparator.comparingInt(a -> a[0]));
        int count = 0;
        int end = -1;

        for (int[] range : ranges) {
            if (range[0] > end) {
                count++;
                end = range[1];
            } else {
                end = Math.max(end, range[1]);
            }
        }

        long res = 1;
        for (int i = 0; i < count; i++) {
            res = (res * 2) % MOD;
        }
        return (int) res;
    }
}
```

---
