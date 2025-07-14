

# Convert Binary Number in a Linked List to Integer

---

### 📘 Problem Statement

You are given the `head` of a singly-linked list. Each node stores a binary digit (`0` or `1`), with the **most significant bit (MSB) at the head**. Your task is to convert the binary number represented by the list into its **decimal equivalent**.

---

### ✨ Example

```plaintext
Input: head = [1 → 0 → 1]
Binary: "101"
Output: 5
```

---

### 🧠 Explanation

Each binary digit corresponds to a power of 2, starting from the MSB:
- Position 0 → \(2^{n-1}\)
- Position 1 → \(2^{n-2}\)
- ...
- Last Position → \(2^0\)

For the list `[1 → 0 → 1]`:
- `1 × 2² + 0 × 2¹ + 1 × 2⁰ = 4 + 0 + 1 = 5`

---

### 💡 Solution Strategy

1. **Traversal:** Read each node from `head → tail`.
2. **Construction:** Build the binary string as you go.
3. **Conversion:** Use Java’s `Integer.parseInt(binaryStr, 2)` to convert to decimal.

This approach is clean and readable—ideal for constraints like ≤ 30 nodes.

---

### 🧾 Java Code

```java
class Solution {
    public int getDecimalValue(ListNode head) {
        StringBuilder sb = new StringBuilder();
        while (head != null) {
            sb.append(head.val); // Append binary digit
            head = head.next;
        }
        return Integer.parseInt(sb.toString(), 2); // Convert binary to decimal
    }
}
```

---

### 🔬 Dry Run: Input = [1 → 0 → 1]

#### 🔄 Linked List Traversal

| Step | `head.val` | `StringBuilder` |
|------|------------|------------------|
| 1    | 1          | "1"              |
| 2    | 0          | "10"             |
| 3    | 1          | "101"            |
| End  | null       | Done             |

#### 🔢 Conversion Step
```java
Integer.parseInt("101", 2) → 5
```

---

### ✅ Final Output: `5`

Binary `"101"` → Decimal `5`  
Perfect match with expected output!

---

