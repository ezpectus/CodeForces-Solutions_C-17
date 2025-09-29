# 🧩 Problem: Beautiful Year  
## 🔢 Number: Codeforces 271A  

---

## 📜 Problem Overview

Given a year `y`, find the next year strictly greater than `y` such that all four digits of the year are distinct.

---

### 🔢 Constraints
- `1000 ≤ y ≤ 9000`  
- Output must be the **first year > y** with all digits unique

---

## 🧠 Explanation

We increment the year one by one starting from `y + 1`.  
For each candidate year, we convert it to a string and check if all digits are distinct.  
Once we find such a year, we print it and terminate.

---

## ⚙️ Algorithm Choice
- **Approach**: Brute-force with digit uniqueness check  
- **Why**: Input size is small, only ~9000 iterations max  
- **Efficiency**: Fast enough for constraints  
- **Memory**: Constant space

---

## 💡 Idea Summary
- Convert year to string  
- Compare all digit pairs to ensure uniqueness  
- Stop at the first valid year

---

## 🧾 Code
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int y;
    cin >> y;

    while (++y <= 10000) {
        string s = to_string(y);
        if (s[0] != s[1] && s[0] != s[2] && s[0] != s[3] &&
            s[1] != s[2] && s[1] != s[3] &&
            s[2] != s[3]) {
            cout << y << endl;
            break;
        }
    }

    return 0;
}
```
## ✅ Complexity, Insights & Notes

### ⏱ Time Complexity
- **O(1)** — bounded brute-force loop, max 9000 iterations  
- Each iteration performs constant-time digit comparison

### 🧠 Space Complexity
- **O(1)** — no extra data structures used  
- Only basic variables and string conversion

---

### 🧨 Tricks / Insights
- Converting the year to a string simplifies digit access  
- Manual digit comparison is acceptable due to fixed length (4 digits)  
- No need for sets, maps, or frequency counters — just direct character comparison  
- Early exit with `break` ensures minimal iterations

---

### 🧠 Notes
- This is a classic **implementation warm-up**  
- Useful for practicing:
  - **String manipulation**  
  - **Brute-force with early exit**  
  - **Digit uniqueness logic**  
- Can be extended to problems involving:
  - Unique digit constraints  
  - Year-based filtering  
  - Simple validation loops
---
