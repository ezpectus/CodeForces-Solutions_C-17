# 🧩 Problem: Magnets  
## 🔢 Number: Codeforces 344A  
**Difficulty**: ✳️ Implementation  
**Language**: C++  
**Status**: ✅ Solved via sequential comparison

---

## 📜 Problem Overview

You're given `n` magnets, each represented by a string `"01"` or `"10"` indicating their poles.  
Magnets can be grouped together if the adjacent poles match.  
Count how many **groups** of magnets will form when placed in a line.

---

### 🔢 Constraints
- `1 ≤ n ≤ 100`  
- Each magnet is either `"01"` or `"10"`

---

## 🧠 Explanation

We read the first magnet and initialize `groups = 1`.  
Then we iterate through the remaining magnets:  
- If the current magnet is **different** from the previous one, it starts a **new group**  
- Otherwise, it continues the current group

---

## ⚙️ Algorithm Steps

1. Read integer `n` — number of magnets  
2. Read the first magnet into `prev`  
3. Initialize `groups = 1`  
4. Loop from `i = 1` to `n - 1`:
   - Read `curr` magnet  
   - If `curr != prev`, increment `groups`  
   - Update `prev = curr`  
5. Output `groups`

---

## 🧾 Code
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    int n;
    cin >> n;

    string prev, curr;
    int groups = 1;

    cin >> prev;
    for (int i = 1; i < n; i++) {
        cin >> curr;
        if (curr != prev) {
            groups++;
        }
        prev = curr;
    }

    cout << groups << endl;
    return 0;
}
```

## ✅ Complexity, Insights & Notes

---

### ⏱ Time Complexity

- **O(n)** — we iterate through the list of magnets once  
- For each magnet, we perform a constant-time comparison with the previous one  
- No nested loops or additional passes are required

---

### 🧠 Space Complexity

- **O(1)** — constant space  
- We only use two strings (`prev`, `curr`) and one integer counter (`groups`)  
- No arrays, vectors, or dynamic structures are needed

---

### 🧨 Tricks / Insights

- **Simple comparison of adjacent strings**:  
  The core logic is a direct equality check between consecutive magnet strings  
  This makes the problem ideal for beginners or warm-up sessions

- **No need for arrays or advanced data structures**:  
  The input is processed sequentially, and no preprocessing or storage is required

- **Ideal warm-up problem**:  
  Tests basic input handling, loop control, and conditional logic  
  Can be solved quickly and cleanly with minimal code

---

### 🔗 Related Concepts

- **Sequential comparison** — checking adjacent elements in a stream  
- **Input parsing in C++** — using `cin` to read structured input  
- **Group counting logic** — incrementing a counter based on change detection

---
