# Fetch API: Дуже детальний конспект за матеріалами MDN

## Загальна інформація

- **Опис**: `fetch` — це метод глобального об’єкта `Window`, який виконує HTTP-запити до серверів і повертає проміс із об’єктом `Response`. Це сучасна альтернатива `XMLHttpRequest` із підтримкою асинхронного програмування.
- **Призначення**: Використовується для отримання ресурсів (JSON, текст, зображення) або відправлення даних (POST, PUT) асинхронно.
- **Особливості**: Повертає проміс, підтримує кастомізацію через `Request` і `Response` об’єкти, дозволяє скасування через `AbortController`.
- **Контекст**: Критичний для роботи з API, інтеграції з фронтенд-фреймворками та обробки мережевих даних.

## 1. Основи використання `fetch`
- **Опис**: `fetch` приймає URL як обов’язковий аргумент і опціональний об’єкт налаштувань. Повертає проміс, який вирішується в об’єкт `Response`.
- **Синтаксис**:
  ```javascript
  fetch("https://api.example.com/data")
    .then(response => {
      if (!response.ok) throw new Error(`Помилка: ${response.status}`);
      return response.json();
    })
    .then(data => console.log("Дані:", data))
    .catch(error => console.error("Помилка:", error));
  ```
- **Приклад (просте завантаження JSON)**:
  ```javascript
  fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => response.json())
    .then(post => console.log("Пост:", post.title))
    .catch(error => console.error("Помилка:", error));
  ```
- **Примітка**: Перевірка `response.ok` (true для 200-299) важлива, оскільки проміс вирішується навіть при помилкових статусах (4xx, 5xx).

## 2. Опції та налаштування
- **Опис**: Другий аргумент `options` дозволяє налаштувати запит із такими полями: `method`, `headers`, `body`, `mode`, `cache`, `credentials` тощо.
- **Ключові поля**:
  - `method`: Визначає HTTP-метод (GET, POST, PUT, DELETE).
  - `headers`: Об’єкт із заголовками (наприклад, `{"Content-Type": "application/json"}`).
  - `body`: Дані для відправки (рядок, FormData, Blob).
  - `mode`: `cors`, `no-cors`, `same-origin` для контролю доступу.
  - `credentials`: `include` для відправки кукі.
- **Приклад (POST із JSON)**:
  ```javascript
  fetch("https://api.example.com/posts", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ title: "Новий пост", body: "Текст", userId: 1 })
  })
    .then(response => response.json())
    .then(data => console.log("Створено:", data))
    .catch(error => console.error("Помилка:", error));
  ```
- **Приклад (завантаження зображення)**:
  ```javascript
  fetch("https://example.com/image.jpg")
    .then(response => response.blob())
    .then(blob => {
      const img = document.createElement("img");
      img.src = URL.createObjectURL(blob);
      document.body.appendChild(img);
    });
  ```
- **Примітка**: Для `body` використовуйте `JSON.stringify` для об’єктів і `FormData` для форм.

## 3. Обробка відповіді
- **Опис**: Об’єкт `Response` надає методи для доступу до даних: `json()`, `text()`, `blob()`, `arrayBuffer()`, `formData()`.
- **Методи та властивості**:
  - `response.json()`: Парсить JSON.
  - `response.text()`: Повертає текст.
  - `response.blob()`: Повертає бінарні дані (наприклад, зображення).
  - `response.ok`: Логічне значення, true для 200-299.
  - `response.status`: HTTP-статус (наприклад, 200, 404).
  - `response.statusText`: Текстове пояснення статусу.
- **Приклад (різні формати)**:
  ```javascript
  fetch("https://api.example.com/data")
    .then(response => {
      console.log("Статус:", response.status, response.statusText);
      return response.ok ? response.json() : response.text();
    })
    .then(data => console.log("Результати:", data))
    .catch(error => console.error("Помилка:", error));
  ```
- **Примітка**: Використовуйте відповідний метод залежно від типу даних (JSON для API, `blob` для файлів).

## 4. Обробка помилок
- **Опис**: `fetch` кидає помилку лише при мережевих проблемах (наприклад, відсутність з’єднання), а не при HTTP-статусах (4xx, 5xx). Обробка помилок вимагає ручної перевірки.
- **Приклад**:
  ```javascript
  fetch("https://api.example.com/nonexistent")
    .then(response => {
      if (!response.ok) throw new Error(`HTTP-помилка! Статус: ${response.status}`);
      return response.json();
    })
    .then(data => console.log("Дані:", data))
    .catch(error => console.error("Помилка:", error.message));
  ```
- **Приклад із `async/await`**:
  ```javascript
  async function fetchData() {
    try {
      const response = await fetch("https://api.example.com/error");
      if (!response.ok) throw new Error(`Помилка: ${response.statusText}`);
      const data = await response.json();
      console.log("Дані:", data);
    } catch (error) {
      console.error("Помилка:", error.message);
    }
  }
  fetchData();
  ```
- **Примітка**: Використовуйте `try/catch` із `async/await` для кращої структури коду.

