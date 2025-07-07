

---

### 🧾 Problem Statement in Easy Words

You are given a list of events.  
Each event has a **start day** and an **end day**, meaning you can attend that event on **any one day** between those two days (inclusive).

But there’s a rule:  
👉 You can only attend **one event per day**.

Your goal is to **attend as many events as possible** without overlapping days.

---

### 🧠 Example

If the input is:

```
events = [[1, 2], [2, 3], [3, 4]]
```

You can attend:
- First event on day 1
- Second event on day 2
- Third event on day 3

✅ So the answer is `3` — you attended all three events!

---



```java
Arrays.sort(events, (a, b) -> {
    if (a[1] == b[1]) {
        return a[0] - b[0]; // compare by start day if end dates are same
    } else {
        return a[1] - b[1]; // otherwise compare by end date
    }
});
```

### ✅ What It Does

1. **Primary sort**: by `a[1]` and `b[1]` → end date.
2. **Secondary sort** (tie-breaker): if end dates are equal, use `a[0]` and `b[0]` → start date.

### ✅ Meaning

> Sort events by **end time**. If two events have the same end time, sort by **start time**.

---

### 💡 Why is this useful?

This logic is commonly used in **interval scheduling** problems (like "Maximum number of non-overlapping events").

Sorting by end time helps **greedily select the event that finishes earliest**, leaving room for more events afterward.

---

### 🔍 Example Input

```java
int[][] events = {{1, 3}, {2, 3}, {3, 4}, {1, 2}};
```

### 🔄 After sorting:

Sorted by end time, then by start time:

```java
[[1, 2], [1, 3], [2, 3], [3, 4]]
```

---

Let’s dry run this part of your code:

```java
for (int[] event : events) {
    // Earliest day to try attending this event
    int start = event[0];
    int end = event[1];
    int day = lastTriedDay.getOrDefault(start, start);
```

---

### 🧪 Dry Run Example

Let’s say your input is:

```java
events = [[1, 2], [2, 3], [3, 4]]
```

And after sorting by end day, the array becomes:

```java
[[1, 2], [2, 3], [3, 4]]
```

Let’s walk through the first iteration:

---

#### 🔁 First Iteration (`event = [1, 2]`)
- `start = 1`
- `end = 2`
- `lastTriedDay` is empty, so:
  ```java
  day = lastTriedDay.getOrDefault(1, 1); // day = 1
  ```

Now the inner loop will try to attend the event on day 1 or 2.

---

#### 🔁 Second Iteration (`event = [2, 3]`)
- `start = 2`
- `end = 3`
- `lastTriedDay.getOrDefault(2, 2)` → returns 2

Try to attend on day 2 or 3.

---

#### 🔁 Third Iteration (`event = [3, 4]`)
- `start = 3`
- `end = 4`
- `lastTriedDay.getOrDefault(3, 3)` → returns 3

Try to attend on day 3 or 4.

---

### 🧠 Purpose of This Line

```java
int day = lastTriedDay.getOrDefault(start, start);
```

This ensures that if we’ve already tried attending an event starting on the same day before, we **don’t retry from the beginning**, but instead **continue from the last tried day**. It avoids redundant checks and improves efficiency.

Let’s dry run this part of your code:

```java
for (int i = day; i <= end; i++) {
    if (!usedDays.contains(i)) {
        usedDays.add(i);
        count++;

        // Update the latest attended day for this start day
        lastTriedDay.put(start, i);
        break;
    }
}
```

---

### 🧪 Dry Run Example

Let’s use this input:

```java
events = [[1, 2], [2, 3], [3, 4]]
```

After sorting by end day, the array remains:

```java
[[1, 2], [2, 3], [3, 4]]
```

We’ll track:
- `usedDays = {}` (initially empty)
- `lastTriedDay = {}` (initially empty)
- `count = 0`

---

#### 🔁 First Event: `[1, 2]`
- `start = 1`, `end = 2`
- `day = lastTriedDay.getOrDefault(1, 1) = 1`

Loop:
- `i = 1`: not in `usedDays`
  - Add 1 to `usedDays → {1}`
  - `count = 1`
  - `lastTriedDay.put(1, 1)`
  - ✅ Break

---

#### 🔁 Second Event: `[2, 3]`
- `start = 2`, `end = 3`
- `day = lastTriedDay.getOrDefault(2, 2) = 2`

Loop:
- `i = 2`: not in `usedDays`
  - Add 2 → `{1, 2}`
  - `count = 2`
  - `lastTriedDay.put(2, 2)`
  - ✅ Break

---

#### 🔁 Third Event: `[3, 4]`
- `start = 3`, `end = 4`
- `day = lastTriedDay.getOrDefault(3, 3) = 3`

Loop:
- `i = 3`: not in `usedDays`
  - Add 3 → `{1, 2, 3}`
  - `count = 3`
  - `lastTriedDay.put(3, 3)`
  - ✅ Break

---

### ✅ Final Result

- `usedDays = {1, 2, 3}`
- `count = 3`

So the function returns `3`, meaning you can attend all three events on days 1, 2, and 3.


