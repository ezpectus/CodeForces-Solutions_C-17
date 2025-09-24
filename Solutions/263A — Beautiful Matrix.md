# Codeforces 263A — Beautiful Matrix / Красивая матрица

## Problem / Условие

You are given a 5×5 matrix with all zeros except a single `1`.  
You can swap adjacent rows or columns.  
Find the minimum number of moves to bring the `1` to the center (position [2][2]).

Дана матрица 5×5, содержащая только один `1`, остальные — `0`.  
Разрешено менять местами соседние строки или столбцы.  
Найти минимальное количество шагов, чтобы переместить `1` в центр — позиция [2][2].

---

## Idea / Идея

We scan the matrix to find the position of `1`.  
Then compute Manhattan distance to center:  
`abs(r - 2) + abs(c - 2)`

Проходим по матрице, находим координаты `1`.  
Считаем расстояние до центра по Манхэттену:  
`abs(r - 2) + abs(c - 2)`

---

## Code (C++17)

```cpp
#include <iostream>
using namespace std;

int main() {
    int r, c;
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            int x;
            cin >> x;
            if (x == 1) {
                r = i;
                c = j;
            }
        }
    }
    cout << abs(r - 2) + abs(c - 2) << endl;
    return 0;
}
```

## Tests / Тесты

| Input / Ввод             | Output / Вывод |
|--------------------------|----------------|
| `0 0 0 0 0`<br>`0 0 0 0 0`<br>`0 0 1 0 0`<br>`0 0 0 0 0`<br>`0 0 0 0 0` | `0` |
| `0 0 0 0 0`<br>`0 0 0 0 0`<br>`1 0 0 0 0`<br>`0 0 0 0 0`<br>`0 0 0 0 0` | `2` |
| `1 0 0 0 0`<br>`0 0 0 0 0`<br>`0 0 0 0 0`<br>`0 0 0 0 0`<br>`0 0 0 0 0` | `4` |

## Conclusion / Вывод

Architecturally — this is a pure Manhattan distance task.  
No simulation, no swaps — just locate and compute.

**What is Manhattan distance?**  
It’s the number of vertical and horizontal steps needed to reach a target cell.  
For a grid, the formula is:
```
distance = abs(current_row - target_row) + abs(current_col - target_col)
```

In this problem, the target is the center of the 5×5 matrix: position `[2][2]`.  
So once we find the `1`, we compute:
```
moves = abs(r - 2) + abs(c - 2)
```


No need to simulate swaps — each swap moves the `1` one step closer to center.  
This formula gives the exact number of moves required.

Архитектурно — задача на чистое расстояние по Манхэттену.  
Никакой симуляции, просто найти и посчитать.


---

