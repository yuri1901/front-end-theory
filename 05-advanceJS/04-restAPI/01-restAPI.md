# REST API — Конспект

## Що таке REST API?

**REST** (Representational State Transfer) — стиль архітектури для створення веб-сервісів.  
**API** (Application Programming Interface) — інтерфейс взаємодії між клієнтом і сервером.  
**REST API** — набір правил і стандартів для створення веб-сервісів, які працюють по протоколу HTTP.

## Основні HTTP методи (CRUD операції)

| Метод  | Призначення                | Опис                                    |
| ------ | -------------------------- | --------------------------------------- |
| GET    | Отримання даних            | Запит на отримання ресурсу (або списку) |
| POST   | Створення нового ресурсу   | Відправка нових даних на сервер         |
| PUT    | Повне оновлення ресурсу    | Замінює існуючий ресурс новими даними   |
| PATCH  | Часткове оновлення ресурсу | Змінює частину даних ресурсу            |
| DELETE | Видалення ресурсу          | Видаляє ресурс на сервері               |

## Приклад URL в REST API

```bash
https://api.example.com/users          # Всі користувачі (GET)
https://api.example.com/users/123      # Користувач з id=123 (GET, PUT, PATCH, DELETE)
```

## Приклади запитів

### 1. GET — отримати список ресурсів

```javascript
fetch("https://api.example.com/users")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 2. GET — отримати ресурс за ID

```javascript
fetch("https://api.example.com/users/123")
  .then((res) => res.json())
  .then((user) => console.log(user));
```

### 3. POST — створити новий ресурс

```javascript
fetch("https://api.example.com/users", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Yuri", age: 21 }),
})
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 4. PUT — повністю оновити ресурс

```javascript
fetch("https://api.example.com/users/123", {
  method: "PUT",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Yuri New", age: 22 }),
})
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 5. PATCH — частково оновити ресурс

```javascript
fetch("https://api.example.com/users/123", {
  method: "PATCH",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ age: 23 }),
})
  .then((res) => res.json())
  .then((data) => console.log(data));
```

### 6. DELETE — видалити ресурс

```javascript
fetch("https://api.example.com/users/123", {
  method: "DELETE",
}).then((res) => {
  if (res.ok) {
    console.log("Користувача видалено");
  }
});
```

## Заголовки (Headers)

- **Content-Type: application/json** — вказує, що тіло запиту має формат JSON.
- **Accept: application/json** — клієнт очікує отримати відповідь у JSON.

## Основні поняття

- **Ресурс** — будь-який об'єкт, який доступний через API (користувач, пост, товар тощо).
- **Ідентифікатор ресурсу** — унікальний ID, який дозволяє звернутися до конкретного ресурсу.

### Статуси HTTP відповіді:

- **200 OK** — успішний запит
- **201 Created** — ресурс успішно створено (POST)
- **204 No Content** — успішне виконання без тіла відповіді (DELETE)
- **400 Bad Request** — некоректний запит
- **404 Not Found** — ресурс не знайдено
- **500 Internal Server Error** — помилка сервера

## Поради

- Використовуй `async/await` або проміси для асинхронних HTTP-запитів.
- Обробляй помилки з `try/catch` або `.catch()`.
- Валідуй дані перед відправкою на сервер.
- Використовуй зрозумілі імена ендпоінтів у URL.
- Для часткових змін ресурсів краще застосовуй PATCH, а не PUT.
- Дотримуйся REST-стандартів для зручності та масштабованості.

## Корисні ресурси

- [MDN Web Docs: Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [REST API Tutorial](https://restfulapi.net/)
- [Postman — тестування API](https://www.postman.com/)
