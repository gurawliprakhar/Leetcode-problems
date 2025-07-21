

---

### 🧩 Problem Ka Essence:
Aapko ek **sorted array `arr`** diya gaya hai aur do integers – `k` (kitne closest elements chahiye) aur `x` (reference point) diye gaye hain.

Aapko `arr` ke **aise `k` elements** chahiye jo `x` ke **sabse kareeb** hon. Aur jo final output hoga, woh bhi **ascending order** mein hona chahiye.

---

### 📏 “Closest” ka kya matlab hai?
- Agar `a` aur `b` do numbers hain:
  - `a` is closer to `x` than `b` if `|a - x| < |b - x|`
  - Agar `|a - x| == |b - x|`, toh chhoti value ko lena hai, i.e. `a < b`

---

### 🧠 Simple Example:
```
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```
Yahan `3` ke sabse kareeb 4 numbers chahiye: toh `[1,2,3,4]` sabse kareeb hain. `5` thoda door hai.

---

### 🔧 Approach Summary (Sliding Window via Binary Search):
- Kyunki array **already sorted hai**, aap directly **window size `k`** ka ek subarray dhund sakte ho jo `x` ke sabse kareeb ho.
- Aap `left` aur `right` pointers use karte ho aur binary search se yeh decide karte ho ki `k` length ka subarray kis position se start kare.

---

### 🧮 Kaise kaam karta hai:
1. `left = 0`, `right = arr.length - k`
2. Jab tak `left < right`:
   - Mid position find karo.
   - Compare karo: `x - arr[mid]` aur `arr[mid + k] - x`
   - Jahan `x` ke comparison mein subarray closer ho, wahin shift karo window.

3. Last mein `arr[left]` se `arr[left + k - 1]` tak ka subarray hi answer hoga.

---


# Code
```java []
class Solution {
    public List<Integer> findClosestElements(int[] arr, int k, int x) {
        int n = arr.length;
        int i = 0;
        int j = n - k;

        while(i < j) {
            int mid = (i + j)/ 2;

            if (x - arr[mid] > arr[mid +k] - x) {
                i = mid + 1;
            } else {
                j = mid;
            }
        }
        List<Integer> res = new ArrayList<>();
        for (int l = i; l < j + k; l++) {
            res.add(arr[l]);
        }
        return res;
    }
}
```


---

### 🧪 Example
**Input:**
```java
arr = [1, 2, 3, 4, 5]
k = 4
x = 3
```

---

### 🦾 Step-by-Step Execution

We’ll run the following loop to find the best window start index:

```java
int left = 0, right = arr.length - k; // right = 5 - 4 = 1
```

#### 🔁 First Iteration
- `mid = (0 + 1) / 2 = 0`
- Compare:
  - `x - arr[mid] = 3 - 1 = 2`
  - `arr[mid + k] - x = 5 - 3 = 2`
- Since both are equal, we shift `right = mid = 0`

👉 Now, `left = 0`, `right = 0`, loop ends.

---

### 🎯 Final Window
Take elements from `arr[0]` to `arr[0 + 4 - 1]`:
```java
[1, 2, 3, 4]
```

---

### ✅ Final Output
```java
return [1, 2, 3, 4];
```

---

