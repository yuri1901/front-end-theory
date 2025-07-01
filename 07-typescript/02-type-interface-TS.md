# Конспект: `type` та `interface` у TypeScript

## 🔹 `type` — Псевдоніми типів

`type` — ключове слово для створення псевдонімів типів. Гнучкий інструмент для опису примітивів, об’єднань, кортежів, об’єктів тощо.

### Особливості

- Підтримує об’єднання (`union types`), перетини (`intersection types`), кортежі.
- Не підтримує декларативне злиття чи `implements` для класів.
- Ідеально для утилітарних типів і складних конструкцій.

### Приклади

#### Прості псевдоніми

```typescript
type UserId = string;
type UserName = string;

type User = {
  id: UserId;
  userName?: UserName;
  isActive: boolean;
};

const User1: User = {
  id: "2",
  userName: "Yura",
  isActive: true,
};

const User2: User = {
  id: "3",
  isActive: true,
};

function displayUserName({ id }: User): void {
  console.log(id);
}
displayUserName(User1); // Виведе: 2
displayUserName(User2); // Виведе: 3
```

#### Об’єднання типів

```typescript
type LoadingStatus = "loading" | "success" | "error";

let currentStatus: LoadingStatus = "loading";
console.log(currentStatus); // Виведе: loading
```

#### Кортежі

```typescript
type Point = [number, number];
const startPoint: Point = [0, 0];
const endPoint: Point = [100, 250];

function calcDist(p1: Point, p2: Point): number {
  return Math.sqrt((p2[0] - p1[0]) ** 2 + (p2[1] - p1[1]) ** 2);
}
console.log(`Відстань: ${calcDist(startPoint, endPoint)}`); // Виведе: Відстань: 269.2582
```

#### Перетини

```typescript
type Person = { name: string };
type Employee = { role: string };
type Worker = Person & Employee;

const worker: Worker = {
  name: "Yura",
  role: "Developer",
};
console.log(worker); // Виведе: { name: "Yura", role: "Developer" }
```

## 🔹 `interface` — Інтерфейси для об’єктів і класів

`interface` описує структуру об’єктів або класів. Підтримує спадкування та декларативне злиття.

### Особливості

- Орієнтований на об’єкти та класи.
- Підтримує `extends` і `implements`.
- Дозволяє декларативне злиття.

### Приклади

#### Опис об’єкта

```typescript
interface User {
  readonly id: string;
  userName: string;
  isActive: boolean;
  nickName?: string;
}

const user: User = {
  id: "1",
  userName: "Yura",
  isActive: true,
  nickName: "Yurik",
};
console.log(user); // Виведе: { id: "1", userName: "Yura", isActive: true, nickName: "Yurik" }
```

#### Інтерфейс із методами

```typescript
interface Book {
  title: string;
  author: string;
  pages: number;
  read: boolean;
  markAsRead(): void;
}

const book1: Book = {
  title: "The Hobbit",
  author: "J.R.R Tolkien",
  pages: 310,
  read: false,
  markAsRead: function () {
    this.read = true;
  },
};
book1.markAsRead();
console.log(book1.read); // Виведе: true
```

#### Розширення

```typescript
interface Person {
  name: string;
}
interface Employee extends Person {
  role: string;
}

const employee: Employee = {
  name: "Yura",
  role: "Developer",
};
console.log(employee); // Виведе: { name: "Yura", role: "Developer" }
```

#### Декларативне злиття

```typescript
interface User {
  id: string;
}
interface User {
  email: string;
}

const userExtended: User = {
  id: "1",
  email: "yura@example.com",
};
console.log(userExtended); // Виведе: { id: "1", email: "yura@example.com" }
```

## 🔹 Порівняння `type` та `interface`

| Характеристика            | `type`                                 | `interface`                             |
| ------------------------- | -------------------------------------- | --------------------------------------- |
| **Опис**                  | Псевдонім для будь-якого типу          | Опис структури об’єктів або класів      |
| **Гнучкість**             | Висока (об’єднання, кортежі, перетини) | Обмежена (фокус на об’єкти та класи)    |
| **Розширення**            | Через `&`                              | Через `extends` або декларативне злиття |
| **Декларативне злиття**   | Не підтримує                           | Підтримує                               |
| **Використання в класах** | Не підтримує `implements`              | Підтримує `implements`                  |

## 🔹 Практичні приклади

### Утилітарні типи з `type`

```typescript
type PartialUser = Partial<User>;
const partialUser: PartialUser = { id: "1" }; // OK

type ReadonlyUser = Readonly<User>;
const readonlyUser: ReadonlyUser = {
  id: "2",
  userName: "Yura",
  isActive: true,
};
// readonlyUser.isActive = false; // Помилка
```

### `interface` із класами

```typescript
interface Printable {
  print(): void;
}
class Document implements Printable {
  constructor(public title: string) {}
  print(): void {
    console.log(`Printing ${this.title}`);
  }
}
const doc: Printable = new Document("Report");
doc.print(); // Виведе: Printing Report
```

### Об’єднання з `type`

