# Детальний конспект: Основи Flexbox (MDN)

## Загальна інформація

- **Опис**: Flexbox (Flexible Box Layout) — це CSS-модуль для створення одновимірних макетів, що дозволяє гнучко розташувати елементи в контейнері вздовж головної або поперечної осі.
- **Контекст**: Використовується для вирівнювання, розподілу простору та адаптивних макетів без використання `float` чи `position`.
- **Основні компоненти**:
  - **Flex-контейнер**: Елемент із `display: flex` або `inline-flex`.
  - **Flex-елементи**: Прямі дочірні елементи контейнера.
  - **Властивості контейнера**:
    - `flex-direction`: Визначає головну вісь (`row`, `column`).
    - `justify-content`: Вирівнювання вздовж головної осі.
    - `align-items`: Вирівнювання вздовж поперечної осі.
    - `flex-wrap`: Контролює перенесення елементів.
  - **Властивості елементів**: `flex-grow`, `flex-shrink`, `flex-basis`, `order`.
- **Особливості**:
  - Ідеальний для одновимірних макетів (рядки або стовпці).
  - Автоматично адаптується до розмірів вмісту.
  - Підтримує динамічне розташування.

## Приклади коду

### 1. Базовий Flex-контейнер

Рядок із вирівнюванням.

```css
.container {
  display: flex;
  justify-content: space-between;
  background-color: #f0f0f0;
}
.item {
  background-color: lightblue;
  padding: 10px;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">Елемент 1</div>
  <div class="item">Елемент 2</div>
  <div class="item">Елемент 3</div>
</div>
```

#### Результат:

Три елементи рівномірно розподілені в рядку.

### 2. Стовпець із вирівнюванням

Вертикальний макет.

```css
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 300px;
}
.item {
  margin: 5px;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">Елемент 1</div>
  <div class="item">Елемент 2</div>
</div>
```

#### Результат:

Елементи в стовпці, центровані горизонтально.

### 3. Перенесення елементів

Використання `flex-wrap`.

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.item {
  width: 100px;
  background-color: coral;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">Елемент 1</div>
  <div class="item">Елемент 2</div>
  <div class="item">Елемент 3</div>
</div>
```

#### Результат:

Елементи переносяться на новий рядок при нестачі місця.

### 4. Зростання елементів

Використання `flex-grow`.

```css
.container {
  display: flex;
}
.item1 {
  flex-grow: 1;
}
.item2 {
  flex-grow: 2;
}
```

#### HTML:

```html
<div class="container">
  <div class="item1">Елемент 1</div>
  <div class="item2">Елемент 2</div>
</div>
```

#### Результат:

Елемент 2 займає вдвічі більше простору, ніж елемент 1.

## Особливості для співбесід — Питання та відповіді

### Що таке Flexbox?

- **Відповідь**: CSS-модуль для одновимірних макетів із гнучким розташуванням елементів.
  ```css
  display: flex;
  ```

### Які основні осі у Flexbox?

- **Відповідь**: Головна (main axis, залежить від `flex-direction`) і поперечна (cross axis).
  ```css
  flex-direction: row;
  ```

### Що робить `justify-content`?

- **Відповідь**: Вирівнює елементи вздовж головної осі (`flex-start`, `space-between` тощо).
  ```css
  justify-content: center;
  ```

### Як працює `flex-grow`?

- **Відповідь**: Визначає, як елемент розтягується для заповнення вільного простору.
  ```css
  flex-grow: 1;
  ```

## Поради

- **Початок**: Починайте з `display: flex` і `flex-direction`.
- **Гнучкість**: Використовуйте `flex-wrap` для адаптивності.
- **Тестування**: Перевіряйте макети в DevTools (Flexbox вкладка).
- **Сумісність**: Додавайте префікси (`-webkit-`) для старих браузерів.
- **Документація**: Звертайтеся до MDN для деталей.

## Додаткові деталі

- **Властивості контейнера**:
  - `flex-direction`: `row`, `column`, `row-reverse`, `column-reverse`.
  - `justify-content`: `flex-start`, `center`, `space-between`, `space-around`.
  - `align-items`: `stretch`, `center`, `flex-start`, `flex-end`.
  - `gap`: Відстань між елементами.
- **Властивості елементів**:
  - `flex`: Скорочення для `flex-grow`, `flex-shrink`, `flex-basis`.
  - `order`: Змінює порядок елементів.
- **Сумісність**: Повна підтримка в сучасних браузерах (IE11 часткова).
- **Обмеження**: Не підходить для двовимірних макетів (використовуйте Grid).
