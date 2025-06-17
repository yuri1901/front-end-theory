# Детальний конспект: Основи CSS Box Model

## Загальна інформація

- **Опис**: CSS box-модель — це основа для розуміння того, як елементи відображаються на сторінці, включаючи їх контент, padding, border і margin.
- **Контекст**: Використовується для створення макетів, контролю розмірів і відстаней між елементами.
- **Основні компоненти**:
  - **Content**: Зона вмісту (текст, зображення).
  - **Padding**: Внутрішній відступ.
  - **Border**: Рамка навколо елемента.
  - **Margin**: Зовнішній відступ.
  - **Box-sizing**: `content-box` або `border-box`.
- **Особливості**:
  - Кожен HTML-елемент є "коробкою".
  - Розміри залежать від `box-sizing` і стилів.
  - Margin collapsing впливає на вертикальні відстані.

## Приклади коду

### 1. Базова box-модель

Усі компоненти.

```css
div {
  width: 100px;
  height: 100px;
  padding: 10px;
  border: 2px solid black;
  margin: 15px;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Ширина = 100px + 20px (padding) + 4px (border) + 30px (margin) = 154px.

### 2. Box-model із `border-box`

Фіксований розмір.

```css
div {
  box-sizing: border-box;
  width: 100px;
  padding: 10px;
  border: 2px solid blue;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Ширина = 100px (включає все).

### 3. Margin collapsing

Злиття відстаней.

```css
.div1 {
  margin-bottom: 20px;
}
.div2 {
  margin-top: 10px;
}
```

#### HTML:

```html
<div class="div1">Блок 1</div>
<div class="div2">Блок 2</div>
```

#### Результат:

Відстань = 20px.

### 4. Практичний приклад

Стилізований блок.

```css
.card {
  box-sizing: border-box;
  width: 200px;
  padding: 15px;
  border: 1px solid #ddd;
  margin: 10px;
  background-color: #fff;
}
```

#### HTML:

```html
<div class="card">Картка</div>
```

#### Результат:

Картка з фіксованою шириною 200px.

## Особливості для співбесід — Питання та відповіді

### Що включає CSS box-модель?

- **Відповідь**: Контент, padding, border, margin.
  ```css
  div {
    padding: 10px;
    border: 1px solid;
    margin: 10px;
  }
  ```

### Як `padding` відрізняється від `margin`?

- **Відповідь**: `padding` — внутрішній відступ, `margin` — зовнішній.
  ```css
  padding: 10px;
  margin: 10px;
  ```

### Що таке `box-sizing`?

- **Відповідь**: Визначає, що включають `width` і `height`: лише контент (`content-box`) або все (`border-box`).
  ```css
  box-sizing: border-box;
  ```

### Як працює margin collapsing?

- **Відповідь**: Вертикальні margins сусідніх block-елементів зливаються в більше значення.
  ```css
  div {
    margin: 20px 0;
  }
  ```

## Поради

- **Box-sizing**: Завжди використовуйте `border-box` для простоти.
- **Візуалізація**: Використовуйте DevTools для аналізу box-моделі.
- **Одиниці**: Застосовуйте `rem` або `%` для адаптивності.
- **Практика**: Експериментуйте з padding і margin для макетів.
- **Документація**: Звертайтеся до W3Schools або MDN.

## Додаткові деталі

- **Компоненти**:
  - Content: Визначається `width`/`height`.
  - Padding: Внутрішній простір.
  - Border: Рамка.
  - Margin: Зовнішній простір, може зливатися.
- **Сумісність**: Повна підтримка у всіх браузерах.
- **Обмеження**: Margin collapsing може заплутати початківців.
- **Альтернативи**: Flexbox/Grid для сучасних макетів.
