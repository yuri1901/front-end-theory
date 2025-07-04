# Детальний конспект: CSS псевдокласи

## Загальна інформація

- **Опис**: Псевдокласи в CSS дозволяють стилізувати елементи на основі їхнього стану, позиції в дереві документа або взаємодії з користувачем без додавання класів у HTML.
- **Контекст**: Використовуються для створення інтерактивних ефектів (наприклад, наведення), стилізації певних елементів у списку чи формах.
- **Основні компоненти**:
  - **Синтаксис**: `selector:pseudo-class { property: value; }`
  - **Категорії**:
    - **Динамічні**: `:hover`, `:active`, `:focus`.
    - **Структурні**: `:first-child`, `:nth-child`, `:last-child`.
    - **Формові**: `:checked`, `:disabled`, `:required`.
    - **Інші**: `:not`, `:where`, `:is`.
  - **Специфічність**: Така ж, як у класу (0,1,0).
- **Особливості**:
  - Залежить від стану або структури документа.
  - Комбінується з іншими селекторами для точності.
  - Не потребує JavaScript для базової інтерактивності.

## Приклади коду

### 1. Використання `:hover`

Інтерактивність при наведенні.

```css
button:hover {
  background-color: #0056b3;
  color: white;
}
```

#### HTML:

```html
<button>Наведи</button>
```

#### Результат:

Кнопка змінює колір при наведенні курсору.

### 2. Використання `:nth-child`

Стилізація парних елементів.

```css
li:nth-child(even) {
  background-color: #f0f0f0;
}
```

#### HTML:

```html
<ul>
  <li>Пункт 1</li>
  <li>Пункт 2</li>
  <li>Пункт 3</li>
  <li>Пункт 4</li>
</ul>
```

#### Результат:

Парні пункти мають сірий фон.

### 3. Використання `:focus`

Стилізація активного поля.

```css
input:focus {
  border: 2px solid blue;
  outline: none;
}
```

#### HTML:

```html
<input type="text" placeholder="Введіть текст" />
```

#### Результат:

Поле з синьою рамкою при фокусі.

### 4. Використання `:not`

Виключення елемента.

```css
p:not(.special) {
  color: gray;
}
```

#### HTML:

```html
<p>Сірий текст</p>
<p class="special">Чорний текст</p>
```

#### Результат:

Усі абзаци, окрім `.special`, сірі.

## Особливості для співбесід — Питання та відповіді

### Що таке псевдокласи?

- **Відповідь**: Селектори, які стилізують елементи за їхнім станом або позицією.
  ```css
  a:hover {
    color: red;
  }
  ```

### Яка специфічність псевдокласів?

- **Відповідь**: (0,1,0), як у класу.
  ```css
  :hover {
    color: blue;
  }
  .class {
    color: red;
  } /* Останній перекриває */
  ```

### Як працює `:nth-child`?

- **Відповідь**: Вибирає елемент за порядковим номером серед дочірніх.
  ```css
  li:nth-child(2n) {
    background: gray;
  } /* Парні */
  ```

### Для чого потрібен `:not`?

- **Відповідь**: Виключає елементи, що відповідають селектору.
  ```css
  p:not(.exclude) {
    margin: 10px;
  }
  ```

## Поради

- **Інтерактивність**: Використовуйте `:hover`, `:focus` для UX.
- **Точність**: Комбінуйте з класами чи ID для уникнення конфліктів.
- **Тестування**: Перевіряйте в DevTools (Styles вкладка).
- **Сумісність**: Уникайте складних псевдокласів (`:where`) у старих браузерах.
- **Документація**: Звертайтеся до MDN для повного списку.

## Додаткові деталі

- **Популярні псевдокласи**:
  - `:hover`, `:active`, `:focus`: Для взаємодії.
  - `:first-child`, `:last-child`, `:nth-child(n)`: Для структури.
  - `:checked`, `:disabled`: Для форм.
  - `:not`, `:is`, `:where`: Для логіки.
- **Сумісність**: Основні псевдокласи підтримуються всюди; `:where`, `:is` — сучасні браузери.
- **Обмеження**: Не всі псевдокласи працюють із псевдоелементами.
- **Альтернативи**: JavaScript для складних станів.
