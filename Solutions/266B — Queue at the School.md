# 🧩 Codeforces 266B — Queue at the School

## 📜 Problem Statement

A queue of students is represented by a string `s` of length `n`, containing only `'B'` (boy) and `'G'` (girl).  
Each second, every boy who stands directly in front of a girl will swap places with her.  
This process is repeated for `t` seconds.

Your task is to simulate the queue after `t` seconds and output the final arrangement.

---

## ✅ Final Code (C++)

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int n, t;
    cin >> n >> t;

    string s;
    cin >> s;

    for (int j = 0; j < t; ++j) {
        for (int i = 0; i < n - 1; ++i) {
            if (s[i] == 'B' && s[i + 1] == 'G') {
                swap(s[i], s[i + 1]);
                ++i; // skip next to avoid double swap
            }
        }
    }

    cout << s << endl;
    return 0;
}
```

## 💡 Idea Behind the Solution

The queue evolves over time through **pairwise swaps**.

Each second, we scan the queue from **left to right**:

- If we find `'B'` followed by `'G'`, we **swap them**
- After a swap, we increment `i` again to **skip the next index**, preventing a boy from swapping twice in the same second

We repeat this process for `t` seconds, simulating the queue evolution step by step.

---

## 🧠 Why This Works

- The simulation mimics the **real-time behavior** of the queue
- The `i++` after swap is **critical** — without it, a boy could swap multiple times in one second, violating the problem constraints
- The outer loop runs `t` times, and the inner loop runs up to `n - 1` each time, giving a total complexity of `O(n × t)`

---

## ⏱ Complexity

| Metric            | Value                                      |
|-------------------|--------------------------------------------|
| **Time Complexity**   | `O(n × t)` — each second processes up to `n` swaps |
| **Space Complexity**  | `O(n)` — for storing the string         |

---

## 🧘 Key Takeaways

- Simulation problems require **careful control of index movement**
- Skipping after a swap avoids **unintended behavior**
- This is a classic example of **state evolution over time**, useful in modeling:
  - Queues
  - Traffic systems
  - Cellular automata

---

## 📦 Module Summary

| Component         | Description                                 |
|------------------|---------------------------------------------|
| **Pattern**       | Simulation with conditional swap            |
| **Reusability**   | Medium — applies to queue dynamics, pairwise swaps |
| **Edge Cases**    | Multiple adjacent `'BG'`, no swaps, full reversal |
| **Performance**   | Efficient for `n ≤ 50`, `t ≤ 50` — as per constraints |

---
