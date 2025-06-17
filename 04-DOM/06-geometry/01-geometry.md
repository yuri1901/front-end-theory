# Геометрія елементів, розміри та прокручування у JavaScript: Дуже детальний конспект

## Загальна інформація

- **Опис**: Цей конспект охоплює Web API для роботи з геометрією елементів, розмірами вікон, прокручуванням та позиціонуванням у DOM. Включає інтерфейси геометрії, методи визначення розмірів і координат, а також управління прокручуванням.
- **Контекст**: Розробка адаптивних інтерфейсів, анімація, обробка подій прокручування.
- **Основні інтерфейси та методи**:
  - Геометрія: `DOMRect`, `getBoundingClientRect`, `getClientRects`.
  - Розміри: `innerHeight`, `innerWidth`, `clientHeight`, `clientWidth`, `offsetHeight`, `offsetWidth`, `scrollHeight`, `scrollWidth`.
  - Прокручування: `scrollX`, `scrollY`, `scrollTo`, `scrollIntoView`.
  - Позиціонування: `elementFromPoint`.
- **Особливості**:
  - Значення можуть варіюватися залежно від viewport і стилів (наприклад, border-box).
  - Сумісність із сучасними браузерами (IE підтримує частково).

## Приклади коду

### 1. Геометрія елементів

#### `getBoundingClientRect`

- Повертає об’єкт `DOMRect` із розмірами і позицією елемента відносно viewport.

```javascript
const div = document.querySelector(".box");
const rect = div.getBoundingClientRect();
console.log(rect.top, rect.right, rect.bottom, rect.left); // Координати
console.log(rect.width, rect.height); // Розміри
```

#### `getClientRects`

- Повертає `DOMRectList` із прямокутниками для кожного рядка елемента (корисне для багаторядкових елементів).

```javascript
const p = document.querySelector("p");
const rects = p.getClientRects();
rects.forEach((rect) => console.log(rect.top, rect.height));
```

### 2. Розміри вікон і елементів

#### `innerHeight` та `innerWidth`

- Повертають висоту і ширину viewport (включаючи прокрутку).

```javascript
console.log(window.innerHeight); // Висота viewport
console.log(window.innerWidth); // Ширина viewport
```

#### `clientHeight` та `clientWidth`

- Повертають внутрішні розміри елемента (без прокрутки, включаючи padding).

```javascript
const div = document.querySelector(".box");
console.log(div.clientHeight, div.clientWidth);
```

#### `offsetHeight` та `offsetWidth`

- Повертають повні розміри елемента (включаючи border і padding).

```javascript
console.log(div.offsetHeight, div.offsetWidth);
```

#### `scrollHeight` та `scrollWidth`

- Повертають повну висоту і ширину елемента, включаючи прокручуваний вміст.

```javascript
console.log(div.scrollHeight, div.scrollWidth);
```

### 3. Позиція прокручування

#### `scrollX` та `scrollY`

- Повертають поточну позицію прокручування відносно viewport.

```javascript
console.log(window.scrollX, window.scrollY); // Координати прокручування
```

### 4. Визначення елемента за координатами

#### `elementFromPoint`

- Повертає елемент у вказаній точці viewport.

```javascript
const elem = document.elementFromPoint(100, 100);
console.log(elem.tagName); // Наприклад, "DIV"
```

### 5. Керування прокручуванням

#### `scrollTo`

- Прокручує елемент до заданих координат.

```javascript
const div = document.querySelector(".container");
div.scrollTo({ top: 500, left: 0, behavior: "smooth" });
```

#### `scrollIntoView`

- Прокручує сторінку, щоб елемент став видимим.

```javascript
const target = document.querySelector("#target");
target.scrollIntoView({ behavior: "smooth", block: "center" });
```

### 6. Інтерактивний приклад

```javascript
const box = document.querySelector(".box");
const log = document.querySelector("#log");

window.addEventListener("scroll", () => {
  const rect = box.getBoundingClientRect();
  log.textContent = `Top: ${rect.top}, ScrollY: ${window.scrollY}`;
});

document.querySelector("#scrollBtn").addEventListener("click", () => {
  box.scrollIntoView({ behavior: "smooth" });
});
```

## Особливості для співбесід — Питання та відповіді

### Що таке `DOMRect` і як його використовувати?

- **Відповідь**: `DOMRect` — об’єкт із координатами і розмірами елемента, отриманий через `getBoundingClientRect`.
  ```javascript
  const rect = document.querySelector("div").getBoundingClientRect();
  console.log(rect.top);
  ```

### Чим відрізняються `clientHeight` і `offsetHeight`?

- **Відповідь**: `clientHeight` — внутрішній розмір (padding), `offsetHeight` — повний розмір (padding + border).
  ```javascript
  console.log(div.clientHeight, div.offsetHeight);
  ```

### Як працює `scrollIntoView`?

- **Відповідь**: Прокручує сторінку, щоб елемент став видимим, із опціями `behavior` і `block`.
  ```javascript
  document.querySelector("#id").scrollIntoView({ behavior: "smooth" });
  ```

### Що повертає `elementFromPoint`?

- **Відповідь**: Елемент у вказаній точці viewport, або `null`, якщо поза документом.
  ```javascript
  console.log(document.elementFromPoint(50, 50));
  ```

### Як визначити, чи елемент видимий у viewport?

- **Відповідь**: Перевірте, чи `rect.top` і `rect.bottom` у межах `0` і `window.innerHeight`.
  ```javascript
  const rect = box.getBoundingClientRect();
  const isVisible = rect.top >= 0 && rect.bottom <= window.innerHeight;
  ```

### Чим відрізняються `scrollHeight` і `clientHeight`?

- **Відповідь**: `scrollHeight` — повна висота з прокручуваним вмістом, `clientHeight` — видимий розмір.
  ```javascript
  console.log(div.scrollHeight, div.clientHeight);
  ```

## Поради

- **Перевірка розмірів**: Використовуйте `getBoundingClientRect` для точних координат.
- **Оптимізація**: Обмежте часті виклики `getBoundingClientRect` через `requestAnimationFrame`.
- **Прокручування**: Використовуйте `behavior: "smooth"` для UX.
- **Сумісність**: Перевіряйте `offset` і `client` властивості в старих браузерах.
- **Відстеження видимості**: Комбінуйте з `IntersectionObserver` для ефективності.
- **Координати**: Враховуйте `scrollX`/`scrollY` для абсолютного позиціонування.
- **Тестування**: Емулюйте різні розміри viewport для адаптивності.

## Додаткові деталі

- **Geometry interfaces**: `DOMRect`, `DOMRectReadOnly`, `DOMPoint`, `DOMMatrix` використовуються для геометричних обчислень.
- **Різниця в моделях**: `client` ігнорує border, `offset` включає, `scroll` враховує прокрутку.
- **Сумісність**: `scrollTo` з `options` підтримується з Chrome 61+, Firefox 36+.
- **Позиціонування**: `elementFromPoint` враховує лише видимий вміст.
- **Продуктивність**: Уникайте частого виклику методів прокручування в циклах.
