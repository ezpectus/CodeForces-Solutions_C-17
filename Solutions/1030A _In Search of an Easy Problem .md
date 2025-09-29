# 🧩 Problem: In Search of an Easy Problem  
## 🔢 Number: Codeforces 1030A  
 
---

## 📜 Problem Overview

You're given `n` integers, each representing whether a problem is easy (`0`) or hard (`1`).  
If **all values are `0`**, the verdict is `"EASY"`.  
If **any value is `1`**, the verdict is `"HARD"`.

---

### 🔢 Constraints
- `1 ≤ n ≤ 100`  
- Each value is either `0` or `1`

---

## 🧠 Explanation

We read `n` values and accumulate their sum.  
If the total sum is `0`, it means all values were `0` → print `"EASY"`  
Otherwise, at least one `1` was present → print `"HARD"`

---

## ⚙️ Algorithm Choice
- **Approach**: Simple loop with sum accumulator  
- **Why**: No need for arrays or conditionals per element  
- **Efficiency**: O(n) time, constant space  
- **Memory**: No extra structures

---

## 💡 Idea Summary
- Read `n` values  
- Accumulate their sum  
- Use sum to determine verdict  
- Print result based on total

---

## 🧾 Code
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    int ans = 0;
    for (int i = 0; i < n; ++i) {
        int a;
        cin >> a;
        ans += a;
    }

    if (ans == 0) {
        cout << "EASY" << endl;
    } else {
        cout << "HARD" << endl;
    }

    return 0;
}
```

## ✅ Complexity, Insights & Notes

### ⏱ Time Complexity
- **O(n)** — single pass through input values  
- Each iteration performs constant-time addition

### 🧠 Space Complexity
- **O(1)** — no extra data structures used  
- Only basic scalar variables are maintained

---

### 🧨 Tricks / Insights
- Using a **sum accumulator** avoids per-element conditional checks  
- No need to store values — just total is enough to determine the verdict  
- Early exit is possible (e.g., break on first `1`), but not necessary given small `n`  
- Clean separation of input, processing, and output logic

---

### 🧠 Notes
- This is a classic **implementation warm-up**  
- Useful for practicing:
  - **Input handling**  
  - **Conditional logic**  
  - **Minimalist decision-making**  
- Can be extended to problems involving:
  - Boolean aggregation  
  - Early termination strategies  
  - Lightweight validation loops

---
