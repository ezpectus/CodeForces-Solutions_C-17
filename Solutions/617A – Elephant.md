# 🐘 Module: 617A – Elephant — Minimum Steps

## 📌 Problem Statement

Given an integer `x` (1 ≤ x ≤ 1,000,000),  
an elephant wants to go from position `0` to position `x` on a number line.  
In one move, it can go `1`, `2`, `3`, `4`, or `5` units forward.  
Find the **minimum number of moves** required to reach exactly position `x`.

---

## 🧩 Architectural Insight

### ✅ Signals from the problem:
- Elephant can move in steps of up to `5`
- Goal: minimize number of steps to reach `x`
- This is a **greedy division** problem

### ❗ Key condition:
- Use as many `5`-steps as possible
- If remainder exists → need **one extra step**

---

## 🔧 Strategy

1. Divide `x` by `5` → gives full steps
2. If `x % 5 != 0` → add one more step for the remainder

---

## ✅ C++ Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    int x;
    cin >> x;

    int steps = x / 5;
    if (x % 5) steps++;

    cout << steps << endl;
    return 0;
}
```

## 📦 Complexity Analysis

| Aspect         | Value             | Explanation                                                                 |
|----------------|-------------------|------------------------------------------------------------------------------|
| Time           | `O(1)`            | Constant-time arithmetic: one division and one conditional increment.       |
| Space          | `O(1)`            | No extra memory used — only scalar variables.                               |
| Edge cases     | Handled inline    | `x = 1` → `steps = 1`, `x = 5` → `steps = 1` — no special logic required.    |
| Total runtime  | Instant           | Executes in microseconds — ideal for competitive programming.               |
| Failure modes  | None              | Input constraints guarantee safe execution: `x ∈ [1, 1_000_000]`.           |

---

### 🧠 Architectural Notes

- This is a **greedy step compression** task — use the largest step size (`5`) first.
- No loops, no arrays — pure arithmetic and minimal branching.
- Ideal for warm-up, speed rounds, and **repo-ready minimalism**.


---
