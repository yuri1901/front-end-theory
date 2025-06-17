# 📝 Конспект: Робота з атрибутами та класами в DOM

Цей конспект охоплює методи та властивості для роботи з атрибутами, класами та стилями HTML-елементів у DOM, а також використання кастомних `data-` атрибутів.

---

## 🛠️ Властивості та методи для роботи з атрибутами

### 🔹 `Element.attributes`

- Властивість, яка повертає **об’єкт `NamedNodeMap`**, що містить усі атрибути HTML-елемента.
- Доступ до атрибутів: через індекс (`attrs[0]`) або назву (`attrs.getNamedItem('id')`).
- Приклад:

```js
const bodyEl = document.body;
const attrs = bodyEl.attributes;
console.log(attrs); // NamedNodeMap {0: id, 1: class, ...}
console.log(attrs.getNamedItem("id").value); // значення атрибута id
```

---

### 🔹 `Element.setAttribute(name, value)`

- **Додає** новий атрибут або **змінює** значення існуючого атрибута.
- Якщо атрибут уже існує, його значення оновлюється.
- Синтаксис: `element.setAttribute(name, value)`
- Приклад:

```js
const div = document.querySelector("div");
div.setAttribute("id", "myDiv");
```

---

### 🔹 `Element.getAttribute(name)`

- **Повертає** значення атрибута за його назвою.
- Якщо атрибут відсутній, повертає `null`.
- Синтаксис: `element.getAttribute(name)`
- Приклад:

```js
const div = document.querySelector("div");
console.log(div.getAttribute("id")); // "myDiv" або null
```

---

### 🔹 `Element.hasAttribute(name)`

- **Перевіряє**, чи є у елемента вказаний атрибут.
- Повертає `true` або `false`.
- Синтаксис: `element.hasAttribute(name)`
- Приклад:

```js
const div = document.querySelector("div");
console.log(div.hasAttribute("id")); // true, якщо id існує
```

---

### 🔹 `Element.removeAttribute(name)`

- **Видаляє** вказаний атрибут з елемента.
- Якщо атрибут відсутній, нічого не відбувається.
- Синтаксис: `element.removeAttribute(name)`
- Приклад:

```js
const div = document.querySelector("div");
div.removeAttribute("id");
```

---

### 🔹 `Element.toggleAttribute(name, [force])`

- **Перемикає** атрибут: додає, якщо його немає, або видаляє, якщо є.
- Параметр `force` (необов’язковий):
  - `true` — завжди додає атрибут.
  - `false` — завжди видаляє атрибут.
- Синтаксис: `element.toggleAttribute(name, [force])`
- Приклад:

```js
const input = document.querySelector("input");
input.toggleAttribute("checked"); // додає або видаляє checked
input.toggleAttribute("disabled", true); // завжди додає disabled
```

---

## 📊 Кастомні `data-` атрибути

- **Data-атрибути** (`data-*`) дозволяють зберігати додаткову інформацію в HTML-елементах.
- Використовуються для передачі даних з HTML до JavaScript.
- Назва атрибута після `data-` може бути будь-якою (наприклад, `data-counter`, `data-user-id`).
- Доступ через:
  - **HTML**: `<span data-counter="19">Текст</span>`
  - **JavaScript**: через властивість `dataset` або методи `getAttribute`/`setAttribute`.

### 🔹 Властивість `dataset`

- Об’єкт `element.dataset` надає доступ до всіх `data-` атрибутів.
- Назва атрибута в `dataset` перетворюється з `kebab-case` на `camelCase` (наприклад, `data-user-id` → `dataset.userId`).
- Приклад:

```js
const span = document.querySelector("span");
span.setAttribute("data-counter", "19");
console.log(span.dataset.counter); // "19"
span.dataset.userId = "123"; // додає data-user-id="123"
```

### 🔹 Чому використовувати `data-` атрибути?

- **Семантика**: Зберігають дані, пов’язані з елементом, без впливу на CSS чи структуру.
- **Зручність**: Легкий доступ через `dataset`.
- **Безпечність**: Уникають конфліктів із зарезервованими атрибутами (наприклад, `id`, `class`).
- Приклад використання:

```html
<div data-product-id="101" data-category="electronics">Смартфон</div>
```

```js
const product = document.querySelector("div");
console.log(product.dataset.productId); // "101"
console.log(product.dataset.category); // "electronics"
```

---

## 🎨 Робота з класами

### 🔹 `Element.className`

- Повертає або встановлює значення атрибута `class` як **рядок**.
- **Не рекомендовано** для використання в JavaScript, оскільки замінює всі класи.
- Приклад:

```js
const div = document.querySelector("div");
div.className = "new-class"; // замінює всі класи на new-class
```

### 🔹 `Element.classList`

- Об’єкт для роботи з CSS-класами елемента.
- Методи:
  - `add(class)` — додає клас.
  - `remove(class)` — видаляє клас.
  - `toggle(class, [force])` — додає або видаляє клас; `force` (true/false) примусово додає/видаляє.
  - `contains(class)` — перевіряє, чи є клас.
  - `replace(oldClass, newClass)` — замінює один клас іншим.
- Приклад:

```js
const div = document.querySelector("div");
div.classList.add("active");
div.classList.remove("inactive");
div.classList.toggle("hidden");
console.log(div.classList.contains("active")); // true
div.classList.replace("active", "current");
```

---

## 🎨 Робота зі стилями

### 🔹 `Element.style.setProperty(property, value, [priority])`

- Встановлює CSS-властивість в inline-стилях елемента.
- Параметр `priority` (необов’язковий): наприклад, `'important'`.
- Приклад:

```js
const div = document.querySelector("div");
div.style.setProperty("color", "blue", "important");
```

### 🔹 `Element.style.getPropertyValue(property)`

- Повертає значення CSS-властивості з inline-стилів.
- Не повертає стилі з CSS-файлів чи `<style>`.
- Приклад:

```js
const div = document.querySelector("div");
console.log(div.style.getPropertyValue("color")); // "blue"
```

---

## 📘 Ключові рекомендації

- Використовуйте **data-атрибути** для зберігання кастомних даних замість нестандартних атрибутів.
- Для роботи з класами використовуйте `classList` замість `className`.
- Для роботи зі стилями віддавайте перевагу `style.setProperty` замість прямого доступу до `style.property`.
