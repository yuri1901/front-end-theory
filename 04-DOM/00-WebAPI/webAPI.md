# Web API у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Web API — це вбудовані інтерфейси браузера, які розширюють JavaScript для взаємодії з веб-оточенням (DOM, мережа, зберігання, таймери тощо). Вони доступні через глобальний об’єкт `window`.
- **Контекст**:
  - Використовуються для маніпуляції DOM, асинхронних операцій і локального зберігання.
  - Є частиною стандарту WHATWG і доступні лише в браузерному середовищі.
- **Основні інтерфейси**:
  - `Window`: Управління вікном і глобальними функціями.
  - `fetch`: Асинхронні HTTP-запити.
  - `localStorage`/`sessionStorage`: Локальне зберігання даних.
  - `setTimeout`/`setInterval`: Таймери.
- **Особливості**:
  - Асинхронні за своєю природою (наприклад, `fetch`, таймери).
  - Не доступні в Node.js без поліфілів.
- **Застосування**: Веб-розробка, динамічний контент, збереження стану.

## Приклади коду

### 1. Window API (Управління вікном)

```javascript
// Розмір вікна
console.log(window.innerWidth, window.innerHeight);

// Таймер
const timer = setTimeout(() => console.log("Таймер сработал"), 2000);
clearTimeout(timer);

// Подія
window.addEventListener("resize", () => console.log("Розмір змінено"));
```

### 2. Fetch API (Мережеві запити)

```javascript
async function getData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Помилка:", error.message);
  }
}
getData();
```

### 3. LocalStorage API (Локальне зберігання)

```javascript
// Збереження
localStorage.setItem("user", JSON.stringify({ name: "Іван", age: 25 }));
// Читання
const user = JSON.parse(localStorage.getItem("user"));
console.log(user.name); // Іван
// Видалення
localStorage.removeItem("user");
// Очищення
localStorage.clear();
```

### 4. setTimeout/setInterval (Таймери)

```javascript
let count = 0;
const interval = setInterval(() => {
  console.log("Тік", ++count);
  if (count === 3) clearInterval(interval);
}, 1000);
```

## Особливості для співбесід — Питання та відповіді

### Що таке Web API і чим воно відрізняється від JavaScript?

- **Відповідь**: Web API — це бібліотеки браузера, які розширюють JavaScript. JS — це мова, а Web API — її інструменти.
  ```javascript
  console.log(typeof window.fetch); // function (Web API)
  ```

### Як працює `fetch`?

- **Відповідь**: Асинхронний запит до сервера, повертає `Promise`.
  ```javascript
  fetch("https://api.example.com")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
  ```

### Чим відрізняються `localStorage` і `sessionStorage`?

- **Відповідь**: `localStorage` зберігає дані безстроково, `sessionStorage` — лише на сесію.
  ```javascript
  localStorage.setItem("key", "value");
  sessionStorage.setItem("key", "value");
  // localStorage зберігається після закриття, sessionStorage — ні
  ```

### Чи можна уникнути витоків пам’яті з таймерами?

- **Відповідь**: Так, використовуйте `clearTimeout`/`clearInterval`.
  ```javascript
  const id = setInterval(() => {}, 1000);
  clearInterval(id);
  ```

### Як перевірити, чи підтримує браузер Web API?

- **Відповідь**: Використовуйте `window` або `typeof`.
  ```javascript
  if ("fetch" in window) console.log("Fetch підтримується");
  ```

## Поради

- **Перевіряйте сумісність**: Використовуйте `if ("api" in window)` для старих браузерів.
- **Обробляйте помилки**: Завжди додавайте `try...catch` або `.catch` до `fetch`.
- **Очищуйте таймери**: Викликайте `clearTimeout`/`clearInterval` для уникнення витоків.
- **Оптимізуйте зберігання**: Використовуйте `localStorage` для малих даних, уникайте великих об’єктів.
- **Тестуйте асинхронність**: Емулюйте затримки для дебагінгу.
- **Документуйте**: Пояснюйте використання API в складному коді.

## Додаткові деталі

- **Інші важливі Web API**:
  - \*\*`navigator`: Інформація про браузер (наприклад, `navigator.userAgent`).
  - \*\*`history`: Управління історією (наприклад, `history.back()`).
  - \*\*`geolocation`: Геолокація (наприклад, `navigator.geolocation.getCurrentPosition()`).
  - \*\*`canvas`: Графіка 2D/3D (наприклад, `canvas.getContext("2d")`).
- **Асинхронність**: Багато API (наприклад, `fetch`, `setTimeout`) базуються на `Promise` або коллбеках.
- **Поліфіли**: Для підтримки старих браузерів використовуйте бібліотеки (наприклад, `whatwg-fetch`).
