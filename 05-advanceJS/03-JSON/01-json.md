# Детальний конспект: JSON у JavaScript

## Загальна інформація

- **Опис**: JSON (JavaScript Object Notation) — це легкий формат обміну даними, який використовується для серіалізації та десеріалізації об’єктів у JavaScript. Об’єкт `JSON` у JavaScript надає методи `JSON.stringify` і `JSON.parse` для роботи з JSON-даними.
- **Призначення**: Використовується для передачі даних між клієнтом і сервером (наприклад, у HTTP-запитах із `fetch`), зберігання конфігурацій, API-взаємодії та обміну даними між різними мовами програмування.
- **Особливості**:
  - `JSON.stringify`: Перетворює JavaScript-об’єкти в JSON-рядок.
  - `JSON.parse`: Перетворює JSON-рядок у JavaScript-об’єкт.
  - JSON підтримує обмежений набір типів даних: об’єкти, масиви, рядки, числа, логічні значення, `null`.
  - Не підтримує функції, `undefined`, `Symbol`, цикли об’єктів чи спеціальні об’єкти (наприклад, `Date`).
- **Контекст**: JSON широко застосовується в HTTP-запитах (REST API, GraphQL), локальному сховищі (`localStorage`), конфігураційних файлах і сучасних веб-додатках.
- **Синтаксис**:
  ```javascript
  const obj = { name: "User", age: 30 };
  const jsonString = JSON.stringify(obj); // '{"name":"User","age":30}'
  const parsedObj = JSON.parse(jsonString); // { name: 'User', age: 30 }
  ```

## Приклади коду

### 1. Серіалізація об’єкта з `JSON.stringify`

Перетворення об’єкта в JSON-рядок.

```javascript
const user = { name: "Anna", age: 25, active: true };
const jsonString = JSON.stringify(user);
console.log(jsonString);
```

#### Результат:

Виводить: `{"name":"Anna","age":25,"active":true}`

### 2. Десеріалізація з `JSON.parse`

Перетворення JSON-рядка в об’єкт.

```javascript
const jsonString = '{"name":"Anna","age":25,"active":true}';
try {
  const user = JSON.parse(jsonString);
  console.log(user.name);
} catch (error) {
  console.error("Помилка парсингу:", error.message);
}
```

#### Результат:

Виводить: `Anna`

### 3. Використання `JSON.stringify` із `fetch` (POST-запит)

Відправлення JSON-даних на сервер.

```javascript
const data = { title: "Новий пост", body: "Текст", userId: 1 };
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify(data),
})
  .then((response) => {
    if (!response.ok) throw new Error(`Помилка: ${response.status}`);
    return response.json();
  })
  .then((result) => console.log("Створено:", result))
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Виводить створений об’єкт із `id`, `title`, `body`.

### 4. Обробка відповіді API з `JSON.parse`

Отримання JSON-даних із сервера.

```javascript
fetch("https://jsonplaceholder.typicode.com/users/1")
  .then((response) => {
    if (!response.ok) throw new Error(`Помилка: ${response.status}`);
    return response.text(); // Отримуємо текст
  })
  .then((text) => {
    try {
      const user = JSON.parse(text);
      console.log("Користувач:", user.name);
    } catch (error) {
      console.error("Помилка парсингу:", error.message);
    }
  })
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Виводить ім’я користувача (наприклад, "Leanne Graham").

### 5. Використання `replacer` у `JSON.stringify`

Фільтрація властивостей.

```javascript
const user = { name: "Bob", age: 30, password: "secret" };
const jsonString = JSON.stringify(user, ["name", "age"]);
console.log(jsonString);
```

#### Результат:

Виводить: `{"name":"Bob","age":30}`

### 6. Використання `reviver` у `JSON.parse`

Трансформація значень.

```javascript
const jsonString = '{"name":"Anna","birth":"2000-01-01"}';
const user = JSON.parse(jsonString, (key, value) => {
  if (key === "birth") return new Date(value);
  return value;
});
console.log(user.birth);
```

#### Результат:

Виводить: `2000-01-01T00:00:00.000Z` (об’єкт `Date`).

### 7. Збереження та відновлення даних у `localStorage`

Серіалізація та десеріалізація.

```javascript
const settings = { theme: "dark", fontSize: 16 };
// Збереження
localStorage.setItem("settings", JSON.stringify(settings));
// Відновлення
try {
  const restored = JSON.parse(localStorage.getItem("settings"));
  console.log("Тема:", restored.theme);
} catch (error) {
  console.error("Помилка парсингу:", error.message);
}
```

#### Результат:

Виводить: `dark`

## Особливості для співбесід — Питання та відповіді

### Що таке JSON і для чого він потрібен?

- **Відповідь**: JSON — формат обміну даними, який використовується для серіалізації об’єктів у рядки та їх передачі між клієнтом і сервером.
  ```javascript
  JSON.stringify({ key: "value" }); // '{"key":"value"}'
  ```

### Чим відрізняються `JSON.stringify` і `JSON.parse`?

- **Відповідь**: `JSON.stringify` перетворює об’єкт у JSON-рядок, `JSON.parse` — JSON-рядок в об’єкт.
  ```javascript
  const obj = { a: 1 };
  const str = JSON.stringify(obj); // '{"a":1}'
  const parsed = JSON.parse(str); // { a: 1 }
  ```

