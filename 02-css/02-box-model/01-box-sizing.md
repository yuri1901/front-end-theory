# Детальний конспект: CSS властивість box-sizing

## Загальна інформація

- **Опис**: Властивість `box-sizing` визначає, як обчислюються розміри елемента (ширина і висота), включаючи контент, padding і border.
- **Контекст**: Використовується для контролю поведінки box-моделі, щоб спростити розрахунки макетів.
- **Основні компоненти**:
  - **Значення**:
    - `content-box`: Ширина/висота включають лише контент (за замовчуванням).
    - `border-box`: Ширина/висота включають контент, padding і border.
    - `inherit`: Успадковує значення від батьківського елемента.
  - **Синтаксис**: `box-sizing: content-box | border-box | inherit;`
- **Особливості**:
  - `border-box` полегшує створення макетів, включаючи padding і border у задану ширину.
  - Зазвичай застосовується глобально через `* { box-sizing: border-box; }`.
  - Впливає на `width`, `height`, `min-width`, `max-width`.

## Приклади коду

### 1. Використання `content-box`

Стандартна поведінка.

```css
div {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Загальна ширина = 200px (контент) + 40px (padding) + 10px (border) = 250px.

### 2. Використання `border-box`

Включення padding і border.

```css
div {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
```

#### HTML:

```html
<div>Контент</div>
```

#### Результат:

Загальна ширина = 200px (включає контент, padding, border).

### 3. Глобальне застосування `border-box`

Універсальний селектор.

```css
* {
  box-sizing: border-box;
}
div {
  width: 100px;
  padding: 10px;
  border: 2px solid blue;
}
```

#### HTML:

```html
<div>Текст</div>
```

#### Результат:

Усі елементи мають `border-box`, ширина div = 100px.

### 4. Порівняння поведінки

Два div із різними `box-sizing`.

```css
.content-box {
  box-sizing: content-box;
  width: 100px;
  padding: 10px;
}
.border-box {
  box-sizing: border-box;
  width: 100px;
  padding: 10px;
}
```

#### HTML:

```html
<div class="content-box">Content</div>
<div class="border-box">Border</div>
```

#### Результат:

`.content-box` ширина = 120px, `.border-box` ширина = 100px.

## Особливості для співбесід — Питання та відповіді

### Що таке `box-sizing`?

- **Відповідь**: Властивість, яка визначає, чи включають `width` і `height` padding і border.
  ```css
  box-sizing: border-box;
  ```

### У чому різниця між `content-box` і `border-box`?

- **Відповідь**: `content-box` враховує лише контент, `border-box` включає padding і border.
  ```css
  div {
    box-sizing: border-box;
    width: 100px;
    padding: 10px;
  } /* 100px загалом */
  ```

### Чому `border-box` популярний?

- **Відповідь**: Спрощує розрахунки, оскільки ширина включає padding і border.
  ```css
  * {
    box-sizing: border-box;
  }
  ```

### Як глобально застосувати `box-sizing`?

- **Відповідь**: Використовуйте універсальний селектор `*`.
  ```css
  * {
    box-sizing: border-box;
  }
  ```

## Поради

- **Глобальне використання**: Застосовуйте `* { box-sizing: border-box; }` для передбачуваних макетів.
- **Тестування**: Перевіряйте розміри елементів у DevTools (Computed вкладка).
- **Сумісність**: `box-sizing` підтримується всюди, але уточнюйте для старих браузерів.
- **Комбінація**: Використовуйте з Flexbox/Grid для точних макетів.
- **Документація**: Звертайтеся до MDN для деталей.

## Додаткові деталі

- **Значення**:
  - `content-box`: Стандарт HTML, але ускладнює розрахунки.
  - `border-box`: Інтуїтивний для макетів.
- **Сумісність**: Повна підтримка у всіх браузерах (IE8+).
- **Обмеження**: Не впливає на `margin`, який додається до загальних розмірів.
- **Альтернативи**: Без `border-box` потрібно вручну розраховувати padding і border.
