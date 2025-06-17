# Ітерація по об’єктах у JavaScript

## Загальна інформація

- **Опис**: Ітерація по об’єктах дозволяє обробляти ключі, значення чи пари ключ-значення. JavaScript пропонує кілька підходів, включаючи цикли та методи об’єктів.
- **Методи ітерації**:
  - **`for...in`**: Ітерує по перелічуваних ключах (власних і успадкованих).
  - **`for...of`**: Використовується з `Object.entries()` для ітерабельних даних.
  - **`Object.keys()`**, **`Object.values()`**, **`Object.entries()`**: Доступ до ключів, значень чи пар.
- **Особливості**:
  - Об’єкти не мають `[Symbol.iterator]`, тому `for...of` потребує конверсії.
  - Властивості з `enumerable: false` ігноруються в `Object.keys()` та `for...in`.
  - Успадковані властивості впливають на `for...in`.
- **Контекст**: Використовується для обробки даних, фільтрації, мапінгу чи агрегації.

## Приклади коду

### Оператор `in`

```javascript
let person = { name: "Alice", age: 25 };
for (let key in person) {
  console.log(`${key}: ${person[key]}`); // name: Alice, age: 25
}
console.log("name" in person); // true
```

### Цикл `for...of` із `Object`

```javascript
let obj = { a: 1, b: 2 };
for (let key of Object.keys(obj)) console.log(key); // a, b
for (let value of Object.values(obj)) console.log(value); // 1, 2
for (let [key, value] of Object.entries(obj)) console.log(key, value); // a 1, b 2
```

### Успадковані та неперелічувані властивості

```javascript
let proto = { inherited: "yes" };
let obj = Object.create(proto);
obj.own = "mine";
Object.defineProperty(obj, "hidden", { value: 42, enumerable: false });
for (let key in obj) console.log(key); // own, inherited
console.log(Object.keys(obj)); // ["own"]
console.log(Object.getOwnPropertyNames(obj)); // ["own", "hidden"]
```

## Особливості для співбесід — Питання та відповіді

### Чим `for...in` відрізняється від `for...of`?

- **Відповідь**: `for...in` ітерує по перелічуваних ключах (включно з успадкованими), `for...of` працює з ітерабельними об’єктами через `Object.entries()`.
  ```javascript
  let obj = { a: 1 };
  for (let key in obj) console.log(key); // a
  for (let key of Object.keys(obj)) console.log(key); // a
  ```

### Чому об’єкти не підтримують `for...of` напряму?

- **Відповідь**: Через відсутність `[Symbol.iterator]`. Використовуйте `Object.entries()` для ітерабельності.
  ```javascript
  let obj = { a: 1 };
  // for (let value of obj) // Помилка
  for (let value of Object.values(obj)) console.log(value); // 1
  ```

### Як обробляти неперелічувані властивості?

- **Відповідь**: Використовуйте `Object.getOwnPropertyNames()` замість `Object.keys()`.
  ```javascript
  let obj = {};
  Object.defineProperty(obj, "hidden", { enumerable: false, value: 1 });
  console.log(Object.getOwnPropertyNames(obj)); // ["hidden"]
  ```

## Поради

- **Використовуйте `Object.entries()`**: Для зручної ітерації з деструктуризацією.
- **Уникайте `for...in` з мутаціями**: Перевіряйте `hasOwnProperty()` для власних властивостей.
- **Оптимізуйте**: Застосовуйте `Object.keys()` для простих завдань.
- **Перевіряйте успадкування**: Розумійте вплив прототипів на ітерацію.
- **Тестуйте символи**: Додавайте `getOwnPropertySymbols()` для повного аналізу.
