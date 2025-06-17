# Модулі в JavaScript

## Загальна інформація

- **Опис**: Модулі дозволяють організувати код, розділяючи його на файли з чіткою областю видимості. Вони замінили глобальні змінні та IIFE.
- **Основи**:
  - Файли JavaScript із `type="module"` у `<script>` або з розширенням `.mjs`.
  - Асинхронне завантаження за замовчуванням.
- **Експорт (`export`)**:
  - Іменований: `export const x = 1`.
  - За замовчуванням: `export default function() {}`.
  - Реекспорт: `export { x } from 'module'`.
- **Імпорт (`import`)**:
  - Іменований: `import { x } from './file.js'`.
  - За замовчуванням: `import x from './file.js'`.
  - Динамічний: `import('./file.js').then(module => ...)`.
- **Особливості**:
  - Область видимості обмежена модулем (немає глобальних конфліктів).
  - Підтримує цикли залежностей, але з обережністю.
  - **Falsy/Truthy**: Залежить від імпортованих даних (наприклад, `null` falsy).
- **Контекст**: Організація великих проєктів, повторне використання коду.

## Приклади коду

### Файл `math.js` (експорт)

```javascript
// Іменований експорт
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Експорт за замовчуванням
export default function multiply(a, b) {
  return a * b;
}

// Реекспорт
export { divide } from "./utils.js";
```

### Файл `main.js` (імпорт)

```javascript
// Іменований імпорт
import { add, subtract } from "./math.js";
console.log(add(2, 3)); // 5
console.log(subtract(5, 2)); // 3

// Імпорт за замовчуванням
import multiply from "./math.js";
console.log(multiply(2, 3)); // 6

// Змішаний імпорт
import multiply, { add } from "./math.js";
console.log(multiply(2, 3), add(1, 2)); // 6, 3

// Динамічний імпорт
async function loadModule() {
  const { default: multiply, add } = await import("./math.js");
  console.log(multiply(2, 3), add(1, 2)); // 6, 3
}
loadModule();
```

### Використання в HTML

```html
<script type="module" src="main.js"></script>
```

### Експорт класу

```javascript
// file.js
export class Calculator {
  add(a, b) {
    return a + b;
  }
}

// main.js
import { Calculator } from "./file.js";
const calc = new Calculator();
console.log(calc.add(2, 3)); // 5
```

## Особливості для співбесід — Питання та відповіді

### У чому різниця між `export` і `export default`?

- `export` дозволяє експортувати кілька іменованих елементів, `export default` — лише один за замовчуванням.
  ```javascript
  // math.js
  export const x = 1; // Іменований
  export default function () {} // За замовчуванням
  // main.js
  import { x } from "./math.js"; // Іменований
  import fn from "./math.js"; // За замовчуванням
  ```

### Як працює динамічний імпорт?

- Повертає Promise, дозволяє асинхронне завантаження.
  ```javascript
  import("./math.js").then(({ add }) => console.log(add(2, 3))); // 5
  ```

### Чи можна імпортувати модулі без `type="module"`?

- Ні, у браузері потрібно явно вказати `type="module"`, інакше JS інтерпретується як скрипт.
  ```html
  <script type="module" src="main.js"></script>
  <!-- Модуль -->
  <script src="main.js"></script>
  <!-- Скрипт -->
  ```

### Як уникнути циклічних залежностей?

- Розділяйте логіку, використовуйте ледачий імпорт.
  ```javascript
  // moduleA.js
  export const a = 1;
  import { b } from "./moduleB.js";
  // moduleB.js
  export const b = 2;
  import { a } from "./moduleA.js"; // Цикл, може викликати помилку
  ```

### Чи підлягають модулі підняттю?

- Ні, імпорти виконуються до коду модуля, але не піднімаються як `var`.
  ```javascript
  console.log(x); // ReferenceError
  import { x } from "./math.js";
  ```

## Поради

- **Використовуй іменований експорт**: Для чіткості кількох експортів.
- **Експорт за замовчуванням**: Для основного елемента модуля.
- **Динамічний імпорт**: Для умовного завантаження.
- **Уникай глобальних змінних**: Замінюйте їх модулями.
- **Перевіряй залежності**: Уникайте циклів, використовуйте інструменти (Webpack, Rollup).
- **Тестуй асинхронність**: Динамічний імпорт потребує `await` або `.then`.
