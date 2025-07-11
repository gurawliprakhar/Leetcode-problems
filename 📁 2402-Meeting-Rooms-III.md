

---


````md
# 🧠 Leetcode 2402 - Meeting Rooms III

### 🚀 Problem Statement

You are given an integer `n`, representing `n` meeting rooms numbered from `0` to `n - 1`, and an array `meetings` where `meetings[i] = [start_i, end_i]` represents the start and end time of the i-th meeting.

You must assign each meeting to a room such that:

1. **Lowest-numbered Room First**: If multiple rooms are available, choose the one with the lowest index.
2. **Delayed if Needed**: If no rooms are available at the meeting's start time, delay it until a room becomes available.
3. **Keep Original Duration**: Delayed meetings retain their original duration.
4. **Respect Arrival Order**: Meetings are assigned in the order of their original start times.

**Return** the number of the room that hosted the most meetings. If there's a tie, return the room with the smallest number.

---

### 🎬 Story: *The Battle of the Boardrooms*

At LogicWorks Ltd., there's chaos in the corridors.

- Rooms are always in demand.
- Meetings are queued up.
- Room 0 is the most wanted.

The rules are strict. The battle? Fair. The challenge? Real-time room assignment based on when rooms become free and who arrived first.

Who will emerge as the **busiest room**?

---

### 🧾 Input

```java
int n = 2;
int[][] meetings = {
    {0, 10},
    {1, 5},
    {2, 7},
    {3, 4}
};
````

---

### 🔍 Step-by-Step Example Walkthrough

1. `{0,10}` → Room 0 is free → Assign it
2. `{1,5}`  → Room 1 is free → Assign it
3. `{2,7}`  → All rooms busy → Wait until Room 1 frees at 5 → Schedule as `{5,10}`
4. `{3,4}`  → Still busy → Wait until Room 0 frees at 10 → Schedule as `{10,11}`

**Result**:

* Room 0 handled: `[0,10]` and `[10,11]` → 2 meetings
* Room 1 handled: `[1,5]` and `[5,10]` → 2 meetings

🎯 **Output**: `0` (lowest-indexed in case of tie)

---

### 🧪 Dry Run Example

```java
n = 3;
meetings = {
    {0, 10},
    {1, 5},
    {2, 7},
    {3, 4}
};
```

#### Initial State:

* Rooms: 0, 1, 2 → all available at time 0
* Meeting Queue: Sorted by start time

#### Scheduling:

1. `{0,10}` → Room 0 → endTime = 10 → count\[0]++
2. `{1,5}` → Room 1 → endTime = 5 → count\[1]++
3. `{2,7}` → Room 2 → endTime = 7 → count\[2]++
4. `{3,4}` → All busy → Room 1 frees at 5

   * Delay meeting to start at 5 → end at 6
   * count\[1]++

Final `count = [1, 2, 1]` → **Room 1 wins**

🟢 **Output**: `1`

---

### 🧑‍💻 Java Code

```java
class Solution {
    class Node {
        int roomIndex;
        long endTime;

        Node (int roomIndex, long endTime) {
            this.roomIndex = roomIndex;
            this.endTime = endTime;
        } 
    }

    public int mostBooked(int n, int[][] meetings) {
        int[] count = new int[n];
        Arrays.sort(meetings, (a, b) -> a[0] - b[0]);

        Node[] ar = new Node[n];
        for (int i = 0; i < n; i++) {
            ar[i] = new Node(i, 0);
        }

        for (int[] m : meetings) {
            int start = m[0];
            int end = m[1];

            Arrays.sort(ar, (a, b) -> {
                if (a.endTime <= start && b.endTime <= start) {
                    return a.roomIndex - b.roomIndex;
                } else {
                    if (a.endTime != b.endTime) {
                        return Long.compare(a.endTime, b.endTime); 
                    } else {
                        return a.roomIndex - b.roomIndex; 
                    }
                }
            });

            if (ar[0].endTime > start) {
                ar[0].endTime += (long) (end - start);
                count[ar[0].roomIndex]++;
            } else {
                ar[0].endTime = (long) end;
                count[ar[0].roomIndex]++;
            }
        }

        int max = 0;
        for (int i : count) {
            max = Math.max(max, i);
        }

        for (int i = 0; i < count.length; i++) {
            if (count[i] == max) {
                return i;
            }
        }
        return 0;
    } 
}
```

---

### 🔗 Solution Link

👉 [View Full Solution on Leetcode](https://leetcode.com/problems/meeting-rooms-iii/solutions/6945110/meeting-rooms-iii-by-triprakhar-70od/)

---

### 🧠 Tags

* Greedy
* Simulation
* Sorting
* Priority Logic
* Room Scheduling

---

### 🧑‍💻 Author

Created with ❤️ by [@triprakhar](https://leetcode.com/triprakhar)

```

---


```
