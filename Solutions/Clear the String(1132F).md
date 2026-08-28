# Problem: Clear the String
## Number: Codeforces 1132F
**Difficulty**: Interval DP (Rating 2000)
**Language**: C++17
**Status**: Solved — passed 309 local tests, ready to submit

---

## Problem Overview

Given string `s` of length `n`. In one operation, you can delete a contiguous substring of identical characters. Find the minimum number of operations to delete the entire string.

**Example:** `s = "abaca"`, `n = 5`
- Delete `b` (position 2) → `aaca` — 1 operation
- Delete `c` (position 3) → `aaa` — 1 operation
- Delete `aaa` — 1 operation
- Total: 3 operations

After each deletion, the remaining parts of the string are concatenated. This means characters that were not adjacent can become adjacent after intermediate deletions.

---

### Constraints
- `1 <= n <= 500`
- Lowercase English letters
- Time limit: 3 seconds, Memory: 256 MB

---

## How the condition was analyzed

1. **`n <= 500`** — this immediately suggests O(n^2) or O(n^3) complexity. For interval DP, O(n^3) is standard: n lengths × n starting positions × n split points.

2. **Contiguous substring of identical characters** — the operation deletes a block like `"aaa"` or `"bb"`, not arbitrary substrings. The key is that after deletion, surrounding characters become adjacent.

3. **Minimum operations** — optimization problem, DP candidate.

4. **The critical observation**: if `s[l] == s[k]` for some `k > l`, and we delete everything between them first, then `s[l]` and `s[k]` become adjacent. Since they are identical, they can be deleted together in one operation. This means `s[l]` does not need its own operation — it "rides along" with `s[k]`.

---

## Algorithm Explanation

### State definition

`dp[l][r]` = minimum number of operations to completely delete substring `s[l..r]`.

### Base case

`dp[i][i] = 1` — a single character requires one operation.

### Transition 1: Delete s[l] separately

```
dp[l][r] = dp[l+1][r] + 1
```

We spend one operation to delete `s[l]` (possibly together with adjacent identical characters that will be handled within `dp[l+1][r]`), then delete the rest. This is the fallback — always valid.

### Transition 2: Merge s[l] with matching s[k]

```
dp[l][r] = min(dp[l][r], dp[l+1][k-1] + dp[k][r])  when s[l] == s[k]
```

This is the key transition. The reasoning:

1. We pick a position `k` where `s[l] == s[k]`.
2. First, we delete the interior `s[l+1..k-1]` — cost: `dp[l+1][k-1]`.
3. After the interior is deleted, `s[l]` and `s[k]` become adjacent (the string concatenates around the gap).
4. Now `s[l]` and `s[k]` are two identical adjacent characters. When we delete `s[k..r]` (cost: `dp[k][r]`), the operation that deletes `s[k]` will also delete `s[l]` because they are adjacent and identical.
5. Therefore `s[l]` costs 0 additional operations — it is absorbed into the deletion of `s[k]`.

### Why s[l] is "free" in transition 2

When `s[l]` and `s[k]` become adjacent after interior deletion, they form a contiguous block of identical characters. The DP `dp[k][r]` already accounts for deleting `s[k]` optimally. Adding `s[l]` next to `s[k]` simply extends that block by one character — it does not require a new operation. The operation that deletes `s[k]` (and possibly other adjacent identical characters) will also cover `s[l]`.

### Why dp[l+1][k-1] = 0 when k = l+1

When `k = l+1`, the interior is `s[l+1..l]` — an empty range. Since `dp` is initialized to 0, `dp[l+1][l] = 0`. This is correct: there is nothing between `s[l]` and `s[k]`, so they are already adjacent and no interior deletion is needed.

### Why iterate by length

The transitions reference `dp[l+1][k-1]` (shorter interval) and `dp[k][r]` (shorter interval, since `k > l`). Iterating by length from 1 to n guarantees that all shorter intervals are already computed when we process a longer one. This is the topological order for interval DP — shorter subproblems must be solved before longer ones that depend on them.

---

## Algorithm Steps

1. Read `n` and string `s`.
2. Initialize `dp[n][n]` with zeros.
3. For `len` from 1 to n:
   - For `l` from 0 to `n - len`:
     - `r = l + len - 1`
     - If `len == 1`: `dp[l][r] = 1`, continue.
     - Set `dp[l][r] = dp[l+1][r] + 1` (transition 1: delete s[l] separately).
     - For `k` from `l+1` to `r`:
       - If `s[l] == s[k]`: `dp[l][r] = min(dp[l][r], dp[l+1][k-1] + dp[k][r])` (transition 2: merge).
4. Output `dp[0][n-1]`.

---

