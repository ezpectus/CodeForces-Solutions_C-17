# 🎁 Problem: 136A - Presents (Codeforces)

## 📜 Statement

There are `n` children, each of whom gives a present to exactly one other child.  
You are given an array `p` of length `n`, where `p[i]` is the number of the child who receives a present from child `i + 1`.

Your task is to **reconstruct the inverse mapping**: for each child `j`, determine **who gave them** the present.

---

## 🔢 Input Format

- First line: integer `n` (1 ≤ n ≤ 100)
- Second line: `n` space-separated integers `p[1], p[2], ..., p[n]`  
  Each `p[i]` is in range [1, n], and all values are distinct.

---

## 🎯 Output Format

- Output `n` space-separated integers `q[1], q[2], ..., q[n]`  
  Where `q[j]` is the number of the child who gave a present to child `j`.

---

## 🧠 Example

### Input
```
4 
2 3 4 1
```
### Output
```
4 1 2 3
```

### Explanation
- Child 1 gave a present to child 2 → `q[2] = 1`
- Child 2 gave a present to child 3 → `q[3] = 2`
- Child 3 gave a present to child 4 → `q[4] = 3`
- Child 4 gave a present to child 1 → `q[1] = 4`

---

## 🧱 C++17 Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> p(n), q(n);
    for (int i = 0; i < n; ++i) {
        cin >> p[i];
        q[p[i] - 1] = i + 1;
    }
    for (int i = 0; i < n; ++i)
        cout << q[i] << " ";
    cout << endl;
    return 0;
}
```

## 🧮 Time & Space Complexity

| Metric      | Value     | Notes                        |
|-------------|-----------|------------------------------|
| Time        | O(n)      | Single pass over input       |
| Space       | O(n)      | Output array `q`             |
| Stability   | High      | No branching or recursion    |
| Scalability | Excellent | Handles full range up to 100 |

---

## 🧠 Engineering Takeaway

This problem is a classic example of:

- ✅ **Inverse mapping** — reconstructing who gave to whom  
- 🧠 **Index manipulation** — careful use of `i + 1` and `p[i] - 1`  
- 🚀 **No extra logic** — direct translation of the problem statement

> You’re not solving — you’re **reversing the direction of the gift flow**.

---

## 🧩 Conclusion

**136A - Presents** is a clean and elegant problem that tests your ability to **invert mappings** and handle **1-based indexing** carefully.  
It’s a great warm-up for mastering **array transformations** and understanding **input-output relationships**.

> **Simplicity with precision — always.**


---
