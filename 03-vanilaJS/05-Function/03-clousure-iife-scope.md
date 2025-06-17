# Замикання, IIFE та область видимості у JavaScript

## Загальна інформація

- **Опис**: Область видимості визначає доступ до змінних. Замикання дозволяють функціям зберігати доступ до зовнішнього стану. IIFE ізолюють код.
- **Область видимості**:
  - Глобальна, функційна (`var`), блокова (`let`, `const`).
  - Підняття (hoisting): `var` і оголошення функцій піднімаються.
- **Замикання**:
  - Функція, яка "запам’ятовує" лексичне оточення.
- **IIFE**:
  - `(function() {})()` — негайно викликаний вираз функції.
- **Особливості**:
  - `var` створює "підняття" без блоку.
  - Замикання використовуються для приватних даних.
  - IIFE замінюються модулями в сучасному JS.
- **Контекст**: Використовуються для модульності, стану, уникнення конфліктів.

## Приклади коду

### Область видимості

```js
var x = 1;
let y = 2;
{
  var x = 3; // Перезаписує глобальну
  let y = 4; // Локальна
}
console.log(x, y); // 3, 2
```

### Замикання

```js
function counter() {
  let count = 0;
  return () => ++count;
}
const inc = counter();
console.log(inc()); // 1
console.log(inc()); // 2
```

### IIFE

```js
const result = (function () {
  const secret = "hidden";
  return secret;
})();
console.log(result); // hidden
```

## Особливості для співбесід — Питання та відповіді

### Що таке підняття (hoisting)?

- Переміщення оголошень `var` і функцій на вершину області.
  ```js
  console.log(a); // undefined
  var a = 1;
  ```

### Як працює замикання?

- Зберігає доступ до зовнішніх змінних після завершення функції.
  ```js
  function outer() {
    let x = 10;
    return () => x;
  }
  const fn = outer();
  console.log(fn()); // 10
  ```

### Для чого потрібні IIFE?

# Замикання, IIFE та область видимості у JavaScript

## Загальна інформація

- **Опис**: Область видимості визначає доступ до змінних. Замикання дозволяють функціям зберігати доступ до зовнішнього оточення. IIFE (Immediately Invoked Function Expression) ізолюють код.
- **Область видимості**:
  - Глобальна, функційна (`var`), блокова (`let`, `const`).
  - Підняття (hoisting): `var` і функції піднімаються.
- **Замикання**:
  - Функція, яка "запам’ятовує" лексичне оточення, навіть після завершення батьківської функції.
- **IIFE**:
  - `(function() {})()` — негайно викликаний вираз для ізоляції.
- **Особливості**:
  - `var` має функційну область і підняття.
  - Замикання використовуються для приватності (наприклад, лічильники).
  - IIFE замінюються модулями (`import/export`) в ES6+.
- **Контекст**: Використовуються для модульності, керування станом, уникнення конфліктів.

## Приклади коду

### Область видимості

```javascript
// Глобальна vs блокова
var x = 1;
let y = 2;
{
  var x = 3; // Перезапис глобальної
  let y = 4; // Локальна
}
console.log(x, y); // 3, 2

// Підняття
console.log(a); // undefined (hoisting)
var a = 5;
```

### Замикання

```javascript
// Лічильник із замиканням
function createCounter() {
  let count = 0;
  return () => ++count;
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2

// Приватні дані
function createPerson() {
  let name = "Іван";
  return {
    getName: () => name,
    setName: (newName) => {
      name = newName;
    },
  };
}
const person = createPerson();
console.log(person.getName()); // Іван
person.setName("Петро");
console.log(person.getName()); // Петро
```

### IIFE

```javascript
// Ізоляція змінних
const result = (function () {
  const secret = "hidden";
  return secret;
})();
console.log(result); // hidden
console.log(typeof secret); // undefined

// IIFE з параметрами
const module = (function (global) {
  const privateVar = "secret";
  return { get: () => privateVar };
})(window);
console.log(module.get()); // secret
```

## Особливості для співбесід — Питання та відповіді

### Що таке підняття (hoisting)?

- **Відповідь**: Переміщення оголошень `var` і функцій на вершину області видимості.
  ```javascript
  console.log(fn()); // "Hello"
  function fn() {
    return "Hello";
  }
  ```

### Як працює замикання?

- **Відповідь**: Зберігає доступ до зовнішніх змінних після завершення функції.
  ```javascript
  function outer() {
    let x = 10;
    return () => x;
  }
  const fn = outer();
  console.log(fn()); // 10
  ```

### Для чого потрібні IIFE?

- **Відповідь**: Ізоляція змінних, уникнення глобальних конфліктів.
  ```javascript
  (function () {
    var local = 1;
  })();
  console.log(typeof local); // undefined
  ```

### Чим `let` відрізняється від `var`?

- **Відповідь**: `let` блочна, `var` функційна, без підняття для `let`.
  ```javascript
  if (true) {
    let a = 1;
    var b = 2;
  }
  console.log(a); // ReferenceError
  console.log(b); // 2
  ```

### Як замикання впливає на продуктивність?

- **Відповідь**: Може збільшувати пам’ять через збереження оточення, але корисно для стану.
  ```javascript
  function heavyClosure() {
    let data = new Array(1000000).fill(1);
    return () => data.length;
  }
  const fn = heavyClosure();
  console.log(fn()); // 1000000
  ```

## Поради

- **Використовуй `let/const`**: Уникай `var` через підняття і перезапис.
- **Створюй замикання для стану**: Наприклад, для лічильників чи приватних даних.
- **Замінюйте IIFE модулями**: Використовуйте `import/export` у сучасних проєктах.
- **Оптимізуй пам’ять**: Уникайте великих замикань у циклах.
- **Тестуй область видимості**: Перевіряй доступ до змінних у різних блоках.
- **Документуй IIFE**: Пояснюйте їхню мету в коді.
- Ізоляція змінних, уникнення глобальних конфліктів.
  ```js
  (function () {
    var local = 1;
  })();
  console.log(typeof local); // undefined
  ```

### Чим `let` відрізняється від `var`?

- `let` блочна, `var` функційна, без підняття.
  ```js
  if (true) {
    let a = 1;
  }
  console.log(a); // ReferenceError
  ```

## Поради

- **Використовуй `let/const`**: Уникай `var` через підняття.
- **Створюй замикання для стану**: Наприклад, лічильники.
- **Замінюйте IIFE модулями**: Використовуйте `import/export`.
- **Перевіряйте область**: Уникайте неочікуваного доступу до змінних.
- **Тестуй hoisting**: Розумій, де змінні доступні.
