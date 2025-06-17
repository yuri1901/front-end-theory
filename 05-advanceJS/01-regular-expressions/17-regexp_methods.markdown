# Детальний конспект: Методи регулярних виразів у JavaScript

## Загальна інформація

- **Опис**: JavaScript надає методи для роботи з регулярними виразами, які дозволяють шукати, перевіряти та маніпулювати строками.
- **Контекст**: Використовуються для валідації, пошуку, заміни або парсингу тексту.
- **Основні компоненти**:
  - **Методи RegExp**: `test`, `exec`.
  - **Методи String**: `match`, `matchAll`, `replace`, `replaceAll`, `search`, `split`.
- **Особливості**:
  - `test` і `exec` працюють із об’єктом RegExp.
  - `matchAll` і `replaceAll` підтримуються з ES2020.

## Приклади коду

### 1. Метод `test`

Перевірка наявності збігу.

```javascript
const regex = /hello/;
console.log(regex.test("hello world")); // true
console.log(regex.test("hi")); // false
```

### 2. Метод `exec`

Деталізований пошук із групами.

```javascript
const str = "2023-12-25";
const regex = /(\d{4})-(\d{2})/;
console.log(regex.exec(str)); // ["2023-12", "2023", "12"]
```

### 3. Метод `match`

Пошук усіх збігів із флагом `g`.

```javascript
const str = "cat dog cat";
const regex = /cat/g;
console.log(str.match(regex)); // ["cat", "cat"]
```

### 4. Метод `matchAll`

Ітерація всіх збігів із групами.

```javascript
const str = "2023-12 2024-01";
const regex = /(\d{4})-(\d{2})/g;
const matches = [...str.matchAll(regex)];
console.log(matches); // [["2023-12", "2023", "12"], ["2024-01", "2024", "01"]]
```

### 5. Метод `replace`

Заміна збігу.

```javascript
const str = "hello world";
const regex = /world/;
console.log(str.replace(regex, "JavaScript")); // "hello JavaScript"
```

## Особливості для співбесід — Питання та відповіді

### Яка різниця між `test` і `exec`?

- **Відповідь**: `test` повертає `true`/`false`, `exec` — деталі збігу (масив або `null`).
  ```javascript
  console.log(/a/.test("abc")); // true
  console.log(/a/.exec("abc")); // ["a"]
  ```

### Що робить `matchAll`?

- **Відповідь**: Повертає ітератор усіх збігів із групами, потребує флага `g`.
  ```javascript
  console.log([..."/a/b/".matchAll(/(\w)/g)]); // [["a", "a"], ["b", "b"]]
  ```

### Як працює `replaceAll`?

- **Відповідь**: Замінює всі збіги, потребує флага `g` (ES2020+).
  ```javascript
  console.log("a a".replaceAll(/a/g, "b")); // "b b"
  ```

### Що повертає `search`?

- **Відповідь**: Індекс першого збігу або -1.
  ```javascript
  console.log("abc".search(/b/)); // 1
  ```

## Поради

- **Вибір методу**: Використовуйте `test` для швидкої перевірки, `exec` для детальних даних.
- **Флаг `g`**: Обов’язковий для `match`, `matchAll`, `replaceAll`.
- **Тестування**: Перевіряйте методи на regex101.com або консолі.
- **Сумісність**: Переконайтеся, що `matchAll` і `replaceAll` підтримуються (ES2020+).

## Додаткові деталі

- **Методи**:
  - `test`: Перевірка наявності.
  - `exec`: Деталі одного збігу.
  - `match`: Усі збіги (з `g`).
  - `matchAll`: Ітератор збігів із групами.
  - `replace`: Заміна першого або всіх (з `g`).
  - `replaceAll`: Заміна всіх (з `g`).
  - `search`: Індекс першого збігу.
  - `split`: Розбиття строки за шаблоном.
- **Сумісність**: `matchAll`, `replaceAll` — Chrome 73+, Firefox 67+, Safari 13+.
- **Обмеження**: `exec` із `g` потребує керування `lastIndex`.