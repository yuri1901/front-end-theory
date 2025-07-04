# Детальний конспект: Набори символів і діапазони в регулярних виразах

## Загальна інформація

- **Опис**: Набори символів (`[...]`) і діапазони (`[a-z]`) у регулярних виразах дозволяють зіставляти групу символів або діапазон символів у строці. Вони є основою для гнучкого пошуку.
- **Контекст**: Використовуються для валідації (наприклад, літери, цифри) або пошуку специфічних груп символів у тексті.
- **Основні компоненти**:
  - **Набір символів**: `[abc]` зіставляє будь-який символ із `a`, `b`, `c`.
  - **Діапазон**: `[a-z]` зіставляє літери від `a` до `z`.
  - **Заперечення**: `[^abc]` зіставляє будь-який символ, крім `a`, `b`, `c`.
- **Особливості**:
  - Діапазони чутливі до регістру без флага `i`.
  - Можна комбінувати набори та діапазони (наприклад, `[a-z0-9]`).
  - Метасимволи в наборах (наприклад, `.`, `*`) втрачають спеціальне значення.

## Приклади коду

### 1. Зіставлення набору символів

Пошук символів `a`, `b` або `c`.

```javascript
const str = "cat and dog";
const regex = /[abc]/g;
console.log(str.match(regex)); // ["a", "c"]
```

### 2. Використання діапазону

Пошук усіх малих літер.

```javascript
const str = "Hello 123!";
const regex = /[a-z]/g;
console.log(str.match(regex)); // ["e", "l", "l", "o"]
```

### 3. Заперечення набору

Пошук символів, крім цифр.

```javascript
const str = "abc123xyz";
const regex = /[^0-9]/g;
console.log(str.match(regex)); // ["a", "b", "c", "x", "y", "z"]
```

### 4. Комбінація діапазонів

Пошук букв і цифр.

```javascript
const str = "Test123!";
const regex = /[a-zA-Z0-9]/g;
console.log(str.match(regex)); // ["T", "e", "s", "t", "1", "2", "3"]
```

### 5. Екранування в наборах

Пошук дефіса або крапки в наборі.

```javascript
const str = "a-b.c";
const regex = /[.-]/g; // Дефіс і крапка без екранування в наборі
console.log(str.match(regex)); // ["-", "."]
```

## Особливості для співбесід — Питання та відповіді

### Що таке набір символів у регулярних виразах?

- **Відповідь**: Набір `[...]` зіставляє будь-який символ із указаних у дужках.
  ```javascript
  console.log("abc".match(/[ab]/g)); // ["a", "b"]
  ```

### Що робить `[^...]`?

- **Відповідь**: Заперечує набір, зіставляючи символи, яких немає в дужках.
  ```javascript
  console.log("abc123".match(/[^a-c]/g)); // ["1", "2", "3"]
  ```

### Як працює діапазон `[a-z]`?

- **Відповідь**: Зіставляє будь-який символ у діапазоні від `a` до `z` (за ASCII).
  ```javascript
  console.log("xyz".match(/[x-z]/g)); // ["x", "y", "z"]
  ```

### Чи потрібно екранувати метасимволи в наборах?

- **Відповідь**: Більшість метасимволів (наприклад, `.`, `*`) втрачають спеціальне значення в `[...]`, але дефіс (`-`) екранується або ставиться на початку/кінці.
  ```javascript
  console.log("a-b".match(/[a\-b]/g)); // ["a", "-", "b"]
  ```

## Поради

- **Читабельність**: Уникайте надмірно складних наборів, розбивайте на кілька виразів.
- **Дефіс**: Ставте `-` на початку або кінці набору, щоб уникнути екранування.
- **Тестування**: Використовуйте regex101.com для перевірки діапазонів.
- **Unicode**: Для не-ASCII діапазонів (наприклад, `[а-я]`) додавайте флаг `u`.

## Додаткові деталі

- **Синтаксис**: `[a-zA-Z]` — літери, `[0-9]` — цифри, `[a-z0-9_]` — еквівалент `\w`.
- **Сумісність**: Повна підтримка у всіх браузерах.
- **Обмеження**: Діапазони в `[...]` базуються на ASCII, для Unicode потрібен флаг `u`.