## 5. Використання з `async/await`
- **Опис**: `fetch` ідеально інтегрується з `async/await`, дозволяючи писати асинхронний код як синхронний.
- **Приклад (посторінкове завантаження)**:
  ```javascript
  async function fetchPages() {
    const urls = ["page1", "page2", "page3"].map(u => `https://api.example.com/${u}`);
    for (const url of urls) {
      try {
        const response = await fetch(url);
        const data = await response.json();
        console.log(`Сторінка ${url}:`, data);
      } catch (error) {
        console.error(`Помилка для ${url}:`, error);
      }
    }
  }
  fetchData();
  ```
- **Примітка**: `await` призупиняє виконання до завершення проміса, що полегшує обробку послідовних запитів.

## 6. Скасування запиту
- **Опис**: `AbortController` дозволяє скасувати `fetch`-запит до його завершення.
- **Приклад**:
  ```javascript
  const controller = new AbortController();
  const signal = controller.signal;

  setTimeout(() => controller.abort(), 3000); // Скасування через 3s

  fetch("https://api.example.com/long-request", { signal })
    .then(response => response.json())
    .then(data => console.log("Дані:", data))
    .catch(error => {
      if (error.name === "AbortError") console.log("Запит скасовано");
      else console.error("Помилка:", error);
    });
  ```
- **Примітка**: `signal` додається до опцій `fetch` для підтримки скасування.

## 7. Покращені сценарії
- **Опис**: `fetch` підтримує складніші випадки, такі як паралельні запити чи кешування.
- **Приклад (паралельні запити з `Promise.all`)**:
  ```javascript
  const urls = [
    "https://api.example.com/post1",
    "https://api.example.com/post2"
  ];
  Promise.all(urls.map(url => fetch(url).then(res => res.json())))
    .then(data => console.log("Усі дані:", data))
    .catch(error => console.error("Помилка:", error));
  ```
- **Приклад (кешування)**:
  ```javascript
  fetch("https://api.example.com/data", { cache: "force-cache" })
    .then(response => response.json())
    .then(data => console.log("Дані з кешу:", data));
  ```
- **Примітка**: Використовуйте `cache: "no-store"` для уникнення кешу.

## Особливості для співбесід — Питання та відповіді

### 1. Що таке `fetch` і як він працює?
- **Відповідь**: `fetch` — метод для HTTP-запитів, повертає проміс із `Response`. Вирішується навіть при помилкових статусах.
  ```javascript
  fetch("url").then(res => res.json());
  ```

### 2. Чим `fetch` відрізняється від `XMLHttpRequest`?
- **Відповідь**: `fetch` базується на промісах, простіший і сучасніший, на відміну від колбеків у `XMLHttpRequest`.
  ```javascript
  // fetch
  fetch("url").then(res => res.text());
  // XMLHttpRequest
  const xhr = new XMLHttpRequest(); xhr.open("GET", "url");
  ```

### 3. Як обробляти помилки в `fetch`?
- **Відповідь**: Перевіряйте `response.ok` і використовуйте `.catch()` або `try/catch`.
  ```javascript
  fetch("url").then(res => { if (!res.ok) throw Error(res.status); });
  ```

### 4. Як відправити дані через POST із `fetch`?
- **Відповідь**: Встановіть `method: "POST"`, додайте `headers` і `body` із `JSON.stringify`.
  ```javascript
  fetch("url", { method: "POST", body: JSON.stringify({ key: "value" }) });
  ```

### 5. Як скасувати запит із `fetch`?
- **Відповідь**: Використовуйте `AbortController` із `signal`.
  ```javascript
  const controller = new AbortController(); controller.abort();
  fetch("url", { signal: controller.signal });
  ```

### 6. Як завантажити бінарні дані (наприклад, зображення)?
- **Відповідь**: Використовуйте `response.blob()` і `URL.createObjectURL`.
  ```javascript
  fetch("image.jpg").then(res => res.blob()).then(blob => {
    document.body.innerHTML = `<img src="${URL.createObjectURL(blob)}">`;
  });
  ```

### 7. Як обробляти паралельні запити?
- **Відповідь**: Використовуйте `Promise.all` для одночасного виконання кількох `fetch`.
  ```javascript
  Promise.all([fetch("url1"), fetch("url2")]).then(responses => Promise.all(responses.map(r => r.json())));
  ```

## Поради
- **Перевіряйте статус**: Завжди перевіряйте `response.ok` перед парсингом.
- **Використовуйте `async/await`**: Для читабельного коду замість ланцюжків `.then()`.
- **Налаштовуйте заголовки**: Додавайте `Content-Type` для коректної обробки `body`.
- **Тестуйте помилки**: Симулюйте 404 або мережеві збої для надійності.
- **Скасовуйте запити**: Застосовуйте `AbortController` для тривалих операцій.
- **Оптимізуйте продуктивність**: Використовуйте `cache` для повторних запитів.
- **Захищайте дані**: Уникайте відправки чутливих даних без шифрування (HTTPS).
- **Тестуйте асинхронність**: Перевіряйте код із затримками чи помилками.