# Основи функцій у JavaScript

## Загальна інформація

- **Опис**: Функції — це блоки коду, які можна повторно використовувати для виконання певних завдань.
- **Типи оголошення**:
  - **Function Declaration**: `function name() {}` — підлягає підняттю (hoisting).
  - **Function Expression**: `const fn = function() {}` — не піднімається.
  - **Arrow Function**: `() => {}` — сучасний синтаксис із фіксованим `this`.
- **Параметри**:
  - Значення за замовчуванням: `function fn(a = 1) {}`.
  - Rest-параметри: `function fn(...args) {}`.
  - Деструктуризація: `function fn({ a }) {}`.
- **Колбеки**: Функція, передана як аргумент для виклику в іншій функції.
- **Особливості**:
  - Підняття (hoisting) працює лише для оголошень.
  - `arguments` — псевдомасив у звичайних функціях (не в стрілкових).
  - Функції є `truthy`, оскільки є об’єктами.
  - Методи: `call()`, `apply()`, `bind()` для управління `this`.
- **Контекст**: Використовуються для логіки, обробки подій, асинхронності.

## Приклади коду

### Оголошення та вирази

```javascript
// Declaration
function greet(name) {
  return `Hello, ${name}`;
}
console.log(greet("Alice")); // Hello, Alice

// Expression
const add = function (a, b) {
  return a + b;
};
console.log(add(2, 3)); // 5

// Зміна контексту з call
const obj = { value: 10 };
function getValue() {
  return this.value;
}
console.log(getValue.call(obj)); // 10
```

### Параметри

```javascript
// Значення за замовчуванням
function fn(a = 0, b = a * 2) {
  return [a, b];
}
console.log(fn(1)); // [1, 2]
console.log(fn()); // [0, 0]

// Rest-параметри
function fn2(...args) {
  return args.reduce((sum, x) => sum + x, 0);
}
console.log(fn2(1, 2, 3)); // 6

// Деструктуризація
function fn3({ name, age = 18 } = {}) {
  return `${name}, ${age}`;
}
console.log(fn3({ name: "Bob" })); // Bob, 18
```

### Колбеки

```javascript
function process(arr, callback) {
  return callback(arr);
}
console.log(process([1, 2, 3], (arr) => arr.map((x) => x * 2))); // [2, 4, 6]

// Колбек із затримкою
setTimeout(() => console.log("Done"), 1000);
```

### Методи контексту

```javascript
const obj2 = { value: 5 };
function multiply(factor) {
  return this.value * factor;
}
console.log(multiply.call(obj2, 2)); // 10
console.log(multiply.apply(obj2, [3])); // 15
const bound = multiply.bind(obj2);
console.log(bound(4)); // 20
```

## Особливості для співбесід — Питання та відповіді

### У чому різниця між оголошенням і виразом функції?

- **Відповідь**: Оголошення піднімається, вираз — ні. Оголошення має ім’я, вираз може бути анонімним.
  ```javascript
  console.log(fn1()); // "OK"
  function fn1() {
    return "OK";
  }
  console.log(fn2()); // Error
  const fn2 = function () {
    return "OK";
  };
  ```

### Як працюють rest-параметри?

- **Відповідь**: Збирають усі аргументи в масив після вказаних параметрів.
  ```javascript
  function fn(...args) {
    return args;
  }
  console.log(fn(1, 2, 3)); // [1, 2, 3]
  ```

### Що таке колбек і як його передати?

- **Відповідь**: Колбек — функція як аргумент. Передається напряму.
  ```javascript
  function exec(callback) {
    callback();
  }
  exec(() => console.log("Колбек!"));
  ```

### Як працює `call`, `apply`, `bind`?

- **Відповідь**: `call` і `apply` викликають функцію з заданим `this`, `bind` створює нову прив’язану функцію.
  ```javascript
  const obj = { x: 10 };
  function show() {
    return this.x;
  }
  console.log(show.call(obj)); // 10
  console.log(show.apply(obj)); // 10
  const boundShow = show.bind(obj);
  console.log(boundShow()); // 10
  ```

### Чи можна змінити `this` у стрілковій функції?

- **Відповідь**: Ні, `this` фіксоване і залежить від зовнішнього контексту.
  ```javascript
  const fn = () => this;
  console.log(fn()); // globalThis
  ```

## Поради

- **Використовуйте значення за замовчуванням**: Уникайте `undefined` у параметрах.
- **Перевіряйте аргументи**: Використовуйте деструктуризацію для зручності.
- **Уникайте `arguments`**: Замінюйте rest-параметрами (`...args`).
- **Керуйте `this`**: Використовуйте `bind` для стабільного контексту.
- **Оптимізуйте колбеки**: Передавайте лише необхідні функції.
- **Тестуйте hoisting**: Розумійте підняття для оголошень.
- **Документуйте**: Додавайте коментарі до складних функцій.
