# 🛠️ Конспект: Element та методи вставки/заміни елементів

Цей конспект охоплює інтерфейс **Element**, методи для вставки та заміни елементів у DOM, а також роботу з HTML і текстом у певних позиціях.

---

## 🖼️ Що таке Element?

- **Element** — це підтип `Node`, який представляє HTML-елементи (наприклад, `<div>`, `<p>`).
- Надає додаткові методи для роботи з атрибутами, класами, стилями та вставкою вмісту.
- Відмінність від `Node`:
  - `Node` включає всі типи вузлів (текст, коментарі, елементи).
  - `Element` працює лише з HTML-елементами.

---

## 🛠️ Методи вставки елементів

### 🔹 `Element.append(...nodesOrDOMStrings)`

- Додає один або кілька вузлів чи рядків (як HTML) як останні дочірні елементи.
- На відміну від `appendChild`, підтримує вставку рядків.
- Приклад:
  ```js
  const parent = document.querySelector(".container");
  parent.append("Текст", document.createElement("span"));
  ```

### 🔹 `Element.insertAdjacentElement(position, element)`

- Вставляє елемент у вказану позицію відносно цільового елемента.
- Позиції:
  - `'beforebegin'`: Перед елементом.
  - `'afterbegin'`: Всередині, на початку.
  - `'beforeend'`: Всередині, в кінці.
  - `'afterend'`: Після елемента.
- Приклад:
  ```js
  const div = document.querySelector(".container");
  const span = document.createElement("span");
  div.insertAdjacentElement("afterbegin", span); // Вставка на початку div
  ```

### 🔹 `Element.insertAdjacentHTML(position, html)`

- Вставляє HTML-рядок у вказану позицію.
- Небезпечно для введення користувачем через ризик XSS.
- Приклад:
  ```js
  const div = document.querySelector(".container");
  div.insertAdjacentHTML("beforeend", "<p>Новий параграф</p>");
  ```

### 🔹 `Element.insertAdjacentText(position, text)`

- Вставляє текстовий рядок у вказану позицію (без парсингу HTML).
- Безпечніше, ніж `insertAdjacentHTML`.
- Приклад:
  ```js
  const div = document.querySelector(".container");
  div.insertAdjacentText("beforeend", "Простий текст");
  ```

---

## 🛠️ Заміна елементів

### 🔹 `Element.replaceWith(...nodesOrDOMStrings)`

- Замінює елемент одним або кількома вузлами чи HTML-рядками.
- На відміну від `replaceChild`, працює на самому елементі, а не на батьківському.
- Приклад:
  ```js
  const div = document.querySelector(".item");
  const span = document.createElement("span");
  div.replaceWith(span, "Текст"); // Замінює div на span і текст
  ```

---

## 📊 Порівняння методів вставки

| Метод                   | Тип вставки     | Позиція           | Безпека (XSS) | Повертає        |
| ----------------------- | --------------- | ----------------- | ------------- | --------------- |
| `appendChild`           | Вузол           | Останній дочірній | Безпечний     | Доданий вузол   |
| `append`                | Вузли/рядки     | Останній дочірній | Залежить      | Нічого          |
| `insertAdjacentElement` | Вузол           | 4 позиції         | Безпечний     | Доданий елемент |
| `insertAdjacentHTML`    | HTML-рядок      | 4 позиції         | Небезпечно    | Нічого          |
| `insertAdjacentText`    | Текстовий рядок | 4 позиції         | Безпечний     | Нічого          |

---

## 📘 Ключові рекомендації

- Використовуйте `append` для зручного додавання кількох вузлів або тексту.
- Для точної вставки в певну позицію віддавайте перевагу `insertAdjacentElement` або `insertAdjacentText`.
- Уникайте `insertAdjacentHTML` для введення користувачем через ризик XSS-атак.
- Для заміни елементів використовуйте `replaceWith` замість `replaceChild`, якщо не потрібна робота з батьківським вузлом.
- Перевіряйте типи вузлів перед операціями, щоб уникнути помилок (наприклад, `insertAdjacentElement` працює лише з елементами).
