# ⚔️ Module: 734A – Anton and Danik — Majority Vote

## 📌 Problem Statement

Anton and Danik play `n` rounds of a game.  
Each round is won by either Anton (`'A'`) or Danik (`'D'`).  
Given the result string `s` of length `n`, determine who won more rounds:

- If Anton won more → output `"Anton"`
- If Danik won more → output `"Danik"`
- If equal → output `"Friendship"`

---

## 🧩 Architectural Insight

### ✅ Signals from the problem:
- Input is a string of `'A'` and `'D'`
- Count frequency of each character
- Compare counts → output winner

---

## 🔧 Strategy

1. Read input `n` and result string `s`
2. Count `'A'` and `'D'` using `std::count`
3. Compare:
   - `count_a > count_b` → `"Anton"`
   - `count_b > count_a` → `"Danik"`
   - Else → `"Friendship"`

---

## ✅ C++ Implementation

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cin >> n;
    string s;
    cin >> s;

    int count_a = count(s.begin(), s.end(), 'A');
    int count_b = count(s.begin(), s.end(), 'D');

    if (count_a > count_b) {
        cout << "Anton" << endl;
    } else if (count_b > count_a) {
        cout << "Danik" << endl;
    } else {
        cout << "Friendship" << endl;
    }

    return 0;
}
```

## 📦 Complexity Analysis

| Aspect         | Value             | Explanation                                                                 |
|----------------|-------------------|------------------------------------------------------------------------------|
| Time           | `O(n)`            | One pass to count `'A'` and `'D'` in the result string.                     |
| Space          | `O(1)`            | Only scalar counters used — no dynamic memory allocation.                   |
| Edge cases     | Handled inline    | Equal wins → output `"Friendship"` without special logic.                   |
| Total runtime  | Instant           | Executes in microseconds for all valid inputs.                              |
| Failure modes  | None              | Input constraints guarantee safe execution — only `'A'` and `'D'` allowed.  |

---

### 🧠 Architectural Notes

- This is a **majority vote task** — count, compare, decide.
- Uses `std::count` for clean STL-based frequency analysis.
- Ideal for warm-up, **repo-ready minimalism**, and character-based logic.

---
