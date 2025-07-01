# Конспект: Змінні та базові типи в TypeScript

## Базові типи даних

### Boolean

Тип `boolean` представляє логічні значення `true` або `false`.

```typescript
let isDone: boolean = true;
isDone = false;
```

### Number

Тип `number` підтримує цілі, дробові числа, а також числа в шістнадцятковій, двійковій та вісімковій системах числення.

```typescript
const a1_int: number = 14;
const a2_float: number = 14.5;
const a3_hex: number = 0x00a; // 10
const a4_binary: number = 0b1010; // 10
const a5_octal: number = 0o12; // 10
```

### String

Тип `string` використовується для текстових даних. Підтримує шаблонні рядки з `${}`.

```typescript
const firstName: string = `Hello Yuri ${a1_int}`; // Виведе: Hello Yuri 14
```

### Symbol

Тип `Symbol` створює унікальні ідентифікатори. Кожен Symbol унікальний.

```typescript
const mySymbol1: Symbol = Symbol("typescript");
const mySymbol2: Symbol = Symbol("typescript");
// mySymbol1 !== mySymbol2
```

### Array

Масиви типізуються з вказівкою типу елементів. Можна використовувати унію типів.

```typescript
const year: string[] = ["January", "February", "March"];
const years: (string | number | boolean)[] = [1, "January", "February", true];
const list: number[] = [1, 2, 3, 4];
const listNested: number[][] = [[1, 2, 3, 4]];

// Обчислення суми елементів масиву
let sum: number = 0;
for (const item of list) {
  sum += item;
}
console.log(sum); // Виведе: 10
```

Альтернативна типізація масивів:

```typescript
const values: Array<number | string> = [-1, -2, -3, "string"];
const valuesNested: Array<Array<number | string>> = [[-1, -2, -3, "string"]];
```

### Tuple (Кортеж)

Кортеж — масив із фіксованою кількістю елементів і чітко визначеними типами.

```typescript
let tupels: [string, number];
tupels = ["Hello", 10];
console.log(tupels); // Виведе: ["Hello", 10]
```

### Enum (Перечислення)

`enum` створює набір іменованих констант.

```typescript
enum StatusCode {
  OK = 200,
  BadRequest = 400,
  Unauthorized = 401,
  NotFound = 404,
}

enum StatusMessage {
  OK = "Success",
  BadRequest = "Bad Request",
  Unauthorized = "Unauthorized",
  NotFound = "Not Found",
}

function getStatusInfo(code: StatusCode): [StatusCode, string] {
  return [code, StatusMessage[StatusCode[code]]];
}
const res: [StatusCode, string] = getaissezInfo(StatusCode.NotFound);
console.log(res); // Виведе: [404, "Not Found"]
```

Приклад використання `enum`:

```typescript
// Без enum (поганий код)
function drawImage1(fruit: number) {
  const domElement: HTMLImageElement = document.createElement("img");
  switch (fruit) {
    case 0:
      domElement.src = "./images/apple.jpg";
      break;
    case 1:
      domElement.src = "./images/orange.jpg";
      break;
    case 2:
      domElement.src = "./images/tomato.jpg";
      break;
  }
  document.body.appendChild(domElement);
}
drawImage1(1);

// З enum (кращий код)
enum Fruit {
  Apple,
  Orange,
  Tomato,
}
function drawImage2(fruit: Fruit) {
  const domElement: HTMLImageElement = document.createElement("img");
  switch (fruit) {
    case Fruit.Apple:
      domElement.src = "./images/apple.jpg";
      break;
    case Fruit.Orange:
      domElement.src = "./images/orange.jpg";
      break;
    case Fruit.Tomato:
      domElement.src = "./images/tomato.jpg";
      break;
  }
  document.body.appendChild(domElement);
}
drawImage2(Fruit.Tomato);
```

### Null та Undefined

Типи `null` і `undefined` представляють відсутність значення.

```typescript
const u: undefined = undefined;
const n: null = null;
```

### Type Assertions (Затвердження типів)

Затвердження типів дозволяють явно вказати компілятору тип значення.

```typescript
let someData: any = "Hello World";
let strLength1: number = (<string>someData).length;
let strLength2: number = (someData as string).length;

let arr: any = [1, 2, 3];
let typeArr = (arr as number[]).length;
console.log(typeArr); // Виведе: 3
```

### Any, Unknown, Never, Void

#### Any

Тип `any` дозволяє присвоювати будь-яке значення без перевірки типів. Небезпечно, бо вимикає типізацію.

```typescript
let someValue: any = "Hello World";
someValue = false; // OK
someValue = 42; // OK
someValue.someMethod(); // OK (але може викликати помилку в рантаймі)
```

#### Unknown

Тип `unknown` дозволяє присвоювати будь-яке значення, але вимагає перевірки типу перед використанням.

```typescript
let someUnknown: unknown = "Hello World";
someUnknown = 42; // OK
// someUnknown.length; // Помилка
if (typeof someUnknown === "string") {
  console.log(someUnknown.length); // OK
}
```

#### Never

Тип `never` для значень, які ніколи не виникають (помилки, нескінченні цикли).

