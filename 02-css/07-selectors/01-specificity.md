# Детальний конспект: CSS специфічність

## Загальна інформація

- **Опис**: Специфічність у CSS визначає, який стильовий правило застосовується до елемента, коли кілька правил конфліктують. Вона базується на вазі селекторів.
- **Контекст**: Використовується для вирішення конфліктів між стилями, особливо в великих проєктах із множинними CSS-правилами.
- **Основні компоненти**:
  - **Розрахунок специфічності**:
    - **ID-селектори**: (1,0,0).
    - **Класи, атрибути, псевдокласи**: (0,1,0).
    - **Елементи, псевдоелементи**: (0,0,1).
    - **Універсальний селектор (`*`)**: (0,0,0).
  - **Правила**:
    - Вища специфічність перекриває нижчу.
    - При однаковій специфічності застосовується останнє правило в коді.
    - `!important` ігнорує специфічність (вага: максимальна).
  - **Синтаксис**: Звичайні CSS-правила, специфічність обчислюється автоматично.
- **Особливості**:
  - Інлайн-стилі (`style="..."`) мають найвищу специфічність (1,0,0,0).
  - Специфічність не залежить від вкладеності, лише від типу селекторів.
  - Комбінатори (наприклад, `>`, `+`) не додають специфічності.

## Приклади коду

### 1. Конфлікт між селекторами

Порівняння специфічності.

```css
#container p {
  /* (1,0,1) */
  color: blue;
}
.text {
  /* (0,1,0) */
  color: red;
}
```

#### HTML:

```html
<div id="container">
  <p class="text">Текст</p>
</div>
```

#### Результат:

Текст синій, оскільки `#container p` має вищу специфічність.

### 2. Однакова специфічність

Порядок у коді.

```css
p.text {
  /* (0,1,1) */
  color: green;
}
p.text {
  /* (0,1,1) */
  color: orange;
}
```

#### HTML:

```html
<p class="text">Текст</p>
```

#### Результат:

Текст помаранчевий, оскільки друге правило останнє.

### 3. Використання `!important`

Ігнорування специфічності.

```css
#container p {
  /* (1,0,1) */
  color: blue;
}
.text {
  /* (0,1,0) */
  color: red !important;
}
```

#### HTML:

```html
<div id="container">
  <p class="text">Текст</p>
</div>
```

#### Результат:

Текст червоний через `!important`.

### 4. Інлайн-стилі

Найвища специфічність.

```css
p {
  /* (0,0,1) */
  color: green;
}
```

#### HTML:

```html
<p style="color: purple;">Текст</p>
```

#### Результат:

Текст пурпуровий, оскільки інлайн-стилі мають вагу (1,0,0,0).

## Особливості для співбесід — Питання та відповіді

### Що таке специфічність у CSS?

- **Відповідь**: Механізм, який визначає, яке правило застосовується при конфлікті.
  ```css
  #id {
    color: blue;
  } /* (1,0,0) */
  ```

### Як обчислюється специфічність?

- **Відповідь**: За вагою селекторів: ID (1,0,0), класи/псевдокласи (0,1,0), елементи (0,0,1).
  ```css
  div.class { /* (0,1,1) */
  ```

### Що перекриває специфічність?

- **Відповідь**: `!important` або інлайн-стилі.
  ```css
  color: red !important;
  ```

### Чи впливає порядок селекторів на специфічність?

- **Відповідь**: Ні, лише тип селекторів; порядок у коді вирішує при рівній специфічності.
  ```css
  .class {
    color: red;
  } /* Останнє */
  ```

## Поради

- **Мінімізація**: Уникайте надмірної специфічності (наприклад, `#id #id`).
- **Організація**: Використовуйте класи замість ID для гнучкості.
- **Важливість**: Рідко використовуйте `!important`, лише для крайніх випадків.
- **Тестування**: Аналізуйте конфлікти в DevTools (Styles вкладка).
- **Документація**: Звертайтеся до MDN для деталей.

## Додаткові деталі

- **Правила**:
  - Інлайн-стилі: (1,0,0,0).
  - `!important`: Перекриває все, крім іншого `!important` із вищою специфічністю.
  - `:not()` не додає специфічності, але його аргумент враховується.
- **Сумісність**: Специфічність стандартна у всіх браузерах.
- **Обмеження**: Складні селектори можуть ускладнити дебагінг.
- **Альтернативи**: CSS-модулі або BEM для уникнення конфліктів.
