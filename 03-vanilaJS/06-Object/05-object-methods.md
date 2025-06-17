# Повний список методів та властивостей об’єктів у JavaScript

## Загальна інформація

- **Опис**: Цей розділ містить таблиці з усіма статичними методами `Object` і методами прототипу `Object.prototype`. Найважливіші та найвикористовуваніші методи виділені з урахуванням ваших коментарів.
- **Важлива інформація**:
  - Об’єкти передаються за посиланням, що робить методи копіювання критичними.
  - Прототипний ланцюжок впливає на доступ до властивостей.
  - Дескриптори дозволяють точно контролювати поведінку властивостей.
- **Контекст**: Глибоке розуміння об’єктів, оптимізація коду, підготовка до співбесід.

## Таблиця найважливіших та найвикористовуваніших методів

| Метод                                              | Опис                                                                                                      | Приклад використання                                                     |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **`Object.keys(obj)`**                             | Повертає масив перелічуваних ключів об’єкта.                                                              | `Object.keys({ a: 1, b: 2 }); // ["a", "b"]`                             |
| **`Object.values(obj)`**                           | Повертає масив перелічуваних значень об’єкта.                                                             | `Object.values({ a: 1, b: 2 }); // [1, 2]`                               |
| **`Object.entries(obj)`**                          | Повертає масив пар `[ключ, значення]` для перелічуваних властивостей.                                     | `Object.entries({ a: 1 }); // [["a", 1]]`                                |
| **`Object.fromEntries(entries)`**                  | Перетворює масив пар `[ключ, значення]` на об’єкт.                                                        | `Object.fromEntries([["a", 1], ["b", 2]]); // { a: 1, b: 2 }`            |
| **`Object.getOwnPropertyDescriptor(obj, prop)`**   | Повертає детальну інформацію (дескриптор) про вказану властивість об’єкта.                                | `Object.getOwnPropertyDescriptor({ x: 1 }, "x"); // { value: 1, ... }`   |
| **`Object.defineProperty(obj, prop, descriptor)`** | Дозволяє змінювати поведінку властивостей об’єкта через дескриптор (наприклад, `writable`, `enumerable`). | `Object.defineProperty({}, "name", { value: "Іван", writable: false });` |
| **`Object.assign(target, ...sources)`**            | Копіює перелічувані властивості з одного або кількох об’єктів у цільовий.                                 | `Object.assign({}, { a: 1 }, { b: 2 }); // { a: 1, b: 2 }`               |
| **`Object.create(proto, descriptors)`**            | Створює новий об’єкт із заданим прототипом і дескрипторами.                                               | `Object.create({ x: 1 }, { y: { value: 2 } });`                          |
| **`Object.freeze(obj)`**                           | Заморожує об’єкт, забороняючи будь-які зміни.                                                             | `Object.freeze({ a: 1 }); {}.a = 2; // Ігнорується`                      |
| **`obj.hasOwnProperty(prop)`**                     | Перевіряє, чи є вказана властивість власною (не успадкованою).                                            | `({ a: 1 }).hasOwnProperty("a"); // true`                                |
| **`obj.toString()`**                               | Повертає рядкове представлення об’єкта.                                                                   | `({}).toString(); // "[object Object]"`                                  |

## Таблиця другорядних методів

