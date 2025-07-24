

# Minimum Score After Removals on a Tree  
**File:** `Solution.java`  
**Problem No:** 2322 (LeetCode)

## Problem Explanation (in Hinglish)

Aapke paas ek *tree* hota hai jisme `n` nodes hote hain, jinke values `nums[]` mein diye gaye hain. Aapko *do edges* remove karne hain taaki tree teen connected components mein split ho jaye. Har component ke nodes ka values XOR karo. Fir teeno XOR values mein se sabse bada aur sabse chhota XOR value ka difference leke, us difference ko **score** kehte hain.

**Goal:** Aise do edges choose karo jinka score minimum ho.

## Sample Test Case

``` 
Input:
nums = [9, 14, 2, 1]
edges = [[2,3], [3,0], [3,1]]

Output:
11
```

## Code (Java)

```java
import java.util.*;

class Solution {
    private int[] subtreeXor;           // subtree ke nodes ka XOR
    private Set[] descendants; // har node ke descendants ka set
    private List[] graph;      // adjacency list

    private void dfs(int node, int parent, int[] nums) {
        subtreeXor[node] = nums[node];
        descendants[node].add(node);  // apne aapko descendant me add karo

        for (int neighbor : graph[node]) {
            if (neighbor != parent) {
                dfs(neighbor, node, nums);
                subtreeXor[node] ^= subtreeXor[neighbor];        // child subtree XOR add karo
                descendants[node].addAll(descendants[neighbor]); // child descendants add karo
            }
        }
    }

    public int minimumScore(int[] nums, int[][] edges) {
        int n = nums.length;
        graph = new ArrayList[n];
        for (int i = 0; i ();
        for (int[] edge : edges) {
            graph[edge[0]].add(edge[1]);
            graph[edge[1]].add(edge[0]);
        }

        subtreeXor = new int[n];
        descendants = new HashSet[n];
        for (int i = 0; i ();

        dfs(0, -1, nums);

        int totalXor = subtreeXor[0];
        int minScore = Integer.MAX_VALUE;

        // Har pair of nodes check karo (i,j)
        for (int i = 1; i < n; i++) {
            for (int j = i+1; j < n; j++) {
                int xorI = subtreeXor[i];
                int xorJ = subtreeXor[j];
                int val1, val2, val3;

                if (descendants[i].contains(j)) {
                    val1 = xorJ;
                    val2 = xorI ^ xorJ;
                    val3 = totalXor ^ xorI;
                } else if (descendants[j].contains(i)) {
                    val1 = xorI;
                    val2 = xorJ ^ xorI;
                    val3 = totalXor ^ xorJ;
                } else {
                    val1 = xorI;
                    val2 = xorJ;
                    val3 = totalXor ^ xorI ^ xorJ;
                }

                int maxVal = Math.max(val1, Math.max(val2, val3));
                int minVal = Math.min(val1, Math.min(val2, val3));
                minScore = Math.min(minScore, maxVal - minVal);
            }
        }
        return minScore;
    }
}
```

## Dry Run Explanation (on Sample Test Case)

`nums = [9][2][1]`  
`edges = [[2][3], [3], [3][1]]`

- Tree connections:  
  `2 — 3 — 0`  
       `|`  
       `1`

- **Subtree XOR Calculation (from DFS):**  
  - Node 2 subtree XOR = 2  
  - Node 1 subtree XOR = 14  
  - Node 3 subtree XOR = 1 ^ 2 ^ 14 = 13  
  - Node 0 subtree XOR = 9 ^ 13 = 4 (root subtree XOR)

- **Descendants Sets:**  
  - For Node 3: {1, 2, 3}  
  - For Node 0: {0, 1, 2, 3}  
  - Others accordingly.

- **Check pairs (i, j):**  
  - Pair (1,3): Since Node 1 is descendant of Node 3,  
    val1 = xorI = 14  
    val2 = xorJ ^ xorI = 13 ^ 14 = 3  
    val3 = totalXor ^ xorJ = 4 ^ 13 = 9  
    Score = max(14, 3, 9) - min(14, 3, 9) = 14 - 3 = 11

- Minimum score for this test case is `11`.

## Notes

- Descendants sets help identify ancestor-descendant relationships.
- Calculating subtree XORs with DFS helps quickly find XOR of any component formed after edge removals.
- This approach can become memory heavy for large trees; Euler tour with timestamps is an alternative (not implemented here).
- The code checks all pairs of nodes to simulate the removal of two edges leading to those subtrees.

Thank you for checking out this project! Feel free to ⭐ star the repo if you found this helpful.  
Happy Coding!

*For any questions or contributions, please open an issue or create a pull request.*

