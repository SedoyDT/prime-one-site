---
publish: true
title: "Задача: Условные операторы"
---

# Задача: Условные операторы

Дано число `temperature`. Выведите "Заморозки", если temperature <= 0; "Прохладно", если от 1 до 15; "Тепло" — иначе.

<details>
<summary>Решение</summary>

```js
function describeWeather(temperature) {
  if (temperature <= 0) return "Заморозки";
  if (temperature <= 15) return "Прохладно";
  return "Тепло";
}

console.log(describeWeather(-3), describeWeather(10), describeWeather(25));
```

</details>
