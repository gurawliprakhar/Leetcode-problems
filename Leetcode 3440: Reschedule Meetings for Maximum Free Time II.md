

---

````markdown
# 🧠 Leetcode 3440: Reschedule Meetings for Maximum Free Time II

[![Leetcode Problem Link](https://img.shields.io/badge/Leetcode-3440-blue)](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-ii/)
[![Java](https://img.shields.io/badge/Language-Java-yellow.svg)](https://www.java.com)
[![Difficulty](https://img.shields.io/badge/Difficulty-Medium-orange.svg)]()

---

## 📘 Problem Statement

You're given an `eventTime` representing the duration of an event, and two arrays:
- `startTime[]`: start times of `n` meetings
- `endTime[]`: end times of `n` meetings

Each meeting:
- Is non-overlapping
- Must stay within `[0, eventTime]`
- Has fixed duration (can’t change duration)
- Can be **rescheduled once** (start time only) if it stays non-overlapping

### 🎯 Objective:
> Reschedule **at most one** meeting to **maximize the longest continuous free time block** within the event.

---

## 🧠 Approach: Greedy + Gap Tracking

The idea is to:
1. Identify all gaps between consecutive meetings (including before the first and after the last).
2. Find the **top 3 largest free gaps**.
3. For each meeting:
   - Check if it can fit in a larger gap (without overlap)
   - If yes, simulate the rescheduling
   - Calculate the **total free time** if the meeting is moved
4. Track and return the **maximum free time possible**.

---

## 📊 Example

```java
eventTime = 10
startTime = [0, 3, 7, 9]
endTime   = [1, 4, 8, 10]
````

Free time gaps:

* \[1,3] → 2
* \[4,7] → 3
* \[8,9] → 1

Rescheduling `[3,4]` to `[8,9]` frees up `[1,7]` → free time = `6`.

**✅ Output: 6**

---

## ✅ Java Solution

```java
class Solution {
    public int maxFreeTime(int eventTime, int[] startTime, int[] endTime) {
        int maxFree = 0;
        int n = startTime.length;

        int firstFree = -1, secondFree = -1, thirdFree = -1;
        int firstIndex = -1, secondIndex = -1;

        // Step 1: Find top 3 largest gaps
        for (int i = 0; i <= n; i++) {
            int freeTime = getFreeTime(eventTime, i, n, startTime, endTime);

            if (freeTime > firstFree) {
                thirdFree = secondFree;
                secondFree = firstFree;
                firstFree = freeTime;
                secondIndex = firstIndex;
                firstIndex = i;
            } else if (freeTime > secondFree) {
                thirdFree = secondFree;
                secondFree = freeTime;
                secondIndex = i;
            } else if (freeTime > thirdFree) {
                thirdFree = freeTime;
            }
        }

        // Step 2: Try moving each meeting into a larger free gap
        for (int i = 0; i < n; i++) {
            int duration = endTime[i] - startTime[i];
            int curFree;

            if ((i != firstIndex && i + 1 != firstIndex && duration <= firstFree) ||
                (i != secondIndex && i + 1 != secondIndex && duration <= secondFree) ||
                duration <= thirdFree) {
                curFree = getFreeTime(eventTime, i, n, startTime, endTime)
                        + getFreeTime(eventTime, i + 1, n, startTime, endTime)
                        + duration;
            } else {
                curFree = getFreeTime(eventTime, i, n, startTime, endTime)
                        + getFreeTime(eventTime, i + 1, n, startTime, endTime);
            }

            maxFree = Math.max(maxFree, curFree);
        }

        return maxFree;
    }

    // Utility to calculate the free gap between meetings
    public int getFreeTime(int eventTime, int index, int n, int[] startTime, int[] endTime) {
        int prevEnd = (index > 0) ? endTime[index - 1] : 0;
        int nextStart = (index < n) ? startTime[index] : eventTime;
        return nextStart - prevEnd;
    }
}
```

---

## 📈 Time & Space Complexity

| Metric | Complexity |
| ------ | ---------- |
| Time   | O(n)       |
| Space  | O(1)       |

* Efficient for large input sizes (`n <= 10^5`)
* No extra memory allocations

---

## 🧪 Test Cases

```java
Input: eventTime = 5, startTime = [1,3], endTime = [2,5]
Output: 2

Input: eventTime = 10, startTime = [0,7,9], endTime = [1,8,10]
Output: 7

Input: eventTime = 5, startTime = [0,1,2,3,4], endTime = [1,2,3,4,5]
Output: 0
```

---

## 🔗 Resources

* 🔍 [Leetcode Problem Link](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-ii/)
* 🧠 [My Leetcode Solution Post](https://leetcode.com/problems/reschedule-meetings-for-maximum-free-time-ii/solutions/6941743/max-free-time-after-rescheduling-one-mee-ig4h/)

---

## ✍️ Author

**Prakhar Tripathi**
Java | DSA | Full-Stack Learner
📺 YouTube Channel Coming Soon!
📬 DM me if you need help explaining this problem in a video.

---

Feel free to ⭐️ this repo if you found the explanation helpful!

```

---

Let me know if you'd like:
- This turned into a `GitHub Pages` blog
- A **thumbnail** or **banner** for the GitHub repo
- Code formatting for **Python**, **C++**, or other languages too.
```
