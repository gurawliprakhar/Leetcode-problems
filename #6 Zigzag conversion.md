

---

### 🪄 Imagine You're Writing in Waves

You're given a word like **"PAYPALISHIRING"** and asked to write it in a zigzag pattern with a certain number of rows. That means:

1. You write letters going **down** the rows.
2. Then you write letters going **diagonally up**.
3. Repeat this down-and-up pattern until all letters are placed.

For example, if you’re told to use **3 rows**, it looks like:

```
Row 1: P   A   H   N  
Row 2: A P L S I I G  
Row 3: Y   I   R  
```

Once the zigzag is complete, you read each row from **left to right** and combine all the letters to get a new string:

👉 `"PAHNAPLSIIGYIR"`

---

### 🎯 So What Do You Have to Do?

Write a program that:
- Takes the original string and number of rows.
- Builds this zigzag pattern.
- Returns the final string by reading row-by-row.

---

Let’s walk through a **step-by-step example** for the string `"PAYPALISHIRING"` with `numRows = 4`, and show how the zigzag pattern builds up:

---

### 🧮 Initial Setup
We’ll create 4 empty rows like this:

```
Row 0: ""
Row 1: ""
Row 2: ""
Row 3: ""
```

We then go **down** from Row 0 to Row 3, then **up diagonally** back to Row 0, and repeat.

---

### 🔁 Character by Character

Let’s process each character in `"PAYPALISHIRING"`:

| Step | Char | Row | Direction | Rows After Update                  |
|------|------|-----|-----------|------------------------------------|
| 1    | P    | 0   | down      | "P" "" "" ""                        |
| 2    | A    | 1   | down      | "P" "A" "" ""                       |
| 3    | Y    | 2   | down      | "P" "A" "Y" ""                      |
| 4    | P    | 3   | down      | "P" "A" "Y" "P"                     |
| 5    | A    | 2   | up        | "P" "A" "YA" "P"                    |
| 6    | L    | 1   | up        | "P" "AL" "YA" "P"                   |
| 7    | I    | 0   | up        | "PI" "AL" "YA" "P"                  |
| 8    | S    | 1   | down      | "PI" "ALS" "YA" "P"                 |
| 9    | H    | 2   | down      | "PI" "ALS" "YAH" "P"                |
|10    | I    | 3   | down      | "PI" "ALS" "YAH" "PI"               |
|11    | R    | 2   | up        | "PI" "ALS" "YAHR" "PI"              |
|12    | I    | 1   | up        | "PI" "ALSI" "YAHR" "PI"             |
|13    | N    | 0   | up        | "PIN" "ALSI" "YAHR" "PI"            |
|14    | G    | 1   | down      | "PIN" "ALSIG" "YAHR" "PI"           |

---

### 📦 Final Output
Now, we read rows line by line:

- Row 0: `"PIN"`
- Row 1: `"ALSIG"`
- Row 2: `"YAHR"`
- Row 3: `"PI"`

➡️ Concatenate: **"PINALSIGYAHRPI"**

---



# Code
```java []
class Solution {
    public String convert(String s, int numRows) {
        //if only one row, zigzag doesnt apply
        if (numRows == 1) {
            return s;
        }

        //use min b/w string length and numsrows to 
        //avoid empty rows
        int len = Math.min(s.length(), numRows);
        String[] rows = new String[len];

        //intilaise empty rows to empty string 
        for (int i = 0; i < len; i++) {
            rows[i] = "";
        }

        int loc = 0;// track curent row index
        boolean down = false; //dirn true = down, false = up
        // Dry-run example for s = "PAYPALISHIRING", numRows = 3:
        // Zigzag Flow:
        // Row 0: P     A     H     N
        // Row 1: A  P  L  S  I  I  G
        // Row 2: Y     I     R
        for (int i = 0; i < s.length(); i++) {
            //append cur character to its row
            rows[loc] += s.substring(i, i + 1);

            //change the dirn if we are at the top or buttom
            if (loc == 0 || loc == numRows - 1) {
                down = !down;
            }

            //move next row based on the dirn
            if (down) {
                loc = loc + 1;
            } else {
                loc = loc - 1;
            }
             // Dry-run trace:
            // i=0, char=P → Row 0: "P"
            // i=1, char=A → Row 1: "A"
            // i=2, char=Y → Row 2: "Y"
            // i=3, char=P → Row 1: "AP"
            // i=4, char=A → Row 0: "PA"
            // i=5, char=L → Row 1: "APL"
            // ...
        }
        //combine all rows to produce final zigzag string
        String ans = "";
        for (String row : rows) {
            ans += row;
        }
        return ans;
    }
}
```