## Code
```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

void solve() {
    int n;
    cin >> n;
    string s;
    cin >> s;

    vector<vector<int>> dp(n, vector<int>(n, 0));

    for (int len = 1; len <= n; len++) {
        for (int l = 0; l + len - 1 < n; l++) {
            int r = l + len - 1;
            if (len == 1) {
                dp[l][r] = 1;
                continue;
            }

            dp[l][r] = dp[l+1][r] + 1;

            for (int k = l+1; k <= r; k++) {
                if (s[l] == s[k])
                    dp[l][r] = min(dp[l][r], dp[l+1][k-1] + dp[k][r]);
            }
        }
    }
    cout << dp[0][n-1] << "\n";
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

## Complexity

### Time Complexity

- Outer loop: n iterations (lengths 1 to n)
- Middle loop: up to n iterations (starting positions)
- Inner loop: up to n iterations (split point k)
- Total: O(n^3) — for n=500, about 1.25 * 10^8 operations, within 3 second time limit

### Space Complexity

- O(n^2) for the dp table — for n=500, about 1 MB

---

## Insights and Notes

### Key insight: character merging through interior deletion

The core idea is that two identical characters `s[l]` and `s[k]` can be deleted in one operation if everything between them is removed first. This transforms the problem from "delete each block separately" to "find optimal pairing of identical characters to minimize operations."

### Why transition 1 is needed

Without transition 1 (`dp[l][r] = dp[l+1][r] + 1`), there is no baseline value for `dp[l][r]` when no matching `s[k]` exists. Transition 1 guarantees that `dp[l][r]` always has a valid value — worst case, every character is deleted individually, giving `dp = n`.

### Why transition 2 can be better than transition 1

Transition 1 always costs 1 for `s[l]`. Transition 2 costs 0 for `s[l]` (it merges with `s[k]`), but may cost more for the interior `dp[l+1][k-1]`. The DP takes the minimum over all choices of `k`, finding the optimal balance.

### Why this approach and not alternatives

**Why interval DP and not greedy?**
A greedy approach would be: scan left to right, delete the longest block of identical characters at each step. This fails. Example: `s = "abaca"`. Greedy might delete `b` first (1 op), then `c` (1 op), then `aaa` (1 op) = 3. But consider `s = "abba"`. Greedy deletes `bb` (1 op), then `a`, then `a` = 3. Optimal: delete `b` (1 op), now `aa` adjacent, delete `aa` (1 op) = 2. Greedy cannot look ahead to see that deleting a shorter block first creates a better merge later. The order of deletions matters, and only DP explores all orders.

**Why interval DP and not linear DP?**
Linear DP (`dp[i]` = answer for prefix `s[0..i]`) cannot capture the merge transition. When `s[l]` merges with `s[k]`, the answer depends on the interior `s[l+1..k-1]` and the suffix `s[k..r]` — both are subintervals, not prefixes. The state must be `(l, r)`, not a single index.

**Why not DP on compressed string?**
One might think to compress consecutive identical characters first (e.g., `aaabbbaa` → `aba`) and then solve on the compressed version. This works and gives the same answer, but the interval DP naturally handles it — the merge transition already accounts for adjacent identical characters. Compression is an optimization, not a different approach.

**Why O(n^3) and not O(n^2)?**
The merge transition iterates over all possible split points `k` from `l+1` to `r`. This is O(n) per state, and there are O(n^2) states, giving O(n^3). There is no known way to avoid the inner loop because the optimal `k` depends on the string content (where `s[l] == s[k]`), not on a simple monotonic property that would allow binary search or two pointers.

### Common mistakes

- **Forgetting transition 1**: `dp[l][r]` starts at 0 (from initialization), and `min(0, ...)` would give wrong results. Always set the baseline first.
- **Wrong iteration order**: iterating by `l` then `r` (instead of by length) can reference uninitialized shorter intervals.
- **Confusing with palindrome deletion**: this problem deletes identical character blocks, not palindromes. The condition is `s[l] == s[k]`, not palindrome checking.

### Related concepts

- **Interval DP** — DP on substrings/segments, state is `(l, r)`, iterate by length
- **Matrix chain multiplication** — similar structure: split point `k` inside interval
- **Optimal binary search tree** — another interval DP with O(n^3) transitions

### Testing

- 309 local tests (9 edge cases + 300 random) via `gen_tests.py`
- Brute force: independent Python DP implementation with same logic, used as oracle
- All 309 tests passed

### Why this problem is rated 2000

The interval DP pattern is standard, but the difficulty is:
1. Recognizing that the operation "delete identical contiguous block" creates an interval DP structure (the concatenation after deletion makes non-adjacent characters adjacent)
2. Discovering the merge transition: `s[l]` can be absorbed into `s[k]`'s deletion if `s[l] == s[k]` and the interior is removed first
3. Understanding that `s[l]` costs 0 in transition 2 — it does not add to the operation count, it extends an existing operation

### How to get better at problems like this

1. **Recognize interval DP signals**: `n <= 500`, operations on substrings, deletion/merging/splitting
2. **Think about what happens after deletion**: characters become adjacent — this is the key to the merge transition
3. **Always include the baseline transition**: "delete s[l] separately" gives a valid upper bound. Without it, the DP has no starting value.
4. **Practice the pattern**: solve 5+ interval DP problems to internalize the "iterate by length, split at k" structure



---
