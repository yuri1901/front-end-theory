# Конспект: JavaScript Promise (на основі MDN)

## Що таке Promise

Promise (обіцянка) — це об'єкт, який представляє результат асинхронної операції. Він може бути в одному з трьох станів:

- **Pending (очікування)** — початковий стан, результат ще не доступний
- **Fulfilled (виконано)** — операція завершена успішно
- **Rejected (відхилено)** — операція завершилась з помилкою

```js
const promise = new Promise((resolve, reject) => {
  // асинхронна операція
});
```

### Аргументи конструктора Promise

Конструктор `new Promise(executor)` приймає одну функцію — **executor**, яка має два параметри:

- `resolve(value)` — викликається при успішному виконанні
- `reject(reason)` — викликається при помилці

```js
const promise = new Promise((resolve, reject) => {
  if (true) {
    resolve("Успішно");
  } else {
    reject("Помилка");
  }
});
```

## Методи екземпляра Promise

### `.then(onFulfilled, onRejected)`

Викликається після того, як Promise завершився (успішно або з помилкою).

- `onFulfilled(value)` — викликається, якщо виконано (fulfilled)
- `onRejected(error)` — викликається, якщо відхилено (rejected)

```js
promise
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

### `.catch(onRejected)`

Обробка помилки. Еквівалент другого параметра в `.then`, але зручніший для ланцюжків.

```js
promise.catch(error => console.error(error));
```

### `.finally(onFinally)`

Виконується після завершення промісу, незалежно від результату. Не змінює значення в ланцюжку.

```js
promise
  .finally(() => console.log("Операція завершена"));
```

## Створення власного Promise

```js
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success) resolve("Успіх!");
    else reject("Помилка!");
  }, 1000);
});
```

## Promise chaining (ланцюжок обробки)

Кожен `.then()` повертає новий Promise, що дозволяє створювати послідовність обробки:

```js
fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

## Статичні методи Promise

### `Promise.resolve(value)`

Створює Promise, який одразу виконується зі значенням `value`.

```js
Promise.resolve(42).then(x => console.log(x)); // 42
```

### `Promise.reject(reason)`

Створює Promise, який одразу відхиляється з причиною `reason`.

```js
Promise.reject("Error").catch(err => console.log(err));
```

### `Promise.all(iterable)`

Очікує виконання **всіх** переданих промісів. Якщо хоча б один відхиляється — весь проміс відхиляється.

```js
Promise.all([
  Promise.resolve(1),
  Promise.resolve(2)
]).then(values => console.log(values)); // [1, 2]
```

### `Promise.allSettled(iterable)`

Повертає масив об’єктів із результатами **всіх** промісів, незалежно від того, були вони виконані чи відхилені.

```js
Promise.allSettled([
  Promise.resolve(1),
  Promise.reject("error")
]).then(results => console.log(results));
// [ { status: "fulfilled", value: 1 }, { status: "rejected", reason: "error" } ]
```

### `Promise.race(iterable)`

Повертає результат **першого завершеного** (fulfilled або rejected) промісу.

```js
Promise.race([
  new Promise(res => setTimeout(() => res("A"), 100)),
  new Promise(res => setTimeout(() => res("B"), 200))
]).then(result => console.log(result)); // "A"
```

### `Promise.any(iterable)`

Повертає **перший успішний** результат (fulfilled). Якщо всі проміси відхилено — повертає AggregateError.

```js
Promise.any([
  Promise.reject("err1"),
  Promise.resolve("ok"),
  Promise.reject("err2")
]).then(result => console.log(result)); // "ok"
```

---

## Висновки

- Promise — основа асинхронного програмування в JS
- Дозволяє уникати "callback hell"
- Підтримує зручне ланцюжне виконання, обробку помилок і фіналізацію
- Має гнучкий API із потужними методами для комбінування та контролю асинхронного коду

---

Докладніше: [MDN - Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

