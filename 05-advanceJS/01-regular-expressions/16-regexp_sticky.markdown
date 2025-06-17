# Детальний конспект: Липкий режим у регулярних виразах

## Загальна інформація

- **Опис**: Липкий режим, активований флагом `y`, змушує регулярний вираз зіставляти шаблон лише з позиції `lastIndex` у строці.
- **Контекст**: Використовується для послідовного парсингу, наприклад, токенізації або обробки великих текстів.
- **Основні компоненти**:
  - **Флаг `y`**: Увімкнення липкого режиму.
  - **Властивість `lastIndex`**: Вказує, звідки починати наступне зіставлення.
- **Особливості**:
  - На відміну від флага `g`, `y` не шукає всі збіги, а лише з `lastIndex`.
  - Зазвичай використовується з `exec`.

## Приклади коду

### 1. Липкий режим із `exec`

Послідовний пошук слів.

```javascript
const str = "cat dog";
const regex = /\w+/y;
regex.lastIndex = 0;
console.log(regex.exec(str)); // ["cat"]
regex.lastIndex = 4;
console.log(regex.exec(str)); // ["dog"]
```

### 2. Порівняння з флагом `g`

Пошук із глобальним і липким режимом.

```javascript
const str = "cat dog";
const regexG = /\w+/g;
const regexY = /\w+/y;
console.log(str.match(regexG)); // ["cat", "dog"]
console.log(regexY.exec(str)); // ["cat"] (лише перший збіг із lastIndex=0)
```

### 3. Використання `lastIndex`

Ручне керування позицією.

```javascript
const str = "a b c";
const regex = /\w/y;
let match;
regex.lastIndex = 0;
while ((match = regex.exec(str))) {
  console.log(match[0], regex.lastIndex); // "a" 1, "b" 3, "c" 5
  regex.lastIndex++;
}
```

### 4. Липкий режим із `test`

Перевірка зіставлення з позиції.

```javascript
const str = "test";
const regex = /t/y;
regex.lastIndex = 0;
console.log(regex.test(str)); // true
regex.lastIndex = 1;
console.log(regex.test(str)); // false
```

## Особливості для співбесід — Питання та відповіді

### Що таке липкий режим?

- **Відповідь**: Режим із флагом `y`, що зіставляє шаблон лише з позиції `lastIndex`.
  ```javascript
  const regex = /a/y;
  regex.lastIndex = 0;
  console.log(regex.test("ab")); // true
  ```

### Чим відрізняється флаг `y` від `g`?

- **Відповідь**: `y` зіставляє лише з `lastIndex`, `g` шукає всі збіги.
  ```javascript
  console.log("ab".match(/a/g)); // ["a"]
  console.log(/a/y.exec("ab")); // ["a"]
  ```

### Як працює `lastIndex`?

- **Відповідь**: Вказує позицію початку зіставлення, оновлюється після `exec`.
  ```javascript
  const regex = /a/y;
  regex.lastIndex = 1;
  console.log(regex.exec("aa")); // null
  ```

### Коли використовувати липкий режим?

- **Відповідь**: Для послідовного парсингу або токенізації.
  ```javascript
  const regex = /\w+/y;
  regex.lastIndex = 0;
  console.log(regex.exec("cat dog")); // ["cat"]
  ```

## Поради

- **Керування `lastIndex`**: Завжди встановлюйте `lastIndex` явно.
- **Тестування**: Перевіряйте на regex101.com із флагом `y`.
- **Комбінація**: Не поєднуйте `y` із `g`, це викликає помилку.
- **Сумісність**: Флаг `y` підтримується з ES6.

## Додаткові деталі

- **Флаг `y`**: Змушує зіставляти з `lastIndex`.
- **Сумісність**: Chrome 49+, Firefox 46+, Safari 10+.
- **Обмеження**: Не підходить для пошуку всіх збігів одразу.