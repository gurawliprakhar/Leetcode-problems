

# Code
```java []
class Solution {
    public String reverseWords(String s) {
         // Step 1: Clean up the string by removing extra spaces
        char[] ch = removeExtraSpaces(s).toCharArray();
        reverse(ch, 0, ch.length - 1);

         // Dry Run Step 1:
        // Input: "  LeetCode   is  awesome  "
        // After removeExtraSpaces → "LeetCode is awesome"
        // ch = ['L','e','e','t','C','o','d','e',' ','i','s',' ','a','w','e','s','o','m','e']

        // Step 2: Reverse the entire character array

        // Dry Run Step 2:
        // After reverse → ['e','m','o','s','e','w','a',' ','s','i',' ','e','d','o','C','t','e','e','L']
        // Full reversed string → "emosewa si edoCteeL"

        // Step 3: Reverse each word in-place
        int i = 0;
        for (int j = 0; j <= ch.length; j++) {
            if (j == ch.length || ch[j] == ' ') {
                reverse(ch, i, j - 1);
                 // Dry Run Step 3 (Each iteration):
                // j = 7 → reverse(0,6) → "emosewa" → "awesome"
                // j = 10 → reverse(8,9) → "si" → "is"
                // j = 18 → reverse(11,17) → "edoCteeL" → "LeetCode"
                i = j + 1;
            }
        }
        // Final result → ['a','w','e','s','o','m','e',' ','i','s',' ','L','e','e','t','C','o','d','e']
        // Returns: "awesome is LeetCode"
        return new String(ch);
    }

    private String removeExtraSpaces(String s) {
        StringBuilder sb = new StringBuilder();
        int i = 0, n = s.length();

        while (i < n) {
            while (i < n && s.charAt(i) == ' ') {
                i++;
            }
            while (i < n && s.charAt(i) != ' ') {
                sb.append(s.charAt(i++));
            }
            while (i < n && s.charAt(i) == ' ') {
                i++;
            }
            if (i < n) {
                sb.append(' ');
            }
        }
        return sb.toString();
    }

    private void reverse(char[] ar, int i, int j) {
        while (i < j) {
            char temp = ar[i];
            ar[i] = ar[j];
            ar[j] = temp;
            i++;
            j--;
        }
    }
}
```
🎬 ****

🧠 **Problem:**  
You're given a sentence like `"  hello   world  "` and you need to:
- Remove extra spaces 🚫
- Reverse the word order 🔁
- Return the cleaned-up string ✅

⚙️ **Rules:**
- Words are made of non-space characters.
- Ignore leading/trailing/multiple spaces.
- Return words with **single spaces only**, in **reverse order**.

👨‍💻 **Example:**
```text
Input:  "  a good   example  "
Output: "example good a"
```

🎯 **Core Logic:**
1. Trim → Get rid of edges.
2. Split → Break into words by `\\s+`.
3. Reverse → Flip the array.
4. Join → Stitch with a single space.



 LeetCode 151 - Reverse Words in a String (Java)**  
📌 *Goal:* Flip the sentence `"  the sky  is  blue  "` to `"blue is sky the"` — clean spaces, reverse word order!

---

### 🚦 Step-by-step breakdown:

```java
public String reverseWords(String s)
```
- The main method that returns the transformed string ✅

```java
char[] ch = removeExtraSpaces(s).toCharArray();
```
- 🧹 *Clean it up!* This removes extra spaces and converts it to a char array so we can work in-place.

```java
reverse(ch, 0, ch.length - 1);
```
- 🔄 *Flip the entire array!* Now words are backwards but letters are too.

---

### 🔁 Word-by-word reversal:

```java
int i = 0;
for (int j = 0; j <= ch.length; j++) {
    if (j == ch.length || ch[j] == ' ') {
        reverse(ch, i, j - 1); // Flip each word back
        i = j + 1;             // Move to the next word
    }
}
```

- 🪄 Each word’s letters get flipped individually to restore proper order.

---

### 🧼 Space cleaner method:
```java
private String removeExtraSpaces(String s)
```
- 🚫 Removes leading/trailing/multiple spaces.
- Only **single space** between words is allowed — perfect for neat output.

---

### 🔧 Utility reverse method:
```java
private void reverse(char[] ar, int i, int j)
```
- Swaps characters from both ends — classic two-pointer move!

---

### ✅ Final Output
- `"  the sky  is  blue  "` ➡️ `"blue is sky the"`

