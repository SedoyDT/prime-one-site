---
publish: true
title: "Задача: Линейный и бинарный поиск"
---

# Задача: Линейный и бинарный поиск

Напишите функцию, находящую первую позицию, где target можно вставить в отсортированный массив, сохранив порядок (аналог `lower_bound`).

<details>
<summary>Решение</summary>

```js
function insertPosition(sortedArr, target) {
  let lo = 0, hi = sortedArr.length;
  while (lo < hi) {
    const mid = Math.floor((lo + hi) / 2);
    if (sortedArr[mid] < target) lo = mid + 1;
    else hi = mid;
  }
  return lo;
}

console.log(insertPosition([1, 3, 5, 7], 4)); // 2
```

</details>
