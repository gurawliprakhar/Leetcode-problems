
---

## 🛣️ Gas Station — README

### 📘 Problem Statement

You're given a circular route with `n` gas stations.  
Each station has:
- `gas[i]`: the amount of fuel you collect at station `i`
- `cost[i]`: the fuel required to travel to station `(i+1)`

You start your journey with **an empty tank**, but can begin at **any station**.

🧭 **Goal**:  
Determine the **starting station index** from which you can complete the full circle without running out of fuel.  
Return `-1` if it's impossible.

✅ If a solution exists, it's **guaranteed to be unique**.

---

### 🎯 Constraints

- `1 <= gas.length == cost.length <= 10⁵`
- `0 <= gas[i], cost[i] <= 10⁴`

---

### 📖 Story-Style Explanation

Imagine you're a lone biker on a circular trail, weaving through gas stations that offer varying amounts of fuel.  
However, to make it from one station to the next, your bike burns fuel depending on terrain and distance.

You start with an **empty fuel tank** but unlimited capacity. So you need to plan smartly:  
Pick one gas station to start from and try to complete the loop, collecting fuel and spending it as you go.  
If you ever run dry between two stops — the journey fails. 🛑  
Can you find that **magical starting station** to complete your quest? 🧙‍♂️

---

## ✅ Greedy Approach — Optimal Solution

### 💡 Insight:
- If total fuel collected `<` total fuel cost → Impossible (`-1`)
- Otherwise, track fuel gain/loss at each step.
- Reset the starting point if fuel drops below `0`.

### 🔍 Java Code (Commented)

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0;     // Total gas collected across all stations
        int totalCost = 0;    // Total cost to travel across all stations
        int tank = 0;         // Current fuel level in tank
        int start = 0;        // Candidate starting station

        for (int i = 0; i < gas.length; i++) {
            totalGas += gas[i];          // Add fuel at station i
            totalCost += cost[i];        // Add cost to next station
            int gain = gas[i] - cost[i]; // Net gain/loss at station i
            tank += gain;                // Update fuel level

            // If tank drops below zero, we can't reach station i+1
            // Reset the start index and empty the tank
            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }

        // Final check: Can we complete the journey?
        if (totalGas >= totalCost) {
            return start;
        } else {
            return -1;
        }
    }
}
```

⏱️ Time Complexity: `O(n)`  
📦 Space Complexity: `O(1)`

---

## 🐢 Brute Force Approach — Intuitive but Inefficient

### 🚨 Strategy:
Try each station as the starting point and simulate the full journey.

### 🔍 Java Code (Commented)

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;

        for (int start = 0; start < n; start++) {
            int tank = 0;
            boolean canTravel = true;

            // Simulate full circle from station 'start'
            for (int i = 0; i < n; i++) {
                int idx = (start + i) % n;        // Circular index
                tank += gas[idx] - cost[idx];     // Update tank

                // If tank drops below 0, trip fails from this start
                if (tank < 0) {
                    canTravel = false;
                    break;
                }
            }

            // If we survived the whole loop, return start index
            if (canTravel) return start;
        }

        // No valid starting station found
        return -1;
    }
}
```

⏱️ Time Complexity: `O(n²)`  
📦 Space Complexity: `O(1)`

---

### 🧪 Example

```text
gas  = [1, 2, 3, 4, 5]
cost = [3, 4, 5, 1, 2]
Start at station 3:
→ tank = 4 - 1 = 3
→ tank = 3 + 5 - 2 = 6
→ tank = 6 + 1 - 3 = 4
→ tank = 4 + 2 - 4 = 2
→ tank = 2 + 3 - 5 = 0 ✅
```

---

