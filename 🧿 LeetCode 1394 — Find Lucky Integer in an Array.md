Lucky Number Finder using Selection Sort in Java



---

### 🧩 Problem Explanation

**Objective:**  
You're given an array of integers. A **lucky integer** is defined as an integer whose **frequency in the array is equal to its value**. Your task is to **find the largest lucky integer** in the array. If no such integer exists, return `-1`.

---

### 📌 Example

**Input:**  
`arr = [1, 2, 2, 3, 3, 3]`  
**Explanation:**  
- `1` appears once → frequency = 1 ✅  
- `2` appears twice → frequency = 2 ✅  
- `3` appears three times → frequency = 3 ✅  
All are lucky, so return the **largest**, which is `3`.

**Input:**  
`arr = [2, 2, 2, 3, 3]`  
**Explanation:**  
- `2` appears 3 times → frequency ≠ 2 ❌  
- `3` appears 2 times → frequency ≠ 3 ❌  
No lucky integers → return `-1`.

---

### 🧠 How to Explain It Simply

> “We’re looking for numbers in the array that appear exactly as many times as their value. For example, if the number 3 appears exactly 3 times, it’s a lucky number. We want to find the biggest such number.”

---

### 🛠️ Constraints

- `1 <= arr.length <= 500`
- `1 <= arr[i] <= 500`

This means the array is small enough to use simple sorting and counting techniques.

---
Let's dry run your `swap` method with a simple example to see how it works step by step.

---

### 🔁 Method: `swap(int[] arr, int i, int j)`

```java
public static void swap(int[] arr, int i, int j) {
    if (i != j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

---

### 🧪 Dry Run Example

Let’s say:

```java
int[] arr = {5, 3, 8, 1};
swap(arr, 1, 3); // swap elements at index 1 and 3
```

#### Step-by-step:

- Initial array: `{5, 3, 8, 1}`
- `i = 1`, `j = 3`
- `arr[i] = 3`, `arr[j] = 1`

**Inside the method:**
1. `temp = arr[i]` → `temp = 3`
2. `arr[i] = arr[j]` → `arr[1] = 1`
3. `arr[j] = temp` → `arr[3] = 3`

**Resulting array:** `{5, 1, 8, 3}`

---

### ✅ Output

```java
Before swap: [5, 3, 8, 1]
After swap:  [5, 1, 8, 3]
```

 Let's dry run your `selectionSort` method step by step to understand how it works.

---

### 🧪 Dry Run Example

Let’s take this array:

```java
int[] arr = {5, 3, 8, 1};
```

---

### 🔁 Step-by-Step Execution

#### Initial array: `{5, 3, 8, 1}`

---

#### 🔹 Pass 1 (`i = 0`)
- `minIndex = 0` → value = 5
- Compare with `arr[1] = 3` → 3 < 5 → `minIndex = 1`
- Compare with `arr[2] = 8` → 8 > 3 → no change
- Compare with `arr[3] = 1` → 1 < 3 → `minIndex = 3`
- Swap `arr[0]` and `arr[3]` → `{1, 3, 8, 5}`

---

#### 🔹 Pass 2 (`i = 1`)
- `minIndex = 1` → value = 3
- Compare with `arr[2] = 8` → 8 > 3 → no change
- Compare with `arr[3] = 5` → 5 > 3 → no change
- Swap `arr[1]` and `arr[1]` → no change → `{1, 3, 8, 5}`

---

#### 🔹 Pass 3 (`i = 2`)
- `minIndex = 2` → value = 8
- Compare with `arr[3] = 5` → 5 < 8 → `minIndex = 3`
- Swap `arr[2]` and `arr[3]` → `{1, 3, 5, 8}`

---

### ✅ Final Sorted Array

```java
{1, 3, 5, 8}
```

---

### 🧠 Summary

- Selection Sort finds the minimum element in the unsorted part and swaps it with the current index.
- It’s **in-place** and easy to understand, but not the most efficient for large arrays (O(n²)).



 `max` method is a clean and correct manual implementation of `Math.max`. Here's a quick dry run to reinforce how it works:

---

### 🧪 Dry Run Example

```java
int result = max(7, 4);
```

### Step-by-step:
- `a = 7`, `b = 4`
- `a > b` → `7 > 4` → true
- So, `return a` → returns `7`

✅ Output: `7`

---

### 🧠 Summary

```java
public static int max(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}
```

- This method returns the greater of two integers.
- It behaves exactly like `Math.max(a, b)` but is written manually.
- You can use it anywhere in your code where you need to compare two values.

quick breakdown of what your code does, with comments and a dry run to reinforce your understanding:

---

### 🔁 Code Breakdown

```java
int maxLucky = -1;
int n = arr.length;
int i = 0;

while (i < n) {
    int j = i;
    while (j < n && arr[j] == arr[i]) {
        j++;
    }
    int count = j - i;
    if (count == arr[i]) {
        // You can use Math.max or your custom max function
        maxLucky = max(maxLucky, arr[i]);
    }
    i = j;
}
return maxLucky;
```

---

### 🧪 Dry Run Example

Let’s say `arr = {1, 2, 2, 3, 3, 3}` (already sorted):

- `i = 0`, `arr[i] = 1`
  - `j = 1`, `arr[0] == arr[1]`? No → `count = 1`
  - `count == arr[i]` → `1 == 1` ✅ → `maxLucky = max(-1, 1) = 1`

- `i = 1`, `arr[i] = 2`
  - `j = 3`, `count = 2`
  - `2 == 2` ✅ → `maxLucky = max(1, 2) = 2`

- `i = 3`, `arr[i] = 3`
  - `j = 6`, `count = 3`
  - `3 == 3` ✅ → `maxLucky = max(2, 3) = 3`

- `i = 6` → loop ends

✅ Final result: `3`

---

### 🧠 Notes

- You can use either `Math.max(maxLucky, arr[i])` or your own `max()` method.
- This loop assumes the array is **already sorted** — which you’ve handled earlier with `selectionSort`.



