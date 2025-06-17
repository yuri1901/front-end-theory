# 🌳 Конспект: Node та робота з вузлами в DOM

Цей конспект охоплює основи роботи з інтерфейсом **Node** у DOM, типи вузлів, методи створення, видалення, заміни вузлів, а також доступ до дочірніх і сусідніх вузлів.

---

## 🖼️ Що таке Node?

- **Node** — базовий інтерфейс у DOM, який представляє будь-який об’єкт у структурі HTML-документа (елементи, текст, коментарі тощо).
- DOM-дерево складається з вузлів, організованих ієрархічно.
- Основні типи вузлів:
  - **Element node** (`<div>`, `<p>`): HTML-теги.
  - **Text node**: Текст усередині елементів.
  - **Comment node**: Коментарі (`<!-- коментар -->`).
  - **Document node**: Корінь документа (`document`).
  - **DocumentType node**: `<!DOCTYPE html>`.
  - **DocumentFragment node**: Тимчасовий контейнер для вузлів.

---

## 🛠️ Створення вузлів

### 🔹 `document.createElement(tagName)`

- Створює новий HTML-елемент із вказаним тегом.
- Приклад:
  ```js
  const div = document.createElement("div");
  div.textContent = "Новий div";
  ```

### 🔹 `document.createTextNode(text)`

- Створює текстовий вузол.
- Приклад:
  ```js
  const text = document.createTextNode("Привіт, світ!");
  ```

### 🔹 `document.createComment(comment)`

- Створює вузол коментаря.
- Приклад:
  ```js
  const comment = document.createComment("Це коментар");
  ```

### 🔹 `document.createDocumentFragment()`

- Створює фрагмент документа для групування вузлів перед додаванням у DOM (зменшує кількість перерисовок).
- Приклад:
  ```js
  const fragment = document.createDocumentFragment();
  const li = document.createElement("li");
  li.textContent = "Елемент списку";
  fragment.appendChild(li);
  ```

---

## 🛠️ Додавання вузлів

### 🔹 `Node.appendChild(node)`

- Додає вузол як останній дочірній до батьківського вузла.
- Повертає доданий вузол.
- Приклад:
  ```js
  const parent = document.querySelector(".container");
  const div = document.createElement("div");
  parent.appendChild(div);
  ```

---

## 🛠️ Видалення та заміна вузлів

### 🔹 `Node.removeChild(node)`

- Видаляє вказаний дочірній вузол із батьківського.
- Повертає видалений вузол.
- Приклад:
  ```js
  const parent = document.querySelector(".container");
  const child = parent.firstChild;
  parent.removeChild(child);
  ```

### 🔹 `Node.remove()`

- Видаляє вузол із DOM (без вказівки батьківського вузла).
- Приклад:
  ```js
  const elem = document.querySelector(".item");
  elem.remove();
  ```

### 🔹 `Node.replaceChild(newNode, oldNode)`

- Замінює старий дочірній вузол новим.
- Повертає замінений вузол.
- Приклад:
  ```js
  const parent = document.querySelector(".container");
  const oldNode = parent.firstChild;
  const newNode = document.createElement("span");
  parent.replaceChild(newNode, oldNode);
  ```

### 🔹 Приклад видалення всіх дочірніх вузлів

```js
function remove(e) {
  while (e.firstChild) {
    e.removeChild(e.firstChild);
  }
}
```

---

## 🛠️ Доступ до вузлів

### 🔹 Колекції дочірніх вузлів

- **`childNodes`**: Повертає `NodeList` усіх дочірніх вузлів (включаючи текст, коментарі).
- **`children`**: Повертає `HTMLCollection` лише HTML-елементів.
- **`childElementCount`**: Кількість дочірніх HTML-елементів.
  ```js
  const parent = document.querySelector(".container");
  console.log(parent.childNodes); // NodeList (всі вузли)
  console.log(parent.children); // HTMLCollection (лише елементи)
  console.log(parent.childElementCount); // Кількість елементів
  ```

### 🔹 Доступ до першого/останнього вузла

- **`firstChild` / `lastChild`**: Перший/останній вузол будь-якого типу.
- **`firstElementChild` / `lastElementChild`**: Перший/останній HTML-елемент.
  ```js
  const parent = document.querySelector(".container");
  console.log(parent.firstChild); // Може бути текстовий вузол
  console.log(parent.firstElementChild); // Лише елемент
  ```

### 🔹 Доступ до сусідніх вузлів

- **`nextSibling` / `previousSibling`**: Наступний/попередній вузол будь-якого типу.
- **`nextElementSibling` / `previousElementSibling`**: Наступний/попередній HTML-елемент.
  ```js
  const elem = document.querySelector(".item");
  console.log(elem.nextSibling); // Може бути текст
  console.log(elem.nextElementSibling); // Лише елемент
  ```

### 🔹 Доступ до батьківського вузла

- **`parentNode`**: Повертає батьківський вузол **будь-якого типу** (наприклад, елемент, документ, фрагмент).
- **`parentElement`**: Повертає батьківський **HTML-елемент**. Якщо батьківський вузол не є елементом (наприклад, `document`), повертає `null`.
  ```js
  const elem = document.querySelector(".item");
  console.log(elem.parentNode); // Батьківський вузол (наприклад, div або document)
  console.log(elem.parentElement); // Батьківський елемент (наприклад, div, або null для document)
  ```

---

## 🛠️ Доступ до вмісту

### 🔹 `Node.textContent`

- Повертає або встановлює текстовий вміст вузла та всіх його нащадків.
- Безпечний, оскільки не парсить HTML.
- Приклад:
  ```js
  const div = document.querySelector("div");
  div.textContent = "Новий текст";
  console.log(div.textContent); // "Новий текст"
  ```

---

## 📘 Ключові рекомендації

- Використовуйте `createDocumentFragment` для групового додавання вузлів, щоб зменшити кількість перерисовок DOM.
- Для видалення всіх дочірніх вузлів застосовуйте `removeChild` у циклі або `innerHTML = ''` для простоти.
- Використовуйте `children` замість `childNodes`, якщо потрібні лише HTML-елементи.
- Перевіряйте тип вузла перед операціями, оскільки `firstChild` може повертати текстовий вузол.
- Використовуйте `parentElement` замість `parentNode`, якщо потрібен саме HTML-елемент, але враховуйте, що `parentElement` може повертати `null`.
