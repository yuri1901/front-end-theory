# Детальний конспект: async/await у JavaScript

## Загальна інформація

- **Опис**: `async/await` — це синтаксичний цукор у JavaScript, введений у ECMAScript 2017, для роботи з промісами, що робить асинхронний код більш читабельним і схожим на синхронний. Використовується для обробки асинхронних операцій, таких як мережеві запити, таймери чи доступ до API.
- **Контекст**: `async/await` спрощує роботу з асинхронними операціями, замінюючи ланцюжки `.then()`. Застосовується в клієнтських (наприклад, `fetch`) і серверних (Node.js) сценаріях.
- **Основні компоненти**:
  - **`async`**: Ключове слово перед функцією, позначає, що функція асинхронна і завжди повертає `Promise`.
  - **`await`**: Працює лише в `async`-функціях, призупиняє виконання до завершення проміса, повертаючи його результат (`Fulfilled` або помилку).
  - **Обробка помилок**: Використовується `try/catch` для перехоплення помилок.
  - **Синтаксис**:
    ```javascript
    async function example() {
      try {
        const result = await somePromise();
        return result;
      } catch (error) {
        console.error(error);
      }
    }
    ```
- **Особливості**:
  - `await` не блокує основний потік, лише призупиняє функцію, дозволяючи Event Loop обробляти інші завдання.
  - Покращує читабельність порівняно з `.then()`.
  - Може використовуватися з `Promise.all`, `Promise.race` для паралельних операцій.
  - Потребує обережності, щоб уникнути послідовного виконання там, де можлива паралельність.

## Приклади коду

### 1. Базовий запит із `async/await`

Отримання даних із API.

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/users/${id}`
    );
    if (!response.ok) throw new Error("HTTP error: " + response.status);
    const user = await response.json();
    return user.name;
  } catch (error) {
    console.error("Помилка запиту:", error.message);
    return null;
  }
}
fetchUser(1).then((name) => console.log(name));
```

#### Результат:

Виводить ім’я користувача (наприклад, "Leanne Graham") або `null` у разі помилки.

### 2. Послідовні запити з `async/await`

Залежні запити.

```javascript
async function getUserAndPosts(id) {
  try {
    const userResponse = await fetch(
      `https://jsonplaceholder.typicode.com/users/${id}`
    );
    const user = await userResponse.json();
    const postsResponse = await fetch(
      `https://jsonplaceholder.typicode.com/posts?userId=${id}`
    );
    const posts = await postsResponse.json();
    return { user: user.name, postCount: posts.length };
  } catch (error) {
    console.error("Помилка:", error.message);
    return null;
  }
}
getUserAndPosts(1).then((data) => console.log(data));
```

#### Результат:

Виводить об’єкт із ім’ям і кількістю постів.

### 3. Паралельні запити з `Promise.all` і `await`

Оптимізація запитів.

```javascript
async function fetchParallel() {
  try {
    const [user, todos] = await Promise.all([
      fetch("https://jsonplaceholder.typicode.com/users/1").then((res) =>
        res.json()
      ),
      fetch("https://jsonplaceholder.typicode.com/todos?userId=1").then((res) =>
        res.json()
      ),
    ]);
    return { user: user.name, todoCount: todos.length };
  } catch (error) {
    console.error("Помилка:", error.message);
    return null;
  }
}
fetchParallel().then((data) => console.log(data));
```

#### Результат:

Виводить ім’я та кількість завдань, виконуючи запити паралельно.

### 4. Використання `await` із затримкою

Таймер у `async`-функції.

```javascript
function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}
async function timedMessage() {
  console.log("Початок");
  await delay(1000);
  console.log("Через 1 секунду");
  await delay(2000);
  console.log("Через ще 2 секунди");
}
timedMessage();
```

#### Результат:

Виводить повідомлення з затримками.

## Особливості для співбесід — Питання та відповіді

### Що робить ключове слово `async`?

- **Відповідь**: Позначає функцію як асинхронну, змушуючи її повертати `Promise`. Дозволяє використовувати `await` усередині.
  ```javascript
  async function fn() {
    return 1;
  } // Повертає Promise.resolve(1)
  ```

### Для чого потрібен `await`?

- **Відповідь**: Очікує виконання проміса, повертаючи його результат або викликаючи помилку. Працює лише в `async`-функціях.
  ```javascript
  const data = await fetch("url");
  ```

### Як обробляти помилки в `async/await`?

- **Відповідь**: Використовуйте `try/catch` для перехоплення помилок у промісах.
  ```javascript
  try {
    await fetch("url");
  } catch (e) {
    console.error(e);
  }
  ```

### Чи можна використовувати `await` із кількома промісами?

- **Відповідь**: Так, через `Promise.all` для паралельного виконання.
  ```javascript
  const [a, b] = await Promise.all([fetch("url1"), fetch("url2")]);
  ```

### Що станеться, якщо використати `await` без `async`?

- **Відповідь**: Виникне синтаксична помилка, бо `await` дозволений лише в `async`-функціях.
  ```javascript
  await fetch("url"); // SyntaxError
  ```

## Поради

- **Обробка помилок**: Завжди використовуйте `try/catch` для надійності.
- **Паралельність**: Використовуйте `Promise.all` замість послідовного `await` для швидкості.
  ```javascript
  // Погано
  const a = await fetch("url1");
  const b = await fetch("url2");
  // Добре
  const [a, b] = await Promise.all([fetch("url1"), fetch("url2")]);
  ```
- **Очищення**: Використовуйте `finally` для закриття ресурсів (наприклад, WebSocket).
- **Тестування**: Перевіряйте в Chrome DevTools, Node.js, або з Jest для асинхронних тестів.
- **Документація**: Звертайтеся до MDN для синтаксису та OpenReplay для практик.
- **Найкращі практики**:
  - Перевіряйте `response.ok` у мережевих запитах.
  - Уникайте вкладених `try/catch`, виносьте логіку в окремі функції.
  - Повертайте значення з `async`-функцій для чіткості.

## Додаткові деталі

- **Механізми**:
  - `async`: Перетворює результат функції в `Promise` (наприклад, `return 1` стає `Promise.resolve(1)`).
  - `await`: Обробляє проміси, включаючи `Promise.resolve` і `Promise.reject`.
  - `Promise.allSettled`: Альтернатива `Promise.all` для обробки часткових помилок.
- **Сумісність**: Chrome 55+, Firefox 52+, Safari 10.1+, Node.js 7.6+ (2017).
- **Обмеження**:
  - `await` у циклах може уповільнити виконання; використовуйте `Promise.all`.
  - Некоректна обробка помилок може призвести до невідловлених винятків.
- **Продуктивність**:
  - Уникайте надмірного `await`:
    ```javascript
    // Погано
    for (const url of urls) {
      await fetch(url);
    }
    // Добре
    await Promise.all(urls.map((url) => fetch(url)));
    ```
  - Використовуйте `Promise.race` для таймаутів:
    ```javascript
    async function withTimeout(promise, ms) {
      const timeout = new Promise((_, reject) =>
        setTimeout(() => reject("Timeout"), ms)
      );
      return await Promise.race([promise, timeout]);
    }
    ```
- **Альтернативи**:
  - Ланцюжки `.then()` для простих сценаріїв.
  - Бібліотеки (Axios) для зручних HTTP-запитів.
