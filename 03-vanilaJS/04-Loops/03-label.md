# Мітки та загальні концепції циклів у JavaScript

## Загальна інформація

- **Опис**: Мітки (`label`) дозволяють позначати цикли або блоки коду для керування виконанням за допомогою `break` і `continue`. Цикли є ключовим механізмом для повторення коду в JavaScript.
- **Мітки**:
  - Використовуються для позначення циклів або блоків, щоб `break` або `continue` могли впливати на зовнішні цикли.
  - Синтаксис: `labelName: statement`.
- **Типи циклів**:
  - `for`, `while`, `do...while` (детально описані в інших конспектах).
  - Ітерація по об’єктах і масивах також може використовувати `for...in`, `for...of` (не розглядаються тут).
- **Особливості**:
  - Мітки рідко використовуються в сучасному коді через складність і можливі альтернативи (наприклад, функції).
  - Цикли залежать від falsy/truthy значень для умов завершення.
  - Некоректне керування циклами може призвести до нескінченних циклів або помилок.
- **Контекст**: Мітки корисні у вкладених циклах, а цикли загалом застосовуються для обробки даних, ітерацій і автоматизації.

## Приклади коду

### Використання міток із `break`

```js
outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) break outerLoop;
    console.log(i, j); // 0 0, 0 1, 0 2, 1 0
  }
}
```

### Використання міток із `continue`

```js
outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (j === 1) continue outerLoop;
    console.log(i, j); // 0 0, 1 0, 2 0
  }
}
```

### Загальні концепції циклів

```js
// Обробка масиву
let arr = [1, 2, 3];
let sum = 0;
for (let i = 0; i < arr.length; i++) {
  sum += arr[i];
}
console.log(sum); // 6

// Використання while для невизначеної кількості ітерацій
let input = "yes";
while (input === "yes") {
  input = prompt("Продовжити? (yes/no)");
}
```

## Особливості для співбесід — Питання та відповіді

### Для чого потрібні мітки в JavaScript?

- Мітки дозволяють `break` або `continue` впливати на зовнішні цикли у вкладених структурах.
  ```js
  outer: for (let i = 0; i < 2; i++) {
    for (let j = 0; j < 2; j++) {
      break outer; // Виходить із зовнішнього циклу
    }
  }
  ```

### Чому мітки рідко використовуються?

- Вони ускладнюють читабельність і можуть бути замінені функціями, ранніми поверненнями або рефакторингом.
  ```js
  // Без міток
  function processArray(arr) {
    for (let i = 0; i < arr.length; i++) {
      if (arr[i] === 0) return;
      console.log(arr[i]);
    }
  }
  ```

### Які типові помилки в циклах?

- Нескінченні цикли через незмінну умову.
- Неправильна робота з межами масиву (вихід за межі).
  ```js
  let i = 0;
  while (i < 3) {
    console.log(i); // Нескінченний цикл, якщо забути i++
  }
  ```

### Як falsy/truthy впливають на цикли?

- Умови циклів приводяться до булевого значення. Falsy значення зупиняють цикл.
  ```js
  let value = "";
  while (value) {
    console.log("Не виконається");
  }
  ```

## Поради

- **Уникай міток**: Замість них використовуй функції або реструктуризуй код для простоти.
- **Перевіряй умови завершення**: Уникай нескінченних циклів, додаючи лічильники або чіткі умови.
- **Оптимізуй цикли**: Використовуй `break` для раннього виходу і `continue` для пропуску непотрібних ітерацій.
- **Використовуй сучасні методи**: Для масивів розглядай `forEach`, `map`, `filter` замість класичних циклів.
- **Тестуй із крайніми випадками**: Перевіряй поведінку з порожніми масивами, `null` або `undefined`.
