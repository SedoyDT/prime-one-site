---
publish: true
title: "Задача: Сортировка пузырьком и вставками"
---

# Задача: Сортировка пузырьком и вставками

Реализуйте сортировку вставками.

<details>
<summary>Решение</summary>

```js
function insertionSort(arr) {
  const a = [...arr];
  for (let i = 1; i < a.length; i++) {
    const key = a[i];
    let j = i - 1;
    while (j >= 0 && a[j] > key) {
      a[j + 1] = a[j];
      j--;
    }
    a[j + 1] = key;
  }
  return a;
}

console.log(insertionSort([5, 2, 8, 1])); // [1, 2, 5, 8]
```

</details>
