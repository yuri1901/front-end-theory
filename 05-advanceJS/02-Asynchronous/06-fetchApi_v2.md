# Детальний конспект: Fetch API у JavaScript

## Загальна інформація

- **Опис**: Fetch API — це сучасний інтерфейс у JavaScript для виконання HTTP-запитів, доступний через глобальний метод `fetch` об’єкта `Window` або `Worker`. Повертає проміс із об’єктом `Response`, замінюючи застарілий `XMLHttpRequest`.
- **Призначення**: Використовується для отримання ресурсів (JSON, текст, зображення, файли) або відправлення даних (POST, PUT, DELETE) до серверів, інтеграції з API та роботи у фронтенд/бекенд-додатках.
- **Особливості**:
  - Базується на промісах, підтримує асинхронне програмування.
  - Надає об’єкти `Request`, `Response`, `Headers` для кастомізації.
  - Дозволяє скасування запитів через `AbortController`.
  - Підтримує потокову передачу даних (`ReadableStream`).
  - Не відхиляє проміс при HTTP-помилках (4xx, 5xx), вимагає ручної перевірки.
- **Контекст**: Введений у ECMAScript 2015, широко використовується у браузерах і Node.js (з версії 18). Критичний для роботи з REST API, GraphQL, завантаження файлів і крос-доменних запитів.
- **Синтаксис**:
  ```javascript
  fetch("https://api.example.com/data")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error("Помилка:", error));
  ```

## Приклади коду

### 1. Простий GET-запит для JSON

Отримання даних із API.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => {
    if (!response.ok) throw new Error(`HTTP помилка: ${response.status}`);
    return response.json();
  })
  .then((post) => console.log("Заголовок:", post.title))
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Виводить заголовок поста або повідомлення про помилку.

### 2. POST-запит із JSON

Відправлення даних.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer token123",
  },
  body: JSON.stringify({
    title: "Новий пост",
    body: "Текст поста",
    userId: 1,
  }),
})
  .then((response) => {
    if (!response.ok) throw new Error(`Помилка: ${response.statusText}`);
    return response.json();
  })
  .then((data) => console.log("Створено:", data))
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Виводить створений об’єкт або помилку.

### 3. Завантаження зображення з `blob`

Обробка бінарних даних.

```javascript
fetch("https://via.placeholder.com/150")
  .then((response) => {
    if (!response.ok) throw new Error("Не вдалося завантажити зображення");
    return response.blob();
  })
  .then((blob) => {
    const img = document.createElement("img");
    img.src = URL.createObjectURL(blob);
    document.body.appendChild(img);
  })
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Додає зображення до сторінки.

### 4. Скасування запиту з `AbortController`

Переривання запиту.

```javascript
const controller = new AbortController();
const signal = controller.signal;

setTimeout(() => controller.abort(), 2000); // Скасування через 2 секунди

fetch("https://jsonplaceholder.typicode.com/posts", { signal })
  .then((response) => response.json())
  .then((data) => console.log("Дані:", data))
  .catch((error) => {
    if (error.name === "AbortError") console.log("Запит скасовано");
    else console.error("Помилка:", error.message);
  });
```

#### Результат:

Скасовує запит через 2 секунди.

### 5. Паралельні запити з `Promise.all`

Одночасне виконання.

```javascript
const urls = [
  "https://jsonplaceholder.typicode.com/users/1",
  "https://jsonplaceholder.typicode.com/posts?userId=1",
];
Promise.all(
  urls.map((url) =>
    fetch(url).then((response) => {
      if (!response.ok) throw new Error(`Помилка: ${response.status}`);
      return response.json();
    })
  )
)
  .then(([user, posts]) =>
    console.log("Користувач:", user.name, "Постів:", posts.length)
  )
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Виводить ім’я користувача та кількість постів.

### 6. Потокова обробка з `ReadableStream`

Читання великих даних.

```javascript
fetch("https://api.example.com/large-file")
  .then((response) => {
    const reader = response.body.getReader();
    return new ReadableStream({
      start(controller) {
        function push() {
          reader.read().then(({ done, value }) => {
            if (done) {
              controller.close();
              return;
            }
            controller.enqueue(value);
            push();
          });
        }
        push();
      },
    });
  })
  .then((stream) => new Response(stream))
  .then((response) => response.text())
  .then((text) => console.log("Дані:", text.slice(0, 100)))
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Читає дані частинами, виводить перші 100 символів.

### 7. Відправлення форми з `FormData`

Обробка форм.

```javascript
const formData = new FormData();
formData.append("username", "user1");
formData.append("file", document.querySelector('input[type="file"]').files[0]);

fetch("https://api.example.com/upload", {
  method: "POST",
  body: formData,
})
  .then((response) => {
    if (!response.ok) throw new Error("Помилка завантаження");
    return response.json();
  })
  .then((data) => console.log("Успіх:", data))
  .catch((error) => console.error("Помилка:", error.message));
