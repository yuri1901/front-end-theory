# Асинхронний JavaScript: Детальний конспект за матеріалами MDN

## Загальна інформація

- **Опис**: Асинхронний JavaScript дозволяє виконувати операції (наприклад, мережеві запити, таймери, анімації) без блокування основного потоку, використовуючи механізми на кшталт Event Loop, промісів, Web Workers і `requestAnimationFrame`.
- **Призначення**: Забезпечує плавність роботи веб-додатків, обробляючи довготривалі задачі асинхронно.
- **Особливості**: Включає проміси, `async/await`, багатопоточність через Workers і послідовне планування анімацій.
- **Контекст**: Критичний для сучасних веб-технологій, таких як API-запити та інтерактивні інтерфейси.

## 1. Вступ до асинхронного JavaScript
- **Опис**: Асинхронність — це спосіб виконання коду, коли певні операції не блокують основний потік. У JavaScript це реалізується через Event Loop і черги завдань.
- **Основні концепції**:
  - **Синхронність**: Код виконується послідовно (наприклад, `console.log("1"); console.log("2");`).
  - **Асинхронність**: Операції (наприклад, `setTimeout`) відкладаються до наступного циклу Event Loop.
  - **Callback-hell**: Вкладені колбеки ускладнюють код; вирішується через проміси чи `async/await`.
  - **Event Loop**: Механізм, який чергує синхронний і асинхронний код.
- **Приклад**:
  ```javascript
  console.log("Початок");
  setTimeout(() => console.log("Асинхронний виклик"), 0);
  console.log("Кінець");
  // Виведе: Початок, Кінець, Асинхронний виклик (через затримку)
  ```
- **Примітка**: Навіть із `setTimeout(0)` асинхронний код виконується після синхронного через Event Loop.

## 2. Проміси
- **Опис**: Проміси — об’єкти, які представляють майбутнє значення асинхронної операції з трьома станами: `pending`, `fulfilled`, `rejected`.
- **Стани та методи**:
  - **Pending**: Початковий стан, доки операція триває.
  - **Fulfilled**: Успішне завершення з результатом.
  - **Rejected**: Помилка з причиною.
  - **`.then(onFulfilled, onRejected)`**: Обробка `fulfilled` або `rejected`.
  - **`.catch(onRejected)`**: Обробка помилок.
  - **`.finally(onFinally)`**: Виконання після завершення (незалежно від стану).
- **Приклад**:
  ```javascript
  let promise = new Promise((resolve, reject) => {
    let success = Math.random() > 0.3;
    setTimeout(() => (success ? resolve("Дані") : reject("Помилка")), 1000);
  });
  promise
    .then(data => console.log(data))
    .catch(error => console.error(error))
    .finally(() => console.log("Завершено"));
  ```
- **Ланцюжок**:
  ```javascript
  Promise.resolve(1)
    .then(x => x + 1)
    .then(y => y * 2)
    .then(console.log); // Виведе: 4
  ```

## 3. Реалізація API на основі промісів
- **Опис**: Створення власного API з промісами для імітації асинхронних операцій, таких як мережеві запити.
- **Приклад**:
  ```javascript
  function fetchUserData(id) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        const user = { id, name: "Іван" };
        Math.random() > 0.2 ? resolve(user) : reject("Користувача не знайдено");
      }, 1000);
    });
  }
  fetchUserData(1)
    .then(user => console.log(`Користувач: ${user.name}`))
    .catch(error => console.error(error));
  ```
- **Порада**: Використовуйте для симуляції API з випадковими затримками чи помилками.

## 4. Вступ до Web Workers
- **Опис**: Web Workers дозволяють виконувати JavaScript у окремому потоці, уникаючи блокування UI.
- **Типи**:
  - **Dedicated Workers**: Прив’язані до одного скрипта.
  - **Shared Workers**: Доступні кільком контекстам (наприклад, кільком вкладкам).
