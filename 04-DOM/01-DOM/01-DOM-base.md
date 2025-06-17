# 🧠 DOM – Основи

## 🔷 Що таке DOM?

- **DOM (Document Object Model)** — це модель HTML-документа як набору **об’єктів**.
- Кожен HTML-елемент перетворюється в **об’єкт**, яким можна керувати через **JavaScript**.
- DOM створюється браузером на основі HTML.
- DOM — **не HTML** і **не JavaScript**, але тісно з ними пов’язаний.
- DOM — це **API**, який дозволяє змінювати документ "на льоту".

## 🌳 DOM як дерево

HTML-документ у DOM — це **дерево вузлів (nodes)**:

- Елементи (`<p>`, `<div>`) → **вузли-елементи**
- Текст → **текстові вузли**
- Коментарі → **вузли-коментарі**

Це дозволяє:

- додавати/видаляти вузли,
- змінювати вміст або структуру документа.

## 🧩 Типи вузлів (Nodes) у DOM

- **Node** — базовий інтерфейс для всіх вузлів DOM.
- Основні типи вузлів:
  - `Document` — корінь документа.
  - `Element` — HTML-теги, наприклад, `<div>`, `<p>`.
  - `Text` — текст всередині елемента.
  - `Comment` — коментарі у HTML.
  - `DocumentType` — інформація про тип документа, наприклад, `<!DOCTYPE html>`.
- Властивості для навігації:
  - `parentNode` — повертає батьківський вузол (може бути будь-яким типом вузла).
  - `parentElement` — повертає батьківський **елемент** (тільки якщо батько — елемент, інакше `null`).

## 🛠️ Методи для пошуку елементів

### 🔹 `getElementById(id)`

- Повертає **один об’єкт** `Element` з вказаним `id`.
- Якщо елемент не знайдено — повертає `null`.

### 🔹 `getElementsByClassName(className)`

- Повертає **"живу" HTML-колекцію** (`HTMLCollection`) елементів.
- Автоматично оновлюється, якщо DOM змінюється.

```js
const cards = document.getElementsByClassName("card");
console.log(cards.length); // кількість елементів
```

### 🔹 `getElementsByTagName(tagName)`

- Також повертає **живу HTMLCollection**.

```js
const inputs = document.getElementsByTagName("input");
const arr = [...inputs]; // перетворення на масив
```

### 🔹 `getElementsByName(name)`

- Повертає **HTMLCollection** елементів за атрибутом `name`.

### 🔹 `querySelector(cssSelector)`

- Повертає **перший знайдений** елемент, що підходить під CSS-селектор.

```js
const firstLi = document.querySelector("ul li");
```

### 🔹 `querySelectorAll(cssSelector)`

- Повертає **NodeList** всіх відповідних елементів.
- **Статичний список** — не оновлюється після змін DOM.

```js
const allLi = document.querySelectorAll("ul li");
```

## 📌 `HTMLCollection` vs `NodeList`

| Характеристика       | `HTMLCollection`                     | `NodeList`                            |
| -------------------- | ------------------------------------ | ------------------------------------- |
| Тип колекції         | Жива (динамічна)                     | Статична (не оновлюється автоматично) |
| Отримується через    | `getElementsBy...`                   | `querySelectorAll()`                  |
| Доступ за індексом   | ✅ Так                               | ✅ Так                                |
| Метод `forEach()`    | ❌ Немає                             | ✅ Є                                  |
| Перетворення в масив | `Array.from()` або `[...collection]` | `Array.from()` або `[...nodeList]`    |

> 🧠 Якщо хочеш обійтись `forEach()` — краще використовуй `querySelectorAll()`, бо `NodeList` його підтримує.

## ⚙️ Відмінності між `parentNode` і `parentElement`

- `parentNode` повертає будь-який батьківський вузол, включно з документом.
- `parentElement` повертає тільки батьківський **елемент** (тип `Element`).
- Приклад:

```js
const textNode = document.createTextNode("Hello");
console.log(textNode.parentNode); // поверне елемент, куди додано текст
console.log(textNode.parentElement); // те саме, але якщо батько не Element, буде null
```

## 🔁 Взаємодія з DOM (JS)

JavaScript дозволяє:

- **Знаходити елементи**  
  `document.getElementById("myId")`, `querySelector("div")`

- **Змінювати вміст**  
  `element.textContent = "Привіт"`

- **Змінювати атрибути**  
  `element.setAttribute("class", "active")`

- **Маніпулювати стилями**  
  `element.style.color = "red"`

- **Додавати/видаляти елементи**  
  `parent.appendChild(newEl)`, `parent.removeChild(el)`

- **Реагувати на події**  
  `element.addEventListener("click", callback)`

- **Робота з класами**  
  `element.classList.add("new-class")`,  
  `element.classList.remove("old")`

## 📘 Важливо

| Порівняння    | HTML              | DOM                     | JavaScript         |
| ------------- | ----------------- | ----------------------- | ------------------ |
| Що це?        | Мова розмітки     | Об’єктна модель         | Мова програмування |
| Що робить?    | Описує структуру  | Дає доступ до елементів | Маніпулює DOM      |
| Відповідає за | Статичну сторінку | Взаємодію з HTML        | Динаміку сторінки  |
