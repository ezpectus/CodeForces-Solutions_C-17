# Codeforces 339A — Helpful Maths / Математика спешит на помощь

## Problem / Условие

You are given a string representing a sum of digits separated by plus signs, like `"3+2+1"`.  
Your task is to reorder the digits in ascending order and output the result in the same format.

Дана строка, представляющая сумму цифр, разделённых знаками плюс, например `"3+2+1"`.  
Нужно отсортировать цифры по возрастанию и вывести результат в том же формате.

---

## Idea / Идея

We parse the string by skipping `'+'` characters and collecting digits.  
Then we sort the digits and reconstruct the string with `'+'` between them.

Проходим по строке, пропуская символы `'+'`, и собираем цифры.  
Сортируем их и собираем строку обратно, вставляя `'+'` между элементами.

---

## Code (C++17)

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
using namespace std;

int main() {
    string s;
    cin >> s;

    vector<int> v;
    for (size_t i = 0; i < s.size(); i += 2) {
        v.push_back(s[i] - '0');
    }

    sort(v.begin(), v.end());

    for (size_t i = 0; i < v.size(); ++i) {
        if (i > 0) cout << "+";
        cout << v[i];
    }

    cout << endl;
    return 0;
}
```

## Tests / Тесты

| Input / Ввод   | Output / Вывод |
|----------------|----------------|
| `3+2+1`         | `1+2+3`        |
| `1+1+3+1`       | `1+1+1+3`      |
| `2`             | `2`            |

## Conclusion / Вывод

Architecturally — this is a parsing and sorting task on symbolic math.  
The string is treated as a structured expression, not raw input.  
We extract digits, sort them, and reconstruct the expression.

Архитектурно — задача на парсинг и сортировку символьной математики.  
Строка — это структурированное выражение, а не просто ввод.  
Извлекаем цифры, сортируем, собираем обратно.



---
