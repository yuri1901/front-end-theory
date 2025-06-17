# Об’єкт String у JavaScript

## Загальна інформація

- **Опис**: `String` — це вбудований об’єкт JavaScript для роботи з текстовими даними. Рядки є примітивним типом, але автоматично обгортаються в об’єкт `String` при виклику методів.
- **Рядок**: Послідовність символів, закодованих у UTF-16.
- **Створення рядків**:
  - **Літерали**: `'text'`, `"text"`, `` `text` `` (шаблонні літерали).
  - **Конструктор**: `new String('text')` (створює об’єкт, не рекомендується через неефективність і потенційні помилки при порівнянні).
- **Незмінність (immutable)**: Рядки не можна змінити після створення; методи повертають нові рядки, не змінюючи оригінал.
- **Тип**: Примітивний тип `string` (`typeof 'text' === "string"`), але `typeof new String('text') === "object"`.
- **Falsy значення**: Порожній рядок `""` є falsy, усі непорожні рядки — truthy.

## Створення рядків

```js
let str1 = "Hello"; // Одинарні лапки
let str2 = "World"; // Подвійні лапки
let str3 = `Template: ${str1}`; // Шаблонний літерал
let str4 = new String("Hi"); // Об’єкт String (не рекомендується)

console.log(str1); // Hello
console.log(str3); // Template: Hello
console.log(typeof str1); // string
console.log(typeof str4); // object
```

## Властивості

- **`.length`**: Повертає кількість символів у рядку (включаючи пробіли та спеціальні символи).
  ```js
  console.log("Hello".length); // 5
  console.log("".length); // 0
  console.log("😊".length); // 2 (емодзі займає 2 кодові одиниці UTF-16)
  ```

## Основні методи

### Доступ до символів

- **`at(index)`**: Повертає символ за вказаним індексом. Підтримує негативні індекси (рахунок від кінця рядка). Додано в ECMAScript 2022.
- **`charAt(index)`**: Повертає символ за вказаним індексом (0-based). Якщо індекс поза межами, повертає `""`.
- **`charCodeAt(index)`**: Повертає Unicode-код (UTF-16) символу за індексом. Якщо індекс поза межами, повертає `NaN`.
- **`codePointAt(index)`**: Повертає Unicode code point (краще для емодзі та символів поза BMP). Повертає `undefined`, якщо індекс поза межами.
- **Індексування через `str[index]`**: Альтернатива `charAt`, але не підтримується в дуже старих браузерах.

```js
let str = "Hello 😊";
console.log(str.at(1)); // 'e'
console.log(str.at(-1)); // '😊'
console.log(str.charAt(1)); // 'e'
console.log(str.charCodeAt(1)); // 101 (Unicode для 'e')
console.log(str.codePointAt(6)); // 128522 (Unicode для '😊')
console.log(str[1]); // 'e'
console.log(str.charAt(10)); // ''
console.log(str.codePointAt(10)); // undefined
```

### Пошук у рядку

- **`indexOf(substring, fromIndex)`**: Повертає індекс першого входження підрядка або `-1`, якщо не знайдено.
- **`lastIndexOf(substring, fromIndex)`**: Повертає індекс останнього входження підрядка.
- **`includes(substring, fromIndex)`**: Повертає `true`, якщо підрядок знайдено.
- **`startsWith(substring, fromIndex)`**: Перевіряє, чи починається рядок із підрядка.
- **`endsWith(substring, length)`**: Перевіряє, чи закінчується рядок підрядком.
- **`search(regexp)`**: Повертає індекс першого збігу з регулярним виразом або `-1`.
- **`match(regexp)`**: Повертає масив збігів із регулярним виразом або `null`.
- **`matchAll(regexp)`**: Повертає ітератор усіх збігів із регулярним виразом (з групами, якщо є).

```js
let text = "JavaScript String methods";
console.log(text.indexOf("Script")); // 4
console.log(text.lastIndexOf("s")); // 23
console.log(text.includes("String")); // true
console.log(text.startsWith("Java")); // true
console.log(text.endsWith("methods")); // true
console.log(text.search(/\w+/)); // 0
console.log(text.match(/\w+/g)); // ['JavaScript', 'String', 'methods']
console.log([...text.matchAll(/\w+/g)]); // Масив об’єктів збігів
```

### Зміна регістру

