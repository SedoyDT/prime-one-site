---
publish: true
title: "Задача: Массивы: основы"
---

# Задача: Массивы: основы

Дан массив чисел. Найдите максимальный элемент без использования `Math.max`.

<details>
<summary>Решение</summary>

```js
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
  }
  return max;
}

console.log(findMax([3, 7, 2, 9, 4])); // 9
```

</details>
