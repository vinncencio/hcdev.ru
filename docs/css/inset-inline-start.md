---
description: Свойство CSS inset-inline-start определяет логическую встроенную начальную вставку элемента, которая сопоставляется с физическим смещением в зависимости от режима записи элемента, направления и ориентации текста.
---

# inset-inline-start

Свойство **`inset-inline-start`** определяет логическую встроенную начальную вставку элемента, которая сопоставляется с физическим смещением в зависимости от режима записи элемента, направления и ориентации текста.

Он соответствует `top`, `right`, `bottom` или `left` свойству в зависимости от значений, определенных для `writing-mode`, `direction` и `text-orientation`.

## Демо

<iframe class="interactive is-default-height" height="200" src="https://interactive-examples.mdn.mozilla.net/pages/css/inset-inline-start.html" title="MDN Web Docs Interactive Example" loading="lazy" data-readystate="complete"></iframe>

??? info "Логическое позиционирование"

    <div class="col3" markdown="1">

    - [inset](inset.md)
    - [inset-block](inset-block.md)
    - [inset-block-end](inset-block-end.md)
    - [inset-block-start](inset-block-start.md)
    - [inset-inline](inset-inline.md)
    - [inset-inline-end](inset-inline-end.md)
    - **inset-inline-start**

    </div>

## Синтаксис

```css
/* <length> values */
inset-inline-start: 3px;
inset-inline-start: 2.4em;

/* <percentage>s of the width or height of the containing block */
inset-inline-start: 10%;

/* Keyword value */
inset-inline-start: auto;

/* Global values */
inset-inline-start: inherit;
inset-inline-start: initial;
inset-inline-start: revert;
inset-inline-start: revert-layer;
inset-inline-start: unset;
```

## Поддержка браузерами

<p class="ciu_embed" data-feature="mdn-css__properties__inset-inline-start" data-periods="future_1,current,past_1,past_2" data-accessible-colours="false"></p>

## Ссылки

- Свойство [`inset-inline-start`](https://developer.mozilla.org/ru/docs/Web/CSS/inset-inline-start) <sup><small>MDN (рус.)</small></sup>
- [CSS Logical Properties and Values Level 1](https://w3c.github.io/csswg-drafts/css-logical/#position-properties) <sup><small>Spec (англ.)</small></sup>
