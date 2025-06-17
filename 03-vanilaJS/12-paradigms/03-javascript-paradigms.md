# Парадигми програмування в JavaScript

## Загальна інформація

- **Опис**: Парадигми програмування визначають підхід до написання коду. JavaScript підтримує кілька стилів, що робить його гнучким.
- **Основні парадигми**:
  - **Процедурне програмування**: Послідовне виконання процедур (функцій без повернення).
  - **Об’єктно-орієнтоване програмування (ООП)**: Використання класів, об’єктів, інкапсуляції, успадкування.
  - **Функціональне програмування**: Декларативний стиль із чистими функціями та уникненням мутацій.
- **Імперативний vs Декларативний**:
  - Імперативний: Покрокові інструкції (як зробити).
  - Декларативний: Опис результату (що зробити).
- **Особливості**:
  - JavaScript дозволяє комбінувати парадигми.
  - **Falsy/Truthy**: Залежить від даних, що обробляються (наприклад, `0` falsy, об’єкти truthy).
- **Контекст**: Вибір парадигми впливає на читабельність, дебагінг і масштабованість.

## Приклади коду

### Процедурне програмування

```js
const arr = [1, 2, 3, 4, 5, 6];
let evenNumbers = [];
let doubleNumbers = [];
let sum = 0;

function filterEven() {
  for (const item of arr) {
    if (item % 2 === 0) evenNumbers.push(item);
  }
}

function double() {
  for (const item of evenNumbers) {
    doubleNumbers.push(item * 2);
  }
}

function sumArray() {
  for (const item of doubleNumbers) {
    sum += item;
  }
}

filterEven();
double();
sumArray();
console.log(evenNumbers, doubleNumbers, sum); // [2, 4, 6], [4, 8, 12], 24
```

### Об’єктно-орієнтоване програмування (ООП)

```js
class NumberProcessor {
  constructor(numbers) {
    this.numbers = numbers;
    this.evenNumbers = [];
    this.doubleNumbers = [];
    this.sum = 0;
  }
  getEvenNumbers() {
    return this.numbers.filter((num) => num % 2 === 0);
  }
  getDoubleNumbers() {
    return this.getEvenNumbers().map((num) => num * 2);
  }
  getSum() {
    return this.getDoubleNumbers().reduce((acc, num) => acc + num, 0);
  }
  process() {
    this.evenNumbers = this.getEvenNumbers();
    this.doubleNumbers = this.getDoubleNumbers();
    this.sum = this.getSum();
    return {
      evenNumbers: this.evenNumbers,
      doubleNumbers: this.doubleNumbers,
      sum: this.sum,
    };
  }
}

const processor = new NumberProcessor([1, 2, 3, 4, 5, 6]);
console.log(processor.process()); // { evenNumbers: [2, 4, 6], doubleNumbers: [4, 8, 12], sum: 24 }
```

### Функціональне програмування

```js
const arrFN = [1, 2, 3, 4, 5, 6];

const solveFunctional = (numbers) => {
  return numbers
    .filter((num) => num % 2 === 0)
    .map((num) => num * 2)
    .reduce((acc, num) => acc + num, 0);
};

console.log(solveFunctional(arrFN)); // 24
```

### Порівняння (Імперативний vs Декларативний)

```js
// Імперативний
let total = 0;
for (let i = 0; i < arr.length; i++) {
  if (arr[i] % 2 === 0) total += arr[i] * 2;
}
console.log(total); // 24

// Декларативний
const totalFunctional = arr
  .filter((n) => n % 2 === 0)
  .map((n) => n * 2)
  .reduce((a, b) => a + b, 0);
console.log(totalFunctional); // 24
```

## Особливості для співбесід — Питання та відповіді

### У чому різниця між процедурним і ООП?

- Процедурне: Фокус на функціях і послідовності.
- ООП: Фокус на об’єктах і їх взаємодії.
  ```js
  // Процедурне
  function add(a, b) {
    return a + b;
  }
  // ООП
  class Calc {
    add(a, b) {
      return a + b;
    }
  }
  ```

### Що таке чиста функція?

- Функція, яка завжди повертає однаковий результат для однакових вхідних даних і не має побічних ефектів.
  ```js
  const pure = (a, b) => a + b; // Чиста
  let x = 0;
  const impure = () => x++; // Неприборка
  ```

### Чим декларативний стиль кращий за імперативний?

- Декларативний легше читати і підтримує (менше коду), але може бути менш ефективним.
  ```js
  // Імперативний: 5 рядків циклу
  // Декларативний: 1 рядок з filter/map/reduce
  ```

### Як ООП використовує успадкування?

- Через `extends` і `super` для повторного використання коду.
  ```js
  class Parent {
    method() {
      return "Parent";
    }
  }
  class Child extends Parent {}
  console.log(new Child().method()); // Parent
  ```

### Чи можна комбінувати парадигми в JavaScript?

- Так, наприклад, ООП із функціональними методами.
  ```js
  class A {
    method(arr) {
      return arr.map((x) => x * 2);
    }
  }
  console.log(new A().method([1, 2])); // [2, 4]
  ```

## Поради

- **Використовуй процедурне для простих завдань**: Якщо логіка лінійна.
- **Обирай ООП для складних структур**: Класи для інкапсуляції.
- **Застосовуй функціональне для чистоти**: Уникай мутацій у критичних частинах.
- **Комбінуй розумно**: Використовуй `map`/`filter` у класах для декларативності.
- **Уникай побічних ефектів**: Особливо в функціональному стилі.
- **Тестуй продуктивність**: Імперативний стиль може бути швидшим для простих циклів.
