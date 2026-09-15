---
publish: true
title: "Задача: Комбинирование техник: DP на графе (топологическая сортировка + самый длинный путь)"
---

# Задача: Комбинирование техник: DP на графе (топологическая сортировка + самый длинный путь)

Дан DAG со взвешенными рёбрами (список смежности вида `{A: [["B", 3], ["C", 2]]}`). Найдите длину самого длинного пути от вершины `start` до любой другой вершины, используя топологическую сортировку + DP.

<details>
<summary>Решение</summary>

```js
function longestPathDAG(weightedGraph, start) {
  // Топологическая сортировка (тот же DFS-подход, но с учётом весов при обходе не нужен)
  const visited = new Set();
  const order = [];
  function dfs(node) {
    visited.add(node);
    for (const [neighbor] of weightedGraph[node] || []) {
      if (!visited.has(neighbor)) dfs(neighbor);
    }
    order.push(node);
  }
  for (const node in weightedGraph) if (!visited.has(node)) dfs(node);
  const topoOrder = order.reverse();

  const dist = {};
  for (const node in weightedGraph) dist[node] = -Infinity;
  dist[start] = 0;

  for (const node of topoOrder) {
    if (dist[node] === -Infinity) continue; // недостижимо из start
    for (const [neighbor, weight] of weightedGraph[node] || []) {
      if (dist[node] + weight > dist[neighbor]) {
        dist[neighbor] = dist[node] + weight;
      }
    }
  }
  return dist;
}

const weightedDag = {
  A: [["B", 3], ["C", 2]],
  B: [["D", 4]],
  C: [["D", 1]],
  D: [["E", 2]],
  E: []
};

console.log(longestPathDAG(weightedDag, "A"));
// { A: 0, B: 3, C: 2, D: 7, E: 9 }
```

</details>
