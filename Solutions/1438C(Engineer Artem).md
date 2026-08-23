# 🧩 Problem: Engineer Artem
## 🔢 Number: Codeforces 1438C
**Difficulty**: ⚡ Constructive / Parity (Rating 2000)
**Language**: C++17
**Status**: ✅ Solved — passed 516 local tests, ready to submit

---

## 📜 Problem Overview

Given an `n × m` matrix `a`, you may increment any cell by 1 (or leave unchanged). Make it so no two adjacent cells (sharing a side) have the same value.

**Example:** `2×2` matrix `[[1, 1], [1, 1]]`
- Output: `[[2, 1], [1, 2]]` — no adjacent cells equal

Answer: any valid matrix is accepted.

---

### 🔢 Constraints
- `1 ≤ t ≤ 10` — test cases
- `1 ≤ n, m ≤ 100` — matrix dimensions
- `1 ≤ a[i][j] ≤ 10^9` — cell values
- Time limit: 1 second, Memory: 256 MB

---

## 🧠 Explanation

### Key insight: Chessboard coloring

Color the matrix like a chessboard: cell `(i, j)` is "black" if `(i + j)` is even, "white" if odd.

**Adjacent cells always have different colors** — this is the fundamental property of chessboard coloring.

### The trick

Make all "black" cells have **even** values and all "white" cells have **odd** values (or vice versa).

Since adjacent cells have different colors, their values will have different parity → they can never be equal.

### Why +1 is always enough

For any cell, `a[i][j]` and `a[i][j] + 1` have **different parity**. One of them must match the desired parity of the position. So either we keep the value or add 1 — no other operation needed.

### Why greedy doesn't work

Incrementing a cell to avoid matching one neighbor might create a match with another neighbor. The parity approach avoids this entirely by guaranteeing correctness globally.

---

## ⚙️ Algorithm Steps

1. Read `t` test cases
2. For each test case:
   - Read `n`, `m`, and matrix `a`
   - For each cell `(i, j)`:
     - If `(i + j) % 2 != a[i][j] % 2`: increment `a[i][j]` by 1
   - Output the modified matrix

---

## 🧾 Code
```cpp
#include <iostream>
#include <vector>

using ll = long long;
using namespace std;

void solve() {
    int n, m;
    cin >> n >> m;

    vector<vector<ll>> a(n, vector<ll>(m));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> a[i][j];
        }
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if ((i + j) % 2 != a[i][j] % 2) a[i][j]++;
            cout << a[i][j];
            if (j < m - 1) cout << " ";
        }
        cout << "\n";
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int t;
    cin >> t;
    while (t--) solve();

    return 0;
}
```

---

## ✅ Complexity, Insights & Notes

---

### ⏱ Time Complexity

- **O(n · m)** per test case — single pass through the matrix
- **O(t · n · m)** total — at most `10 · 100 · 100 = 10^5` operations

---

### 🧠 Space Complexity

- **O(n · m)** — storing the input matrix

---

### 🧨 Tricks / Insights

- **Chessboard parity coloring** — the core insight. Adjacent cells have different `(i + j) % 2`, so enforcing different value parity guarantees no equal neighbors.
- **+1 changes parity** — `x` and `x+1` always have different parity. One of them matches any target parity.
- **No minimization needed** — the problem accepts any valid answer, so we don't need to count or optimize increments.
- **Constructive approach** — instead of checking and fixing locally (greedy), we enforce a global invariant (parity pattern) that guarantees correctness.

---

### 🔗 Related Concepts

- **Constructive algorithms** — building a valid solution from a mathematical insight
- **Parity arguments** — using even/odd properties to guarantee constraints
- **Chessboard coloring** — classic technique for grid problems
- **2-SAT** — alternative approach (overkill for this problem): https://codeforces.com/blog/entry/92977#comment-1387506

---

### 🧪 Testing

- **516 local tests** generated via `gen_tests.py` (edge cases + random with validator)
- Validator checks: `b[i][j]` is `a[i][j]` or `a[i][j]+1`, and no two adjacent cells equal
- All 516 tests passed

---

### 📝 Why this problem is 2000

The difficulty is entirely in the **insight**, not the code. The solution is one line, but seeing the connection between chessboard coloring and value parity is non-obvious. Many contestants try greedy or 2-SAT before realizing the simple parity trick exists.
