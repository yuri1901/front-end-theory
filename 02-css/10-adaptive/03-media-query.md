# Детальний конспект: CSS медіа-запити

## Загальна інформація

- **Опис**: Медіа-запити (`@media`) — це CSS-техніка для застосування стилів залежно від характеристик пристрою, таких як ширина екрана, орієнтація чи роздільна здатність.
- **Контекст**: Ключовий інструмент для респонсивного дизайну, дозволяє адаптувати макети до десктопів, планшетів, смартфонів. Визначені в CSS3, широко підтримуються.
- **Основні компоненти**:
  - **Синтаксис**:
    ```css
    @media (media-type) and (media-feature) {
      /* Стилі */
    }
    ```
  - **Media Types**: `all` (за замовчуванням), `screen`, `print`.
  - **Media Features**:
    - `width`, `min-width`, `max-width`: Ширина вьюпорту.
    - `height`, `min-height`, `max-height`: Висота.
    - `orientation`: `portrait` або `landscape`.
    - `resolution`: Роздільна здатність (наприклад, `300dpi`).
    - `aspect-ratio`: Співвідношення сторін.
    - `prefers-color-scheme`: Темна/світла тема (`dark`, `light`).
    - `hover`: Підтримка наведення.
  - **Логічні оператори**:
    - `and`, `or` (через кому), `not`.
  - **Брейкпоїнти**:
    - Мобільні: ~320–600px.
    - Планшети: ~600–1024px.
    - Десктопи: ~1024px+.
- **Особливості**:
  - Mobile-first (`min-width`) або desktop-first (`max-width`).
  - Підтримують складні умови (наприклад, `(min-width: 600px) and (max-width: 1024px)`).
  - Можуть застосовуватися до `<link>` або `@import`.

## Приклади коду

### 1. Mobile-first із `min-width`

Прогресивна адаптація.

```css
body {
  font-size: 14px;
}
@media (min-width: 600px) {
  body {
    font-size: 16px;
  }
}
@media (min-width: 1024px) {
  body {
    font-size: 18px;
  }
}
```

#### Результат:

Шрифт зростає з розміром екрана.

### 2. Desktop-first із `max-width`

Зворотна адаптація.

```css
.container {
  width: 1200px;
}
@media (max-width: 1024px) {
  .container {
    width: 768px;
  }
}
@media (max-width: 600px) {
  .container {
    width: 100%;
  }
}
```

#### Результат:

Контейнер звужується на менших екранах.

### 3. Орієнтація та тема

Комбіновані умови.

```css
.element {
  background: white;
}
@media (orientation: landscape) and (prefers-color-scheme: dark) {
  .element {
    background: #333;
  }
}
```

#### Результат:

Темний фон у горизонтальній орієнтації та темній темі.

### 4. Стандартні брейкпоїнти

Типові пристрої.

```css
/* Смартфони */
@media (max-width: 480px) {
  .nav {
    flex-direction: column;
  }
}
/* Планшети */
@media (min-width: 481px) and (max-width: 768px) {
  .nav {
    font-size: 16px;
  }
}
/* Десктопи */
@media (min-width: 1025px) {
  .nav {
    font-size: 18px;
  }
}
```

#### Результат:

Навігація адаптується до пристроїв.

## Особливості для співбесід — Питання та відповіді

### Що таке медіа-запити?

- **Відповідь**: CSS-правила для адаптації стилів під характеристики пристрою.
  ```css
  @media (max-width: 600px) {
  }
  ```

### У чому різниця між `min-width` і `max-width`?

- **Відповідь**: `min-width` застосовує стилі для екранів ширших за значення, `max-width` — для вужчих.
  ```css
  @media (min-width: 600px) {
  }
  ```

### Що таке mobile-first підхід?

- **Відповідь**: Базові стилі для мобільних, медіа-запити для більших екранів (`min-width`).
  ```css
  @media (min-width: 600px) {
  }
  ```

### Які медіа-фічі ви знаєте?

- **Відповідь**: `width`, `orientation`, `resolution`, `prefers-color-scheme`, `hover`.
  ```css
  @media (prefers-color-scheme: dark) {
  }
  ```

## Поради

- **Mobile-first**: Використовуйте `min-width` для простоти.
- **Брейкпоїнти**: Обирайте на основі контенту, а не пристроїв.
- **Тестування**: Використовуйте Chrome DevTools, BrowserStack.
- **Оптимізація**: Об’єднуйте медіа-запити для зменшення CSS.
- **Документація**: Звертайтеся до MDN, CSS-Tricks, W3Schools.

## Додаткові деталі

- **Фічі**:
  - `prefers-reduced-motion`: Для зменшення анімацій.
  - `color-gamut`: Для HDR-дисплеїв.
- **Сумісність**: Повна підтримка в Chrome, Firefox, Safari, Edge.
- **Обмеження**: Надмір медіа-запитів ускладнює підтримку.
- **Альтернативи**: CSS Grid, Flexbox, container queries.
