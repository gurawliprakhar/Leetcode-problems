

---

### 🧠 What Is the H-Index?

The **H-Index** is a metric used to measure a researcher's productivity and impact based on their publications.

> A researcher has an h-index of **h** if they have **at least h papers** that have been **cited at least h times** each.

---

### 📦 Problem Statement (in your own words)

You're given an array `citations[]`, where each element represents the number of citations a researcher received for one of their papers.

Your task is to **find the maximum value of `h`** such that the researcher has **at least `h` papers** with **`≥ h` citations**.

---

### 🧪 Example

```java
Input:  citations = [3, 0, 6, 1, 5]
Output: 3
```

**Why?**
- The researcher has 5 papers.
- 3 of them have at least 3 citations: `[3, 6, 5]`
- The other 2 have fewer than 3 citations: `[0, 1]`
- So the h-index is **3**.

---

### 🧩 How to Think About It

You're trying to find the **largest number `h`** such that:
- There are **`h` or more papers** with **`≥ h` citations**.

You can brute-force this by trying every possible `h` from `n` down to `0`, and checking how many papers meet the condition.

---

Here’s a clear and structured explanation of the **approach** you used for solving the H-Index problem using brute force:

---

### 🧭 Brute Force Approach to H-Index

#### 🔹 Goal:
Find the **maximum value of `h`** such that the researcher has **at least `h` papers** with **`≥ h` citations**.

---

### 🧱 Step-by-Step Breakdown:

1. **Loop through all possible h-values** from `n` (total number of papers) down to `0`.
   - Why from high to low? Because we want the **maximum** valid h-index.

2. For each `h`, **count how many papers** have at least `h` citations.

3. If the count is **greater than or equal to `h`**, then `h` is a valid h-index — return it immediately.

4. If no such `h` is found, return `0`.

---



- Outer loop: tries every possible h-index `i`.
- Inner loop: counts how many papers have `≥ i` citations.
- If that count is `≥ i`, then `i` is the answer.

---

### ⏱️ Time Complexity:
- **O(n²)** — because of the nested loops.
- Acceptable for small inputs (n ≤ 5000).

---


# Code
```java []
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;

        for (int i = n; i >= 0; i--) {
            int count = 0;
            for (int j = 0; j < n; j++) {
                if (citations[j] >= i) {
                    count++;
                }
            }

            if (count >= i)  {
                return i;
            }
        }
        return 0;
    }
}
```
Absolutely, Prakhar! Let’s go through your code **line by line** with a **detailed dry run** using the input:

```java
citations = [3, 0, 6, 1, 5]
```

---

### 🧠 Code:
```java
int n = citations.length;
```
- `n = 5` (there are 5 papers)

---

### 🔁 Outer loop: `for (int i = n; i >= 0; i--)`

We try every possible h-index value from 5 down to 0.

---

### 🔍 i = 5
```java
int count = 0;
```
- Start with `count = 0`

```java
for (int j = 0; j < n; j++) {
    if (citations[j] >= 5) {
        count++;
    }
}
```
- j = 0 → 3 ≥ 5? ❌  
- j = 1 → 0 ≥ 5? ❌  
- j = 2 → 6 ≥ 5? ✅ → count = 1  
- j = 3 → 1 ≥ 5? ❌  
- j = 4 → 5 ≥ 5? ✅ → count = 2  

```java
if (count >= 5) → 2 >= 5? ❌
```
→ Continue to next i

---

### 🔍 i = 4
- count = 0  
- j = 0 → 3 ≥ 4? ❌  
- j = 1 → 0 ≥ 4? ❌  
- j = 2 → 6 ≥ 4? ✅ → count = 1  
- j = 3 → 1 ≥ 4? ❌  
- j = 4 → 5 ≥ 4? ✅ → count = 2  

```java
if (count >= 4) → 2 >= 4? ❌
```
→ Continue to next i

---

### 🔍 i = 3
- count = 0  
- j = 0 → 3 ≥ 3? ✅ → count = 1  
- j = 1 → 0 ≥ 3? ❌  
- j = 2 → 6 ≥ 3? ✅ → count = 2  
- j = 3 → 1 ≥ 3? ❌  
- j = 4 → 5 ≥ 3? ✅ → count = 3  

```java
if (count >= 3) → 3 >= 3? ✅
```
→ ✅ Return **3**

---

### ✅ Final Output:
```java
return 3;
```

---

### 🧩 Summary:
- You loop from the max possible h-index down to 0.
- For each value `i`, you count how many papers have `≥ i` citations.
- The first time `count >= i`, you return `i` as the h-index.

