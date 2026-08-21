# 🧩 Problem: The Best Vacation
## 🔢 Number: Codeforces 1358D
**Difficulty**: ⚡ Sliding Window / Two Pointers (Rating 1900)
**Language**: C++17
**Status**: ✅ Solved — passed 1909 local tests, ready to submit

---

## 📜 Problem Overview

You want to visit Coronavirus-chan for exactly `x` consecutive days.

The year in Naha has `n` months, `i`-th month lasts `d_i` days. Days in the `i`-th month are numbered from `1` to `d_i`.

If you visit on the `j`-th day of a month, you get `j` hugs.

Your trip may start and end in different years (the calendar repeats).

Find the maximum total number of hugs you can get during `x` consecutive days.

**Example:** `n=3, x=2`, months `[1, 3, 1]`
- Days of the year: `{1, 1, 2, 3, 1}`
- Best start: day 3 (2nd month) → `2 + 3 = 5` hugs

Answer: **5**

---

### 🔢 Constraints
- `1 ≤ n ≤ 2·10^5` — number of months
- `1 ≤ d_i ≤ 10^6` — days per month
- `1 ≤ x ≤ d_1 + d_2 + ... + d_n` — vacation length
- Total days can be up to `2·10^11` — cannot enumerate all days
- Time limit: 2 seconds, Memory: 256 MB
- One test case per input

---

## 🧠 Explanation

### Why naive enumeration doesn't work

If we expand the calendar into a flat array of days, its size is `n · max(d_i) = 2·10^5 · 10^6 = 2·10^11`. This doesn't fit in memory and would TLE. We must work with **months**, not individual days.

### Key observation: structure of any window

Any window of `x` consecutive days consists of:
1. **Tail of some month** — the last `k` days of the leftmost month
2. **Full months** — zero or more complete months in the middle
3. **Head of some month** — the first `k'` days of the rightmost month

This means we can slide a window over **months** (not days) and use arithmetic progression formulas to compute hugs for partial months.

### Handling cyclicality

The year is cyclic — after the last month, the first month begins. To avoid wrap-around logic, we **duplicate the array**: `dd = d + d`. Now any window of `x` days can be represented as a contiguous segment of `dd`.

### Arithmetic progression formulas

- **Full month** `d` days: `hugs = 1 + 2 + ... + d = d*(d+1)/2`
- **First `k` days** of month `d`: `hugs = 1 + 2 + ... + k = k*(k+1)/2`
- **Last `k` days** of month `d`: `hugs = (d-k+1) + ... + d = k*(2*d - k + 1)/2`

### The algorithm (sliding window)

1. Duplicate the array: `dd[i] = d[i % n]` for `i = 0..2n-1`
2. Maintain a window `[l, r]` over months with `curd` (total days) and `curh` (total hugs)
3. For each right pointer `r`:
   - Add month `r` entirely: `curd += dd[r]`, `curh += dd[r]*(dd[r]+1)/2`
   - While `curd > x`: remove month `l` entirely, advance `l`
   - Now `curd <= x`:
     - If `curd == x`: update `res = max(res, curh)`
     - If `curd < x` and `l > 0`: "borrow" `k = x - curd` days from month `l-1` (last `k` days), add their hugs to `curh` and update `res`

The "borrowing" step doesn't modify `curd`/`curh` — it only computes a candidate answer by looking left.

---

## ⚙️ Algorithm Steps

1. Read `n`, `x`, and array `d`
2. Build `dd` = duplicated array of size `2n`
3. Initialize `res = 0`, `curd = 0`, `curh = 0`, `l = 0`
4. For `r` from `0` to `2n-1`:
   - Add `dd[r]` to window (days and hugs)
   - Shrink from left while `curd > x`
   - If `curd == x`: update `res`
   - If `curd < x` and `l > 0`: compute extra hugs from last `k = x - curd` days of `dd[l-1]`, update `res`
5. Output `res`

---

## 🧾 Code
```cpp
#include <iostream>
#include <vector>

using ll = long long;
using namespace std;

void solve() {
    int n;
    ll x;
    cin >> n >> x;

    vector<ll> d(2*n);
    for (int i = 0; i < n; i++) cin >> d[i];

    vector<ll> dd(2*n);
    for (int i = 0; i < 2*n; i++) dd[i] = d[i % n];

    ll res = 0;
    ll curd = 0;
    ll curh = 0;
    int l = 0;

    for (int r = 0; r < 2 * n; r++) {
        curd += dd[r];
        curh += (dd[r] * (dd[r] + 1)) / 2;

        while (curd > x) {
            curd -= dd[l];
            curh -= dd[l] * (dd[l] + 1) / 2;
            l++;
        }

        if (curd <= x) {
            if (curd == x) res = max(res, curh);

            if (l > 0) {
                ll k = x - curd;
                ll ex = k * (2 * dd[l-1] - k + 1) / 2;
                res = max(res, curh + ex);
            }
        }
    }

    cout << res << "\n";
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

- **O(n)** — each month is added once and removed at most once by the left pointer
- The "borrowing" step is O(1) per iteration

---

### 🧠 Space Complexity

- **O(n)** — duplicated array `dd` of size `2n`

---

### 🧨 Tricks / Insights

- **Duplicate cyclic arrays** — standard technique for circular problems. Avoids modular arithmetic and wrap-around edge cases.
- **Work with months, not days** — the key insight that makes this O(n) instead of O(total_days).
- **Arithmetic progression for partial months** — `k*(2*d - k + 1)/2` for the last `k` days of a month of length `d`.
- **Borrowing from the left** — when the window has fewer than `x` days, peek at the previous month without actually moving the window. This is a "virtual" extension.
- **Guard against `l == 0`** — when `l` is at the start, there's no previous month to borrow from.
- **Use `long long`** — total hugs can reach `~10^11`, which overflows 32-bit `int`.

---

### 🔗 Related Concepts

- **Sliding window / Two pointers** — maintaining a valid window while expanding right and shrinking left
- **Circular array handling** — duplication technique
- **Arithmetic progression sums** — `1 + 2 + ... + n = n*(n+1)/2`
- **Prefix sums** — alternative approach using binary search (O(n log n))

---

### 🧪 Testing

- **1909 local tests** generated via `gen_tests.py` (edge cases + random with brute force validator)
- All 1909 tests passed — solution matches expected output on every case
- Test files: `tests_input.txt`, `tests_expected.txt`, `run_tests.py`

---

### 📝 Why this problem is 1900

The difficulty comes from three things:
1. **Seeing that you must work with months, not days** — the naive approach is tempting but impossible due to constraints.
2. **Handling partial months correctly** — different formulas for "first k" and "last k" days, and the "borrowing" trick is non-obvious.
3. **Cyclicality** — the year wraps around, requiring either duplication or modular indexing.

The sliding window itself is straightforward once the structure is understood, but getting there requires careful analysis of the problem constraints.
