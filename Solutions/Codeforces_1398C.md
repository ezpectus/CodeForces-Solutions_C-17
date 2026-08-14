# 🧩 Problem: Good Subarrays
## 🔢 Number: Codeforces 1398C
**Difficulty**: ⚡ Prefix Sums + Hash Map (Rating 1600)
**Language**: C++17
**Status**: ✅ Solved — passed 2000 local tests, ready to submit

---

## 📜 Problem Overview

You are given an array `a[1..n]` of digits (0–9), provided as a string.
A subarray `a[l..r]` is called **good** if the sum of its elements equals its length:

```
sum(a[l..r]) = r - l + 1
```

Count the total number of good subarrays.

**Example:** `a = [1, 2, 0]` (string `"120"`)
- `[1]` — sum 1, length 1 → ✅
- `[2, 0]` — sum 2, length 2 → ✅
- `[1, 2, 0]` — sum 3, length 3 → ✅

Answer: **3**

---

### 🔢 Constraints
- `1 ≤ t ≤ 1000` — number of test cases
- `1 ≤ n ≤ 10^5` — length of array per test
- `sum of n over all test cases ≤ 10^5`
- Array elements are digits `0–9`
- Time limit: 2 seconds, Memory: 256 MB

---

## 🧠 Explanation

### Why naive O(N²) doesn't work

Checking every subarray pair `(l, r)` is `O(N²)`. For `N = 10^5` that's `10^10` operations — way too slow for 2 seconds. We need `O(N)` or `O(N log N)`.

### The mathematical trick

**Step 1.** Introduce prefix sums: `P[i] = a[1] + a[2] + ... + a[i]`, with `P[0] = 0`.

```
sum(a[l..r]) = P[r] - P[l-1]
```

**Step 2.** Substitute into the condition "sum = length":

```
P[r] - P[l-1] = r - (l - 1)
```

**Step 3.** Regroup — all `r` terms left, all `l-1` terms right:

```
P[r] - r = P[l-1] - (l - 1)
```

**Step 4.** Define `B[i] = P[i] - i`. The condition collapses to:

```
B[r] = B[l-1]
```

**Step 5.** The problem is now: count pairs `(i, j)` where `i < j` and `B[i] == B[j]`.
This is a classic "count equal pairs" problem — one pass with a hash map.

### Base case: why count[0] = 1?

`B[0] = P[0] - 0 = 0`. The empty prefix (index 0) has value 0.
We set `count[0] = 1` before the loop so that subarrays starting at `l = 1`
(where `l - 1 = 0`) are correctly counted. Without this, we'd miss every good
subarray that starts at the first element.

### Overflow: why long long?

Worst case: all `1`s → every subarray is good → answer = `N*(N+1)/2`.
For `N = 10^5`: `~5 * 10^9` — overflows 32-bit `int` (max `~2.1 * 10^9`).
`long long` (max `~9.2 * 10^18`) is required.

---

## ⚙️ Algorithm Steps

1. Read `t` — number of test cases
2. For each test case:
   - Read `n` and string `s`
   - Build prefix sum array: `pref[0] = 0`, `pref[i+1] = pref[i] + (s[i] - '0')`
   - Initialize `map<int, int> count` with `count[0] = 1`
   - Initialize `long long res = 0`
   - For `i = 1` to `n`:
     - Compute `d = pref[i] - i` (this is `B[i]`)
     - Add `count[d]` to `res` (number of previous indices with same `B` value)
     - Increment `count[d]`
   - Output `res`

---

## 🧾 Code
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <map>

using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        string s;
        cin >> s;

        // pref[i] = sum of first i elements. pref[0] = 0 (empty prefix).
        // Size n+1: indices 0..n. 0 = initial value.
        vector<int> pref(n + 1, 0);
        for (int i = 0; i < n; i++)
            pref[i + 1] = pref[i] + (s[i] - '0');

        // map: B value -> how many times seen so far
        map<int, int> count;
        // B[0] = P[0] - 0 = 0. Empty prefix already exists once.
        count[0] = 1;

        long long res = 0;
        for (int i = 1; i <= n; i++) {
            int d = pref[i] - i;   // B[i]
            res += count[d];       // how many previous B values match
            count[d]++;
        }
        cout << res << endl;
    }
    return 0;
}
```

---

## ✅ Complexity, Insights & Notes

---

### ⏱ Time Complexity

- **O(N log N) per test** — one pass through the array, each `map` operation is `O(log N)`
- Using `unordered_map` instead of `map` would make it **O(N)** average, but `map` is fast enough for `N = 10^5`
- Total across all tests: `O(sum_n * log(max_n))` — well within 2 seconds

---

### 🧠 Space Complexity

- **O(N)** — prefix sum array of size `N+1` + map storing up to `N+1` distinct `B` values
- Can be reduced to **O(N)** just for the map if prefix sum is computed on the fly (see commented `solve()` variant in solution.cpp)

---

### 🧨 Tricks / Insights

- **Prefix sum + algebraic transformation**:  
  The core trick is rewriting `sum = length` as `B[r] = B[l-1]` where `B[i] = P[i] - i`.
  This converts a subarray problem into a "count equal pairs" problem.

- **Reduction to counting equal pairs**:  
  Once you have `B[r] = B[l-1]`, the problem becomes identical to "count pairs with equal values"
  — a classic hash map pattern. One pass, add `count[val]` to answer, then increment `count[val]`.

- **Base case initialization (count[0] = 1)**:  
  The empty prefix `B[0] = 0` must be seeded into the map before the loop.
  Forgetting this is the most common source of Wrong Answer — you lose all good subarrays
  that start at index 1.

- **long long for the answer**:  
  At `N = 10^5` with all `1`s, the answer is `~5 * 10^9` — overflows `int`.
  Always use `long long` for the result variable.

- **Input as string, not integers**:  
  The array is given as a string of digits (`"120"` not `1 2 0`).
  Convert each character with `s[i] - '0'`.

---

### 🔗 Related Concepts

- **Prefix sums** — converting range sum queries into point differences
- **Hash map frequency counting** — counting pairs/groups with equal values in one pass
- **Algebraic manipulation** — rearranging equations to simplify conditions
- **Overflow awareness** — knowing when `int` is not enough and `long long` is needed

---

### 🧪 Testing

- **2000 local tests** generated via `gen_tests.py` (edge cases + random)
- Brute force `O(N²)` reference solution in Python used to compute expected answers
- All 2000 tests passed — solution matches expected output on every case
- Test files: `tests_input.txt`, `tests_expected.txt`

---

### 📝 Notes on the solve() variant

The commented-out variant in `solution.cpp` uses:
- `ios_base::sync_with_stdio(false)` + `cin.tie(NULL)` — faster I/O (3-5x)
- Separate `solve()` function — cleaner code structure
- Prefix sum computed on the fly (no array) — saves memory

Both variants produce identical results. The acceleration is not strictly needed
for this problem but is a good habit for harder problems with tight time limits.
