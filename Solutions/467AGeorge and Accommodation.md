# 🧩 Problem: George and Accommodation  
## 🔢 Number: Codeforces 467A  
**Difficulty**: ✳️ Implementation  
**Language**: C++  
**Status**: ✅ Solved via simple condition check

---

## 📜 Problem Overview

George is looking for a room in a dormitory.  
Each room has a current number of occupants `p` and a maximum capacity `q`.  
George will choose a room only if `q - p ≥ 2` — meaning at least two spots are free.

You're given `n` rooms.  
Count how many rooms George can choose.

---

### 🔢 Constraints
- `1 ≤ n ≤ 100`  
- `0 ≤ p ≤ q ≤ 100`

---

## 🧠 Explanation

We iterate over all `n` rooms.  
For each room, we check if `q - p ≥ 2` — if yes, we increment the counter.  
At the end, we print the total number of suitable rooms.

---

## ⚙️ Algorithm Steps

1. Read integer `n` — number of rooms  
2. Initialize counter `rooms = 0`  
3. Loop `n` times:
   - Read `p` and `q`  
   - If `q - p ≥ 2`, increment `rooms`  
4. Output `rooms`

---

## 🧾 Code
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    int rooms = 0;

    for (int i = 0; i < n; i++) {
        int p, q;
        cin >> p >> q;
        if (q - p >= 2) {
            rooms++;
        }
    }

    cout << rooms << endl;
    return 0;
}
```

## ✅ Complexity, Insights & Notes

---

### ⏱ Time Complexity

- **O(n)** — we iterate through the list of rooms once  
- For each room, we perform a constant-time check: `q - p ≥ 2`  
- No nested loops or additional passes are required

---

### 🧠 Space Complexity

- **O(1)** — constant space  
- We only use a few integer variables (`n`, `p`, `q`, `rooms`)  
- No arrays, maps, or dynamic structures are needed

---

### 🧨 Tricks / Insights

- **Simple condition check**:  
  The core logic is a direct comparison: `q - p ≥ 2`  
  This makes the problem ideal for beginners or warm-up sessions

- **No need for sorting or extra data structures**:  
  The input is processed sequentially, and no preprocessing is required

- **Can be solved in under 5 minutes**:  
  The problem is straightforward and tests basic input handling and conditional logic

---

### 🔗 Related Concepts

- **Basic iteration** — looping through a fixed-size input  
- **Conditional filtering** — selecting elements based on a simple rule  
- **Input parsing in C++** — using `cin` to read structured input

---
