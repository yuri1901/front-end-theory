# 📆 JavaScript `Date` – Конспект

## 📌 Основне

- `Date` — вбудований об’єкт для роботи з датою та часом.
- ❗ **Недостатньо надійний**: проблеми з таймзонами, форматуванням, літнім часом.
- 🔧 Кращі альтернативи:  
  `date-fns`, `dayjs`, `luxon` — сучасні, надійні.  
  `moment.js` — більше не оновлюється.
- 🚀 Майбутнє — [**Temporal API**](https://tc39.es/proposal-temporal/docs/).

## 🧪 Створення об'єктів Date

```js
const now = new Date(); // Поточна дата і час
const fromISO = new Date("2025-06-03T17:28:21Z"); // ISO рядок
const fromMillis = new Date(123123123123); // З мітки часу (мс)
const exact = new Date(2020, 4, 1, 14, 15, 0, 0); // Рік, місяць (0-based), день...
```

## 📥 Отримання значень (get)

| Метод                 | Пояснення                        |
| --------------------- | -------------------------------- |
| `getFullYear()`       | Рік                              |
| `getMonth()`          | Місяць (0–11)                    |
| `getDate()`           | День місяця (1–31)               |
| `getDay()`            | День тижня (0 — неділя)          |
| `getHours()`          | Години                           |
| `getMinutes()`        | Хвилини                          |
| `getSeconds()`        | Секунди                          |
| `getMilliseconds()`   | Мілісекунди                      |
| `getTime()`           | Мітка часу з 1970-01-01 UTC (мс) |
| `getTimezoneOffset()` | Зсув від UTC у хвилинах          |

## 📤 Зміна значень (set)

| Метод                   | Пояснення                     |
| ----------------------- | ----------------------------- |
| `setFullYear(year)`     | Змінити рік                   |
| `setMonth(month)`       | Місяць (0–11)                 |
| `setDate(day)`          | День місяця                   |
| `setHours(h)`           | Година                        |
| `setMinutes(m)`         | Хвилини                       |
| `setSeconds(s)`         | Секунди                       |
| `setMilliseconds(ms)`   | Мілісекунди                   |
| `setTime(ms)`           | Задати мітку часу (мс з 1970) |
| `setHours(h, m, s, ms)` | Одразу всі значення часу      |

```js
const date = new Date();
date.setFullYear(1500);
date.setHours(0, 0, 0, 0); // Скидає час до 00:00:00.000
```

## 🧮 Різниця між датами

```js
const date1 = new Date(2000, 0, 1);
const date2 = new Date(2025, 5, 1);

const diffMillis = Math.abs(date2 - date1);
const dayMillis = 1000 * 60 * 60 * 24;
const diffDays = diffMillis / dayMillis;
```

## 🧾 Формати дати і часу

```js
const d = new Date("2004-01-19T12:30:00");

console.log(d.toString()); // Людський формат
console.log(d.toDateString()); // Тільки дата
console.log(d.toTimeString()); // Тільки час
console.log(d.toISOString()); // ISO 8601 (UTC)
```

## ⚠️ Проблеми з Date

- Не підтримує локалізовані календарі.
- Різна поведінка в браузерах при парсингу рядків.
- Обмежена точність і контроль над таймзонами.

## 🌐 Temporal API (нова специфікація)

📘 [Офіційна документація](https://tc39.es/proposal-temporal/docs/)

- Замінює `Date` об’єктами без побічних ефектів.
- Підтримує:
  - `Temporal.PlainDate`
  - `Temporal.ZonedDateTime`
  - `Temporal.Instant`
  - `Temporal.Duration`
- ✅ Явна робота з часовими зонами та календарями.

```js
const today = Temporal.Now.plainDateISO();
const birthday = Temporal.PlainDate.from("1990-01-01");
const age = today.since(birthday).years;
```

## 📦 Корисні бібліотеки

| Бібліотека  | Коментар                                  |
| ----------- | ----------------------------------------- |
| `moment.js` | застаріла, велика                         |
| `date-fns`  | модульна, сучасна                         |
| `dayjs`     | легка, як moment, з плагінами             |
| `luxon`     | потужна, підтримує таймзони               |
| `Temporal`  | майбутнє (можна підключати через поліфіл) |

## 📚 Джерела

- [MDN Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
- [ECMAScript Date формат](https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-date-time-string-format)
- [Temporal API](https://tc39.es/proposal-temporal/docs/)
