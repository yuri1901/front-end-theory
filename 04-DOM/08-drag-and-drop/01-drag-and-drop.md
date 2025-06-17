# Детальний конспект: HTML Drag and Drop API та атрибут draggable

## Загальна інформація

- **Опис**: HTML Drag and Drop API — це набір інструментів у веб-розробці, який дозволяє користувачам перетягувати (drag) елементи та скидати (drop) їх у визначені зони. Атрибут `draggable` визначає, чи елемент може бути перетягнутим. API базується на подіях і об’єкті `DataTransfer` для передачі даних.
- **Контекст**: Використовується для створення інтерактивних інтерфейсів, таких як сортування списків, переміщення елементів, завантаження файлів або створення редакторів (наприклад, Kanban-дошки).
- **Основні компоненти**:
  - **Атрибут `draggable`**: HTML-атрибут (`true`, `false`, `auto`), що визначає, чи можна перетягувати елемент.
  - **Події Drag and Drop**:
    - `dragstart`: Починається, коли користувач починає перетягувати елемент.
    - `drag`: Викликається під час перетягування.
    - `dragenter`: Елемент входить у зону скидання.
    - `dragover`: Елемент рухається над зоною скидання.
    - `dragleave`: Елемент покидає зону скидання.
    - `drop`: Елемент скинуто у зону.
    - `dragend`: Перетягування завершено.
  - **Об’єкт `DataTransfer`**: Зберігає дані (текст, файли, типи MIME) під час операції перетягування.
- **Особливості**:
  - Потребує явного дозволу для скидання через `e.preventDefault()` у подіях `dragover` та `dragenter`.
  - Атрибут `draggable` за замовчуванням працює для зображень (`<img>`) та посилань (`<a>`), якщо не вказано інше.
  - Підтримка у всіх сучасних браузерах (Chrome, Firefox, Safari, Edge), але є нюанси в старих версіях (наприклад, IE9+).
  - Можливість кастомізації, наприклад, стилізація елемента під час перетягування або створення "примарного" зображення (drag image).

## Приклади коду

### 1. Базовий приклад Drag and Drop

#### HTML-структура

Створюємо елемент, який можна перетягувати, та зону для скидання.

```html
<div id="draggable" draggable="true">Перетягни мене!</div>
<div id="dropzone">Скинь сюди</div>
```

#### CSS

Стилі для кращої візуалізації.

```css
#draggable {
  width: 100px;
  height: 100px;
  background: lightblue;
  text-align: center;
  line-height: 100px;
  cursor: move;
}
#dropzone {
  width: 200px;
  height: 200px;
  background: lightgray;
  border: 2px dashed black;
  text-align: center;
  line-height: 200px;
}
```

#### JavaScript

Обробка подій для перетягування та скидання.

```javascript
const draggable = document.getElementById("draggable");
const dropzone = document.getElementById("dropzone");

// Початок перетягування
draggable.addEventListener("dragstart", (e) => {
  e.dataTransfer.setData("text/plain", e.target.id); // Зберігаємо ID елемента
  e.target.style.opacity = "0.5"; // Візуальний ефект
});

// Дозволяємо скидання в зону
dropzone.addEventListener("dragover", (e) => {
  e.preventDefault(); // Дозволяємо скидання
});

// Обробка входження в зону
dropzone.addEventListener("dragenter", (e) => {
  e.target.style.background = "lightgreen"; // Візуальний ефект
});

// Обробка покидання зони
dropzone.addEventListener("dragleave", (e) => {
  e.target.style.background = "lightgray"; // Повертаємо стиль
});

// Обробка скидання
dropzone.addEventListener("drop", (e) => {
  e.preventDefault();
  const id = e.dataTransfer.getData("text/plain"); // Отримуємо ID
  const draggedElement = document.getElementById(id);
  e.target.appendChild(draggedElement); // Переміщуємо елемент
  e.target.style.background = "lightgray"; // Повертаємо стиль
  draggedElement.style.opacity = "1"; // Повертаємо прозорість
});

// Завершення перетягування
draggable.addEventListener("dragend", (e) => {
  e.target.style.opacity = "1"; // Повертаємо прозорість
});
```

### 2. Передача даних через `DataTransfer`

Передаємо текстовий вміст елемента під час перетягування.

```javascript
draggable.addEventListener("dragstart", (e) => {
  e.dataTransfer.setData("text/plain", "Привіт, це дані!");
});

dropzone.addEventListener("drop", (e) => {
  e.preventDefault();
  const data = e.dataTransfer.getData("text/plain");
  e.target.textContent = `Отримано: ${data}`;
});
```

### 3. Кастомне зображення для перетягування

Задаємо власне зображення для відображення під час перетягування.

