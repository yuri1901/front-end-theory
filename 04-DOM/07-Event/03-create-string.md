# Робота зі строками у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Робота зі строками включає створення, маніпуляцію та аналіз тексту за допомогою об’єкта `String`, `fromCharCode` і кодування (ASCII/Unicode).
- **Контекст**: Обробка введення користувача, генерація тексту, інтеграція з подіями.
- **Основні компоненти**:
  - `String` об’єкт: методи `toUpperCase`, `slice`, `indexOf`.
  - `String.fromCharCode`: Створення строк із кодів.
  - Кодування: ASCII (0-127), Unicode (розширене).
- **Особливості**:
  - Строки незмінні, нові методи повертають нові екземпляри.
  - Підтримка багатобайтних символів (Unicode).

## Приклади коду

### 1. Створення строк із кодів

#### `String.fromCharCode`

- Генерує рядок із кодів символів.

```javascript
console.log(String.fromCharCode(65, 66, 67)); // "ABC" (ASCII)
console.log(String.fromCharCode(0x1f600)); // "😀" (Unicode смайлик)
```

### 2. Маніпуляція строками

#### Базові методи

- Робота з текстом.

```javascript
const str = "Hello, World!";
console.log(str.length); // 13
console.log(str.toUpperCase()); // "HELLO, WORLD!"
console.log(str.slice(0, 5)); // "Hello"
console.log(str.indexOf("World")); // 7
console.log(str.charCodeAt(0)); // 72 (код 'H')
```

### 3. Інтерактивний приклад

```javascript
const input = document.querySelector("input");
const log = document.querySelector("#log");

input.addEventListener("input", (e) => {
  const text = e.data || "";
  const charCode = text.charCodeAt(0) || 0;
  log.textContent = `Текст: ${text}, Код: ${charCode}`;
  if (charCode === 32) log.textContent += " (Пробіл)";
});
```

## Особливості для співбесід — Питання та відповіді

### Що таке об’єкт `String` у JavaScript?

- **Відповідь**: Об’єкт для роботи зі строками, включає методи як `toUpperCase` і `slice`.
  ```javascript
  console.log("test".toUpperCase()); // "TEST"
  ```

### Як працює `String.fromCharCode`?

- **Відповідь**: Створює рядок із кодів символів (ASCII/Unicode).
  ```javascript
  console.log(String.fromCharCode(65)); // "A"
  ```

### Чим відрізняються ASCII і Unicode?

- **Відповідь**: ASCII — 7-бітна таблиця (0-127), Unicode — розширена (мільйони символів).
  ```javascript
  console.log(String.fromCharCode(128)); // Поза ASCII, залежить від кодування
  ```

### Чи є строки незмінними?

- **Відповідь**: Так, методи повертають нові строки.
  ```javascript
  let str = "test";
  str.toUpperCase(); // "TEST", але str залишається "test"
  ```

### Як знайти код символу в строці?

- **Відповідь**: Використовуйте `charCodeAt`.
  ```javascript
  console.log("A".charCodeAt(0)); // 65
  ```

## Поради

- **Незмінність**: Плануйте ланцюжок методів для економії пам’яті.
- **Unicode**: Перевіряйте підтримку символів у цільових браузерах.
- **Оптимізація**: Уникайте надмірного конкатенації, використовуйте шаблонні рядки.
- **Валідація**: Перевіряйте `length` перед операціями.
- **Тестування**: Емулюйте введення для різних кодувань.

## Додаткові деталі

- **Методи `String`**: `split`, `replace`, `trim`, `substring`.
- **ASCII**: 128 символів, включаючи літери, цифри, знаки.
- **Unicode**: Підтримка емодзі, ієрогліфів, розширених мов.
- **Сумісність**: `fromCharCode` підтримується з ES1, але обмежена для Unicode вище U+FFFF.
