# 🧩 Problem: Odd-Even Subsequence
## 🔢 Number: Codeforces 1370D
**Difficulty**: ⚡ Binary Search + Greedy (Rating 2000)
**Language**: C++17
**Status**: ✅ Solved — passed 308 local tests, ready to submit

---

## 📜 Problem Overview

Given array `a[1..n]`, choose a subsequence of length `k`. The cost is `min(max(odd-indexed elements), max(even-indexed elements))`. Minimize the cost.

**Example:** `a = [5, 3, 4, 2, 6]`, `k = 3`
- Subsequence `{3, 4, 2}`: odd positions = `{3, 2}`, even = `{4}`. Cost = `min(3, 4) = 3`
- Subsequence `{3, 50, 2}`: odd = `{3, 2}`, even = `{50}`. Cost = `min(3, 50) = 3`
- Best: `{5, 3, 2}` → odd = `{5, 2}`, even = `{3}` → cost = `min(5, 3) = 2`

---

### 🔢 Constraints
- `2 ≤ k ≤ n ≤ 2·10^5`
- `1 ≤ a[i] ≤ 10^9`
- Time limit: 2 seconds, Memory: 256 MB

---

## 🧠 Explanation

### Key insight: Binary search on answer + two cases

We binary search on the answer `x`. For each `x`, we check: can we pick a subsequence of length `k` where either:
1. All **odd-positioned** elements are `≤ x` (even-positioned can be anything)
2. All **even-positioned** elements are `≤ x` (odd-positioned can be anything)

The answer is `min` of both binary searches.

### Why two cases?

The cost is `min(max_odd, max_even)`. If the answer is `x`, then either `max_odd ≤ x` or `max_even ≤ x`. We try both and take the minimum.

### Greedy check

For `check(x, odd_limited)`:
- Go through the array, picking elements greedily
- If the current position in the subsequence is odd and `odd_limited = true`: only pick if `a[i] ≤ x`
- If the current position is even and `odd_limited = false`: only pick if `a[i] ≤ x`
- Otherwise: pick any element (no restriction)
- If we pick `≥ k` elements: return `true`

### Why greedy works

We always want to pick as many elements as possible. When a position has no restriction, we pick any element (it doesn't matter which — we just need to fill the slot). When a position has a restriction (`≤ x`), we pick only qualifying elements. This maximizes the subsequence length.

---

## ⚙️ Algorithm Steps

1. Read `n`, `k`, array `a`
2. Define `check(x, odd)`:
   - `res = 0` (elements picked so far)
   - For each `a[i]`: if position `res+1` is odd and `odd=true`: pick if `a[i] ≤ x`. If position is even and `odd=false`: pick if `a[i] ≤ x`. Else: always pick.
   - Return `res >= k`
3. For `odd` in `{true, false}`:
   - Binary search: `l=1, r=max(a)`, find minimum `x` where `check(x, odd)` is true
4. Answer = `min` of both binary search results

---

## 🧾 Code
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

void solve() {
    int n, k;
    cin >> n >> k;

    vector<int> a(n);
    for (int i = 0; i < n; i++) cin >> a[i];

    auto check = [&](int x,bool odd) -> bool{
        int res = 0;
        for (int i = 0; i < n; i++) {
            bool curr_odd = (res % 2 == 0);
            if (curr_odd == odd) {
                if (a[i] <= x) res++;
            } else res++;
        }
        return res >= k;
    };

    int ans = 1e9;
    for (int odd = 0; odd < 2; odd++) {
        int l = 1, r = *max_element(a.begin(), a.end());
        while (l < r) {
            int m = l + (r - l) / 2;
            if (check(m, odd)) r = m;
            else l = m + 1;
        }
        ans = min(ans, l);
    }
    cout << ans << "\n";
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int t = 1;
    while (t--) solve();

    return 0;
}
```

---

## ✅ Complexity, Insights & Notes

---

### ⏱ Time Complexity

- **O(n)** per `check` call
- **O(log max_a)** binary search iterations per case
- **2 cases** (odd/even)
- **Total: O(n · log max_a)** — at most `2·10^5 · 30 = 6·10^6` operations

---

### 🧠 Space Complexity

- **O(n)** — storing the input array

---

### 🧨 Tricks / Insights

- **Binary search on answer** — instead of constructing the subsequence directly, search for the minimum possible cost value
- **Two cases** — since cost = `min(max_odd, max_even)`, we try minimizing each separately and take the minimum
- **Greedy check** — when filling unrestricted positions, pick any element; when filling restricted positions, pick only qualifying ones. This maximizes the subsequence length
- **Position tracking** — `res % 2 == 0` means the next position is odd (1-indexed), since `res` elements have been picked and the next is `res + 1`

---

### 🔗 Related Concepts

- **Binary search on answer** — classic CP pattern for minimization problems
- **Greedy validation** — checking feasibility for a given threshold
- **Subsequence construction** — picking elements with position-dependent constraints

---

### 🧪 Testing

- **308 local tests** (8 edge cases + 300 random) via `gen_tests.py`
- Brute force: enumerate all `C(n, k)` subsequences, compute cost for each
- All 308 tests passed

---

### 📝 Why this problem is 2000

The binary search pattern is standard, but the key difficulty is:
1. Seeing that `min(max_odd, max_even)` splits into two independent subproblems
2. Designing the greedy check with position-dependent constraints
3. Correctly tracking odd/even positions during greedy selection


---
