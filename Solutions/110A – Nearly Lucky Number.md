# 🍀 Module: 110A – Nearly Lucky Number — Digit Frequency Filter

## 📌 Problem Statement

Given a number `n` as a string,  
check whether the **total number of lucky digits** (`4` and `7`) in `n` is itself a **lucky number**.  
Lucky numbers are defined as numbers consisting only of digits `4` and `7`.

---

## 🧩 Architectural Insight

### ✅ Signals from the problem:
- Input is a string → digit-wise analysis
- Lucky digits: `'4'` and `'7'`
- Count how many lucky digits appear
- If count is `4` or `7` → output `"YES"`, else `"NO"`

---

## 🔧 Strategy

1. Read input as `string s`
2. Count occurrences of `'4'` and `'7'`
3. Sum the counts → `happy_digits`
4. If `happy_digits == 4 || happy_digits == 7` → `"YES"`
5. Else → `"NO"`

---

## ✅ C++ Implementation

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s;
    cin >> s;

    int count_4 = count(s.begin(), s.end(), '4');
    int count_7 = count(s.begin(), s.end(), '7');
    int happy_digits = count_4 + count_7;

    if (happy_digits == 4 || happy_digits == 7) {
        cout << "YES" << endl;
    } else {
        cout << "NO" << endl;
    }

    return 0;
}
```

## 📦 Complexity Analysis

| Aspect         | Value             | Explanation                                                                 |
|----------------|-------------------|------------------------------------------------------------------------------|
| Time           | `O(n)`            | One pass to count lucky digits in the string.                               |
| Space          | `O(1)`            | Only scalar counters used — no dynamic memory allocation.                   |
| Edge cases     | Handled inline    | Example: `s = "447"` → `happy_digits = 3` → output `"NO"`.                  |
| Total runtime  | Instant           | Executes in microseconds for all valid inputs.                              |
| Failure modes  | None              | Input constraints guarantee safe execution — only digits are present.       |

---

### 🧠 Architectural Notes

- This is a **digit frequency filter** task — count specific digits, apply condition.
- Uses `std::count` for clean STL-based counting — expressive and minimal.
- Ideal for warm-up, **repo-ready minimalism**, and digit-based logic tasks.

---
