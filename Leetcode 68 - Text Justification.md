
---

### 📜 Problem Ka Summary:

Tere paas ek array `words[]` diya gaya hai—ismein alag-alag words hain. Saath hi `maxWidth` diya hai, jo batata hai ki har line mein max kitne characters allowed hain.

Tera kaam hai words ko lines mein **aise divide karna** ki:
- Har line exactly `maxWidth` characters ki ho.
- Line **fully justified** ho—matlab left aur right dono side se neatly aligned ho.

---

### 📋 Rules:

1. Har line mein **greedy approach se** jitne words fit ho sakte hain, utne daal (pehle line bhar, baad mein justify kar).
2. Line mein extra spaces ko words ke beech **evenly distribute** kar.
3. Agar spaces evenly divide nahi ho paate, toh **left wale gaps** ko extra spaces milega.
4. **Last line** hamesha **left justified** honi chahiye (matlab words ke beech extra spaces nahi, bas end mein spaces lagao).
5. Agar line mein **sirf ek word** hai, toh wo bhi left justified hoga.

---

### 📌 Example:

```java
words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16
```

#### Output:
```
"This    is    an"
"example  of text"
"justification.  "
```

🔹 Pehli line mein 3 words hain, 8 letters total, bacha 8 space → 4 spaces each between "This" and "is", and "is" and "an".

🔹 Last line ko left justified kiya gaya—words ke baad trailing spaces diye gaye.

---


# Code
```java []
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<>();
        List<String> line = new ArrayList<>();
        int len = 0;
        int i = 0;
        int n = words.length;
        
        while (i < n) {
            if (len + line.size() + words[i].length() > maxWidth) {
                int extraSpace = maxWidth - len;
                int slots = Math.max(1, line.size() - 1);
                int spaces = extraSpace / slots; 
                int remainder = extraSpace % slots;

                for (int j = 0; j < slots; j++) {
                    StringBuilder word = new StringBuilder(line.get(j));
                    word.append(" ".repeat(spaces));
                    if (remainder > 0) {
                        word.append(" ");
                        remainder--;
                    }
                    line.set(j, word.toString());
                }
                res.add(String.join("", line));
                line.clear();
                len = 0;
            }
            line.add(words[i]);
            len += words[i].length();
            i++;
        }

        String lastLine = String.join(" ", line);
        int trailSpace = maxWidth - lastLine.length();
        lastLine += " ".repeat(trailSpace);
        res.add(lastLine);
        return res;
    }
}
```
 iss Java code ka ek *rough* dry run karte hain— Hum line-by-line walk-through karenge jaise interview ya debugging mein karta banda apne dimaag mein karta hai 😄

---

### 🏁 Input
```java
words = ["This", "is", "an", "example", "of", "text", "justification."]
maxWidth = 16
```

---

### 📦 Dry Run Start

- `res = []`, `line = []`, `len = 0`, `i = 0`, `n = 7`

#### 🔄 First Iteration (i = 0)

- word = "This", length = 4  
- `len + line.size() + words[i].length()` = `0 + 0 + 4 = 4` < 16 → ✅  
- `line = ["This"]`, `len = 4`, `i++`

#### 🔄 Second Iteration (i = 1)

- word = "is", length = 2  
- current calc = `4 + 1 + 2 = 7` → ✅  
- `line = ["This", "is"]`, `len = 6`, `i++`

#### 🔄 Third Iteration (i = 2)

- word = "an", length = 2  
- current calc = `6 + 2 + 2 = 10` → ✅  
- `line = ["This", "is", "an"]`, `len = 8`, `i++`

#### 🔄 Fourth Iteration (i = 3)

- word = "example", length = 7  
- current calc = `8 + 3 + 7 = 18` → ❌  
**Too big ho gaya, ab line justify karni hai**

---

### ✍️ Justifying Line: ["This", "is", "an"]

- `extraSpace = 16 - 8 = 8`  
- `slots = line.size() - 1 = 2`  
- `spaces = 8 / 2 = 4`, `remainder = 0`

Apply 4 spaces after "This" and "is":

- `"This    "` + `"is    "` + `"an"`  
→ `"This    is    an"`

Add to result:  
`res = ["This    is    an"]`  
Reset: `line = []`, `len = 0`

---

#### 🔄 Continue Iteration (i = 3 again)

- word = "example", length = 7  
- fits → ✅  
- `line = ["example"]`, `len = 7`, `i++`

#### 🔄 i = 4 ("of", length = 2)

- calc = `7 + 1 + 2 = 10` → ✅  
- `line = ["example", "of"]`, `len = 9`, `i++`

#### 🔄 i = 5 ("text", length = 4)

- calc = `9 + 2 + 4 = 15` → ✅  
- `line = ["example", "of", "text"]`, `len = 13`, `i++`

#### 🔄 i = 6 ("justification.", length = 14)

- calc = `13 + 3 + 14 = 30` → ❌  
**Justify current line**

---

### ✍️ Justifying Line: ["example", "of", "text"]

- `extraSpace = 16 - 13 = 3`  
- `slots = 2`, `spaces = 1`, `remainder = 1`

Apply:

- `"example "` (1 space) + extra → `"example  "`  
- `"of "` + no extra → `"of "`  
- `"text"`

→ `"example  of text"`

Add to result:  
`res = ["This    is    an", "example  of text"]`  
Reset line

---

#### 🔄 Continue Iteration (i = 6)

- `"justification."` fits alone  
→ `line = ["justification."]`, `len = 14`, `i++`

---

### 🎯 Last Line Handling

- Join with space → `justification.`  
- `trailSpace = 16 - 14 = 2`  
→ `"justification.  "`  
Add to result:  
`res = ["This    is    an", "example  of text", "justification.  "]`

---

### ✅ Final Output

```java
[
  "This    is    an",
  "example  of text",
  "justification.  "
]
```

---

