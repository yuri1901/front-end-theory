# Масиви у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: //! Масив — впорядкований список значень. Масиви є гнучкими, можуть містити елементи різних типів і динамічно змінювати розмір.
- **Створення**:
  - //! `Array.of(7)` — створює масив із єдиним елементом зі значенням 7; `Array(7)` — створює sparse масив із довжиною 7 (елементи `undefined`).
  - //! `Array.from()` — перетворює ітерабельні структури (наприклад, `Set`, `NodeList`) на масив.
  - //! `Array.isArray()` — перевіряє, чи є об’єкт масивом.
- **Особливості**:
  - Передаються за посиланням, мутабельні.
  - Індексація починається з 0.
  - Підтримують методи для ітерації, маніпуляції та копіювання.
- **Контекст**: Використовуються для зберігання списків, обробки даних, алгоритмів.

## Приклади коду

### Створення масивів

```javascript
console.log(Array.of(7)); // [7]
console.log(Array(7)); // [empty × 7]
console.log(Array.from("abc")); // ["a", "b", "c"]
console.log(Array.isArray([1, 2])); // true
console.log(Array.isArray({})); // false
```

## Копіювання масивів

- **Опис**: Копіювання необхідно для уникнення мутацій оригінального масиву, оскільки масиви передаються за посиланням.
- **Типи**:
  - **Поверхневе (shallow)**: Копіює верхній рівень; вкладені масиви/об’єкти залишаються посиланнями.
  - **Глибоке (deep)**: Створює повну незалежну копію всіх рівнів.
- **Методи**:
  - **Поверхневе**: `slice()`, `concat()`, оператор `...` (spread), `Array.from()`.
  - **Глибоке**: `JSON.parse(JSON.stringify())`, рекурсивна функція.
- **Приклади**:
  ```javascript
  let arr = [1, [2, 3]];
  let shallow1 = arr.slice(); // Поверхневе
  shallow1[0] = 10;
  console.log(arr[0]); // 1
  shallow1[1][0] = 20;
  console.log(arr[1][0]); // 20
  let shallow2 = [...arr]; // Поверхневе з spread
  shallow2[1][0] = 30;
  console.log(arr[1][0]); // 30
  let deepCopy = JSON.parse(JSON.stringify(arr)); // Глибоке
  deepCopy[1][0] = 40;
  console.log(arr[1][0]); // 30
  ```

## Особливості для співбесід — Питання та відповіді

### Чим відрізняється `Array.of()` від `Array()`?

- **Відповідь**: `Array.of(7)` створює `[7]`, а `Array(7)` — sparse масив із довжиною 7.
  ```javascript
  console.log(Array.of(7)); // [7]
  console.log(Array(7)); // [empty × 7]
  ```

### Як працює `Array.from()`?

- **Відповідь**: Перетворює ітерабельні об’єкти чи масивоподібні структури на масив.
  ```javascript
  console.log(Array.from({ length: 3 }, (_, i) => i)); // [0, 1, 2]
  ```

### Чим поверхневе копіювання відрізняється від глибокого?

- **Відповідь**: Поверхневе копіює лише верхній рівень, глибоке — усі рівні.
  ```javascript
  let arr = [1, [2]];
  let shallow = [...arr];
  shallow[1][0] = 3;
  console.log(arr[1][0]); // 3
  let deep = JSON.parse(JSON.stringify(arr));
  deep[1][0] = 4;
  console.log(arr[1][0]); // 3
  ```

### Чому `JSON.parse(JSON.stringify())` не завжди підходить для копіювання?

- **Відповідь**: Не підтримує функції, `undefined`, `Date` чи цикли.
  ```javascript
  let arr = [() => {}, new Date()];
  console.log(JSON.parse(JSON.stringify(arr))); // [null, "2025-06-17..."]
  ```

## Поради

- **Використовуйте `Array.of()`**: Для створення масивів із заданими значеннями.
- **Перевіряйте тип**: Застосовуйте `Array.isArray()` перед маніпуляціями.
- **Копіюйте розумно**: Вибирайте `slice()` чи `...` для поверхневого, `JSON` — для простого глибокого копіювання.
- **Уникайте мутацій**: Створюйте копії перед змінами.
- **Тестуйте вкладеність**: Перевіряйте поведінку при копіюванні вкладених структур.
