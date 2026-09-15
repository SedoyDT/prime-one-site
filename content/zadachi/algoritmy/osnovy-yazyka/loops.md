---
publish: true
title: "Задача: Циклы"
---

# Задача: Циклы

Выведите сумму всех чисел от 1 до 100 без формулы Гаусса — используя цикл.

<details>
<summary>Решение</summary>

```js
let sum = 0;
for (let i = 1; i <= 100; i++) {
  sum += i;
}
console.log(sum); // 5050
```

</details>
