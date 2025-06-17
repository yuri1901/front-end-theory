# Шпаргалка: API для роботи з геометрією у браузері (JavaScript)


## 1. Прямокутники та квадрати

| API | Що повертає / робить | Підтримка |
|-----|----------------------|-----------|
| [`element.getBoundingClientRect()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect) | `DOMRect` з координатами відносно вʼюпорту | усі сучасні |
| [`element.getClientRects()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getClientRects) | `DOMRectList` для multi‑column / inline‑box | усі сучасні |
| [`element.getBoxQuads()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoxQuads) | `DOMQuad` для content / padding / border box | Chrome 125+, Firefox 124+ |
| [`DOMRect`](https://developer.mozilla.org/en-US/docs/Web/API/DOMRect) / [`DOMRectReadOnly`](https://developer.mozilla.org/en-US/docs/Web/API/DOMRectReadOnly) | Створення та зберігання прямокутників «у памʼяті» | усі сучасні |

## 2. Відступи й розміри елемента

| Властивість | Опис |
|-------------|------|
| [`offsetWidth`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetWidth) / [`offsetHeight`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetHeight) | **border‑box** – ширина/висота з рамкою |
| [`offsetTop`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetTop) / [`offsetLeft`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetLeft) | позиція елемента в потоці (relative до offsetParent) |
| [`clientWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientWidth) / [`clientHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientHeight) | **padding‑box** без скрол-барів |
| [`clientTop`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientTop) / [`clientLeft`](https://developer.mozilla.org/en-US/docs/Web/API/Element/clientLeft) | товщина рамки |
| [`scrollWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollWidth) / [`scrollHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollHeight) | повний контент усередині елемента |
| [`scrollTop`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollTop) / [`scrollLeft`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollLeft) | поточний зсув прокрутки |

## 3. Вʼюпорт і екран

| API | Опис |
|-----|------|
| [`window.innerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerWidth) / [`innerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/innerHeight) | розмір видимої частини сторінки |
| [`window.outerWidth`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerWidth) / [`outerHeight`](https://developer.mozilla.org/en-US/docs/Web/API/Window/outerHeight) | розмір вікна браузера разом із рамкою |
| [`window.visualViewport`](https://developer.mozilla.org/en-US/docs/Web/API/VisualViewport) (`width`, `height`, `scale`) | реальна зона відображення з урахуванням мобільного зуму |
| [`screen.width`](https://developer.mozilla.org/en-US/docs/Web/API/Screen/width) / [`screen.height`](https://developer.mozilla.org/en-US/docs/Web/API/Screen/height) | фізичний монітор / дисплей |

## 4. Обсервери (реактивні API)

| API | Для чого |
|-----|----------|
| [`ResizeObserver`](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver) | реагує на зміну розміру елемента / вʼюпорту |
| [`IntersectionObserver`](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver) | відстежує перетин елемента з вʼюпортом чи ін. елементом |

## 5. Матриці, точки, SVG та Canvas

| API | Сфера застосування |
|-----|--------------------|
| [`DOMMatrix`](https://developer.mozilla.org/en-US/docs/Web/API/DOMMatrix) / [`DOMMatrixReadOnly`](https://developer.mozilla.org/en-US/docs/Web/API/DOMMatrixReadOnly) | 2D/3D‑трансформації (translate / rotate / scale) |
| [`DOMPoint`](https://developer.mozilla.org/en-US/docs/Web/API/DOMPoint) / [`DOMPointReadOnly`](https://developer.mozilla.org/en-US/docs/Web/API/DOMPointReadOnly) | 2D/3D‑координати точок |
| [`Path2D`](https://developer.mozilla.org/en-US/docs/Web/API/Path2D) | складні контури в `<canvas>` |
| [`CanvasRenderingContext2D.measureText()`](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/measureText) | вимір тексту в `<canvas>` |
| [`SVGGeometryElement.getBBox()`](https://developer.mozilla.org/en-US/docs/Web/API/SVGGraphicsElement/getBBox) | реальний bounding‑box SVG‑елемента |
| [`SVGGeometryElement.getTotalLength()`](https://developer.mozilla.org/en-US/docs/Web/API/SVGGeometryElement/getTotalLength) / [`getPointAtLength()`](https://developer.mozilla.org/en-US/docs/Web/API/SVGGeometryElement/getPointAtLength) | довжина та точки контуру для path / line / polyline |

## 6. CSS Typed OM

| API | Можливості |
|-----|------------|
| [`element.attributeStyleMap`](https://developer.mozilla.org/en-US/docs/Web/API/Element/attributeStyleMap) <br>→ `CSSUnitValue` тощо | читання / запис CSS‑властивостей як обʼєктів (без парсингу рядків) |

## 7. Інші корисні дрібниці

| API | Опис |
|-----|------|
| [`pageXOffset`](https://developer.mozilla.org/en-US/docs/Web/API/Window/pageXOffset) / [`pageYOffset`](https://developer.mozilla.org/en-US/docs/Web/API/Window/pageYOffset) | глобальний скрол документа |
| [`matchMedia()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/matchMedia) | програмні media‑queries у JS |
| [`element.scrollIntoView()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/scrollIntoView) | плавне позиціювання елемента у вʼюпорті |

---

## 8. Швидкі рецепти (приклади коду)

```js
// Центруємо модальне вікно у вʼюпорті
const { width, height } = document.documentElement.getBoundingClientRect();
popup.style.left = `${(width - popup.offsetWidth) / 2}px`;
popup.style.top  = `${(height - popup.offsetHeight) / 2}px`;

// Показуємо картку, коли вона видима на ≥50 %
const io = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) e.target.classList.add('visible');
  });
}, { threshold: 0.5 });

document.querySelectorAll('.card').forEach(card => io.observe(card));

// Логін розміру <aside> у консолі при ресайзі
const ro = new ResizeObserver(([entry]) => {
  console.log('New width:', entry.contentRect.width);
});

ro.observe(document.querySelector('aside'));
```

---

### TL;DR

- **Разове вимірювання:** `getBoundingClientRect`, `getBoxQuads`, `offset*`, `client*`  
- **Реактивність:** `ResizeObserver`, `IntersectionObserver`  
- **Серйозна математика:** `DOMMatrix`, `DOMPoint`, SVG‑методи  
- **Мобільний зум:** `window.visualViewport`  

</br>
