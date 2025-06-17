# Детальний конспект: Керівництво по Flexbox (CSS-Tricks)

## Загальна інформація

- **Опис**: Flexbox — це CSS-модуль, який забезпечує гнучке розташування елементів у контейнері, оптимізуючи макети для рядків або стовпців із динамічним вирівнюванням і розподілом простору.
- **Контекст**: Використовується для створення адаптивних інтерфейсів, замінюючи старі методи (`float`, `inline-block`) для навігації, карток, форм тощо.
- **Основні компоненти**:
  - **Flex-контейнер**: `display: flex` або `inline-flex`.
  - **Flex-елементи**: Дочірні елементи контейнера.
  - **Властивості контейнера**: `flex-direction`, `justify-content`, `align-items`, `flex-wrap`, `gap`.
  - **Властивості елементів**: `flex-grow`, `flex-shrink`, `flex-basis`, `align-self`, `order`.
- **Особливості**:
  - Простий для одновимірних макетів.
  - Підтримує автоматичне масштабування елементів.
  - Широко застосовується в сучасному веб-дизайні.

## Приклади коду

### 1. Центрування елементів

Повне вирівнювання.

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 200px;
  background-color: #f0f0f0;
}
.item {
  background-color: coral;
  padding: 20px;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">Центрований</div>
</div>
```

#### Результат:

Елемент розташований у центрі контейнера.

### 2. Рівномірний розподіл

Використання `space-between`.

```css
.container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.item {
  width: 100px;
  background-color: lightblue;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

#### Результат:

Елементи розподілені рівномірно, переносяться при нестачі місця.

### 3. Індивідуальне вирівнювання

Використання `align-self`.

```css
.container {
  display: flex;
  align-items: flex-start;
  height: 150px;
}
.item2 {
  align-self: flex-end;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item item2">2</div>
  <div class="item">3</div>
</div>
```

#### Результат:

Другий елемент вирівняний знизу, інші — зверху.

### 4. Зміна порядку

Використання `order`.

```css
.container {
  display: flex;
}
.item2 {
  order: -1;
}
```

#### HTML:

```html
<div class="container">
  <div class="item">1</div>
  <div class="item item2">2</div>
  <div class="item">3</div>
</div>
```

#### Результат:

Елемент 2 відображається першим.

## Особливості для співбесід — Питання та відповіді

### Що таке Flexbox і для чого він потрібен?

- **Відповідь**: Модуль для гнучких одновимірних макетів, що спрощує вирівнювання і розподіл.
  ```css
  display: flex;
  ```

### Що робить `align-items`?

- **Відповідь**: Вирівнює елементи вздовж поперечної осі (`center`, `stretch` тощо).
  ```css
  align-items: center;
  ```

### Як працює `flex-wrap`?

- **Відповідь**: Контролює, чи переносяться елементи на новий рядок (`wrap`, `nowrap`).
  ```css
  flex-wrap: wrap;
  ```

### Що таке `flex` скорочення?

- **Відповідь**: Комбінує `flex-grow`, `flex-shrink`, `flex-basis`.
  ```css
  flex: 1 1 auto;
  ```

## Поради

- **Візуалізація**: Використовуйте CSS-Tricks Flexbox-постер для швидкого довідника.
- **Практика**: Експериментуйте з `justify-content` і `align-items`.
- **Тестування**: Перевіряйте в DevTools (Flexbox вкладка).
- **Адаптивність**: Комбінуйте з медіа-запитами і `flex-wrap`.
- **Документація**: Звертайтеся до CSS-Tricks для прикладів.

## Додаткові деталі

- **Властивості контейнера**:
  - `flex-flow`: Скорочення для `flex-direction` і `flex-wrap`.
  - `gap`: Відстань між flex-елементами.
- **Властивості елементів**:
  - `flex-grow`: Коефіцієнт зростання.
  - `flex-shrink`: Коефіцієнт стиснення.
  - `align-self`: Індивідуальне вирівнювання.
- **Сумісність**: Широка підтримка, але IE10+ потребує префіксів.
- **Обмеження**: Не для складних двовимірних макетів (використовуйте Grid).
