# 🧠 Codeforces 116A — Tram

## 📜 Problem Statement
A tram has **n stops**.  
At each stop:
- `a` passengers exit,  
- `b` passengers enter.  

The tram starts empty.  
Find the **minimum capacity** of the tram so that the number of passengers inside never exceeds it.

---

## 💡 Idea
- Maintain a running counter `passengers`.  
- At each stop:  
  - Subtract `a` (exiting).  
  - Add `b` (entering).  
- Track the maximum value of `passengers` across all stops.  
- That maximum is the required **capacity**.  

---

## 🚀 Implementation (C++)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int passengers = 0, capacity = 0;

    for (int i = 0; i < n; i++) {
        int a, b;
        cin >> a >> b;
        passengers -= a;
        passengers += b;
        capacity = max(capacity, passengers);
    }

    cout << capacity << "\n";
    return 0;
}
```

## ⏱️ Complexity Analysis

- **Time:** O(n) — one pass through the stops.  
- **Space:** O(1) — only counters are stored.  

---

## ⚠️ Pitfalls

- **Order of operations:** Forgetting to subtract exiting passengers before adding new ones.  
- **Maximum tracking:** Not updating the maximum after each stop.  
- **Initial state:** Assuming the tram starts with passengers (it starts empty).  

---

## ✅ Conclusion

This is a **simulation problem**:

- ⚡ Just track passengers step by step.  
- 📊 The answer is the maximum occupancy observed.  
- 🛡️ Runs in linear time with constant memory.  

👉 **Key takeaway:** Sometimes the hardest‑looking problems are just careful bookkeeping — update, track, and take the max.

---
