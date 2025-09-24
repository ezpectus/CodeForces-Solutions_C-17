# 🧩 Codeforces 50A — Domino Piling / Укладка доминошками

## 📌 Problem / Условие

Given a rectangle of size ```m*n```,  
you need to cover it with dominoes of size ```2*1```, without overlaps or going out of bounds.  
What’s the maximum number of dominoes you can place?

Дано прямоугольное поле размером  ```m*n```.  
Нужно покрыть его доминошками размером  ```2*1```, не перекрывая и не выходя за границы.  
Сколько максимум доминошек можно уложить?

## 💡 Idea / Идея

Each domino covers 2 cells.  
So the maximum number is simply ```m*n /2```.  
No checks needed — just compute.

Каждая доминошка занимает 2 клетки.  
Значит, максимум можно уложить ```m*n /2``` штук.  
Никаких проверок — просто считаем.

## 💻 Code (C++17)

```cpp
#include <iostream>
using namespace std;

int main() {
    int m, n;
    cin >> m >> n;
    cout << m * n / 2 << endl;
    return 0;
}

```
## 🧪 Тесты

| Ввод      | Вывод   |
|-----------|---------|
| `2 4`     | `4`     |
| `3 3`     | `4`     |
| `1 1`     | `0`     |
| `999 999` | `499000`|

## 🧠 Conclusion / Вывод
- Architecturally — this is a formula task, not an algorithm. 
- One-line solution, but with a clear idea. Fixed as a case: “maximum by area divided by 2”

- Архитектурно — задача на формулу, не на алгоритм 
- Решение — одна строка, но с чёткой идеей Фиксируем как кейс: “максимум по площади, делённой на 2”


---