### Які типи даних підтримує JSON?

- **Відповідь**: Об’єкти, масиви, рядки, числа, логічні значення, `null`. Не підтримує `undefined`, функції, `Symbol`.
  ```javascript
  JSON.stringify({ a: undefined }); // '{}'
  ```

### Як обробляти помилки в `JSON.parse`?

- **Відповідь**: Використовуйте `try/catch`, оскільки невалідний JSON викликає `SyntaxError`.
  ```javascript
  try {
    JSON.parse("invalid");
  } catch (e) {
    console.error(e);
  }
  ```

### Що таке `replacer` у `JSON.stringify`?

- **Відповідь**: Функція або масив, який фільтрує чи трансформує значення під час серіалізації.
  ```javascript
  JSON.stringify({ a: 1, b: 2 }, ["a"]); // '{"a":1}'
  ```

### Що таке `reviver` у `JSON.parse`?

- **Відповідь**: Функція, яка трансформує значення під час десеріалізації.
  ```javascript
  JSON.parse('{"date":"2023-01-01"}', (k, v) =>
    k === "date" ? new Date(v) : v
  );
  ```

### Як JSON використовується в HTTP-запитах?

- **Відповідь**: `JSON.stringify` для відправки даних (`body`), `response.json()` (який використовує `JSON.parse`) для обробки відповіді.
  ```javascript
  fetch("url", { method: "POST", body: JSON.stringify({ key: "value" }) });
  ```

## Поради

- **Обробка помилок**: Завжди використовуйте `try/catch` для `JSON.parse` через можливі `SyntaxError`.
- **Перевірка даних**: Перед парсингом перевіряйте, чи є відповідь валідним JSON (наприклад, `response.headers.get('Content-Type')`).
- **Фільтрація**: Використовуйте `replacer` у `JSON.stringify` для виключення чутливих даних (паролі, токени).
- **Трансформація**: Застосовуйте `reviver` у `JSON.parse` для відновлення типів (наприклад, `Date`).
- **Оптимізація**: Уникайте серіалізації великих об’єктів, щоб зменшити витрати пам’яті.
- **Сумісність**: Переконайтеся, що сервер повертає правильний `Content-Type: application/json`.
- **Тестування**: Перевіряйте JSON у Chrome DevTools або з бібліотеками (Postman, Jest).
- **Безпека**: Уникайте парсингу ненадійних JSON-даних, щоб запобігти ін’єкціям.
- **Документація**: Звертайтеся до MDN для деталей про `JSON` і Eloquent JavaScript для прикладів HTTP.

## Додаткові деталі

- **Методи `JSON`**:
  - **`JSON.stringify(value, replacer?, space?)`**:
    - `value`: Об’єкт для серіалізації.
    - `replacer`: Функція або масив для фільтрації/трансформації.
    - `space`: Число (відступи) або рядок для форматування.
      ```javascript
      JSON.stringify({ a: 1 }, null, 2); // "{\n  \"a\": 1\n}"
      ```
  - **`JSON.parse(text, reviver?)`**:
    - `text`: JSON-рядок для парсингу.
    - `reviver`: Функція для трансформації значень.
      ```javascript
      JSON.parse('{"n":1}', (k, v) => (typeof v === "number" ? v * 2 : v)); // { n: 2 }
      ```
- **Обмеження JSON**:
  - Не підтримує цикли об’єктів (викликає `TypeError`).
    ```javascript
    const obj = {};
    obj.self = obj;
    JSON.stringify(obj); // TypeError
    ```
  - Ігнорує `undefined`, функції, `Symbol`.
    ```javascript
    JSON.stringify({ fn: () => {}, sym: Symbol("id") }); // '{}'
    ```
  - `Date` серіалізується як рядок ISO.
    ```javascript
    JSON.stringify({ d: new Date("2023-01-01") }); // '{"d":"2023-01-01T00:00:00.000Z"}'
    ```
- **Використання з HTTP**:
  - У `fetch` метод `response.json()` автоматично викликає `JSON.parse`.
  - Заголовок `Content-Type: application/json` обов’язковий для JSON-запитів.
  - Приклад із Eloquent JavaScript:
    ```javascript
    fetch("/data.json")
      .then((response) => response.json())
      .then((data) => console.log(data));
    ```
- **Сумісність**:
  - Повна підтримка в усіх сучасних браузерах (Chrome, Firefox, Safari, Edge) і Node.js.
  - Введено в ECMAScript 5 (2009).
  - Для старих браузерів (IE6/7) використовуйте поліфіл `json2.js`.
- **Безпека**:
  - Некоректний JSON може викликати помилки, завжди перевіряйте джерело.
  - Уникайте використання `eval` замість `JSON.parse` через ризик XSS.
- **Альтернативи**:
  - YAML: Більш читабельний формат для конфігурацій.
  - MessagePack: Компактніший бінарний формат.
  - `FormData`: Для відправки форм замість JSON.
- **Продуктивність**:
  - Для великих об’єктів використовуйте потокову обробку (наприклад, `stream-json` у Node.js).
  - Уникайте глибоких об’єктів із циклами.
  - Кешуйте серіалізовані дані в `localStorage` для повторного використання.
