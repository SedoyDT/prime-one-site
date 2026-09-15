---
publish: true
title: "Задача: Обход графов: BFS и DFS"
---

# Задача: Обход графов: BFS и DFS

Напишите DFS для того же графа, используя рекурсию.

<details>
<summary>Решение</summary>

```js
function dfs(node, visited = new Set(), order = []) {
  visited.add(node);
  order.push(node);
  for (const neighbor of graph[node]) {
    if (!visited.has(neighbor)) dfs(neighbor, visited, order);
  }
  return order;
}

console.log(dfs("A")); // ["A", "B", "D", "C"]
```

</details>
