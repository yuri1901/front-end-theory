# Основи класів у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Класи — це синтаксичний цукор для створення об’єктів із прототипами. Вони є шаблонами для інстанціювання.
- **Оголошення класів**:
  - Declaration: `class Name {}`.
  - Anonymous: `const Name = class {}`.
- **Конструктор**:
  - Метод `constructor` ініціалізує об’єкт.
- **Модифікатори доступу**:
  - `public`: Доступні всередині і зовні (за замовчуванням).
  - `private (#)`: Доступні лише всередині класу.
  - `protected` (частково у TypeScript): Доступні в класі та нащадках.
- **Геттери/сеттери**:
  - `get`: Зчитування значень.
  - `set`: Зміна значень із валідацією.
- **Особливості**:
  - Класи базуються на прототипах.
  - **Falsy/Truthy**: Екземпляри класів (об’єкти) завжди truthy.
- **Контекст**: Створення об’єктів, інкапсуляція, структури даних.

## Приклади коду

### Оголошення класів

```javascript
// Declaration
class Declar {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  sayHello() {
    return `Hello ${this.width} and ${this.height}`;
  }
}

// Anonymous
const Anonym = class {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  sayHello() {
    return `Hello ${this.width} and ${this.height}`;
  }
};
console.log(new Declar(10, 5).sayHello()); // Hello 10 and 5
```

### Конструктор та приватні поля

```javascript
class Product {
  #name = "";
  #price = 0;
  constructor(name, price) {
    this.#name = name;
    this.#price = price;
  }
  getName() {
    return this.#name;
  }
}
const prod = new Product("Book", 10);
console.log(prod.getName()); // Book
// console.log(prod.#name); // SyntaxError
```

### Геттери та сеттери

```javascript
class User {
  #name = "";
  get name() {
    return this.#name;
  }
  set name(value) {
    if (typeof value !== "string") throw new Error("Must be string");
    this.#name = value;
  }
}
const user = new User();
user.name = "Alex";
console.log(user.name); // Alex
// user.name = 123; // Error
```

## Особливості для співбесід — Питання та відповіді

### У чому різниця між `class` і `function` конструктором?

- **Відповідь**: `class` — синтаксичний цукор із вбудованим `new`, `function` — ручне створення прототипів.
  ```javascript
  class A {}
  let a = new A();
  function B() {}
  let b = new B();
  ```

### Як працюють приватні поля (#)?

- **Відповідь**: Доступні лише всередині класу.
  ```javascript
  class C {
    #x = 1;
    getX() {
      return this.#x;
    }
  }
  console.log(new C().getX()); // 1
  // console.log(new C().#x); // SyntaxError
  ```

### Що таке геттер/сеттер?

- **Відповідь**: Геттер зчитує, сеттер валімує й змінює.
  ```javascript
  class D {
    #x = 0;
    get x() {
      return this.#x;
    }
    set x(v) {
      this.#x = v;
    }
  }
  let d = new D();
  d.x = 5;
  console.log(d.x); // 5
  ```

### Чи підлягають класи підняттю?

- **Відповідь**: Ні, оголошення класів не піднімаються (Temporary Dead Zone для `let/const`).
  ```javascript
  // console.log(new MyClass()); // ReferenceError
  class MyClass {}
  ```

## Поради

- **Використовуйте класи для структури**: Замість об’єктів із літералів.
- **Приватні поля (#)**: Для інкапсуляції даних.
- **Валідація в сеттерах**: Перевіряйте вхідні значення.
- **Уникайте прямого доступу**: Використовуйте геттери/сеттери.
- **Тестуйте екземпляри**: Перевірте сумісність із `instanceof`.
