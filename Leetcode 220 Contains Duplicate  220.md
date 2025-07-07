Contains Duplicate III

To explain the **"Contains Duplicate III"** problem to someone else, you can break it down like this:

---

### 🧩 Problem Summary

You're given:
- An integer array `nums`
- Two integers: `indexDiff` and `valueDiff`

You need to determine if there exist two distinct indices `i` and `j` in the array such that:

1. `i != j`
2. `|i - j| <= indexDiff` → the indices are close
3. `|nums[i] - nums[j]| <= valueDiff` → the values are close

If such a pair exists, return `true`; otherwise, return `false`.

---

### 📌 Example

**Input:**  
`nums = [1, 2, 3, 1]`, `indexDiff = 3`, `valueDiff = 0`  
**Output:** `true`  
**Why?**  
- Choose `i = 0`, `j = 3`
- `|0 - 3| = 3 <= 3` ✅  
- `|1 - 1| = 0 <= 0` ✅  
- So the pair `(0, 3)` satisfies all conditions.

---

### 🧠 How to Think About It

This is a **sliding window + value proximity** problem:
- You’re looking for **duplicates or near-duplicates** within a **window of size `indexDiff`**.
- But not just exact duplicates—values that are **within `valueDiff`** of each other.

---

### 🛠️ Real-World Analogy

Imagine you're monitoring stock prices over time:
- You want to know if **any two prices within a few days (`indexDiff`)** are **close enough in value (`valueDiff`)** to trigger a trade.
- This problem helps you detect such opportunities efficiently.

---
Let’s walk through **Example 1** from the problem step by step:

---

### 🔍 Example Input

```text
nums = [1, 2, 3, 1]
indexDiff = 3
valueDiff = 0
```

We need to find two indices `i` and `j` such that:

- `i != j`
- `|i - j| <= 3`
- `|nums[i] - nums[j]| <= 0`

---

### 🧮 Step-by-Step Walkthrough

We’ll use a **sliding window** of size at most `indexDiff = 3`.

#### Step 1: i = 0
- Window: `[1]`
- No previous elements to compare with.

#### Step 2: i = 1
- Window: `[1, 2]`
- Compare `nums[1] = 2` with `nums[0] = 1`
  - `|1 - 0| = 1 <= 3` ✅
  - `|2 - 1| = 1 > 0` ❌ → Not valid

#### Step 3: i = 2
- Window: `[1, 2, 3]`
- Compare `nums[2] = 3` with:
  - `nums[0] = 1` → `|3 - 1| = 2 > 0` ❌
  - `nums[1] = 2` → `|3 - 2| = 1 > 0` ❌

#### Step 4: i = 3
- Window: `[1, 2, 3, 1]`
- Compare `nums[3] = 1` with:
  - `nums[0] = 1` → `|3 - 0| = 3 <= 3` ✅ and `|1 - 1| = 0 <= 0` ✅

✅ **Match found!** Return `true`.

---

### ✅ Final Output

```text
true
```

---

The line:

```java
if (valueDiff < 0) {
    return false;
}
```

is a **defensive check** to ensure the input is valid. Here's why it's important:

---

### 🧠 Why This Check Matters

- The problem constraint is:  
  `0 <= valueDiff <= 10^9`

- So **valueDiff should never be negative**. But this check ensures that **if a negative valueDiff is passed accidentally**, the function will safely return `false` instead of behaving unpredictably.

- It also prevents issues in the **bucket-based approach**, where we calculate:

  ```java
  long size = (long) valueDiff + 1;
  ```

  If `valueDiff` were negative, `size` could become zero or invalid, leading to a **division by zero** when computing `bucketId = num / size`.

---

### ✅ Summary

This line is a **safety guard**:
- It ensures the function behaves correctly even if the input is invalid.
- It prevents runtime errors like division by zero.

Great question! Let's break down this line from your code:

