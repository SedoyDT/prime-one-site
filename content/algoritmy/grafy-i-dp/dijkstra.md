---
publish: true
title: "Задача: Кратчайшие пути: алгоритм Дейкстры"
---

# Задача: Кратчайшие пути: алгоритм Дейкстры

Модифицируйте функцию так, чтобы она возвращала не только расстояния, но и сам кратчайший путь (список вершин) от `start` до заданной вершины.

<details>
<summary>Решение</summary>

```js
function dijkstraWithPath(graph, start) {
  const dist = {}, prev = {};
  for (const node in graph) dist[node] = Infinity;
  dist[start] = 0;
  const visited = new Set();

  while (visited.size < Object.keys(graph).length) {
    let current = null;
    for (const node in dist) {
      if (!visited.has(node) && (current === null || dist[node] < dist[current])) current = node;
    }
    if (current === null || dist[current] === Infinity) break;
    visited.add(current);
    for (const [neighbor, weight] of graph[current]) {
      const newDist = dist[current] + weight;
      if (newDist < dist[neighbor]) { dist[neighbor] = newDist; prev[neighbor] = current; }
    }
  }

  function pathTo(target) {
    const path = [];
    let cur = target;
    while (cur !== undefined) { path.unshift(cur); cur = prev[cur]; }
    return path;
  }
  return { dist, pathTo };
}

const { pathTo } = dijkstraWithPath(graph, "A");
console.log(pathTo("D")); // ["A", "C", "B", "D"]
```

</details>