```typescript
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {}
}

enum Color {
  Red,
  Blue,
}
function getColorName(color: Color): string {
  switch (color) {
    case Color.Red:
      return "Red";
    case Color.Blue:
      return "Blue";
    default:
      return assertNever(color); // Захищає від нових значень
  }
}
function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${value}`);
}
```

#### Void

Тип `void` вказує на відсутність повернення функцією.

```typescript
function myProcedure(): void {
  console.log("void");
}
let someVoid: void = undefined;
someVoid = null; // Допустимо в нестрогому режимі
```

#### Порівняння `any`, `unknown`, `never`, `void`

| Тип         | Опис                                                                 | Коли використовувати                           | Обмеження                                  |
| ----------- | -------------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------------ |
| **any**     | Дозволяє будь-який тип без перевірки.                                | Динамічні дані, міграція JavaScript-коду.      | Небезпечно, втрата перевірки типів.        |
| **unknown** | Дозволяє будь-який тип, але вимагає перевірки.                       | Невідомі дані (API), коли потрібна безпека.    | Потрібно звужувати тип.                    |
| **never**   | Значення, яке ніколи не виникає.                                     | Помилки, нескінченні цикли, вичерпний перебір. | Не можна присвоїти значення, крім `never`. |
| **void**    | Відсутність повернення (`undefined` або `null` у нестрогому режимі). | Функції без повернення.                        | Обмежене використання.                     |

**Приклад**:

```typescript
let valueAny: any = "test";
valueAny = 42; // OK
valueAny.someMethod(); // OK (але небезпечно)

let valueUnknown: unknown = "test";
valueUnknown = 42; // OK
// valueUnknown.someMethod(); // Помилка
if (typeof valueUnknown === "string") {
  console.log(valueUnknown.length); // OK
}

function error(): never {
  throw new Error("Error");
}

function log(): void {
  console.log("No return");
}
```

#### Object

Тип `object` позначає будь-який некритичний об’єкт (не примітиви, не `null`).

```typescript
let obj: object = { a: 1 };
obj = [1, 2, 3]; // OK
obj = new Date(); // OK
// obj = 42; // Помилка
```

## Типи, унікальні для TypeScript

- **Tuple**: Фіксований масив із чіткими типами (`[string, number]`).
- **Enum**: Іменовані константи (`enum Status { OK = 200 }`).
- **Any**: Будь-який тип без перевірки.
- **Unknown**: Будь-який тип із перевіркою.
- **Never**: Ніколи не виникає.
- **Void**: Відсутність повернення.
- **Union Types**: Об’єднання типів (`string | number`).
- **Type Assertions**: Явне вказання типу (`as string`).

## Типові запитання на співбесіді

1. Які типи є в TypeScript, але відсутні в JavaScript?
2. Що таке тип `boolean` у TypeScript і як він використовується?
3. Як працюють числа в TypeScript? Чи є різниця між різними системами числення?
4. Як оголосити масив із кількома типами даних?
5. Що таке кортеж (tuple) і в чому його відмінність від масиву?
6. Для чого використовуються перечислення (enums)? Наведіть приклад.
7. Чому тип `any` вважається небезпечним?
8. Що таке тип `void` і де він застосовується?
9. Як працюють затвердження типів (type assertions)?
10. Як би ви покращили код із "магічними" числами, наприклад, у функції `drawImage1`?
11. Чим відрізняються `any` і `unknown`?
12. Коли використовувати тип `never`?
13. Чим `void` відрізняється від `never`?
14. Як безпечно працювати з `unknown`?
15. Що виведе цей код?
    ```typescript
    let value: unknown = "Hello";
    console.log((value as string).length); // ?
    ```

## Відповіді на запитання на співбесіді

1. **Які типи є в TypeScript, але відсутні в JavaScript?**

   - Tuple, enum, any, unknown, never, void, union types, type assertions.

2. **Що таке тип `boolean` у TypeScript і як він використовується?**

   - Тип `boolean` представляє значення `true` або `false`. Наприклад: `let isActive: boolean = true`.

3. **Як працюють числа в TypeScript? Чи є різниця між різними системами числення?**

   - Тип `number` підтримує цілі, дробові, шістнадцяткові, двійкові, вісімкові числа. Усі є числами з плаваючою комою, різниця лише в синтаксисі.

4. **Як оголосити масив із кількома типами даних?**

   - Використовуйте унію: `(string | number)[]` або `Array<string | number>`.

5. **Що таке кортеж (tuple) і в чому його відмінність від масиву?**

   - Кортеж — масив із фіксованою кількістю елементів і чіткими типами в порядку. Наприклад: `[string, number]`. Масив не обмежує порядок і кількість.

6. **Для чого використовуються перечислення (enums)? Наведіть приклад.**

   - `enum` створює іменовані константи для заміни "магічних" значень. Наприклад: `enum Status { OK = 200, Error = 400 }`.

7. **Чому тип `any` вважається небезпечним?**

   - Вимикає перевірку типів, що може призвести до помилок у рантаймі.

8. **Що таке тип `void` і де він застосовується?**

   - Вказує на відсутність повернення функцією. Наприклад: `function log(): void { console.log("Hi"); }`.

9. **Як працюють затвердження типів (type assertions)?**

   - Дозволяють явно вказати тип: `let len = (someValue as string).length`.

10. **Як би ви покращили код із "магічними" числами, наприклад, у функції `drawImage1`?**

    - Замініть числа на `enum`, як у `drawImage2`, для читабельності та безпеки.

11. **Чим відрізняються `any` і `unknown`?**

    - `any` дозволяє будь-які операції без перевірки, `unknown` вимагає перевірки типу перед використанням.

12. **Коли використовувати тип `never`?**

    - Для функцій, що кидають помилки, мають нескінченний цикл, або для вичерпного перебору в `switch`.

13. **Чим `void` відрізняється від `never`?**

    - `void` — для функцій, що повертають `undefined` або нічого, `never` — для функцій, що ніколи не завершуються.

14. **Як безпечно працювати з `unknown`?**

    - Використовуйте перевірки типу (`typeof`, `instanceof`) або затвердження типів.

15. **Що виведе цей код?**
    ```typescript
    let value: unknown = "Hello";
    console.log((value as string).length); // 5
    ```

## Корисні ресурси

- [TypeScript Official Documentation](https://www.typescriptlang.org/docs/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
