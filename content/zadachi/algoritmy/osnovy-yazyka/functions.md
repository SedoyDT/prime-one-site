---
publish: true
title: "Задача: Функции и область видимости"
---

# Задача: Функции и область видимости

Напишите функцию `isPrime(n)`, возвращающую `true`, если число простое.

<details>
<summary>Решение</summary>

```js
function isPrime(n) {
  if (n < 2) return false;
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}

console.log(isPrime(17), isPrime(18)); // true false
```

</details>
