# 🔠 Module: 59A – Word — Case Conversion by Majority

## 📌 Problem Statement

Given a word consisting of uppercase and lowercase Latin letters,  
convert the entire word to either **lowercase** or **uppercase** based on the following rule:

- If the number of **uppercase letters** is **strictly greater** than lowercase → convert to uppercase
- Otherwise → convert to lowercase

---

## 🧩 Architectural Insight

### ✅ Signals from the problem:
- Input is a single word → `string s`
- Need to **count uppercase vs lowercase**
- Decision is based on **majority case**
- Conversion must apply to **entire string**

---

## 🔧 Strategy

1. Traverse the string and count:
   - `lower++` if `islower(s[i])`
   - `upper++` otherwise
2. Apply conversion:
   - If `upper > lower` → convert all to `toupper`
   - Else → convert all to `tolower`

---

## ✅ C++ Implementation

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string s;
    cin >> s;
    int lower = 0, upper = 0;

    for (char c : s) {
        if (islower(c)) lower++;
        else upper++;
    }

    for (char& c : s) {
        c = (upper > lower) ? toupper(c) : tolower(c);
    }

    cout << s << endl;
    return 0;
}
```
## 📦 Complexity Analysis

| Aspect         | Value             | Explanation                                                                 |
|----------------|-------------------|------------------------------------------------------------------------------|
| Time           | `O(n)`            | One pass to count case distribution, one pass to apply conversion.          |
| Space          | `O(1)`            | In-place modification of the string — no extra memory used.                 |
| Edge cases     | Handled inline    | Equal counts of upper/lower → default to lowercase conversion.              |
| Total runtime  | Instant           | Executes in microseconds — ideal for short strings and competitive input.   |
| Failure modes  | None              | Input constraints guarantee safe execution — only Latin letters allowed.    |

---

### 🧠 Architectural Notes

- This is a **majority-based transformation** task — count, compare, convert.
- Uses standard library functions: `islower`, `toupper`, `tolower` — clean and portable.
- Conversion logic is **branchless** via ternary operator — minimal and expressive.
- Ideal for warm-up, **repo-ready minimalism**, and style-based logic tasks.



---
