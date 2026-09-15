---
publish: true
title: "Задача: Стек и очередь"
---

# Задача: Стек и очередь

Используя стек, проверьте, сбалансированы ли скобки в строке, например `"([{}])"` — true, `"([)]"` — false.

<details>
<summary>Решение</summary>

```js
function isBalanced(str) {
  const pairs = { ")": "(", "]": "[", "}": "{" };
  const stack = [];
  for (const ch of str) {
    if (ch === "(" || ch === "[" || ch === "{") stack.push(ch);
    else if (pairs[ch]) {
      if (stack.pop() !== pairs[ch]) return false;
    }
  }
  return stack.length === 0;
}

console.log(isBalanced("([{}])"), isBalanced("([)]")); // true false
```

</details>
