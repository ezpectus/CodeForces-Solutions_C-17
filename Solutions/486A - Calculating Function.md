# 🧮 Problem: 486A - Calculating Function (Codeforces)

## 📜 Statement

You are given a single integer `n`.  
Define a function `f(n)` as follows:

- If `n` is even, then `f(n) = n / 2`
- If `n` is odd, then `f(n) = - (n + 1) / 2`

Print the value of `f(n)`.

---

## 🔢 Input Format

- A single integer `n` (1 ≤ n ≤ 10¹⁵)

---

## 🎯 Output Format

- A single integer — the value of `f(n)`

---

## 🧠 Example

### Input
```
4
```

### Output
```
2
```

### Input
```
5
```

### Output
```
-3
```

---

## 🧱 C++17 Implementation

```cpp
#include <iostream>
using namespace std;

int main() {
    long long n;
    cin >> n;
    if (n % 2 == 0)
        cout << n / 2 << endl;
    else
        cout << - (n + 1) / 2 << endl;
    return 0;
}
```
## 🧮 Time & Space Complexity

| Metric      | Value     | Notes                          |
|-------------|-----------|--------------------------------|
| Time        | O(1)      | Constant-time arithmetic       |
| Space       | O(1)      | No extra memory used           |
| Stability   | High      | No branching beyond parity     |
| Scalability | Excellent | Handles full range up to 10¹⁵  |

---

## 🧠 Engineering Takeaway

This problem is a classic example of:

- ✅ **Parity-based branching** — even vs odd logic  
- 🧠 **Mathematical simplification** — no loops or simulation  
- 🚀 **Constant-time evaluation** — pure arithmetic

> You’re not computing — you’re **applying a parity-aware formula**.

---

## 🧩 Conclusion

**486A - Calculating Function** is a minimalistic problem that tests your ability to **translate mathematical definitions into code**.  
It’s a great warm-up for mastering **conditional logic** and **integer arithmetic** at scale.

> **Simplicity with mathematical elegance — always.**


---