```java
Map<Long, Long> map = new HashMap<>();
long size = (long) valueDiff + 1;
```

---

### 🧠 What This Does

#### 1. `Map<Long, Long> map = new HashMap<>();`
- This creates a **HashMap** to store the **bucket ID** as the key and the **number** as the value.
- We use `Long` instead of `Integer` to avoid overflow when dealing with large values (since `nums[i]` can be up to ±10⁹).

#### 2. `long size = (long) valueDiff + 1;`
- This defines the **size of each bucket**.
- Why `+1`? Because we want to ensure that **any two numbers in the same bucket differ by at most `valueDiff`**.
- For example, if `valueDiff = 3`, then:
  - Bucket 0 contains numbers from `0` to `3`
  - Bucket 1 contains numbers from `4` to `7`
  - And so on...

This way, if two numbers fall into the **same bucket**, they are guaranteed to be within `valueDiff` of each other.

---

### 📦 Why Buckets?

The idea is to **group numbers into buckets** so that:
- If two numbers fall into the same bucket → they’re close in value ✅
- If they fall into **neighboring buckets**, we still check them because they might be close enough (e.g., one at the end of one bucket and one at the start of the next)

---
Let’s do a **dry run** of this loop:

```java
for (int i = 0; i < nums.length; i++) {
    long num = (long) nums[i];
    long bucketId = num / size;
    if (num < 0) bucketId--;
}
```

We’ll use the example:

```java
nums = [1, 5, 9, 1, 5, 9]
indexDiff = 2
valueDiff = 3
```

So:

- `size = valueDiff + 1 = 4`
- Buckets will each span a range of 4 values:  
  Bucket 0 → [0, 3], Bucket 1 → [4, 7], Bucket 2 → [8, 11], etc.

---

### 🔎 Dry Run Table

| i | nums[i] | num (long) | bucketId = num / 4 | Adjusted bucketId (if num < 0) |
|---|---------|------------|---------------------|-------------------------------|
| 0 | 1       | 1          | 0                   | 0                             |
| 1 | 5       | 5          | 1                   | 1                             |
| 2 | 9       | 9          | 2                   | 2                             |
| 3 | 1       | 1          | 0                   | 0                             |
| 4 | 5       | 5          | 1                   | 1                             |
| 5 | 9       | 9          | 2                   | 2                             |

---

### 🧠 Key Insight

- The `bucketId` helps group numbers that are close in value.
- If two numbers fall into the **same bucket**, they are guaranteed to be within `valueDiff`.
- If they fall into **neighboring buckets**, we still check them because they might be close enough.

Let’s walk through this block of code with a **dry run** and explain what each part does:

```java
if (num < 0) {
    bucketId--;
}

if (map.containsKey(bucketId)) {
    return true;
}

if (map.containsKey(bucketId - 1) && Math.abs(num - map.get(bucketId - 1)) <= valueDiff) {
    return true;
}

if (map.containsKey(bucketId + 1) && Math.abs(num - map.get(bucketId + 1)) <= valueDiff) {
    return true;
}
```

---

### 🧠 Purpose of Each Line

#### 1. `if (num < 0) bucketId--;`
- This ensures that **negative numbers** are placed in the correct bucket.
- Without this, `-1 / size` and `0 / size` would both go to bucket `0`, which is incorrect.

#### 2. `if (map.containsKey(bucketId)) return true;`
- If the current number falls into a bucket that already has a number, then:
  - The difference between the two numbers is ≤ `valueDiff` (because bucket size = `valueDiff + 1`)
  - And if they’re within `indexDiff` (handled by sliding window), we return `true`.

#### 3. `if (map.containsKey(bucketId - 1) && ...)`
- Check the **left neighbor bucket**.
- Even if two numbers fall into adjacent buckets, they might still be within `valueDiff`.
- So we check if the number in the left bucket is close enough.

#### 4. `if (map.containsKey(bucketId + 1) && ...)`
- Same as above, but for the **right neighbor bucket**.

