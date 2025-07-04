# Детальний конспект: Респонсивний веб-дизайн

## Загальна інформація

- **Опис**: Респонсивний веб-дизайн (RWD, Responsive Web Design) — це підхід до веб-розробки, який забезпечує оптимальне відображення сайту на різних пристроях (десктоп, планшет, смартфон) за допомогою гнучких макетів, зображень і CSS медіа-запитів.
- **Контекст**: Запропонований Ітаном Маркоттом у 2010 році (A List Apart). Зростання мобільного трафіку (понад 60% у 2024 році, за Exploding Topics) робить RWD критичним для UX і SEO.
- **Основні компоненти**:
  - **Гнучкі макети**: Використання відносних одиниць (`%`, `vw`, `vh`, `rem`, `em`) замість фіксованих (`px`).
  - **Адаптивні зображення**: Використання `max-width: 100%`, `<picture>`, `srcset` для оптимізації.
  - **Медіа-запити**: CSS `@media` для адаптації стилів під розміри екрана.
  - **Технології**:
    - CSS: Flexbox, Grid, `@media`.
    - HTML: `<meta name="viewport">`.
    - JavaScript: Для динамічних змін (рідко).
  - **Синтаксис**:
    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    ```
    ```css
    @media (max-width: 600px) {
      body {
        font-size: 16px;
      }
    }
    ```
- **Особливості**:
  - Єдиний код для всіх пристроїв, що спрощує підтримку.
  - Покращує SEO, оскільки Google віддає перевагу mobile-friendly сайтам.
  - Залежить від медіа-запитів для адаптації контенту.

## Приклади коду

### 1. Гнучкий макет із Flexbox

Адаптивна навігація.

```html
<nav class="nav">
  <a href="#">Головна</a>
  <a href="#">Про нас</a>
  <a href="#">Контакти</a>
</nav>
```

#### CSS:

```css
.nav {
  display: flex;
  justify-content: space-around;
}
@media (max-width: 600px) {
  .nav {
    flex-direction: column;
    align-items: center;
  }
}
```

#### Результат:

На десктопі — горизонтальна навігація, на мобільних — вертикальна.

### 2. Адаптивне зображення

Оптимізація зображень.

```html
<picture>
  <source media="(max-width: 600px)" srcset="small.jpg" />
  <img src="large.jpg" alt="Зображення" style="max-width: 100%;" />
</picture>
```

#### Результат:

Менше зображення для мобільних, більше для десктопів.

### 3. Адаптивна типографіка

Зміна розміру шрифту.

```css
body {
  font-size: 1rem;
}
@media (min-width: 768px) {
  body {
    font-size: 1.2rem;
  }
}
```

#### Результат:

Шрифт більший на великих екранах.

### 4. Мобільний viewport

Правильне масштабування.

```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

#### CSS:

```css
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}
```

#### Результат:

Сайт адаптується до ширини екрана.

## Особливості для співбесід — Питання та відповіді

### Що таке респонсивний веб-дизайн?

- **Відповідь**: Підхід до створення сайтів, які адаптуються до різних пристроїв за допомогою гнучких макетів, зображень і медіа-запитів.
  ```css
  @media (max-width: 600px) {
  }
  ```

### Чому RWD важливий?

- **Відповідь**: Понад 60% трафіку з мобільних (2024), покращує UX і SEO.
  ```html
  <meta name="viewport" />
  ```

### Які основні принципи RWD?

- **Відповідь**: Гнучкі макети (`%`, `rem`), адаптивні зображення (`srcset`), медіа-запити.
  ```css
  img {
    max-width: 100%;
  }
  ```

### Що робить `<meta name="viewport">`?

- **Відповідь**: Забезпечує коректне масштабування на мобільних.
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  ```

## Поради

- **Viewport**: Завжди додавайте `<meta name="viewport">`.
- **Одиниці**: Використовуйте `rem`, `em`, `%` для гнучкості.
- **Медіа-запити**: Починайте з mobile-first (`min-width`).
- **Тестування**: Перевіряйте в Chrome DevTools, BrowserStack, реальних пристроях.
- **Оптимізація**: Використовуйте `srcset` і стиснуті зображення.
- **Документація**: Звертайтеся до A List Apart і CSS-Tricks.

## Додаткові деталі

- **Технології**:
  - Flexbox і Grid для гнучких макетів.
  - `<picture>`, `srcset` для зображень.
- **Сумісність**: Повна підтримка в сучасних браузерах.
- **Обмеження**: Складні макети потребують більше медіа-запитів.
- **Альтернативи**: Адаптивний дизайн (окремі макети), серверна адаптація.
