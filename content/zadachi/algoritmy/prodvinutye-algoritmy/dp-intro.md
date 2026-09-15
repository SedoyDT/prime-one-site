---
publish: true
title: "Задача: Динамическое программирование: введение"
---

# Задача: Динамическое программирование: введение

Решите задачу "минимальное число монет": дан набор номиналов монет и сумма, найдите минимальное количество монет, дающих эту сумму (или -1, если невозможно). Используйте tabulation.

<details>
<summary>Решение</summary>

```js
function minCoins(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let sum = 1; sum <= amount; sum++) {
    for (const coin of coins) {
      if (coin <= sum) dp[sum] = Math.min(dp[sum], dp[sum - coin] + 1);
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}

console.log(minCoins([1, 5, 10, 25], 63)); // 6 (25+25+10+1+1+1)
```

</details>