```javascript
draggable.addEventListener("dragstart", (e) => {
  const img = new Image();
  img.src = "custom-drag-image.png"; // Шлях до зображення
  e.dataTransfer.setDragImage(img, 10, 10); // Зміщення (x, y)
  e.dataTransfer.setData("text/plain", e.target.id);
});
```

### 4. Обробка файлів через Drag and Drop

Дозволяємо скидати файли в зону.

```javascript
dropzone.addEventListener("dragover", (e) => {
  e.preventDefault();
});

dropzone.addEventListener("drop", (e) => {
  e.preventDefault();
  const files = e.dataTransfer.files; // Отримуємо файли
  for (const file of files) {
    console.log(`Файл: ${file.name}, розмір: ${file.size} байт`);
    // Наприклад, виведення назви та розміру файлу
    dropzone.textContent = `Завантажено: ${file.name}`;
  }
});
```

## Особливості для співбесід — Питання та відповіді

### Що таке атрибут `draggable`?

- **Відповідь**: HTML-атрибут, який визначає, чи можна перетягувати елемент. Значення: `true` (дозволяє), `false` (забороняє), `auto` (залежить від браузера, зазвичай для `<img>` і `<a>`).
  ```html
  <div draggable="true">Перетягуй!</div>
  ```

### Які основні події Drag and Drop API?

- **Відповідь**: `dragstart`, `drag`, `dragenter`, `dragover`, `dragleave`, `drop`, `dragend`. Наприклад:
  ```javascript
  element.addEventListener("dragstart", (e) => {
    e.dataTransfer.setData("text/plain", "дані");
  });
  ```

### Що робить об’єкт `DataTransfer`?

- **Відповідь**: Зберігає дані, які передаються під час перетягування. Основні методи: `setData`, `getData`, `setDragImage`.
  ```javascript
  e.dataTransfer.setData("text/plain", "дані");
  const data = e.dataTransfer.getData("text/plain");
  ```

### Чому потрібно викликати `preventDefault` у `dragover`?

- **Відповідь**: За замовчуванням браузер блокує скидання. `e.preventDefault()` дозволяє зону для скидання.
  ```javascript
  dropzone.addEventListener("dragover", (e) => e.preventDefault());
  ```

### Як стилізувати елемент під час перетягування?

- **Відповідь**: Використовуйте подію `dragstart` для зміни стилів або `setDragImage` для кастомного зображення.
  ```javascript
  draggable.addEventListener("dragstart", (e) => {
    e.target.style.opacity = "0.5";
  });
  ```

### Чи можна перетягувати файли?

- **Відповідь**: Так, через `e.dataTransfer.files` у події `drop`.
  ```javascript
  dropzone.addEventListener("drop", (e) => {
    e.preventDefault();
    const files = e.dataTransfer.files;
    console.log(files[0].name);
  });
  ```

## Поради

- **Очищення слухачів**: Видаляйте обробники подій (`removeEventListener`), якщо елементи динамічно видаляються, щоб уникнути витоків пам’яті.
- **Запобігання помилкам**: Завжди викликайте `preventDefault` у `dragover` і `dragenter` для зон скидання.
- **Оптимізація**: Обмежуйте кількість слухачів для великих DOM-структур, використовуйте делегування подій.
- **Тестування**: Перевіряйте поведінку в різних браузерах, особливо для кастомних зображень (`setDragImage`) та файлів.
- **Доступність**: Додавайте альтернативні способи взаємодії (наприклад, клавіатура) для користувачів, які не можуть використовувати мишу.
- **Кастомізація**: Використовуйте `setDragImage` для кращого UX, наприклад, для відображення зменшеної копії елемента.

## Додаткові деталі

- **Типи даних у `DataTransfer`**:
  - `text/plain`: Звичайний текст.
  - `text/html`: HTML-вміст.
  - `Files`: Для завантаження файлів.
- **Властивості `DataTransfer`**:
  - `dropEffect`: Визначає тип операції (наприклад, `copy`, `move`, `link`).
  - `effectAllowed`: Обмежує дозволені операції.
  - `items`: Список переданих даних.
- **Сумісність**:
  - Повна підтримка у Chrome, Firefox, Safari, Edge.
  - Обмежена підтримка в IE (з версії 9, без `setDragImage`).
- **Альтернативи**:
  - Бібліотеки, такі як `react-dnd` або `sortable.js`, спрощують складні сценарії.
- **Обмеження**:
  - Не всі елементи підтримують `draggable="true"` за замовчуванням (наприклад, `<div>` потребує явного встановлення).
  - Мобільні пристрої мають обмежену підтримку Drag and Drop (краще використовувати touch-події).
