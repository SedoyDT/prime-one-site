---
publish: true
title: "Задача: Быстрая сортировка и сортировка слиянием"
---

# Задача: Быстрая сортировка и сортировка слиянием

Реализуйте быструю сортировку (quick sort).

<details>
<summary>Решение</summary>

```js
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const [pivot, ...rest] = arr;
  const left = rest.filter(x => x < pivot);
  const right = rest.filter(x => x >= pivot);
  return [...quickSort(left), pivot, ...quickSort(right)];
}

console.log(quickSort([5, 2, 8, 1, 9])); // [1, 2, 5, 8, 9]
```

</details>