- **`toLowerCase()`**: Перетворює рядок у нижній регістр.
- **`toUpperCase()`**: Перетворює рядок у верхній регістр.
- **`toLocaleLowerCase([locales])`**: Перетворює в нижній регістр із урахуванням локалізації.
- **`toLocaleUpperCase([locales])`**: Перетворює у верхній регістр із урахуванням локалізації.

```js
let str = "Hello";
console.log(str.toLowerCase()); // 'hello'
console.log(str.toUpperCase()); // 'HELLO'
console.log(str.toLocaleLowerCase("tr")); // 'hello' (турецька локалізація)
console.log(str.toLocaleUpperCase("tr")); // 'HELLO'
```

### Вирізання та заміна

- **`slice(start, end)`**: Вирізає підрядок від `start` до `end` (не включно). Підтримує негативні індекси.
- **`substring(start, end)`**: Аналог `slice`, але не підтримує негативні індекси; якщо `start > end`, міняє їх місцями.
- **`substr(start, length)`**: Вирізає підрядок заданої довжини від `start` (застарілий, уникайте).
- **`replace(searchValue, replaceValue)`**: Замінює перше входження підрядка або регулярного виразу.
- **`replaceAll(searchValue, replaceValue)`**: Замінює усі входження (з’явився в ES2021).

```js
let str = "Hello world";
console.log(str.slice(0, 5)); // 'Hello'
console.log(str.slice(-5)); // 'world'
console.log(str.substring(6, 11)); // 'world'
console.log(str.replace("world", "JS")); // 'Hello JS'
console.log(str.replaceAll("l", "L")); // 'HeLLo worLd'
```

### Розділення та об’єднання

- **`split(separator, limit)`**: Розбиває рядок на масив підрядків за роздільником.
- **`concat(...strings)`**: Об’єднує рядки (рідко використовується, краще `+` або шаблонні літерали).

```js
let sentence = "JavaScript is fun";
console.log(sentence.split(" ")); // ['JavaScript', 'is', 'fun']
console.log("Hello".concat(" ", "World")); // 'Hello World'
```

### Очищення та форматування

- **`trim()`**: Видаляє пробіли з початку та кінця рядка.
- **`trimStart()`**: Видаляє пробіли з початку.
- **`trimEnd()`**: Видаляє пробіли з кінця.
- **`padStart(targetLength, padString)`**: Доповнює початок рядка до вказаної довжини.
- **`padEnd(targetLength, padString)`**: Доповнює кінець рядка.

```js
console.log("  text  ".trim()); // 'text'
console.log("  text".trimStart()); // 'text'
console.log("text  ".trimEnd()); // 'text'
console.log("42".padStart(4, "0")); // '0042'
console.log("42".padEnd(4, "0")); // '4200'
```

### Інші методи

- **`repeat(count)`**: Повторює рядок указану кількість разів.
- **`localeCompare(otherString, [locales, options])`**: Порівнює рядки з урахуванням локалізації (повертає `-1`, `0`, `1`).
- **`normalize([form])`**: Нормалізує Unicode-представлення рядка (наприклад, для порівняння символів із діакритикою).
- **`valueOf()`**: Повертає примітивне значення об’єкта `String`.
- **`toString()`**: Повертає примітивне значення рядка (аналогічно `valueOf`).
- **Застарілі методи** (HTML-обгортки, не рекомендуються): `anchor`, `big`, `blink`, `bold`, `fixed`, `fontcolor`, `fontsize`, `italics`, `link`, `small`, `strike`, `sub`, `sup`.

```js
console.log("ha".repeat(3)); // 'hahaha'
console.log("a".localeCompare("b")); // -1
console.log("café".normalize("NFC")); // 'café'
let strObj = new String("test");
console.log(strObj.valueOf()); // 'test'
console.log(strObj.toString()); // 'test'
console.log("text".anchor("name")); // '<a name="name">text</a>' (застарілий)
```

## Шаблонні літерали

