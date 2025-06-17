# 🧭 BOM (Browser Object Model)

- DOM — модель документа, а BOM — модель браузера.
- BOM (Browser Object Model) — це набір об’єктів, які надають доступ до функцій браузера, незалежних від вмісту сторінки.
- BOM **не стандартизований** офіційно, але широко підтримується браузерами.
- Основний об’єкт BOM — `window`, який є глобальним об’єктом, що містить усі інші об’єкти BOM, а також DOM і таймери.

## 🔑 Основні об’єкти BOM

- **`window`**:

  - Глобальний об’єкт браузера, що представляє вікно браузера.
  - Містить методи та властивості для роботи з DOM, BOM і JavaScript.
  - Приклади: `window.alert()`, `window.setTimeout()`, `window.document`.

- **`window.location`**:
  - Надає інформацію про поточний URL і методи для навігації.
  - Властивості:
    - `href` — повний URL (наприклад, `https://example.com/path`).
    - `protocol` — протокол (наприклад, `https:`).
    - `host` — домен і порт (наприклад, `example.com:80`).
    - `pathname` — шлях (наприклад, `/path`).
    - `search` — параметри запиту (наприклад, `?id=123`).
  - Методи:
    - `assign(url)` — завантажує новий URL.
    - `reload()` — перезавантажує сторінку.
    - `replace(url)` — замінює поточний URL без додавання до історії.

```js
console.log(window.location.href); // поточний URL
window.location.assign("https://example.com"); // перехід на новий URL
window.location.reload(); // перезавантаження сторінки
```

- **`window.history`**:
  - Дозволяє працювати з історією браузера.
  - Методи:
    - `back()` — повертається на попередню сторінку.
    - `forward()` — переходить до наступної сторінки.
    - `go(n)` — переміщення на n сторінок вперед (позитивне n) або назад (негативне n).
    - `pushState(state, title, url)` — додає новий запис до історії.
    - `replaceState(state, title, url)` — замінює поточний запис історії.

```js
window.history.back(); // повернутися на одну сторінку назад
window.history.pushState({ page: 1 }, "", "/page1"); // додати новий стан
```

- **`window.navigator`**:
  - Надає інформацію про браузер і систему користувача.
  - Властивості:
    - `userAgent` — інформація про браузер і ОС.
    - `language` — мова браузера.
    - `onLine` — чи є підключення до мережі (true/false).
    - `platform` — операційна система (наприклад, `Win32`).
    - `geolocation` — доступ до геолокації (з дозволу користувача).

```js
console.log(navigator.userAgent); // інформація про браузер
if (navigator.onLine) {
  console.log("Онлайн!");
} else {
  console.log("Офлайн!");
}
```

- **`window.screen`**:
  - Інформація про екран користувача.
  - Властивості:
    - `width` і `height` — розміри екрана.
    - `availWidth` і `availHeight` — доступна область екрана (без панелей браузера).
    - `colorDepth` — глибина кольору екрана.

```js
console.log(window.screen.width); // ширина екрана
console.log(window.screen.availHeight); // доступна висота
```

- **`window.document`**:
  - Посилання на DOM-документ, який є частиною `window`.
  - Це точка входу для роботи з DOM через BOM.

## ⏲️ Таймери в BOM

- **`setTimeout(callback, delay)`**:
  - Виконує функцію один раз після затримки (у мілісекундах).
- **`setInterval(callback, interval)`**:
  - Виконує функцію повторно через заданий інтервал.
- **`clearTimeout(id)`** і **`clearInterval(id)`**:
  - Зупиняють виконання таймера за його ідентифікатором.

```js
const timeoutId = setTimeout(() => console.log("Виклик через 2 сек"), 2000);
clearTimeout(timeoutId); // скасувати таймер

const intervalId = setInterval(() => console.log("Кожні 3 сек"), 3000);
clearInterval(intervalId); // зупинити інтервал
```

## 🔔 Діалогові вікна

- **`alert(message)`**:
  - Показує просте сповіщення з повідомленням.
- **`confirm(message)`**:
  - Показує діалогове вікно з кнопками "OK" і "Cancel". Повертає `true` (OK) або `false` (Cancel).
- **`prompt(message, default)`**:
  - Запитує введення даних від користувача. Повертає введений текст або `null`.

```js
alert("Це сповіщення!");
const isConfirmed = confirm("Ви впевнені?");
const userInput = prompt("Введіть ваше ім’я:", "Гість");
```

## 📘 Важливо

- BOM не є частиною офіційної специфікації ECMAScript, але підтримується всіма сучасними браузерами.
- Об’єкти BOM часто використовуються для управління поведінкою браузера, навігацією, розмірами вікон і взаємодією з користувачем.
- BOM тісно пов’язаний з DOM, оскільки `window.document` є точкою доступу до DOM.
