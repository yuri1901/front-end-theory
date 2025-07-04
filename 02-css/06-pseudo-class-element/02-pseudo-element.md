# Детальний конспект: CSS псевдоелементи

## Загальна інформація

- **Опис**: Псевдоелементи в CSS дозволяють стилізувати певні частини елемента або створювати віртуальні елементи без додавання HTML, наприклад, перший рядок тексту чи декоративні маркери.
- **Контекст**: Використовуються для декоративних ефектів, стилізації контенту або додавання елементів (наприклад, стрілки, іконки).
- **Основні компоненти**:
  - **Синтаксис**: `selector::pseudo-element { property: value; }`
  - **Основні псевдоелементи**:
    - `::before`: Додає вміст перед елементом.
    - `::after`: Додає вміст після елемента.
    - `::first-line`: Стилізує перший рядок тексту.
    - `::first-letter`: Стилізує першу літеру.
    - `::selection`: Стилізує виділений текст.
  - **Специфічність**: Така ж, як у класу (0,1,0).
- **Особливості**:
  - Псевдоелементи генерують віртуальні коробки.
  - `::before` і `::after` потребують `content` (навіть порожній `""`).
  - Обмежена підтримка складних псевдоелементів у старих браузерах.

## Приклади коду

### 1. Використання `::before`

Додавання іконки.

```css
li::before {
  content: "★ ";
  color: gold;
}
```

#### HTML:

```html
<ul>
  <li>Пункт 1</li>
  <li>Пункт 2</li>
</ul>
```

#### Результат:

Зірочка перед кожним пунктом.

### 2. Використання `::after`

Декоративний елемент.

```css
.button::after {
  content: " →";
  margin-left: 5px;
}
```

#### HTML:

```html
<button class="button">Клікни</button>
```

#### Результат:

Стрілка після тексту кнопки.

### 3. Використання `::first-line`

Стилізація першого рядка.

```css
p::first-line {
  font-weight: bold;
  color: navy;
}
```

#### HTML:

```html
<p>Це перший рядок.<br />Це другий рядок.</p>
```

#### Результат:

Перший рядок жирний і синій.

### 4. Використання `::selection`

Стилізація виділення.

```css
::selection {
  background-color: yellow;
  color: black;
}
```

#### HTML:

```html
<p>Виділи цей текст.</p>
```

#### Результат:

Виділений текст із жовтим фоном.

## Особливості для співбесід — Питання та відповіді

### Що таке псевдоелементи?

- **Відповідь**: Селектори, які стилізують частини елемента або додають віртуальний вміст.
  ```css
  p::before {
    content: "• ";
  }
  ```

### Чим псевдоелементи відрізняються від псевдокласів?

- **Відповідь**: Псевдоелементи стилізують частини або додають вміст, псевдокласи — стани.
  ```css
  p:hover {
    color: red;
  } /* Псевдоклас */
  p::first-letter {
    font-size: 2em;
  } /* Псевдоелемент */
  ```

### Що обов’язкове для `::before` і `::after`?

- **Відповідь**: Властивість `content`, навіть якщо порожня.
  ```css
  div::after {
    content: "";
  }
  ```

### Чи можна стилізувати `::selection` у всіх браузерах?

- **Відповідь**: Так, але обмежено (`background`, `color`); деякі браузери мають префікси.
  ```css
  ::selection {
    background: blue;
  }
  ```

## Поради

- **Декорація**: Використовуйте `::before`, `::after` для іконок чи маркерів.
- **Тестування**: Перевіряйте в DevTools, як генерується вміст.
- **Сумісність**: Використовуйте `::` (сучасний синтаксис) замість `:` (старий).
- **Оптимізація**: Уникайте складних псевдоелементів для продуктивності.
- **Документація**: Звертайтеся до MDN для повного списку.

## Додаткові деталі

- **Популярні псевдоелементи**:
  - `::before`, `::after`: Для віртуального вмісту.
  - `::first-line`, `::first-letter`: Для тексту.
  - `::selection`: Для UX при виділенні.
- **Сумісність**: Повна підтримка основних псевдоелементів; `::marker` — сучасні браузери.
- **Обмеження**: Не всі псевдоелементи працюють із усіма тегами (наприклад, `::first-line` не для `img`).
- **Альтернативи**: SVG або HTML для складних декоративних елементів.