- **Обмеження**: Не мають доступу до DOM, але можуть обмінюватися даними через `postMessage`.
- **Приклад**:
  ```javascript
  // main.js
  const worker = new Worker("worker.js");
  worker.postMessage({ task: "compute", data: 1000000 });
  worker.onmessage = (e) => console.log(`Результат: ${e.data}`);

  // worker.js
  self.onmessage = (e) => {
    let sum = 0;
    for (let i = 0; i < e.data.data; i++) sum += i;
    self.postMessage(sum);
  };
  ```
- **Примітка**: Ідеально для обчислень, які займають багато часу.

## 5. Послідовність анімацій
- **Опис**: Використання `requestAnimationFrame` для створення плавних анімацій із контролем послідовності.
- **Механізм**: Викликається перед кожним рендером кадру, оптимізуючи продуктивність.
- **Приклад**:
  ```javascript
  const canvas = document.createElement("canvas");
  document.body.appendChild(canvas);
  const ctx = canvas.getContext("2d");
  let x = 0;
  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillRect(x, 50, 20, 20);
    x = (x + 1) % canvas.width;
    requestAnimationFrame(animate);
  }
  animate();
  ```
- **Асинхронна послідовність із промісами**:
  ```javascript
  function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
  async function sequence() {
    for (let i = 0; i < 5; i++) {
      ctx.fillRect(i * 20, 50, 20, 20);
      await delay(500);
    }
  }
  sequence();
  ```

## Особливості для співбесід — Питання та відповіді

### 1. Що таке асинхронний JavaScript і як він працює?
- **Відповідь**: Асинхронність дозволяє виконувати задачі у фоновому режимі через Event Loop. Наприклад, `setTimeout` відкладає код.
  ```javascript
  setTimeout(() => console.log("Пізніше"), 1000);
  ```

### 2. Які стани має проміс і як їх обробляти?
- **Відповідь**: `pending`, `fulfilled`, `rejected`. Обробка: `.then()` (успіх), `.catch()` (помилка), `.finally()` (завершення).
  ```javascript
  new Promise((res) => res("OK")).then(console.log);
  ```

### 3. Як працює ланцюжок `.then()`?
- **Відповідь**: Кожен `.then()` повертає новий проміс, дозволяючи послідовну обробку.
  ```javascript
  Promise.resolve(1).then(x => x + 1).then(console.log); // 2
  ```

### 4. У чому різниця між `Promise.all()` і `Promise.race()`?
- **Відповідь**: `Promise.all()` чекає всіх промісів, `Promise.race()` повертає перший результат.
  ```javascript
  Promise.all([Promise.resolve(1), Promise.resolve(2)]).then(console.log); // [1, 2]
  Promise.race([Promise.resolve(1), new Promise(r => setTimeout(r, 1000))]).then(console.log); // 1
  ```

### 5. Що таке Web Workers і для чого вони?
- **Відповідь**: Workers виконують код у фоновому потоці, уникаючи блокування UI.
  ```javascript
  const worker = new Worker("worker.js");
  worker.postMessage("Обчислити");
  ```

### 6. Як створювати плавні анімації?
- **Відповідь**: Використовуйте `requestAnimationFrame` для синхронізації з рендером.
  ```javascript
  function animate() { requestAnimationFrame(animate); }
  animate();
  ```

### 7. Як уникнути "callback hell" із промісами?
- **Відповідь**: Використовуйте ланцюжок `.then()` або `async/await`.
  ```javascript
  async function fetchData() { let data = await Promise.resolve("Дані"); console.log(data); }
  ```

## Поради
- **Розумійте Event Loop**: Вивчіть, як асинхронний код потрапляє в чергу.
- **Практикуйте проміси**: Пишіть ланцюжки з `.then()` і тестуйте помилки.
- **Використовуйте Workers**: Для складних обчислень, щоб не гальмувати UI.
- **Оптимізуйте анімації**: Застосовуйте `requestAnimationFrame` замість `setInterval`.
- **Експериментуйте з `async/await`**: Перетворюйте складні проміси на читабельний код.
- **Тестуйте**: Перевіряйте асинхронні операції з `jest` (`.resolves`, `.rejects`).