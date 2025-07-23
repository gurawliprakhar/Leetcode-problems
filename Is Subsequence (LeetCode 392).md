

```markdown
# Is Subsequence (LeetCode 392)

![LeetCode](https://img.shields.io/badge/LeetCode-392-blue)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-brightgreen)
![Language-Java](https://img.shields.io/badge/Language-Java-green)

---

## Problem Explanation (Hinglish)

Aapko do strings di gayi hain — **s** aur **t**.  
Aapko check karna hai ki kya string **s** string **t** ka subsequence hai ya nahi.

### Subsequence kya hota hai?  
Subsequence ka matlab hai, kisi string me se kuch characters delete kar ke (ya bina delete kiye),  
jo bachi hui string hai, uska order original string ke order ke saath match karta ho.

**Example:**  
- `"ace"` string **"abcde"** ka subsequence hai, kyunki `"a"`, `"c"`, `"e"` waise hi order me hain.  
- `"aec"` string **"abcde"** ka subsequence nahi hain, kyunki `"e"` `c` ke baad nahi hai original string me.

---

## Example Walkthrough

```
Input:
s = "abc"
t = "ahbgdc"

Output: true

Explanation:
'a' milta hai 'a' se
'b' milta hai 'b' se
'c' milta hai 'c' se
Order maintain hua, toh result true.
```

```
Input:
s = "axc"
t = "ahbgdc"

Output: false

Explanation:
'a' milta hai 'a' se
'x' nahi milta hai 'a' ke baad 't' me
Toh result false.
```

---

## Solution Approach: Two Pointer (Brute Force)

- Ek pointer `sIndex` string `s` ke liye, ek `tIndex` string `t` ke liye.
- Dono pointers start se chalein.
- `t` me se match karte hue `s` ke characters dhundho.
- Agar `s` ke saare characters mil gaye order ke saath, return true.
- Agar end tak nahi mile, return false.

---

## Code (Java) with Dry Run Comments

```
public boolean isSubsequence(String s, String t) {
    int sIndex = 0, tIndex = 0;  // Dono strings ke start pointers
    
    // Jab tak dono strings ke andar ho
    while (sIndex < s.length() && tIndex < t.length()) {
        if (s.charAt(sIndex) == t.charAt(tIndex)) {
            // Agar characters match to dono pointers aage badhao
            sIndex++;
            tIndex++;
        } else {
            // Agar match nahi to sirf tIndex badhao
            tIndex++;
        }
    }
    
    // Agar s ke saare characters mil gaye hain to sIndex == s.length() hoga
    return sIndex == s.length();
}
```

---

## Dry Run Example:

`s = "abc"`  
`t = "ahbgdc"`

| Step | sIndex (char) | tIndex (char) | Action                         |
|-------|---------------|---------------|--------------------------------|
| 1     | 0 ('a')       | 0 ('a')       | Match! Both pointers increment  |
| 2     | 1 ('b')       | 1 ('h')       | No Match! Increment tIndex only |
| 3     | 1 ('b')       | 2 ('b')       | Match! Both pointers increment  |
| 4     | 2 ('c')       | 3 ('g')       | No Match! Increment tIndex only |
| 5     | 2 ('c')       | 4 ('d')       | No Match! Increment tIndex only |
| 6     | 2 ('c')       | 5 ('c')       | Match! Both pointers increment  |
| End   | 3 (end)       | 6 (end)       | sIndex == s.length(), return true |

---

## Complexity

- **Time:** O(n), jahan n = length of string `t`  
- **Space:** O(1), constant extra space

---

## Follow-up Tip

Agar aapko **bohot zyada queries** ke liye baar-baar `s` strings check karne hain against same `t`,  
toh aap `t` pe pre-processing kar ke character indexes store kar sakte hain aur binary search se queries ko optimize kar sakte hain.

---

## Author

Happy Coding!  
If you liked this explanation, please ⭐ this repo and share!  
Feel free to open issues or suggest improvements.

```