---

### 🧪 Dry Run Example

Let’s use:

```java
nums = [1, 5, 9, 1]
indexDiff = 3
valueDiff = 3
```

So:
- `size = 4`
- Buckets:  
  - Bucket 0: [0–3]  
  - Bucket 1: [4–7]  
  - Bucket 2: [8–11]

#### Step-by-step:

| i | num | bucketId | map contents | Action |
|---|-----|----------|--------------|--------|
| 0 | 1   | 0        | {}           | Add 1 to bucket 0 |
| 1 | 5   | 1        | {0:1}        | Add 5 to bucket 1 |
| 2 | 9   | 2        | {0:1, 1:5}    | Add 9 to bucket 2 |
| 3 | 1   | 0        | {0:1, 1:5, 2:9} | ✅ Bucket 0 already has 1 → return `true` |

---

Let’s walk through the final part of your bucket-based sliding window solution:

```java
map.put(bucketId, num);

if (i >= indexDiff) {
    long oldBucketId = (long) nums[i - indexDiff] / size;
    if (nums[i - indexDiff] < 0) {
        oldBucketId--;
    }
    map.remove(oldBucketId);
}
```

---

### 🧠 Purpose of This Block

This is where you **maintain the sliding window of size `indexDiff`** by removing old elements that are no longer within the allowed index range.

---

### 🔍 Step-by-Step Explanation

1. **`map.put(bucketId, num);`**
   - After checking for nearby almost duplicates, we add the current number to its bucket.

2. **`if (i >= indexDiff)`**
   - Once the window exceeds `indexDiff`, we remove the number that is now too far away (i.e., `i - indexDiff`).

3. **`long oldBucketId = (long) nums[i - indexDiff] / size;`**
   - We compute the bucket ID of the number that’s sliding out of the window.

4. **`if (nums[i - indexDiff] < 0) oldBucketId--;`**
   - Adjust for negative numbers to ensure correct bucket placement.

5. **`map.remove(oldBucketId);`**
   - Remove the outdated number from the map to keep the window size valid.

---

### 🧪 Example

Let’s say:

```java
nums = [1, 5, 9, 1]
indexDiff = 2
valueDiff = 3
```

- `size = 4`
- At `i = 3`, we remove the number at `i - indexDiff = 1` → `nums[1] = 5`
- `bucketId = 5 / 4 = 1`
- So we remove bucket `1` from the map

This ensures that we’re only comparing numbers within the last `indexDiff` indices.

---
Let’s do a **full dry run** of your bucket-based sliding window code using the input:

```java
nums = [1, 2, 3, 1]
indexDiff = 3
valueDiff = 0
```

---

### 🧮 Setup

- `size = valueDiff + 1 = 1`
- Buckets will each hold **exactly one value**, since `valueDiff = 0`
- So:  
  - Bucket 1 → [1]  
  - Bucket 2 → [2]  
  - Bucket 3 → [3]  
  - etc.

---

### 🔄 Dry Run Table

| i | nums[i] | num | bucketId | map (before) | Action |
|---|---------|-----|----------|--------------|--------|
| 0 | 1       | 1   | 1        | {}           | Add 1 to bucket 1 |
| 1 | 2       | 2   | 2        | {1:1}        | No match, add 2 to bucket 2 |
| 2 | 3       | 3   | 3        | {1:1, 2:2}   | No match, add 3 to bucket 3 |
| 3 | 1       | 1   | 1        | {1:1, 2:2, 3:3} | ✅ Bucket 1 already has 1 → return `true` |

---

### ✅ Output

```java
true
```

---

### 🧠 Why It Works

At `i = 3`, we find that `nums[3] = 1` falls into the **same bucket** as `nums[0] = 1`, and since:
- `|3 - 0| = 3 <= indexDiff`
- `|1 - 1| = 0 <= valueDiff`

All conditions are satisfied, so the function returns `true`.

