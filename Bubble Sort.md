---

## 📚 Bubble Sort Explanation (In Simple Java Terms):

### What is Bubble Sort?

Bubble Sort is a **simple comparison-based sorting algorithm**.
It works by **repeatedly swapping adjacent elements if they are in the wrong order**.

---

### How Bubble Sort Works:

* Imagine you have an array:
  `[5, 1, 4, 2, 8]`

* It compares **each pair of adjacent elements** and **swaps them if needed**.

* After the first full pass, the **largest element will "bubble up" to the end**.

* This process **repeats**, ignoring the sorted part at the end each time.

---

### Dry Run Example:

For array `[5, 1, 4, 2, 8]`

**Pass 1:**

```
Compare 5 and 1 → Swap → [1, 5, 4, 2, 8]
Compare 5 and 4 → Swap → [1, 4, 5, 2, 8]
Compare 5 and 2 → Swap → [1, 4, 2, 5, 8]
Compare 5 and 8 → No Swap → [1, 4, 2, 5, 8]
```

(Largest element 8 reached end.)

**Pass 2:**

```
Compare 1 and 4 → No Swap → [1, 4, 2, 5, 8]
Compare 4 and 2 → Swap → [1, 2, 4, 5, 8]
Compare 4 and 5 → No Swap → [1, 2, 4, 5, 8]
```

**Pass 3:**

```
Compare 1 and 2 → No Swap → [1, 2, 4, 5, 8]
Compare 2 and 4 → No Swap → [1, 2, 4, 5, 8]
```

Array is sorted!

---

## ✅ Java Code for Bubble Sort:

```java
public class BubbleSortExample {
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;

        // Outer loop for passes
        for (int i = 0; i < n - 1; i++) {
            swapped = false;

            // Inner loop for pairwise comparison
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j + 1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;

                    swapped = true;
                }
            }

            // Optimization: If no swaps done, array is already sorted
            if (!swapped) {
                break;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 1, 4, 2, 8};

        System.out.println("Original Array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }

        bubbleSort(arr);

        System.out.println("\nSorted Array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

### ✅ Output:

```
Original Array:
5 1 4 2 8
Sorted Array:
1 2 4 5 8
```

---

### ✅ Time Complexity:

* Worst Case: **O(n²)**
* Best Case (already sorted): **O(n)**
* Space Complexity: **O(1)** (in-place)

---