---


---

### 🧼 **Goal:**  
Take a messy string like `"   Java    is   fun "` and clean it up to `"Java is fun"` — one space between words, no extras at the ends!

---

### 🚀 **Method Logic Step-by-Step**

```java
private String removeExtraSpaces(String s) {
    StringBuilder sb = new StringBuilder();   // To build the cleaned-up string
    int i = 0, n = s.length();
```
- 🔧 Start scanning the original string `s` from left to right.
- Use `StringBuilder` to construct the final clean string.

---

```java
while (i < n && s.charAt(i) == ' ') i++;
```
- ⏩ Skip all leading spaces before the first word.

---

```java
while (i < n && s.charAt(i) != ' ') {
    sb.append(s.charAt(i++));
}
```
- 📝 Copy characters of the current word into `sb`.

---

```java
while (i < n && s.charAt(i) == ' ') i++;
```
- 🧹 Skip spaces *after* the word — we only want one space between words, not many.

---

```java
if (i < n) sb.append(' ');
```
- 🚪 If there’s more to scan, drop a **single space** between this word and the next.

---

### 🔁 Repeat until the end of string  
Every loop iteration handles one word and ensures **just one space** follows — unless it’s the last word!

---

### 🔚 Final Output:
```java
return sb.toString();
```
- Returns the polished string — no gunk, no clutter 🎯

---

### 🧪 Example Trace:  
Input → `"   Java   is   fun "`  
After cleaning → `"Java is fun"`

---




---

### 🔧 **Purpose:**  
Flip a section of a character array — classic two-pointer trick to reverse words or the entire sentence!

---

### 🧠 **Function Signature:**
```java
private void reverse(char[] ar, int i, int j)
```
- `ar`: the char array you're working with 🔤
- `i`: starting index 🚩
- `j`: ending index 🏁

---

### 🌀 **What's Happening Inside?**
```java
while (i < j) {
    char temp = ar[i];
    ar[i] = ar[j];
    ar[j] = temp;
    i++;
    j--;
}
```
- 🔁 Swap characters from both ends → move inward toward the center.
- 🫴 `temp` temporarily holds the left character so you can flip positions safely.

---

### 📌 **Real-Life Analogy:**
Like flipping a word `"blue"` letter-by-letter:
`['b', 'l', 'u', 'e']` → `['e', 'u', 'l', 'b']`

Used twice in this problem:
1. To reverse the **entire array** first.
2. Then to reverse **each word** back to readable form.

---
*detailed dry run walkthrough** of your two-pointer string reversal code — 

---

### 🧩 Input:  
```text
"  LeetCode   is  awesome  "
```

---

## 🧼 Phase 1: `removeExtraSpaces()`

This function cleans up the messy input string to produce:
```text
"LeetCode is awesome"
```

**How?**  
We scan character-by-character and:
- Skip leading spaces  
- Copy each word  
- Skip in-between spaces  
- Add a single space only if another word follows

**Intermediate Steps (visual):**
```
i → 0 to skip leading spaces
sb = "LeetCode"
i → skip space(s)
sb = "LeetCode is"
i → skip space(s)
sb = "LeetCode is awesome"
```

🧠 Final result: `"LeetCode is awesome"`

---

## 🔁 Phase 2: Reverse Entire Char Array

Convert to char array:
```text
['L','e','e','t','C','o','d','e',' ','i','s',' ','a','w','e','s','o','m','e']
```

**After full reverse (0 to length-1):**
```text
['e','m','o','s','e','w','a',' ','s','i',' ','e','d','o','C','t','e','e','L']
```

🧠 Full string now: `"emosewa si edoCteeL"`

---

## 🔀 Phase 3: Reverse Each Word Back

We walk through word-by-word (separated by `' '`):

### Iteration 1: j = 0 → 6 → word: `"emosewa"`  
Reverses to → `"awesome"`

### Iteration 2: j = 8 → 9 → word: `"si"`  
Reverses to → `"is"`

### Iteration 3: j = 11 → 18 → word: `"edoCteeL"`  
Reverses to → `"LeetCode"`

**Final array:**
```text
['a','w','e','s','o','m','e',' ','i','s',' ','L','e','e','t','C','o','d','e']
```

✅ Final output: `"awesome is LeetCode"`

---

## 📜 Final Return:
```java
return new String(ch);
```

### 🏁 Output:
```text
"awesome is LeetCode"
```

---


