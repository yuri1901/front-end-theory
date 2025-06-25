# Конспект з основ TypeScript: Змінні та базові типи

## Базові типи даних

### Boolean

Тип `boolean` представляє логічні значення `true` або `false`.

```typescript
let isDone: boolean = true;
isDone = false;
```

### Number

Тип `number` підтримує цілі числа, дробові, а також числа в шістнадцятковій, двійковій та вісімковій системах числення.

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

Тип `Symbol` створює унікальні ідентифікатори. Кожен `Symbol` є унікальним, навіть якщо описи однакові.

```typescript
const mySymbol1: Symbol = Symbol("typescript");
const mySymbol2: Symbol = Symbol("typescript");
// mySymbol1 !== mySymbol2
```

### Array

Масиви в TypeScript типізуються, вказуючи тип елементів. Можна використовувати унію типів для змішаних даних.

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

Альтернативна типізація масивів за допомогою `Array<T>`:

```typescript
const values: Array<number | string> = [-1, -2, -3, "string"];
const valuesNested: Array<Array<number | string>> = [[-1, -2, -3, "string"]];
```

### Tuple (Кортеж)

Кортеж — це масив із фіксованою кількістю елементів і чітко визначеними типами в певному порядку.

```typescript
let tupels: [string, number];
tupels = ["Hello", 10];
console.log(tupels); // Виведе: ["Hello", 10]
```

### Enum (Перечислення)

`enum` створює набір іменованих констант, що полегшує роботу з фіксованими значеннями.

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
const res: [StatusCode, string] = getStatusInfo(StatusCode.NotFound);
console.log(res); // Виведе: [404, "Not Found"]
```

Приклад використання `enum` для покращення коду:

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

### Any

Тип `any` дозволяє присвоювати будь-яке значення, але його використання зменшує переваги TypeScript, тому бажано уникати.

```typescript
let someValue: any = "Hello World";
someValue = false; // Без помилок
```

### Void

Тип `void` вказує на відсутність значення, що повертається функцією (процедура).

```typescript
function myProcedure(): void {
  console.log("void");
}
let someVoid: void = undefined;
someVoid = null; // Допустимо в нестрогому режимі
```

### Null та Undefined

Типи `null` і `undefined` представляють відсутність значення.

```typescript
const u: undefined = undefined;
const n: null = null;
```

### Type Assertions (Затвердження типів)

Затвердження типів дозволяють вказати компілятору, що значення має певний тип. Не змінює дані в рантаймі.

```typescript
let someData: any = "Hello World";
let strLength1: number = (<string>someData).length;
let strLength2: number = (someData as string).length;

