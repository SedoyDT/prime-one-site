---
publish: true
title: "Задача: Хеш-таблицы (Map / объекты)"
---

# Задача: Хеш-таблицы (Map / объекты)

Найдите первый неповторяющийся символ в строке за O(n), используя хеш-таблицу (вместо O(n²) вложенных циклов).

<details>
<summary>Решение</summary>

```js
function firstUniqueChar(str) {
  const counts = new Map();
  for (const ch of str) counts.set(ch, (counts.get(ch) || 0) + 1);
  for (const ch of str) if (counts.get(ch) === 1) return ch;
  return null;
}

console.log(firstUniqueChar("swiss")); // "w"
```

</details>
