# Обробка помилок у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Обробка помилок у JavaScript дозволяє контролювати та управляти помилковими ситуаціями за допомогою конструкцій `try...catch`, `throw` та `finally`. Це забезпечує стабільність і зрозумілість коду.
- **Основні компоненти**:
  - **`try`**: Блок коду, який перевіряється на помилки.
  - **`catch`**: Обробка помилки, якщо вона сталася.
  - **`finally`**: Виконується завжди, незалежно від результату.
  - **`throw`**: Створює власну помилку.
- **Особливості**:
  - Помилки є об’єктами типу `Error` або його похідних.
  - Підтримує асинхронну обробку з `async/await`.
- **Контекст**: Захист від збоїв, дебагінг, користувацький досвід.

## Приклади коду

### Базовий `try...catch`

```javascript
try {
  let result = someUndefinedFunction(); // Викликає помилку
} catch (error) {
  console.log("Помилка: " + error.message); // Помилка: someUndefinedFunction is not defined
}
```

### Використання `throw`

```javascript
function checkAge(age) {
  if (age < 0) {
    throw new Error("Вік не може бути від’ємним!");
  }
  return "Вік валідний";
}
try {
  console.log(checkAge(-1)); // Викличе помилку
} catch (error) {
  console.log(error.message); // Вік не може бути від’ємним!
}
```

### Використання `finally`

```javascript
try {
  let result = JSON.parse("{invalid json}");
} catch (error) {
  console.log("Помилка парсингу: " + error.message);
} finally {
  console.log("Блок finally виконано"); // Виконується завжди
}
```

### Обробка асинхронних помилок

```javascript
async function fetchData() {
  try {
    let response = await fetch("https://invalid.url");
    let data = await response.json();
    return data;
  } catch (error) {
    console.log("Помилка: " + error.message);
  }
}
fetchData();
```

## Особливості для співбесід — Питання та відповіді

### Що таке `try...catch` і як він працює?

- **Відповідь**: `try` виконує код, `catch` обробляє помилки, якщо вони виникають.
  ```javascript
  try {
    console.log(x);
  } catch (e) {
    console.log("x не визначено");
  } // x не визначено
  ```

### Чи можна кинути власну помилку?

- **Відповідь**: Так, за допомогою `throw new Error()`.
  ```javascript
  function validate() {
    throw new Error("Помилка валідції");
  }
  try {
    validate();
  } catch (e) {
    console.log(e.message);
  } // Помилка валідції
  ```

### Чи завжди виконується `finally`?

- **Відповідь**: Так, навіть якщо є `return` чи виняток не оброблено.
  ```javascript
  try {
    return 1;
  } catch (e) {
  } finally {
    console.log("Finally");
  } // Finally
  ```

### Як обробляти помилки в асинхронному коді?

- **Відповідь**: Використовуйте `try...catch` навколо `await`.
  ```javascript
  async function test() {
    try {
      await Promise.reject("Помилка");
    } catch (e) {
      console.log(e);
    }
  }
  test(); // Помилка
  ```

### Які типи помилок є в JavaScript?

- **Відповідь**: `Error`, `SyntaxError`, `TypeError`, `ReferenceError` тощо.
  ```javascript
  try {
    throw new TypeError("Невірний тип");
  } catch (e) {
    console.log(e.name);
  } // TypeError
  ```

## Поради

- **Використовуйте `try...catch`**: Для захисту критичних блоків коду.
- **Кидати осмислені помилки**: Додавайте деталі в `throw new Error(message)`.
- **Завжди додавайте `finally`**: Для очищення ресурсів (наприклад, закриття файлів).
- **Обробляйте асинхронність**: Використовуйте `try...catch` з `async/await`.
- **Логуйте помилки**: Використовуйте `console.error` чи зовнішні сервіси.
- **Тестуйте сценарії**: Перевіряйте поведінку при різних типах помилок.

## Додаткові деталі

- **Типи помилок**:
  - `ReferenceError`: Посилання на неіснуючу змінну.
  - `TypeError`: Невірний тип даних.
  - `RangeError`: Значення поза допустимим діапазоном.
  - `SyntaxError`: Синтаксична помилка.
- **Стек виклику**: Властивість `error.stack` показує ланцюжок викликів.
  ```javascript
  try {
    throw new Error("Тест");
  } catch (e) {
    console.log(e.stack);
  }
  ```
