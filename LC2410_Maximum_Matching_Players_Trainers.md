



---

## 📌 Problem: Maximum Matching of Players With Trainers

**LeetCode Problem 2410**

You are given two integer arrays:
- `players[i]`: the ability of the i-th player.
- `trainers[j]`: the training capacity of the j-th trainer.

### ✅ Matching Rules:
- A player can be matched **if their ability ≤ trainer's capacity**.
- Each player and each trainer can be used in **only one match**.

### 🎯 Goal:
Return the **maximum number of matchings** that satisfy the above conditions.

---

## 💡 Greedy Matching Strategy

We aim to pair each player with the lowest available trainer capable of handling them. To achieve this:
1. Sort both `players` and `trainers`.
2. Use two pointers to greedily construct matchings.

---

## 💻 Java Code

```java
import java.util.Arrays;

class Solution {
    public int matchPlayersAndTrainers(int[] players, int[] trainers) {
        Arrays.sort(players);
        Arrays.sort(trainers);

        int i = 0;
        int j = 0;
        int matches = 0;

        while (i < players.length && j < trainers.length) {
            if (players[i] <= trainers[j]) {
                matches++;
                i++;
                j++;
            } else {
                j++;
            }
        }
        return matches;
    }
}
```

---

## 🔁 Dry Run: Step-by-Step Matching

### Input:

```java
players = [4, 7, 9];
trainers = [8, 2, 5, 8];
```

### After Sorting:

```java
players = [4, 7, 9];
trainers = [2, 5, 8, 8];
```

### Matching Walkthrough:

| Step | i (player) | j (trainer) | players[i] | trainers[j] | Comparison | Match? | matches | Pointer Movement |
|------|------------|-------------|------------|-------------|------------|--------|---------|------------------|
| 1    | 0          | 0           | 4          | 2           | 4 > 2      | ❌     | 0       | j++              |
| 2    | 0          | 1           | 4          | 5           | 4 ≤ 5      | ✅     | 1       | i++, j++         |
| 3    | 1          | 2           | 7          | 8           | 7 ≤ 8      | ✅     | 2       | i++, j++         |
| 4    | 2          | 3           | 9          | 8           | 9 > 8      | ❌     | 2       | j++              |
| 5    | 2          | 4           | —          | —           | End        | ✋     | 2       | Loop exits       |

### 🔚 Final Output:
```java
return 2;  // Max matchings
```

---

## 📎 Related Link

This post is inspired by the official LeetCode solution [here](https://leetcode.com/problems/maximum-matching-of-players-with-trainers/solutions/6951469/greedy-matching-algorithm-maximize-playe-927p/)

---

