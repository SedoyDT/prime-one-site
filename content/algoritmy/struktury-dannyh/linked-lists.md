---
publish: true
title: "Задача: Связные списки"
---

# Задача: Связные списки

Напишите функцию, разворачивающую связный список на месте (без создания нового списка).

<details>
<summary>Решение</summary>

```js
function reverse(list) {
  let prev = null;
  let cur = list.head;
  while (cur) {
    const next = cur.next;
    cur.next = prev;
    prev = cur;
    cur = next;
  }
  list.head = prev;
  return list;
}
```

</details>
