# 🔗 Конспект: URLSearchParams API

Цей конспект охоплює **URLSearchParams API**, яке дозволяє працювати з параметрами запиту URL (частиною URL після `?`) для їх створення, редагування та аналізу.

---

## 🖼️ Що таке URLSearchParams?

- **URLSearchParams** — це інтерфейс для маніпуляції рядком запиту URL (наприклад, `?name=John&age=30`).
- Надає методи для додавання, зміни, видалення та отримання параметрів.
- **Не розбирає повні URL**, лише частину запиту (параметри після `?`).
- Часто використовується разом із `window.location.search` або об’єктом `URL`.

---

## 🛠️ Створення об’єкта `URLSearchParams`

### 🔹 Конструктори

- **З рядка запиту**:

  ```js
  const params1 = new URLSearchParams("?name=John&age=30");
  console.log(params1.toString()); // "name=John&age=30"
  ```

- **З масиву пар ключ-значення**:

  ```js
  const params2 = new URLSearchParams([
    ["name", "John"],
    ["age", "30"],
  ]);
  console.log(params2.toString()); // "name=John&age=30"
  ```

- **З об’єкта**:
  ```js
  const params3 = new URLSearchParams({ name: "John", age: "30" });
  console.log(params3.toString()); // "name=John&age=30"
  ```

---

## 🛠️ Основні методи

### 🔹 `append(key, value)`

- Додає нове значення до ключа. Якщо ключ уже існує, додає ще одне значення.
- Приклад:
  ```js
  const params = new URLSearchParams();
  params.append("name", "Yuri");
  params.append("name", "John");
  console.log(params.toString()); // "name=Yuri&name=John"
  ```

### 🔹 `set(key, value)`

- Встановлює значення для ключа. Якщо ключ існує, замінює всі попередні значення.
- Приклад:
  ```js
  const params = new URLSearchParams("name=John");
  params.set("name", "Test");
  console.log(params.toString()); // "name=Test"
  ```

### 🔹 `get(key)`

- Повертає перше значення для вказаного ключа.
- Приклад:
  ```js
  const params = new URLSearchParams("name=John&name=Yuri");
  console.log(params.get("name")); // "John"
  ```

### 🔹 `getAll(key)`

- Повертає масив усіх значень для вказаного ключа.
- Приклад:
  ```js
  const params = new URLSearchParams("name=John&name=Yuri");
  console.log(params.getAll("name")); // ["John", "Yuri"]
  ```

### 🔹 `has(key)`

- Перевіряє, чи існує ключ (повертає `true`/`false`).
- Приклад:
  ```js
  const params = new URLSearchParams("name=John");
  console.log(params.has("name")); // true
  ```

### 🔹 `delete(key)`

- Видаляє всі значення для вказаного ключа.
- Приклад:
  ```js
  const params = new URLSearchParams("name=John&age=30");
  params.delete("age");
  console.log(params.toString()); // "name=John"
  ```

### 🔹 Ітерація

- **`entries()`**: Повертає ітератор пар `[key, value]`.

  ```js
  const params = new URLSearchParams("name=John&age=30");
  for (const [key, value] of params.entries()) {
    console.log(key, value); // "name John", "age 30"
  }
  ```

- **`keys()`**: Повертає ітератор ключів.

  ```js
  for (const key of params.keys()) {
    console.log(key); // "name", "age"
  }
  ```

- **`values()`**: Повертає ітератор значень.
  ```js
  for (const value of params.values()) {
    console.log(value); // "John", "30"
  }
  ```

---

## 🛠️ Робота з `URL` та `URLSearchParams`

- Використовуйте `URL` для розбору повного URL і доступу до параметрів через `searchParams`.
- Приклад:

  ```js
  const url = new URL(
    "https://example.com/search?query=React+%26+TypeScript&lang=en"
  );
  const searchParams = url.searchParams;
  console.log(searchParams.get("query")); // "React & TypeScript"
  console.log(searchParams.get("lang")); // "en"
  ```

- Додавання параметра до поточного URL:
  ```js
  const url = new URL(window.location.href);
  url.searchParams.append("name", "Yuri");
  window.location.href = url.toString(); // Оновлює URL
  ```

---

## 🛠️ Percent Encoding

- **Percent encoding** — це спосіб кодування спеціальних символів у URL (наприклад, пробілів, `&`, `=`).
- `URLSearchParams` автоматично кодує спеціальні символи:
  ```js
  const params = new URLSearchParams();
  params.append("query", "React & TypeScript");
  console.log(params.toString()); // "query=React+%26+TypeScript"
  ```

---

## 📘 Ключові рекомендації

- Використовуйте `URLSearchParams` для зручної роботи з параметрами запиту замість ручного парсингу рядка `location.search`.
- Застосовуйте `set` для заміни значень і `append` для додавання кількох значень до одного ключа.
- Для ітерації використовуйте `entries()`, якщо потрібні пари ключ-значення.
- Перевіряйте наявність параметрів за допомогою `has` перед їх отриманням.
- Уникайте ручного кодування спеціальних символів, оскільки `URLSearchParams` робить це автоматично.