| Метод                                           | Опис                                                           | Приклад використання                                                                        |
| ----------------------------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **`Object.defineProperties(obj, descriptors)`** | Додає кілька властивостей із дескрипторами.                    | `Object.defineProperties({}, { x: { value: 1 } });`                                         |
| **`Object.getOwnPropertyNames(obj)`**           | Повертає масив усіх власних ключів (включаючи неперелічувані). | `Object.getOwnPropertyNames({}); // []`                                                     |
| **`Object.getOwnPropertySymbols(obj)`**         | Повертає масив символів як ключів.                             | `Object.getOwnPropertySymbols({ [Symbol("x")]: 1 }); // [Symbol(x)]`                        |
| **`Object.getOwnPropertyDescriptors(obj)`**     | Повертає дескриптори всіх власних властивостей.                | `Object.getOwnPropertyDescriptors({ x: 1 });`                                               |
| **`Object.getPrototypeOf(obj)`**                | Повертає прототип об’єкта.                                     | `Object.getPrototypeOf({}); // Object.prototype`                                            |
| **`Object.is(value1, value2)`**                 | Порівнює значення з урахуванням +0/-0.                         | `Object.is(NaN, NaN); // true`                                                              |
| **`Object.isExtensible(obj)`**                  | Перевіряє, чи можна додавати властивості.                      | `Object.isExtensible({}); // true`                                                          |
| **`Object.isFrozen(obj)`**                      | Перевіряє, чи заморожений об’єкт.                              | `Object.isFrozen(Object.freeze({})); // true`                                               |
| **`Object.isSealed(obj)`**                      | Перевіряє, чи запечатаний об’єкт.                              | `Object.isSealed(Object.seal({})); // true`                                                 |
| **`Object.preventExtensions(obj)`**             | Забороняє додавати нові властивості.                           | `Object.preventExtensions({}); {}.x = 1; // Ігнорується`                                    |
| **`Object.seal(obj)`**                          | Запечатує об’єкт, забороняючи додавання/видалення.             | `Object.seal({}); delete {}.x; // Ігнорується`                                              |
| **`Object.setPrototypeOf(obj, proto)`**         | Встановлює прототип об’єкта.                                   | `Object.setPrototypeOf({}, { x: 1 });`                                                      |
| **`obj.isPrototypeOf(obj2)`**                   | Перевіряє, чи є об’єкт прототипом іншого.                      | `Object.prototype.isPrototypeOf({}); // true`                                               |
| **`obj.propertyIsEnumerable(prop)`**            | Перевіряє, чи перелічувана властивість.                        | `Object.defineProperty({}, "x", { enumerable: false }).propertyIsEnumerable("x"); // false` |
| **`obj.toLocaleString()`**                      | Повертає локалізоване рядкове представлення.                   | `({}).toLocaleString(); // "[object Object]"`                                               |
| **`obj.valueOf()`**                             | Повертає примітивне значення об’єкта.                          | `({}).valueOf(); // {}`                                                                     |

## Важлива інформація

- **Найвикористовуваніші методи**: `Object.keys()`, `Object.values()`, `Object.entries()`, `Object.fromEntries()`, `Object.getOwnPropertyDescriptor()`, `Object.defineProperty()`, `Object.assign()`, `Object.create()`, `Object.freeze()`, `hasOwnProperty()`, `toString()` — основа для роботи з об’єктами, як зазначено у ваших коментарях.
- **Дескриптори**: Включають `value` (значення), `writable` (дозволяє зміну), `enumerable` (перелічуваність), `configurable` (можливість конфігурації).
  - **Приклад**: `Object.defineProperty({}, "name", { value: "Іван", writable: false });`
- **Прототипний ланцюжок**: Властивості шукаються в об’єкті, потім у прототипах (до `Object.prototype`).
  - **Приклад**: `let obj = Object.create({ x: 1 }); console.log(obj.x); // 1`
- **Символи**: Унікальні ключі, доступні через `getOwnPropertySymbols()`, невидимі для `Object.keys()`.
  - **Приклад**: `let sym = Symbol("key"); let obj = { [sym]: 1 };`
- **Замороження та запечатування**: `freeze` блокує всі зміни, `seal` — лише додавання/видалення.
  - **Приклад**: `Object.freeze({ a: 1 }); Object.seal({ a: 1 });`

## Поради

- **Фокус на ключові методи**: Використовуйте `keys`, `values`, `entries` для ітерації, `defineProperty` для конфігурації.
- **Контролюйте властивості**: Застосовуйте дескриптори для безпеки.
- **Перевіряйте стан**: Використовуйте `isFrozen()`, `isSealed()` перед змінами.
- **Оптимізуйте**: Уникайте надмірного копіювання чи глибоких ланцюжків.
- **Тестуйте**: Перевіряйте поведінку методів на складних об’єктах.
