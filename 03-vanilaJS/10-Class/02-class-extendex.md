# Успадкування та статичні методи класів у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Успадкування дозволяє класам-нащадкам використовувати логіку батьківських класів. Статичні методи належать класу, а не екземплярам.
- **Успадкування**:
  - `extends`: Успадковує методи та властивості.
  - `super`: Викликає конструктор або методи батьківського класу.
- **Статичні методи**:
  - `static`: Визначає методи/властивості класу.
- **Перевірка типу**:
  - `instanceof`: Перевіряє належність об’єкта класу з урахуванням успадкування.
- **Стилі програмування**:
  - Процедурне: Покрокове виконання.
  - ООП: Об’єкти та класи.
  - Функціональне: Декларативність, чисті функції.
- **Особливості**:
  - `super` вимагає виклику в конструкторі нащадка.
  - Статичні методи доступні через клас, а не екземпляр.
- **Контекст**: Створення ієрархій, утиліти, порівняння парадигм.

## Приклади коду

### Успадкування та `super`

```javascript
class Product {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }
  getPrice() {
    return `${this.price} USDT`;
  }
}

class Shoes extends Product {
  constructor(name, price, size) {
    super(name, price);
    this.size = size;
  }
  getPrice() {
    return `${super.getPrice()}, size ${this.size}`;
  }
}
const shoes = new Shoes("Sneakers", 50, 42);
console.log(shoes.getPrice()); // 50 USDT, size 42
```

### Приватні поля та `super`

```javascript
class Product {
  #price = 0;
  constructor(price) {
    this.#price = price;
  }
  getPrice() {
    return this.#price;
  }
}

class Shoes extends Product {
  #size = 0;
  constructor(price, size) {
    super(price);
    this.#size = size;
  }
  getDetails() {
    return `${super.getPrice()} size ${this.#size}`;
  }
}
console.log(new Shoes(100, 41).getDetails()); // 100 size 41
```

### Статичні методи та `instanceof`

```javascript
class VideoEditor {
  static formats = ["mp4", "mov"];
  static getFormats() {
    return this.formats;
  }
}
console.log(VideoEditor.getFormats()); // ["mp4", "mov"]

class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
}
const rect = new Rectangle(10, 5);
console.log(rect instanceof Rectangle); // true
```

### Стилі програмування

```javascript
// Процедурне
const arr = [1, 2, 3, 4, 5, 6];
let even = [];
for (let item of arr) if (item % 2 === 0) even.push(item);

// ООП
class NumberProcessor {
  constructor(numbers) {
    this.numbers = numbers;
  }
  getEven() {
    return this.numbers.filter((n) => n % 2 === 0);
  }
}
console.log(new NumberProcessor(arr).getEven()); // [2, 4, 6]

// Функціональне
const getEvenSum = (arr) =>
  arr.filter((n) => n % 2 === 0).reduce((a, b) => a + b, 0);
console.log(getEvenSum(arr)); // 12
```

## Особливості для співбесід — Питання та відповіді

### Як працює `extends` і `super`?

- **Відповідь**: `extends` успадковує, `super` викликає батьківський конструктор.
  ```javascript
  class A {
    constructor() {
      this.x = 1;
    }
  }
  class B extends A {
    constructor() {
      super();
    }
  }
  console.log(new B().x); // 1
  ```

### Що таке статичні методи?

- **Відповідь**: Належить класу, а не екземплярам.
  ```javascript
  class C {
    static method() {
      return "static";
    }
  }
  console.log(C.method()); // static
  // console.log(new C().method()); // TypeError
  ```

### Як працює `instanceof`?

- **Відповідь**: Перевіряє належність із урахуванням прототипів.
  ```javascript
  console.log(new Shoes() instanceof Product); // true
  ```

### Чим відрізняються стилі програмування?

- **Відповідь**: Процедурне: Покрокове, мутації. ООП: Об’єкти, інкапсуляція. Функціональне: Імутабельність, чистота.
  ```javascript
  let x = 1;
  x += 2; // Процедурне
  class X {
    setValue(v) {
      this.v = v;
    }
  } // ООП
  const add = (a, b) => a + b; // Функціональне
  ```

## Поради

- **Використовуйте `extends`**: Для логічних ієрархій.
- **Викликайте `super`**: У конструкторі нащадка.
- **Статичні методи**: Для утиліт, а не логіки екземплярів.
- **Перевіряйте типи**: `instanceof` для динамічної перевірки.
- **Обирайте парадигму**: ООП для структур, функціональне для чистоти.
