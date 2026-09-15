---
publish: true
title: "Задача: DP продвинутый: задача о рюкзаке"
---

# Задача: DP продвинутый: задача о рюкзаке

Модифицируйте решение, чтобы оно возвращало не только максимальную ценность, но и список индексов выбранных предметов (восстановление пути по таблице DP).

<details>
<summary>Решение</summary>

```js
function knapsackWithItems(weights, values, capacity) {
  const n = weights.length;
  const dp = Array.from({ length: n + 1 }, () => new Array(capacity + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      dp[i][w] = weights[i - 1] > w
        ? dp[i - 1][w]
        : Math.max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
    }
  }

  const chosen = [];
  let w = capacity;
  for (let i = n; i > 0; i--) {
    if (dp[i][w] !== dp[i - 1][w]) {
      chosen.push(i - 1);
      w -= weights[i - 1];
    }
  }
  return { best: dp[n][capacity], items: chosen.reverse() };
}

console.log(knapsackWithItems([2, 3, 4, 5], [3, 4, 5, 6], 5));
// { best: 7, items: [0, 1] }
```

</details>
