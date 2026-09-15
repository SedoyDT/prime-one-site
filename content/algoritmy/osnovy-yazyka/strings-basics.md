---
publish: true
title: "Задача: Строки: основы и операции"
---

# Задача: Строки: основы и операции

Напишите функцию, проверяющую, является ли строка палиндромом (читается одинаково в обе стороны), без учёта регистра.

<details>
<summary>Решение</summary>

```js
function isPalindrome(str) {
  const clean = str.toLowerCase().replace(/[^a-zа-я0-9]/g, "");
  const reversed = clean.split("").reverse().join("");
  return clean === reversed;
}

console.log(isPalindrome("A man a plan a canal Panama")); // true
```

</details>
