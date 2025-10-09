# 🥤 Codeforces 200B – Drinks
## 📌 Problem Statement
There are n friends. Each of them poured themselves a drink that contains a certain percentage of orange juice. 
You need to determine what percentage of orange juice will be in the final mixture if all drinks are combined together.

Input:

- The first line contains an integer n (1 ≤ n ≤ 100).
- The second line contains n integers p1, p2, …, pn (0 ≤ pi ≤ 100), where pi is the percentage of orange juice in the i‑th drink.

Output:

- Print the percentage of orange juice in the final mixture.
- The answer will be accepted if the absolute or relative error does not exceed 10^-4.

## 💡 Idea of the Solution
The problem reduces to finding the average of the given percentages. 
If each drink has pi percent orange juice, then the final mixture percentage is:
```
result = 𝑝1 + 𝑝2+ ⋯ +𝑝𝑛
         _______________
               𝑛
```
So the algorithm is straightforward:

- Read the number of drinks n.
- Read all percentages and compute their sum.
- Divide the sum by n to get the average percentage.
- Print the result.

## 🔎 Step‑by‑Step Explanation
- Each friend contributes a fraction of orange juice.
- When mixing, the total percentage is just the arithmetic mean.
- Example: if n = 3 and the values are 50 100 0, then
```
50+100+0 = 50
________
  3
```
So the mixture contains 50% orange juice.

✅ C++17 Implementation
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    int sum_p = 0;
    for (int i = 0; i < n; i++) {
        int p;
        cin >> p;
        sum_p += p;
    }

    double avg = static_cast<double>(sum_p) / n;
    cout << avg << endl;

    return 0;
}
```
## 📝 Notes
- Time complexity: O(n) — we just read and sum all values once.
- Memory complexity: O(1) — only a few variables are used.
- Default cout precision is enough to pass this problem on Codeforces.


---