let arr: any = [1, 2, 3];
let typeArr = (arr as number[]).length;
console.log(typeArr); // Виведе: 3
```

## Типи, унікальні для TypeScript (немає в JavaScript)

TypeScript додає кілька типів і конструкцій, яких немає в JavaScript через його динамічну природу. Ось основні:

1. **Tuple (Кортеж)**

   - Фіксований масив із чітко визначеними типами елементів і їх порядком.
   - Приклад: `let tuple: [string, number] = ["Hello", 10];`.
   - У JavaScript масиви не мають такої строгої типізації.

2. **Enum (Перечислення)**

   - Набір іменованих констант, що спрощує роботу з фіксованими значеннями.
   - Приклад: `enum Status { OK = 200, Error = 400 }`.
   - У JavaScript для цього використовують об’єкти або константи, але без такої зручної синтаксичної конструкції.

3. **Any**

   - Тип, що дозволяє присвоювати будь-яке значення без перевірки. У JavaScript усі змінні за замовчуванням поводяться як `any`, але в TypeScript це явний тип.
   - Приклад: `let value: any = "text"; value = 123;`.

4. **Void**

   - Вказує на відсутність значення, що повертається функцією. У JavaScript функції, що нічого не повертають, повертають `undefined` неявно, але в TypeScript `void` є окремим типом.
   - Приклад: `function log(): void { console.log("Hi"); }`.

5. **Never**

   - Тип для функцій, які ніколи не завершуються (наприклад, кидають помилку або мають нескінченний цикл).
   - Приклад: `function throwError(): never { throw new Error("Error"); }`.
   - У JavaScript такого типу немає.

6. **Union Types (Об’єднання типів)**

   - Дозволяють вказати, що значення може бути одним із кількох типів.
   - Приклад: `let mixed: string | number = "text"; mixed = 123;`.
   - У JavaScript типи визначаються динамічно без явного оголошення.

7. **Type Assertions (Затвердження типів)**
   - Механізм, що дозволяє явно вказати компілятору тип значення.
   - Приклад: `let value: any = "text"; let len = (value as string).length;`.
   - У JavaScript немає аналогічного механізму, оскільки типи не перевіряються.

## Додаткові зауваження

- **Типізація масивів**: Використовуйте `T[]` або `Array<T>` для простоти. Для змішаних типів застосовуйте унію (`number | string`).
- **Перечислення**: Використовуйте `enum` для заміни "магічних" чисел чи рядків.
- **Any**: Уникайте, замінюючи конкретними типами чи уніями.
- **Strict-режим**: Увімкнення `strictNullChecks` у `tsconfig.json` забороняє присвоєння `null` до `void` без явного дозволу.
- **Never**: Корисно для функцій, які завжди завершуються помилкою або не завершуються.

## Типові запитання на співбесіді

1. **Які типи є в TypeScript, але відсутні в JavaScript?**

   - Відповідь: Унікальні типи в TypeScript: `tuple`, `enum`, `any`, `void`, `never`, об’єднання типів (`string | number`), затвердження типів (`as string`). JavaScript не має цих конструкцій через динамічну типізацію.

2. **Що таке тип `boolean` у TypeScript і як він використовується?**

   - Відповідь: Тип `boolean` представляє значення `true` або `false`. Наприклад: `let isActive: boolean = true`.

3. **Як працюють числа в TypeScript? Чи є різниця між різними системами числення?**

   - Відповідь: Тип `number` підтримує цілі, дробові, шістнадцяткові, двійкові та вісімкові числа. Усі вони є числами з плаваючою комою, різниця лише в синтаксисі.

4. **Як оголосити масив із кількома типами даних?**

   - Відповідь: Використовуйте унію типів, наприклад: `(string | number)[]` або `Array<string | number>`.

5. **Що таке кортеж (tuple) і в чому його відмінність від масиву?**

   - Відповідь: Кортеж — це масив із фіксованою кількістю елементів і чітко визначеними типами в певному порядку, наприклад: `[string, number]`. Масив не обмежує порядок і кількість.

6. **Для чого використовуються перечислення (enums)? Наведіть приклад.**

   - Відповідь: `enum` створює набір іменованих констант для заміни "магічних" значень. Наприклад: `enum Status { OK = 200, Error = 400 }`.

7. **Чому тип `any` вважається небезпечним?**

   - Відповідь: Тип `any` вимикає перевірку типів, що може призвести до помилок у рантаймі, нівелюючи переваги TypeScript.

8. **Що таке тип `void` і де він застосовується?**

   - Відповідь: Тип `void` вказує, що функція нічого не повертає, наприклад: `function log(): void { console.log("Hi"); }`.

9. **Як працюють затвердження типів (type assertions)?**

   - Відповідь: Затвердження типів (`as` або `<T>`) дозволяють вказати компілятору тип, наприклад: `(someValue as string).length`.

10. **Як би ви покращили код із "магічними" числами, наприклад, у функції `drawImage1`?**
    - Відповідь: Замініть числа на `enum`, як у `drawImage2`, щоб зробити код читабельним і безпечним.

## Корисні ресурси

- [TypeScript Official Documentation](https://www.typescriptlang.org/docs/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
