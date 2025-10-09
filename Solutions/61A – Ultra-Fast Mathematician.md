# ⚡ Codeforces 61A – Ultra-Fast Mathematician
## 📌 Problem Statement
You are given two binary strings s1 and s2 of the same length.
You need to construct a new string s3 of the same length, where each character is determined as follows:

- If the corresponding bits in s1 and s2 are the same → the result is 0.
- If the corresponding bits are different → the result is 1.
- In other words, the result is the bitwise XOR of the two binary strings.
- Input Two binary strings s1 and s2 (1 ≤ |s1| = |s2| ≤ 100).
- Output Print the resulting binary string s3.

## 💡 Idea of the Solution
The task is equivalent to applying the XOR operation on each pair of corresponding characters in the two strings.

- If s1[i] == s2[i] → output 0.
- Else → output 1.

## 🔎 Step‑by‑Step Explanation

- Read the two binary strings.
- Iterate over their characters.
- Compare each pair of characters:
- If equal → print 0.
- If different → print 1.
- Concatenate results into the final string.

## ✅ C++17 Implementation 1.1
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1, s2;
    cin >> s1 >> s2;

    for (size_t i = 0; i < s1.size(); ++i) {
        if (s1[i] == s2[i])
            cout << '0';
        else
            cout << '1';
    }
    cout << endl;

    return 0;
}
```

## ✅ C++17 Implementation 1.2
```cpp

#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
#include <cctype>
#include <map>

using namespace std;

int main() {
	string s1, s2;
	cin >> s1 >> s2;

	for (size_t i = 0; i < s1.size(); ++i) {
		cout << ((int)s1[i] ^ (int)s2[i]);
	}
	cout << endl;


    return 0;
}
```

## 📝 Notes
- Time complexity: O(n), where n is the length of the strings.
- Memory complexity: O(1), since we only store the strings and output directly.
- This is a direct implementation of the XOR logic for binary strings.


---
