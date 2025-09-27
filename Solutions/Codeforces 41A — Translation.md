# 🧠 Codeforces 41A — Translation

## 📜 Problem Statement
You are given two strings **s** and **t**.  
Determine whether string **t** is exactly the reverse of string **s**.  

- If yes → print `"YES"`.  
- Otherwise → print `"NO"`.  

---

## 💡 Idea
- Reverse the first string `s`.  
- Compare it with the second string `t`.  
- If they match → answer is `"YES"`.  
- Else → `"NO"`.  

This is a direct string manipulation problem, no tricks.  

---

## 🚀 Implementation (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s, t;
    cin >> s >> t;

    reverse(s.begin(), s.end());
    if (s == t) cout << "YES\n";
    else cout << "NO\n";

    return 0;
}
```

## ⏱️ Complexity Analysis

- **Reversing string:** O(n)  
- **Comparison:** O(n)  
- **Total:** O(n), where n = length of the string.  
- **Space:** O(1) extra (in‑place reverse).  

---

## ⚠️ Pitfalls

- **In‑place reverse:** Forgetting to reverse directly in the same string (copying works but is less efficient).  
- **Case sensitivity:** Problem requires exact match, so `"abc"` vs `"CBA"` → `"NO"`.  
- **Input/output format:** Extra whitespace or newline differences can cause wrong answers.  

---

## ✅ Conclusion

This is a **warm‑up string problem**:

- ⚡ Reverse + compare in O(n).  
- 📊 No advanced data structures needed.  
- 🛡️ Great intro to Codeforces string manipulation tasks.  

👉 **Key takeaway:** Sometimes the shortest path is the right one — just reverse and compare.

---
