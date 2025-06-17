# Обробка подій у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Обробка подій дозволяє реагувати на дії користувача (кліки, введення) або системні події (зміна розміру). Використовує Web API для додавання, видалення та диспетчеризації подій.
- **Контекст**: Створення інтерактивних вебінтерфейсів, управління поведінкою сторінки.
- **Основні компоненти**:
  - `addEventListener`, `removeEventListener`, `dispatchEvent`.
  - Модифікатори: `preventDefault`, `stopPropagation`.
  - Типи подій: `click`, `input`, `scroll`, тощо.
- **Особливості**:
  - Асинхронна природа, потреба в очищенні слухачів.
  - Сумісність із HTML-атрибутами (onClick).

## Приклади коду

### 1. Додавання та видалення подій

#### `addEventListener`

- Додає обробник із підтримкою стрілкових функцій.

```javascript
const btn = document.querySelector("button");
btn.addEventListener("click", () => console.log("Клікнуто!"));
```

#### `removeEventListener`

- Видаляє обробник, вимагаючи однакову функцію.

```javascript
const handleClick = () => console.log("Клік");
btn.addEventListener("click", handleClick);
btn.removeEventListener("click", handleClick); // Точно та сама функція
```

### 2. Диспетчеризація подій

#### `dispatchEvent`

- Викликає кастомну подію.

```javascript
const event = new Event("customEvent");
btn.addEventListener("customEvent", () => console.log("Кастомна подія!"));
btn.dispatchEvent(event);
```

### 3. Модифікація поведінки

#### `preventDefault` і `stopPropagation`

- Керує стандартною поведінкою та поширенням.

```javascript
const link = document.querySelector("a");
link.addEventListener("click", (e) => {
  e.preventDefault(); // Блокує перехід
  e.stopPropagation(); // Зупиняє поширення
  console.log("Посилання заблоковано");
});
```

### 4. Інтерактивний приклад

```javascript
const input = document.querySelector("input");
const log = document.querySelector("#log");

input.addEventListener("input", (e) => {
  log.textContent = `Введено: ${e.data}`;
});

const customBtn = document.querySelector("#customBtn");
customBtn.addEventListener("click", () => {
  const event = new Event("customInput");
  input.dispatchEvent(event);
  log.textContent += " (Кастомна подія)";
});
```

## Особливості для співбесід — Питання та відповіді

### Що таке подія в JavaScript?

- **Відповідь**: Подія — сигнал про дію (клік, введення), обробляється через `addEventListener`.
  ```javascript
  btn.addEventListener("click", () => console.log("Подія"));
  ```

### Чим відрізняються `preventDefault` і `stopPropagation`?

- **Відповідь**: `preventDefault` блокує стандартну поведінку, `stopPropagation` — поширення.
  ```javascript
  e.preventDefault(); // Блокує
  e.stopPropagation(); // Зупиняє
  ```

### Як видалити обробник події?

- **Відповідь**: Використовуйте `removeEventListener` із тією самою функцією.
  ```javascript
  const fn = () => {};
  btn.addEventListener("click", fn);
  btn.removeEventListener("click", fn);
  ```

### Чи можна диспетчеризувати кастомні події?

- **Відповідь**: Так, через `new Event` і `dispatchEvent`.
  ```javascript
  const event = new Event("custom");
  document.dispatchEvent(event);
  ```

### Чи впливають стрілкові функції на `this` у подіях?

- **Відповідь**: Так, `this` посилається на глобальний об’єкт, а не елемент.
  ```javascript
  btn.addEventListener("click", () => console.log(this)); // undefined
  ```

## Поради

- **Очищення**: Завжди видаляйте `removeEventListener` для уникнення витоків.
- **Стрілкові функції**: Уникайте їх для методів, де потрібен `this` (використовуйте `function`).
- **Блокування**: Використовуйте `preventDefault` лише за потреби.
- **Оптимізація**: Обмежте слухачі для складних DOM-структур.
- **Тестування**: Емулюйте події для дебагінгу.

## Додаткові деталі

- **Типи подій**: `click`, `keydown`, `resize`, `submit` (див. MDN Events).
- **Event об’єкт**: Властивості `target`, `type`, `bubbles`, `cancelable`.
- **Сумісність**: `dispatchEvent` з IE9+, стрілкові функції з ES6.
- **HTML-атрибути**: `onclick`, `onchange` як альтернатива.
