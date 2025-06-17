# Детальний конспект: Огляд CSS Box Model

## Загальна інформація

- **Опис**: CSS box-модель — це концепція, яка описує, як кожен елемент на сторінці представлений прямокутником із контентом, padding, border і margin.
- **Контекст**: Використовується для розуміння розмірів, відстаней і макетів елементів у CSS.
- **Основні компоненти**:
  - **Content**: Вміст (текст, зображення).
  - **Padding**: Внутрішній відступ між контентом і border.
  - **Border**: Рамка навколо padding.
  - **Margin**: Зовнішній відступ поза border.
  - **Box-sizing**: Визначає, що включають `width` і `height` (`content-box` або `border-box`).
- **Особливості**:
  - Кожен елемент (block або inline) має box-модель.
  - Розміри залежать від `box-sizing` і margin collapsing.
  - Важлива для створення адаптивних макетів.

## Приклади коду

### 1. Повна box-модель

Усі компоненти.

```css
div {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  margin: 30px;
  box-sizing: content-box;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Загальна ширина = 200px + 40px (padding) + 10px (border) + 60px (margin) = 310px.

### 2. Box-model із `border-box`

Контроль розмірів.

```css
div {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid blue;
  margin: 10px;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Ширина = 200px (включає padding і border), плюс 20px margin.

### 3. Margin collapsing

Злиття margin.

```css
.div1 {
  margin-bottom: 20px;
}
.div2 {
  margin-top: 30px;
}
```

#### HTML:

```html
<div class="div1">Блок 1</div>
<div class="div2">Блок 2</div>
```

#### Результат:

Відстань між блоками = 30px.

### 4. Inline елемент

Box-модель для inline.

```css
span {
  padding: 5px;
  border: 1px solid red;
  margin: 10px;
}
```

#### HTML:

```html
<span>Текст</span>
```

#### Результат:

Padding і border застосовуються, але margin не впливає вертикально.

## Особливості для співбесід — Питання та відповіді

### Що таке CSS box-модель?

- **Відповідь**: Модель, яка описує елемент як прямокутник із контентом, padding, border і margin.
  ```css
  div {
    padding: 10px;
    border: 1px solid;
  }
  ```

### Як `box-sizing` впливає на box-модель?

- **Відповідь**: `content-box` враховує лише контент, `border-box` включає padding і border.
  ```css
  box-sizing: border-box;
  ```

### Що таке margin collapsing?

- **Відповідь**: Злиття вертикальних margin сусідніх block-елементів у більше значення.
  ```css
  div {
    margin: 20px 0;
  } /* Зливається */
  ```

### Як box-модель працює з inline-елементами?

- **Відповідь**: Padding і border застосовуються, але вертикальний margin ігнорується.
  ```css
  span {
    padding: 5px;
    margin: 10px;
  }
  ```

## Поради

- **Box-sizing**: Використовуйте `border-box` для передбачуваних макетів.
- **Тестування**: Перевіряйте розміри в DevTools (Box Model вкладка).
- **Адаптивність**: Використовуйте `rem`, `%` для padding і margin.
- **Розуміння**: Враховуйте margin collapsing у block-елементах.
- **Документація**: Звертайтеся до web.dev або MDN.

## Додаткові деталі

- **Компоненти**:
  - Content: Задується через `width`/`height`.
  - Padding: Внутрішній простір.
  - Border: Зовнішня рамка.
  - Margin: Зовнішній простір.
- **Сумісність**: Box-модель стандартна у всіх браузерах.
- **Обмеження**: Inline-елементи мають обмеження з margin.
- **Альтернативи**: Flexbox і Grid для складних макетів.
