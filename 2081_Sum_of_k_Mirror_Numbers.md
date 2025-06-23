

---

```markdown
# K-Mirror Number Finder (Java)

This project implements a solution for finding the sum of the first `n` **k-mirror numbers**—numbers that are palindromic in both base-10 and a given base `k` (where 2 ≤ k ≤ 9). The solution uses a depth-first search (DFS) strategy to generate palindromic numbers in base-k and then validates if their corresponding base-10 number is also a palindrome.

## Problem Overview

A **k-mirror number** is defined as a positive integer (without leading zeros) that is a palindrome in:
- **Base-10 (decimal)**
- **Base-k** (for a given k with 2 ≤ k ≤ 9)

### Example

For example, when `k = 2` and `n = 5`, the 5 smallest 2-mirror numbers are:

- **1 (base-10),** which is `"1"` in base-2.
- **3 (base-10),** which is `"11"` in base-2.
- **5 (base-10),** which is `"101"` in base-2.
- **7 (base-10),** which is `"111"` in base-2.
- **9 (base-10),** which is `"1001"` in base-2.

Thus, the sum is:
```

1 + 3 + 5 + 7 + 9 = 25

````

## Approach

The solution flips the usual process:
1. **Generate Palindromic Strings in Base-k:**  
   Use DFS to generate palindromic candidates in base-k. This minimizes the search space by only considering numbers that are palindromic in the given base.
   
2. **Convert and Validate:**  
   For each generated candidate (as a character array), convert it from base-k to its base-10 integer. Then, check if this integer is a palindrome in base-10.

3. **Collect Results:**  
   Continue the process for increasing digit lengths until `n` valid k-mirror numbers are found, summing them up as they are validated.

## Dry Run Example

Let's walk through a dry run for `k = 2` and `n = 5` with the DFS method. The DFS starts with palindromes of increasing length.

### Step 1: One-digit Palindromes (`d = 1`)
- Generate `["1"]`
- Convert `"1"` in base-2 → 1 in base-10 (palindrome? Yes)  
  **Sum = 1, Remaining = 4**

### Step 2: Two-digit Palindromes (`d = 2`)
- Generate `["1","1"]` forming `"11"`
- Convert `"11"` in base-2 → 3 in base-10 (palindrome? Yes)  
  **Sum = 1 + 3 = 4, Remaining = 3**

### Step 3: Three-digit Palindromes (`d = 3`)
- Generate candidates:
  - `"101"` → base-2 → 5 in base-10 (palindrome? Yes)  
    **Sum = 4 + 5 = 9, Remaining = 2**
  - `"111"` → base-2 → 7 in base-10 (palindrome? Yes)  
    **Sum = 9 + 7 = 16, Remaining = 1**

### Step 4: Four-digit Palindromes (`d = 4`)
- Generate `"1001"` → base-2 → 9 in base-10 (palindrome? Yes)  
  **Sum = 16 + 9 = 25, Remaining = 0**

The process stops once we have found 5 valid k-mirror numbers. The final sum is **25**.

## Code

Below is the complete Java implementation.

```java
public class KMirrorNumber {

    private long remaining;
    private long sum = 0;

    // Entry method to find the sum of the first n k-mirror numbers.
    public long kMirror(int k, int n) {
        remaining = n;
        // Start with palindromes of increasing lengths.
        for (int d = 1; remaining > 0; d++) {
            char[] s = new char[d];
            dfs(k, d, s, 0, d - 1);
        }
        return sum;
    }

    // DFS to generate palindromes of length d in base-k.
    private void dfs(int k, int d, char[] s, int i, int j) {
        if (remaining == 0) return;  // Early stop if we've found enough numbers.
        if (i > j) {
            long val = convertAndValidate(s, k);
            if (val > 0) {
                sum += val;
            }
            return;
        }
        // Prevent leading zeros: if i==0, start x from 1.
        int start = (i == 0) ? 1 : 0;
        for (int x = start; x < k; x++) {
            char digit = (char) ('0' + x);
            s[i] = digit;
            s[j] = digit;
            dfs(k, d, s, i + 1, j - 1);
        }
    }

    // Convert the char[] (representing a base-k number) to decimal and check for palindrome property.
    private long convertAndValidate(char[] s, int k) {
        long num = 0, base = 1;
        for (int i = s.length - 1; i >= 0; i--) {
            num += (s[i] - '0') * base;
            base *= k;
        }
        if (isPalindrome(Long.toString(num))) {
            remaining--;
            return num;
        }
        return 0;
    }

    // Utility method to check if a string is a palindrome.
    private boolean isPalindrome(String s) {
        int l = 0, r = s.length() - 1;
        while (l < r) {
            if (s.charAt(l) != s.charAt(r)) return false;
            l++;
            r--;
        }
        return true;
    }

    // Main method to test the code.
    public static void main(String[] args) {
        KMirrorNumber solver = new KMirrorNumber();
        int k = 2;
        int n = 5;
        System.out.println("Sum of first " + n + " " + k + "-mirror numbers: " + solver.kMirror(k, n));
    }
}
````

## How to Run

1. **Compile the Code:**

   ```bash
   javac KMirrorNumber.java
   ```

2. **Run the Program:**

   ```bash
   java KMirrorNumber
   ```

When run, the program will print the sum of the first `n` k-mirror numbers for the given base `k`. For `k = 2` and `n = 5`, the output will be:

```
Sum of first 5 2-mirror numbers: 25
```

## Conclusion

This project demonstrates an efficient recursive solution to generate and validate k-mirror numbers by leveraging DFS and careful base conversion. It's an excellent exercise in algorithm design, recursion, and number theory. Feel free to explore and extend the code, add more test cases, or even implement additional features!

Happy coding!

```

---


```
