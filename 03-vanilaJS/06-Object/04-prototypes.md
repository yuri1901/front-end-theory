# Прототипи та деструктуризація у JavaScript

## Загальна інформація

- **Опис**: Прототипи забезпечують механізм успадкування в JavaScript. Деструктуризація спрощує витягування даних із об’єктів чи масивів.
- **Прототипи**:
  - Ланцюжок прототипів: `Object.getPrototypeOf()`, `Object.setPrototypeOf()`.
  - Створення: `Object.create()`.
- **Деструктуризація**:
  - Об’єкти: `{ a, b } = obj`.
  - Масиви: `[x, y] = arr`.
  - Значення за замовчуванням: `{ a = 0 } = {}`.
- **Особливості**:
  - `this` залежить від контексту виклику.
  - Прототипи впливають на доступ до властивостей.
- **Контекст**: Успадкування, спрощення коду, організація даних.

## Приклади коду

### Прототипи

```javascript
let proto = {
  sayHi() {
    return "Hi";
  },
};
let obj = Object.create(proto);
console.log(obj.sayHi()); // Hi
console.log(Object.getPrototypeOf(obj) === proto); // true
Object.setPrototypeOf(obj, {
  greet() {
    return "Hello";
  },
});
console.log(obj.greet()); // Hello
```

### Деструктуризація

```javascript
let obj = { name: "Іван", age: 25 };
let { name, age } = obj;
console.log(name, age); // Іван 25
let { city = "Київ" } = obj;
console.log(city); // Київ
let [first, second] = [1, 2];
console.log(first, second); // 1 2
```

### Контекст `this`

```javascript
let obj = {
  value: 1,
  getValue() {
    return this.value;
  },
};
console.log(obj.getValue()); // 1
let fn = obj.getValue;
console.log(fn()); // undefined
```

## Особливості для співбесід — Питання та відповіді

### Як працює `this` у методах об’єктів?

- **Відповідь**: Залежить від способу виклику; прив’язується до об’єкта при виклику через крапку.
  ```javascript
  let obj = {
    value: 1,
    get() {
      return this.value;
    },
  };
  console.log(obj.get()); // 1
  let fn = obj.get;
  console.log(fn()); // undefined
  ```

### Що таке ланцюжок прототипів?

- **Відповідь**: Ієрархія об’єктів, де властивості шукаються в прототипах.
  ```javascript
  let proto = { x: 10 };
  let obj = Object.create(proto);
  console.log(obj.x); // 10
  ```

### Як працює деструктуризація з значеннями за замовчуванням?

- **Відповідь**: Дозволяє задавати значення, якщо властивість відсутня.
  ```javascript
  let { a = 0 } = {};
  console.log(a); // 0
  ```

### Як змінити прототип об’єкта?

- **Відповідь**: Використовуйте `Object.setPrototypeOf()` або `Object.create()`.
  ```javascript
  let obj = {};
  Object.setPrototypeOf(obj, { x: 1 });
  console.log(obj.x); // 1
  ```

## Поради

- **Використовуйте прототипи**: Для успадкування замість дублювання коду.
- **Перевіряйте `this`**: Використовуйте `bind()` чи стрілкові функції для фіксації контексту.
- **Деструктуризуйте з розумом**: Застосовуйте значення за замовчуванням для гнучкості.
- **Уникайте мутацій прототипів**: Зміни впливають на всі об’єкти в ланцюжку.
- **Тестуйте деструктуризацію**: Перевіряйте сумісність структури перед витягуванням.
