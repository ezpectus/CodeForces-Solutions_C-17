# Codeforces 112A — Petya and Strings / Петя и строки

## Problem / Условие

You are given two strings of equal length.  
Compare them lexicographically **ignoring case**.  
Print:

- `-1` if the first string is smaller  
- `1` if the first string is greater  
- `0` if they are equal

Даны две строки одинаковой длины.  
Сравнить их лексикографически **без учёта регистра**.  
Вывести:

- `-1`, если первая меньше  
- `1`, если первая больше  
- `0`, если равны

---

## Idea / Идея

Transform both strings to lowercase using `std::transform`.  
Then compare directly using `<`, `>`, `==`.

Преобразуем обе строки в нижний регистр через `std::transform`.  
Сравниваем напрямую через `<`, `>`, `==`.

---

## Code (C++17)

```cpp
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;

int main() {
    string s1, s2;
    cin >> s1 >> s2;
    transform(s1.begin(), s1.end(), s1.begin(), ::tolower);
    transform(s2.begin(), s2.end(), s2.begin(), ::tolower);
    if (s1 < s2) cout << -1 << endl;
    else if (s1 > s2) cout << 1 << endl;
    else cout << 0 << endl;
    return 0;
}
```

## Tests / Тесты

| Input / Ввод | Output / Вывод |
|--------------|----------------|
| `aAa AAA`    | `0`            |
| `abc Abd`    | `-1`           |
| `xyz XYA`    | `1`            |

## Conclusion / Вывод

Architecturally — this is a pure transform-and-compare task.  
No parsing, no loops — just lowercase and compare.  
`std::transform + < > ==` — clean, minimal, scalable.

Архитектурно — задача на преобразование и сравнение.  
Никакого парсинга, просто lowercase и сравнение.  
`transform + < > ==` — чисто, минимально, масштабируемо.


---
