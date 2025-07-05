
---

# 📘 Selection Sort in Java

## 📌 What is Selection Sort?

Selection Sort is a simple comparison-based sorting algorithm. It divides the input list into two parts: the sublist of items already sorted and the sublist of items remaining to be sorted. It repeatedly selects the smallest (or largest) element from the unsorted sublist, swapping it with the leftmost unsorted element.

---

## 🧠 Algorithm (Step-by-Step)

1. Start from the first element, assume it as the minimum.
2. Compare this minimum with the rest of the elements.
3. If a smaller element is found, set it as the new minimum.
4. Swap the new minimum with the first element.
5. Move to the next element and repeat until the list is sorted.

---

## 🧪 Dry Run

### Input:

```java
arr = [29, 10, 14, 37, 13]
```

### Iterations:

| Pass | Array State             | Minimum Found | Swap With |
| ---- | ----------------------- | ------------- | --------- |
| 1    | \[29, 10, 14, 37, 13]   | 10 (index 1)  | 29        |
|      | → \[10, 29, 14, 37, 13] |               |           |
| 2    | \[10, 29, 14, 37, 13]   | 13 (index 4)  | 29        |
|      | → \[10, 13, 14, 37, 29] |               |           |
| 3    | \[10, 13, 14, 37, 29]   | 14 (index 2)  | 14        |
|      | → \[10, 13, 14, 37, 29] | (no swap)     |           |
| 4    | \[10, 13, 14, 37, 29]   | 29 (index 4)  | 37        |
|      | → \[10, 13, 14, 29, 37] |               |           |

### Final Output:

```java
[10, 13, 14, 29, 37]
```

---

## 💻 Java Code

```java
public class SelectionSort {

    // Function to perform selection sort
    public static void selectionSort(int[] arr) {
        int n = arr.length;

        // One by one move the boundary of unsorted subarray
        for (int i = 0; i < n - 1; i++) {
            // Find the minimum element in the unsorted part
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            // Swap the found minimum with the first element
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }

    // Main method to test the sorting
    public static void main(String[] args) {
        int[] arr = {29, 10, 14, 37, 13};
        System.out.println("Before Sorting:");
        printArray(arr);

        selectionSort(arr);

        System.out.println("After Sorting:");
        printArray(arr);
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}
```

---

## 🧾 Time & Space Complexity

| Case    | Time Complexity |
| ------- | --------------- |
| Best    | O(n²)           |
| Average | O(n²)           |
| Worst   | O(n²)           |

* **Space Complexity**: O(1) (In-place sorting)
* **Stable**: ❌ (Not stable in general)
* **In-place**: ✅

---

## ✅ When to Use Selection Sort

* When memory space is a constraint
* When data size is small
* For learning purposes (due to simplicity)

---

