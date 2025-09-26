# ➖ Module: 977A – Wrong Subtraction — Digit-Aware Reduction

## 📌 Problem Statement

Given two integers `n` and `k`,  
perform `k` operations on `n` as follows:

- If the last digit of `n` is not zero → subtract `1`
- Else → divide `n` by `10`

Return the final value of `n` after `k` operations.

---

## 🧩 Architectural Insight

### ✅ Signals from the problem:
- Operation depends on **last digit** of `n`
- Requires **exactly `k` steps**, no early termination
- Each step is **digit-aware**, not arithmetic-only

---

## 🔧 Strategy

1. Loop `k` times
2. In each iteration:
   - If `n % 10 != 0` → `n--`
   - Else → `n /= 10`
3. Output final `n`

---

## ✅ C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    while (k--) {
        if (n % 10 != 0) n--;
        else n /= 10;
    }

    cout << n << endl;
    return 0;
}
```

## 📦 Complexity Analysis

| Aspect         | Value             | Explanation                                                                 |
|----------------|-------------------|------------------------------------------------------------------------------|
| Time           | `O(k)`            | Each operation is constant-time, loop runs `k` times.                       |
| Space          | `O(1)`            | No extra memory used — only scalar variables.                               |
| Edge cases     | Handled inline    | `n = 10`, `k = 1` → `n = 1`; `n = 100`, `k = 2` → `n = 1`.                   |
| Total runtime  | Instant           | Executes in microseconds for all valid inputs.                              |
| Failure modes  | None              | Input constraints guarantee safe execution.                                 |

---

### 🧠 Architectural Notes

- This is a **digit-aware reduction loop** — logic depends on `n % 10`.
- No branching complexity — pure conditional arithmetic.
- Ideal for warm-up, **repo-ready minimalism**, and digit-based logic tasks.


---
