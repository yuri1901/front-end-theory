# Копіювання об’єктів і масивів у JavaScript

## Загальна інформація

- **Опис**: Копіювання об’єктів і масивів необхідно для уникнення мутацій оригінальних даних, оскільки вони передаються за посиланням.
- **Типи копіювання**:
  - **Поверхневе (shallow)**: Копіює лише верхній рівень; вкладені об’єкти/масиви залишаються посиланнями.
  - **Глибоке (deep)**: Створює повністю незалежну копію всіх рівнів.
- **Методи**:
  - Поверхневе: `Object.assign()`, оператор `...`, `Array.slice()`, `Array.concat()`.
  - Глибоке: `JSON.parse(JSON.stringify())`, бібліотеки (наприклад, Lodash).
- **Особливості**:
  - Присвоєння (`=`) копіює лише посилання.
  - Циклічні посилання чи спеціальні об’єкти (`Date`, функції) ускладнюють копіювання.
- **Контекст**: Захист даних, immutable програмування, уникнення побічних ефектів.

## Приклади коду

### Поверхневе копіювання об’єктів

```javascript
let obj = { a: 1, b: { c: 2 } };
let shallow1 = Object.assign({}, obj);
shallow1.a = 10;
console.log(obj.a); // 1
shallow1.b.c = 20;
console.log(obj.b.c); // 20
let shallow2 = { ...obj };
shallow2.b.c = 30;
console.log(obj.b.c); // 30
```

### Поверхневе копіювання масивів

```javascript
let arr = [1, [2, 3]];
let shallow1 = arr.slice();
shallow1[0] = 10;
console.log(arr[0]); // 1
shallow1[1][0] = 20;
console.log(arr[1][0]); // 20
let shallow2 = [...arr];
shallow2[1][0] = 30;
console.log(arr[1][0]); // 30
```

### Глибоке копіювання

```javascript
let obj = { a: 1, b: { c: 2 } };
let deepCopy = JSON.parse(JSON.stringify(obj));
deepCopy.b.c = 10;
console.log(obj.b.c); // 2
let objWithDate = { date: new Date() };
let deepCopyDate = JSON.parse(JSON.stringify(objWithDate));
console.log(deepCopyDate.date); // Рядок, а не Date
```

## Особливості для співбесід — Питання та відповіді

### У чому різниця між поверхневим і глибоким копіюванням?

- **Відповідь**: Поверхневе копіює лише верхній рівень, зберігаючи посилання на вкладені об’єкти; глибоке створює повну копію.
  ```javascript
  let obj = { a: { b: 1 } };
  let shallow = { ...obj };
  let deep = JSON.parse(JSON.stringify(obj));
  shallow.a.b = 2;
  console.log(obj.a.b); // 2
  deep.a.b = 3;
  console.log(obj.a.b); // 2
  ```

### Чому `JSON.parse(JSON.stringify())` має обмеження?

- **Відповідь**: Не підтримує функції, `undefined`, `Symbol`, циклічні посилання чи об’єкти типу `Date`.
  ```javascript
  let obj = { fn: () => {}, date: new Date() };
  let copy = JSON.parse(JSON.stringify(obj));
  console.log(copy.fn, copy.date); // undefined, рядок
  ```

### Як скопіювати об’єкт із прототипом?

- **Відповідь**: Використовуйте `Object.create()` із дескрипторами.
  ```javascript
  let proto = { type: "base" };
  let obj = Object.create(proto);
  obj.a = 1;
  let copy = Object.create(
    Object.getPrototypeOf(obj),
    Object.getOwnPropertyDescriptors(obj)
  );
  console.log(copy.a, copy.type); // 1, base
  ```

## Поради

- **Використовуйте `...`**: Для швидкого поверхневого копіювання.
- **Застосовуйте `Object.assign`**: Для об’єктів, але перевіряйте вкладеність.
- **Обережно з `JSON`**: Використовуйте бібліотеки (наприклад, Lodash) для складних структур.
- **Перевіряйте вкладені об’єкти**: Вибирайте глибоке копіювання за потреби.
- **Уникайте мутацій**: Створюйте копії для безпечної роботи з даними.
