# Тип undefined у JavaScript

## Основні поняття

- **Опис**: `undefined` — це примітивне значення, яке вказує на **відсутність ініціалізації** змінної, аргументу функції чи поверненого значення.
- **Тип**: `undefined` є окремим примітивним типом (`typeof undefined` повертає `"undefined"`).
- **Falsy значення**: `undefined` завжди приводиться до `false` у логічному контексті.
- **Коли виникає**:
  - Змінна оголошена, але не ініціалізована.
  - Функція не повертає значення (або повертає `return` без значення).
  - Доступ до неіснуючої властивості об’єкта.
  - Аргумент функції не переданий.
- **Порівняння**:
  - Нестрога рівність (`==`): `undefined` дорівнює лише `null` і `undefined`.
  - Строга рівність (`===`): `undefined` дорівнює лише `undefined`.

## Приклади коду

### Використання undefined

```js
let value;
console.log(value); // undefined
console.log(typeof value); // "undefined"

function test() {}
console.log(test()); // undefined

let obj = {};
console.log(obj.someProp); // undefined
```

### Undefined у логічному контексті

```js
if (undefined) {
  console.log("Це не виконається"); // undefined є falsy
} else {
  console.log("undefined є falsy"); // Виведе
}
```

### Порівняння з undefined

```js
console.log(undefined == null); // true
console.log(undefined === null); // false
console.log(undefined == 0); // false
console.log(undefined === undefined); // true
```

## Особливості для співбесід — Питання та відповіді

### Чим відрізняються `undefined` і `null`?

- `undefined` — автоматичне значення для неініціалізованих змінних, невизначених властивостей або функцій без повернення.
- `null` — явне значення, яке програміст присвоює для позначення відсутності значення.
- **Питання**: Який результат `typeof undefined` і `typeof null`?
  - **Відповідь**: `typeof undefined` → `"undefined"`, `typeof null` → `"object"` (історична помилка).

### Чому `undefined == null` повертає `true`?

- При нестрогому порівнянні (`==`) JavaScript вважає `undefined` і `null` еквівалентними.
- При строгому порівнянні (`===`) вони різні через різні типи.
  ```js
  console.log(undefined == null); // true
  console.log(undefined === null); // false
  ```

### Чи безпечно перевизначати `undefined`?

- У старих версіях JavaScript `undefined` можна було перевизначити, але в сучасному коді (`use strict`) це неможливо.
- **Питання**: Що станеться, якщо спробувати змінити `undefined`?
  - **Відповідь**: У строгому режимі це викличе помилку. Без строгого режиму — може призвести до багів.
  ```js
  "use strict";
  // undefined = 42; // TypeError
  ```

### Як перевірити, чи змінна є `undefined`?

- Використовуй `=== undefined` або перевірку `typeof value === "undefined"`.
  ```js
  let x;
  console.log(x === undefined); // true
  console.log(typeof x === "undefined"); // true
  ```

## Поради

- **Уникай явного присвоєння `undefined`**: Залиш `undefined` для автоматичних випадків (неініціалізовані змінні). Для явної відсутності значення використовуй `null`.
- **Використовуй `===` для порівняння**: Нестрога рівність (`==`) може призвести до плутанини через порівняння з `null`.
- **Перевіряй `undefined` перед доступом до властивостей**: Це допоможе уникнути помилок (`TypeError`).
- **Уникай перевизначення `undefined`**: Завжди використовуй строгий режим (`'use strict'`) для безпеки.
