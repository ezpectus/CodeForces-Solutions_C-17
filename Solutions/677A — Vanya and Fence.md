# 🧩 Codeforces 677A — Vanya and Fence

## 📜 Problem Statement

Vanya and his friends are walking along a restricted area next to a fence of height `h`.  
To avoid being seen by the guard, each friend must either:
- Walk upright if their height `≤ h` → takes **1 unit of width**
- Bend down if their height `> h` → takes **2 units of width**

All friends walk in a single row.  
Determine the **minimum total width** of the road required to fit them all unseen.

---

## ✅ Sample Input
```
n = 6, h = 5
a = [7, 6, 8, 9, 10, 5]
```

### Output:
```11```

### Explanation:
- Friends taller than `h` must bend → width += 2
- Friends of height `≤ h` walk normally → width += 1  
- Total width = 2 + 2 + 2 + 2 + 2 + 1 = 11

---

## 🧾 Final Code (C++)

```cpp
#include <iostream>
using namespace std;

int main() {
    int n, h;
    cin >> n >> h;

    int width = 0;
    for (int i = 0; i < n; ++i) {
        int a;
        cin >> a;
        width += (a > h) ? 2 : 1;
    }

    cout << width << endl;
    return 0;
}
```

## ⏱ Complexity

| Metric            | Value         |
|-------------------|---------------|
| **Time Complexity**   | `O(n)` — single pass over the input array |
| **Space Complexity**  | `O(1)` — constant space for counters only |

### 🔍 Breakdown
- The loop runs exactly `n` times, once per friend.
- No auxiliary data structures are used — just a scalar `width` counter.
- Input is processed inline, making the solution memory-light and efficient.

---

## 🧘 Key Takeaways

- The core logic is a **simple conditional width counter** — no sorting, no arrays, no maps.
- Using a **ternary operator** (`(a > h) ? 2 : 1`) improves readability and keeps the loop compact.
- This is an **ideal warm-up problem** for:
  - Input parsing
  - Basic control flow
  - Translating real-world constraints into code
- **Common mistake**: misreading input order (`n h` vs `h n`) — always double-check format against the problem statement.

---

## 📦 Module Summary

| Component         | Description                          |
|------------------|--------------------------------------|
| **Pattern**       | Linear scan with conditional logic   |
| **Reusability**   | Low — problem-specific width counter |
| **Edge Cases**    | All friends taller or shorter than `h` |
| **Performance**   | Fast and memory-light — ideal for beginners |
| **Debuggability** | Easy to trace — print each `a[i]` and its contribution to `width` if needed |


---

