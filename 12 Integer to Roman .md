
### Roman Numeral Conversion using Greedy Algorithm

---

### 📘 Problem Statement

Convert an integer in the range `1` to `3999` into its Roman numeral representation. Roman numerals are composed using these seven base symbols:

| Symbol | Value |
|--------|-------|
| I      | 1     |
| V      | 5     |
| X      | 10    |
| L      | 50    |
| C      | 100   |
| D      | 500   |
| M      | 1000  |

---

### ⚙️ Approach: Greedy Mapping

The algorithm follows a greedy strategy:
1. Use a `LinkedHashMap` to preserve insertion order: values are stored from highest to lowest.
2. For each Roman value:
   - While the current number is ≥ value, append the symbol to the result and subtract the value.
3. Repeat until the input is reduced to 0.

---

### ✅ Special Subtractive Cases

These are required for correct Roman numeral formation:

| Decimal | Roman |
|--------:|:------|
| 4       | "IV"  |
| 9       | "IX"  |
| 40      | "XL"  |
| 90      | "XC"  |
| 400     | "CD"  |
| 900     | "CM"  |

---

### 🔧 Implementation (Java)
```java
class Solution {
    public String intToRoman(int num) {
        Map<Integer, String> map = new LinkedHashMap<>();
        map.put(1000, "M");
        map.put(900, "CM");
        map.put(500, "D");
        map.put(400, "CD");
        map.put(100, "C");
        map.put(90, "XC");
        map.put(50, "L");
        map.put(40, "XL");
        map.put(10, "X");
        map.put(9, "IX");
        map.put(5, "V");
        map.put(4, "IV");
        map.put(1, "I");

        StringBuilder sb = new StringBuilder();
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            while (num >= entry.getKey()) {
                sb.append(entry.getValue());
                num -= entry.getKey();
            }
        }
        return sb.toString();
    }
}
```

---

### 🧪 Dry Run Example: `num = 2949`

| Place     | Computation                | Roman |
|-----------|----------------------------|-------|
| Thousands | 2949 / 1000 = 2            | MM    |
| Hundreds  | (2949 % 1000) / 100 = 9    | CM    |
| Tens      | (2949 % 100) / 10 = 4      | XL    |
| Ones      | 2949 % 10 = 9              | IX    |

📦 Final Result: `"MMCMXLIX"`

---

### 🔍 Example: `num = 3888` → `"MMMDCCCLXXXVIII"`

---