- Використовують зворотні лапки (`` ` ``) і дозволяють:
  - Вставляти вирази через `${expression}`.
  - Створювати багаторядкові строки без `\n`.
- Приклад:
  ```js
  let name = "Alice";
  let greeting = `Hello, ${name}!
  Welcome to JS!`;
  console.log(greeting);
  // Hello, Alice!
  // Welcome to JS!
  ```

## Особливості для співбесід — Питання та відповіді

### Чому рядки в JavaScript незмінні?

- Незмінність означає, що методи не модифікують оригінальний рядок, а повертають новий. Це забезпечує безпеку даних і передбачуваність.
  ```js
  let str = "Hello";
  str.toUpperCase();
  console.log(str); // 'Hello' (оригінал не змінився)
  ```

### У чому різниця між `slice`, `substring` і `substr`?

- `slice(start, end)`: Підтримує негативні індекси, вирізає від `start` до `end` (не включно).
- `substring(start, end)`: Не підтримує негативні індекси, якщо `start > end`, міняє їх місцями.
- `substr(start, length)`: Вирізає `length` символів від `start` (застарілий, уникайте).
  ```js
  let str = "Hello";
  console.log(str.slice(1, 4)); // 'ell'
  console.log(str.substring(1, 4)); // 'ell'
  console.log(str.substr(1, 3)); // 'ell'
  ```

### Чим відрізняється `at` від `charAt`?

- `at(index)` підтримує негативні індекси (наприклад, `str.at(-1)` повертає останній символ), доданий у ES2022.
- `charAt(index)` повертає `""` для некоректних індексів, не підтримує негативні індекси.
  ```js
  let str = "Hello";
  console.log(str.at(-1)); // 'o'
  console.log(str.charAt(10)); // ''
  ```

### Чому не варто використовувати `new String()`?

- Створює об’єкт, а не примітив, що призводить до:
  - Більшого споживання пам’яті.
  - Проблем із порівнянням (`new String('a') !== 'a'`).
  - Несподіваної поведінки (`typeof` повертає `"object"`).
  ```js
  let strObj = new String("test");
  console.log(typeof strObj); // 'object'
  console.log(strObj === "test"); // false
  ```

### Як працює `replace` з регулярними виразами?

- Якщо передати регулярний вираз із прапорцем `g`, замінить усі входження. Без `g` — лише перше.
  ```js
  let str = "hello hello";
  console.log(str.replace(/hello/g, "hi")); // 'hi hi'
  console.log(str.replace("hello", "hi")); // 'hi hello'
  ```

### Що таке `codePointAt` і коли його використовувати?

- Повертає Unicode code point, що краще для символів поза BMP (наприклад, емодзі). Використовуй для коректної роботи з емодзі чи спеціальними символами.
  ```js
  console.log("😊".codePointAt(0)); // 128522
  console.log("😊".charCodeAt(0)); // 55357 (лише частина кодової точки)
  ```

### Як перевірити порожній рядок?

- Перевірка `str.length === 0` або `str === ''`. Порожній рядок є falsy, але явна перевірка `length` підвищує читабельність.
  ```js
  let str = "";
  console.log(str.length === 0); // true
  console.log(str === ""); // true
  ```

## Поради

- **Використовуй шаблонні літерали**: Вони зручніші за конкатенацію (`+`) і підтримують багаторядкові строки.
- **Віддай перевагу `at` над `charAt`**: Якщо потрібна підтримка негативних індексів, `at` є сучаснішим (ES2022).
- **Уникай `new String()`**: Завжди використовуй літерали (`'text'`, `"text"`) для простоти та ефективності.
- **Перевіряй індекси**: Перед використанням `at`, `charAt` чи `slice` переконайся, що індекс у межах рядка.
- **Регулярні вирази для складних замін**: Використовуй `replace` або `replaceAll` із `/g` для заміни всіх входжень.
- **Уникай застарілих методів**: Замість `substr` використовуй `slice` або `substring`. Не використовуй HTML-методи (`bold`, `anchor`).
- **Оптимізуй код**: Наприклад, `includes` ефективніший за `indexOf() !== -1`.
- **Робота з емодзі**: Використовуй `codePointAt` і `String.fromCodePoint` для коректної обробки символів Unicode.

## Приклад повного використання

```js
"use strict";

const name = "Alice";
console.log(name.length); // 5
console.log(name.at(-1)); // 'e'

const message = `Hello, ${name.toUpperCase()}!`;
console.log(message); // 'Hello, ALICE!'

const words = message.split(" ");
console.log(words); // ['Hello,', 'ALICE!']

const newMessage = message.replace("ALICE", "Bob");
console.log(newMessage); // 'Hello, Bob!'

console.log("  text  ".trim()); // 'text'
console.log("test123".match(/\d+/)); // ['123']
console.log("JS".padStart(5, "*")); // '***JS'
console.log("😊".codePointAt(0)); // 128522
```
