# Детальний конспект: Shadow DOM

## Загальна інформація

- **Опис**: Shadow DOM — це частина Web Components, яка ізолює DOM і CSS компонента від решти сторінки, забезпечуючи інкапсуляцію стилів і структури.
- **Контекст**: Використовується для створення кастомних компонентів (наприклад, `<custom-button>`), які не впливають на глобальні стилі та не залежать від них.
- **Основні компоненти**:
  - **Shadow DOM**:
    - **Shadow Root**: Кореневий вузол, створений через `element.attachShadow({ mode: 'open' })`.
    - **Mode**: `open` (доступний через JS) або `closed` (ізольований).
  - **Пов’язані технології**:
    - Custom Elements: Кастомні HTML-теги.
    - HTML Templates: `<template>` для повторного використання.
  - **Особливості**:
    - Стили в Shadow DOM не просочуються назовні й не впливають на глобальні.
    - Події (click) проходять через межу, але фокус і стилі ізольовані.
    - Доступність потребує ARIA та семантики.
  - **Синтаксис**:
    ```javascript
    const shadow = element.attachShadow({ mode: "open" });
    shadow.innerHTML = "<p>Shadow Content</p>";
    ```

## Приклади коду

### 1. Простий Shadow DOM компонент

Кастомна кнопка.

```html
<custom-button>Клікни</custom-button>
```

#### JavaScript:

```javascript
class CustomButton extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `
      <style>
        button { background: #007bff; color: white; border: none; padding: 8px; }
      </style>
      <button><slot></slot></button>
    `;
  }
}
customElements.define("custom-button", CustomButton);
```

#### Результат:

Кнопка із ізольованими стилями, текст із `<slot>`.

### 2. Використання `<template>`

Повторюваний компонент.

```html
<template id="my-component">
  <style>
    p {
      color: blue;
    }
  </style>
  <p>Shadow Content</p>
</template>
<my-component></my-component>
```

#### JavaScript:

```javascript
class MyComponent extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    const template = document.querySelector("#my-component");
    shadow.appendChild(template.content.cloneNode(true));
  }
}
customElements.define("my-component", MyComponent);
```

#### Результат:

Ізольований параграф із синіми стилями.

### 3. Події в Shadow DOM

Обробка кліків.

```html
<custom-input></custom-input>
```

#### JavaScript:

```javascript
class CustomInput extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `
      <input type="text">
    `;
    shadow.querySelector("input").addEventListener("input", (e) => {
      this.dispatchEvent(new CustomEvent("change", { detail: e.target.value }));
    });
  }
}
customElements.define("custom-input", CustomInput);
```

#### Результат:

Компонент надсилає подію `change` назовні.

### 4. Стилізація через CSS-перемінні

Зовнішній вплив.

```html
<custom-box></custom-box>
```

#### JavaScript:

```javascript
class CustomBox extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `
      <style>
        div { background: var(--box-bg, #f0f0f0); }
      </style>
      <div>Box</div>
    `;
  }
}
customElements.define("custom-box", CustomBox);
```

#### CSS:

```css
custom-box {
  --box-bg: #007bff;
}
```

#### Результат:

Фон блоку задається через змінну.

## Особливості для співбесід — Питання та відповіді

### Що таке Shadow DOM?

- **Відповідь**: Ізольований DOM для Web Components, який забезпечує інкапсуляцію стилів і структури.
  ```javascript
  element.attachShadow({ mode: "open" });
  ```

### Чим відрізняються `open` і `closed` режими?

- **Відповідь**: `open` дозволяє доступ через JS (`element.shadowRoot`), `closed` блокує.
  ```javascript
  {
    mode: "closed";
  }
  ```

### Як стилі із Shadow DOM взаємодіють із глобальними?

- **Відповідь**: Ізольовані, але CSS-перемінні та `::part` дозволяють зовнішній вплив.
  ```css
  :host {
    --color: blue;
  }
  ```

### Як забезпечити доступність у Shadow DOM?

- **Відповідь**: Використовуйте семантику, ARIA, тестуйте зі скрінрідерами.
  ```html
  <button aria-label="Дія"></button>
  ```

## Поради

- **Інкапсуляція**: Використовуйте Shadow DOM для ізоляції стилів.
- **Доступність**: Додавайте ARIA та семантичні теги.
- **Тестування**: Перевіряйте в Chrome, Firefox, Safari (Safari має особливості).
- **Продуктивність**: Уникайте складних DOM-дерев у Shadow Root.
- **Документація**: Звертайтеся до MDN для Web Components.

## Додаткові деталі

- **API**:
  - `attachShadow()`: Створює Shadow Root.
  - `<slot>`: Вставляє вміст із Light DOM.
  - `::part`: Дозволяє стилізувати ззовні.
- **Сумісність**: Chrome 53+, Firefox 63+, Safari 10+, Edge 79+.
- **Обмеження**: Складна стилізація фокусу, Safari має слабшу підтримку.
- **Альтернативи**: CSS-модулі, фреймворки (React, Vue).