```

#### Результат:

Відправляє форму з файлом.

## Особливості для співбесід — Питання та відповіді

### Що таке Fetch API?

- **Відповідь**: Сучасний інтерфейс для HTTP-запитів, який повертає проміс із `Response`. Замінює `XMLHttpRequest`.
  ```javascript
  fetch("url").then((res) => res.json());
  ```

### Чим `fetch` відрізняється від `XMLHttpRequest`?

- **Відповідь**: `fetch` використовує проміси, простіший у використанні, підтримує потоки та `AbortController`, тоді як `XMLHttpRequest` базується на колбеках.
  ```javascript
  fetch("url").then((res) => res.text());
  ```

### Чому `fetch` не відхиляє проміс при 404?

- **Відповідь**: `fetch` відхиляє проміс лише при мережевих помилках. HTTP-статуси (4xx, 5xx) вважаються валідними відповідями, тому потрібна перевірка `response.ok`.
  ```javascript
  if (!response.ok) throw new Error(res.status);
  ```

### Як відправити POST-запит із `fetch`?

- **Відповідь**: Використовуйте `method: 'POST'`, `headers` і `body` із `JSON.stringify` або `FormData`.
  ```javascript
  fetch("url", { method: "POST", body: JSON.stringify({ key: "value" }) });
  ```

### Як скасувати `fetch`-запит?

- **Відповідь**: Використовуйте `AbortController` і передайте `signal` в опції.
  ```javascript
  const controller = new AbortController();
  fetch("url", { signal: controller.signal });
  ```

### Як обробити бінарні дані?

- **Відповідь**: Використовуйте `response.blob()` для зображень чи файлів і `URL.createObjectURL`.
  ```javascript
  fetch("image.jpg")
    .then((res) => res.blob())
    .then(URL.createObjectURL);
  ```

### Як виконати паралельні запити?

- **Відповідь**: Використовуйте `Promise.all` для одночасного виконання кількох `fetch`.
  ```javascript
  Promise.all([fetch("url1"), fetch("url2")]).then((responses) =>
    responses.map((r) => r.json())
  );
  ```

### Що таке `Headers` у Fetch API?

- **Відповідь**: Об’єкт для керування HTTP-заголовками, дозволяє додавати, видаляти чи отримувати заголовки.
  ```javascript
  const headers = new Headers({ "Content-Type": "application/json" });
  ```

## Поради

- **Перевірка статусу**: Завжди перевіряйте `response.ok` і `response.status` перед обробкою.
- **Заголовки**: Додавайте `Content-Type` для JSON або залишайте порожнім для `FormData`.
- **Скасування**: Використовуйте `AbortController` для тривалих чи непотрібних запитів.
- **Потоки**: Застосовуйте `ReadableStream` для великих файлів, щоб уникнути перевантаження пам’яті.
- **Кешування**: Налаштовуйте `cache` (`no-store`, `force-cache`) для контролю повторних запитів.
- **Безпека**: Використовуйте HTTPS і `credentials: 'include'` лише за потреби.
- **Тестування**: Симулюйте помилки (404, 500) і мережеві збої в Chrome DevTools.
- **Бібліотеки**: Розгляньте Axios для спрощення роботи з `fetch` у складних проєктах.
- **Документація**: Звертайтеся до MDN для деталей про `Request`, `Response`, `Headers`.

## Додаткові деталі

- **Об’єкти Fetch API**:
  - **`Request`**: Дозволяє створювати кастомні запити з тими ж опціями, що й `fetch`.
    ```javascript
    const request = new Request("url", {
      method: "GET",
      headers: { "X-Custom": "value" },
    });
    fetch(request).then((res) => res.json());
    ```
  - **`Headers`**: Керує HTTP-заголовками, підтримує методи `append`, `get`, `set`, `delete`.
    ```javascript
    const headers = new Headers();
    headers.append("X-API-Key", "key123");
    ```
  - **`Response`**: Містить методи (`json`, `text`, `blob`) і властивості (`status`, `headers`, `body`).
- **Крос-доменні запити**:
  - Використовуйте `mode: 'cors'` для запитів до іншого домену.
  - Налаштуйте `Access-Control-Allow-Origin` на сервері для CORS.
  - `mode: 'no-cors'` обмежує доступ до відповіді, використовується рідко.
- **Потоки**:
  - `response.body` повертає `ReadableStream` для поступової обробки.
  - Корисно для великих файлів або стрімінгу (відео, аудіо).
- **Сумісність**:
  - Повна підтримка в Chrome 42+, Firefox 39+, Safari 10.1+, Edge 14+ (2015–2017).
  - Node.js: Нативна підтримка з версії 18 (2022), раніше через `node-fetch`.
  - Для старих браузерів використовуйте поліфіл (наприклад, `whatwg-fetch`).
- **Обмеження**:
  - Не відхиляє проміс при HTTP-помилках, що вимагає додаткової логіки.
  - Обмежена підтримка прогресу завантаження (на відміну від `XMLHttpRequest`).
  - `no-cors` обмежує доступ до даних відповіді.
- **Альтернативи**:
  - `XMLHttpRequest`: Застарілий, але підтримує прогрес завантаження.
  - Axios: Бібліотека з автоматичною обробкою JSON і помилок.
  - `ky`: Легка бібліотека на основі `fetch`.
- **Продуктивність**:
  - Використовуйте `Promise.all` для паралельних запитів.
  - Уникайте зайвих парсингів (`response.json()` лише для JSON).
  - Застосовуйте `cache: 'no-store'` для чутливих даних.
