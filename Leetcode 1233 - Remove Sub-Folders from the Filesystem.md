

```markdown
# 🗂️ Leetcode 1233 - Remove Sub-Folders from the Filesystem

> Java solution with full explanation and dry run.

## 🔗 Problem Link

[Leetcode 1233 - Remove Sub-Folders from the Filesystem](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/solutions/6976216/leetcode-1233-remove-sub-folders-from-th-ivoq/)

---

## 🧾 Problem Statement

You are given a list of folder paths in a filesystem. Some folders may be **sub-folders** of others.

Your task is to **remove all sub-folders**, and return the remaining **top-level folders** only.

### 🧠 Definition

A folder `a` is a **sub-folder** of folder `b` if:
- It starts with `b + '/'`
- It has additional characters after that

### 📥 Example

```

Input:  \["/a", "/a/b", "/c/d", "/c/d/e", "/c/f"]
Output: \["/a", "/c/d", "/c/f"]

````

---

## ✅ Java Solution

```java
import java.util.*;

public class Solution {
    public List<String> removeSubfolders(String[] folder) {
        Set<String> folderSet = new HashSet<>(Arrays.asList(folder));
        List<String> res = new ArrayList<>();

        for (String f : folder) {
            boolean isSubfolder = false;

            for (int i = 1; i < f.length(); i++) {
                if (f.charAt(i) == '/' && folderSet.contains(f.substring(0, i))) {
                    isSubfolder = true;
                    break;
                }
            }

            if (!isSubfolder) {
                res.add(f);
            }
        }

        return res;
    }
}
````

---

## 🔄 Dry Run (Input)

```java
Input: ["/a", "/a/b", "/c/d", "/c/d/e", "/c/f"]
```

| Folder   | Parent Exists? | Is Subfolder? | Kept? |
| -------- | -------------- | ------------- | ----- |
| `/a`     | —              | No            | ✅     |
| `/a/b`   | `/a`           | Yes           | ❌     |
| `/c/d`   | —              | No            | ✅     |
| `/c/d/e` | `/c/d`         | Yes           | ❌     |
| `/c/f`   | —              | No            | ✅     |

---

## 🕒 Complexity

* **Time Complexity:** `O(n * l)`
* **Space Complexity:** `O(n)`

Where:

* `n` = number of folders
* `l` = average length of folder path

---

## 📘 Conclusion

This solution efficiently removes sub-folders using prefix matching with a HashSet and is well-suited for large datasets. No need to sort the input, and it's easy to understand.

Feel free to fork, modify, and use in your own coding projects!

---

## 🙌 Connect

Created with ❤️ by \Prakhar Tripathi.
Let’s connect on [Prakhar](https://www.linkedin.com) | [GitHub](https://github.com/gurawliprakhar)

```

---

e?
```