```typescript
type Status = "active" | "inactive";
type UserStatus = { id: string; status: Status };
const userStatus: UserStatus = { id: "1", status: "active" };
console.log(userStatus); // Виведе: { id: "1", status: "active" }
```

## 🔹 Типові запитання на співбесіді

### Теоретичні питання

1. Що таке `type` у TypeScript? Для чого він використовується?
2. Що таке `interface` у TypeScript? У чому його особливості?
3. Чим відрізняються `type` та `interface`?
4. Як працює декларативне злиття в `interface`? Чи підтримує це `type`?
5. Як реалізувати спадкування в `interface` та `type`?
6. Чи можна використовувати `type` для опису класів?
7. Що таке `readonly` у `interface`? Як його відтворити в `type`?
8. Як використовувати утилітарні типи (`Partial`, `Readonly`, тощо) з `type`?
9. Чи можна комбінувати `type` та `interface`?
10. Що виведе цей код?
    ```typescript
    interface User {
      id: string;
    }
    interface User {
      name: string;
    }
    const user: User = { id: "1" }; // Помилка чи OK?
    ```

### Практичні питання

1. Створіть `type` для точки та функцію для обчислення відстані.
2. Створіть `interface` для книги з методом `markAsRead`.
3. Напишіть `interface` для класу `Car`, який має метод `drive`. Реалізуйте клас.
4. Створіть `type` для статусів завантаження (`loading`, `success`, `error`).
5. Як зробити усі поля об’єкта необов’язковими за допомогою `type`?
6. Напишіть `interface`, який розширює інший `interface`.
7. Створіть `type` для RGB-колору (`[number, number, number]`).
8. Як заборонити зміну полів об’єкта, визначеного через `type`?
9. Напишіть код із декларативним злиттям для `interface`.
10. Що виведе цей код?
    ```typescript
    type Status = "active" | "inactive";
    const status: Status = "active";
    console.log(status);
    ```

## 🔹 Відповіді на запитання

### Теоретичні відповіді

1. `type` — псевдонім для створення типів (примітиви, об’єкти, кортежі, об’єднання). Спрощує код і підвищує безпеку.
2. `interface` описує структуру об’єктів або класів. Підтримує `extends`, `implements`, декларативне злиття.
3. `type` гнучкіший (об’єднання, кортежі), `interface` — для об’єктів/класів, підтримує злиття.
4. `interface` дозволяє додавати поля при повторному оголошенні. `type` цього не підтримує.
5. `interface` — через `extends`, `type` — через `&`.
6. `type` не підтримує `implements`, але описує об’єкти.
7. `readonly` забороняє зміну поля. У `type` — через `Readonly<T>`.
8. Наприклад, `Partial<T>` робить поля необов’язковими, `Readonly<T>` — незмінними.
9. Так, `type` може розширювати `interface` через `&`, а `interface` — `type` через `extends`.
10. Помилка: бракує обов’язкового поля `name`.

### Практичні відповіді

1. ```typescript
   type Point = [number, number];
   const p1: Point = [0, 0];
   const p2: Point = [3, 4];
   function calcDist(p1: Point, p2: Point): number {
     return Math.sqrt((p2[0] - p1[0]) ** 2 + (p2[1] - p1[1]) ** 2);
   }
   console.log(calcDist(p1, p2)); // 5
   ```
2. ```typescript
   interface Book {
     title: string;
     read: boolean;
     markAsRead(): void;
   }
   const book: Book = {
     title: "Book",
     read: false,
     markAsRead: function () {
       this.read = true;
     },
   };
   book.markAsRead();
   console.log(book.read); // true
   ```
3. ```typescript
   interface Car {
     model: string;
     drive(): void;
   }
   class MyCar implements Car {
     constructor(public model: string) {}
     drive(): void {
       console.log(`Driving ${this.model}`);
     }
   }
   const car = new MyCar("Toyota");
   car.drive(); // Driving Toyota
   ```
4. ```typescript
   type Status = "loading" | "success" | "error";
   function handleStatus(status: Status): void {
     console.log(`Status: ${status}`);
   }
   handleStatus("success"); // Status: success
   ```
5. ```typescript
   type User = { id: string; name: string };
   type PartialUser = Partial<User>;
   const user: PartialUser = { id: "1" };
   ```
6. ```typescript
   interface Person {
     name: string;
   }
   interface Employee extends Person {
     role: string;
   }
   const emp: Employee = { name: "Yura", role: "Developer" };
   ```
7. ```typescript
   type RGB = [number, number, number];
   const color: RGB = [255, 128, 0];
   console.log(color); // [255, 128, 0]
   ```
8. ```typescript
   type User = { id: string; name: string };
   type ReadonlyUser = Readonly<User>;
   const user: ReadonlyUser = { id: "1", name: "Yura" };
   ```
9. ```typescript
   interface User {
     id: string;
   }
   interface User {
     name: string;
   }
   const user: User = { id: "1", name: "Yura" };
   ```
10. ```typescript
    type Status = "active" | "inactive";
    const status: Status = "active";
    console.log(status); // active
    ```
