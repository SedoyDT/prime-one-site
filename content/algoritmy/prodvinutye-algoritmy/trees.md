---
publish: true
title: "Задача: Деревья и бинарные деревья поиска"
---

# Задача: Деревья и бинарные деревья поиска

Напишите функцию `inorderTraversal(node)`, возвращающую значения BST в отсортированном порядке (обход "left → node → right").

<details>
<summary>Решение</summary>

```js
function inorderTraversal(node, result = []) {
  if (!node) return result;
  inorderTraversal(node.left, result);
  result.push(node.value);
  inorderTraversal(node.right, result);
  return result;
}

console.log(inorderTraversal(root)); // [1, 3, 4, 5, 8]
```

</details>
