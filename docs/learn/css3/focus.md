---
description: Поймите важность фокуса в веб-приложениях. Вы узнаете, как управлять фокусом и как сделать так, чтобы путь по странице был удобен как для людей, пользующихся мышью, так и для тех, кто использует клавиатуру для навигации.
icon: material/image-filter-center-focus
---

# Фокус

<big>Поймите важность фокуса в веб-приложениях. Вы узнаете, как управлять фокусом и как сделать так, чтобы путь по странице был удобен как для людей, пользующихся мышью, так и для тех, кто использует клавиатуру для навигации.</big>

!!!info "CSS подкаст"

    018: Фокус

    <audio style="width: 100%;" controls src="https://traffic.libsyn.com/secure/thecsspodcast/TCP_CSS_Podcast_Episode_018_v1.0.mp3?dest-id=1891556"></audio>

На веб-странице пользователь нажимает на ссылку, которая переводит его к основному содержанию сайта. Такие ссылки часто называют пропускными или якорными. Когда эта ссылка активизируется с клавиатуры клавишами ++tab++ и ++enter++, вокруг контейнера с основным содержимым появляется кольцо фокуса. Почему так происходит?

<iframe src="https://codepen.io/web-dot-dev/embed/poRWRjp?height=500&amp;theme-id=light&amp;default-tab=result&amp;editable=true" style="height: 500px; width: 100%; border: 0;" loading="lazy"></iframe>

Это связано с тем, что `<main>` имеет значение атрибута `tabindex="-1"`, а значит, может быть программно сфокусирован. Когда на `<main>` нацеливаются - поскольку `#main-content` в строке URL браузера совпадает с `id` - он получает программный фокус. В таких ситуациях возникает соблазн убрать стили фокусировки, но правильное и осторожное обращение с фокусом помогает создать хороший, доступный пользовательский опыт. Это также может стать отличным местом для придания интереса взаимодействию.

## Почему фокус важен?

Ваша работа как веб-разработчика заключается в том, чтобы сделать сайт доступным и инклюзивным для всех. Создание доступных состояний фокуса с помощью CSS является частью этой задачи.

Стили фокуса помогают людям, использующим такие устройства, как клавиатура или [переключатель управления](https://www.24a11y.com/2018/i-used-a-switch-control-for-a-day/), осуществлять навигацию и взаимодействие с веб-сайтом. Если элемент получает фокус, а визуальная индикация отсутствует, пользователь может потерять трек, на котором он находится. Это может создать проблемы с навигацией и привести к нежелательному поведению, если, например, перейти не по той ссылке.

!!!note ""

    Подробнее о важности фокуса для обеспечения доступности читайте в [Изучам доступность: Фокус](../accessibility/focus.md), а о том, как управлять фокусом в HTML - в [Изучаем HTML: Фокус](../html/focus.md).

## Как элементы получают фокус

Некоторые элементы автоматически фокусируются; это элементы, которые принимают взаимодействие и ввод, такие как `<a>`, `<button>`, `<input>` и `<select>`. Короче говоря, все элементы форм, кнопки и ссылки. Обычно для навигации по фокусируемым элементам сайта используется клавиша _tab_ для перемещения вперед по странице и _shift_ + _tab_ для перемещения назад.

Существует также HTML-атрибут `tabindex`, который позволяет изменять индекс табуляции - порядок фокусировки элементов - каждый раз, когда кто-то нажимает клавишу ++tab++, или фокус смещается при изменении хэша в URL или по событию JavaScript. Если `tabindex` для HTML-элемента установлен в `0`, то он может получать фокус по клавише ++tab++ и будет соблюдать глобальный индекс табуляции, который определяется порядком источника документа.

Если задать `tabindex` равным `-1`, то он сможет получать фокус только программно, то есть только при наступлении JavaScript-события или изменении хэша (совпадении `id` элемента с URL). Если задать `tabindex` больше `0`, то он будет удален из глобального индекса вкладок, определяемого порядком источника документа. Порядок табуляции теперь будет определяться значением `tabindex`, поэтому элемент с `tabindex="1"` будет получать фокус, например, перед элементом с `tabindex="2"`.

!!!note ""

    Соблюдение порядка следования документов очень важно, и менять порядок следования фокусов следует только в том случае, если это **абсолютно необходимо**. Это касается как установки `tabindex` **так и** изменения визуального порядка с помощью CSS-макетов, таких как flexbox и grid. Все, что создает непредсказуемый порядок фокуса в Интернете, может создать недоступные для пользователя условия.

## Стилизация фокуса

По умолчанию, когда элемент получает фокус, в браузере появляется кольцо фокуса. В разных браузерах и операционных системах это кольцо может быть разным.

<video controls>
<source src="/learn/css3/focus-1.mp4" />
</video>

Это поведение можно изменить с помощью CSS, используя псевдоклассы `:focus`, `:focus-within` и `:focus-visible`, о которых вы узнали в уроке [pseudo-classes](pseudo-classes.md). Важно задать стиль фокуса, который **контрастирует** со стилем элемента по умолчанию. Например, распространенным подходом является использование свойства `outline`.

```css
a:focus {
    outline: 2px solid slateblue;
}
```

<iframe src="https://codepen.io/web-dot-dev/embed/ZELXLMw?height=500&amp;theme-id=light&amp;default-tab=result&amp;editable=true" style="height: 300px; width: 100%; border: 0;" loading="lazy"></iframe>

Свойство `outline` может оказаться слишком близко к тексту ссылки, но свойство `outline-offset` может помочь в этом, поскольку оно добавляет дополнительную визуальную "подложку", не влияя на геометрический размер, который заполняет элемент. Положительное значение числа для `outline-offset` выдвигает контур наружу, отрицательное - внутрь.

<iframe src="https://codepen.io/web-dot-dev/embed/xxgXgQx?height=500&amp;theme-id=light&amp;default-tab=result&amp;editable=true" style="height: 300px; width: 100%; border: 0;" loading="lazy"></iframe>

В настоящее время в некоторых браузерах, если для элемента задан `border-radius` и используется `outline`, он не будет соответствовать контуру - контур будет иметь острые углы. В связи с этим возникает соблазн использовать `box-shadow` с небольшим радиусом размытия, поскольку `box-shadow` фиксирует форму, соблюдая `border-radius`, но **такой стиль не будет отображаться в режиме Windows High Contrast Mode**. Это связано с тем, что режим высокой контрастности Windows не применяет тени и в основном игнорирует фоновые изображения, чтобы отдать предпочтение настройкам пользователя.

<iframe src="https://codepen.io/web-dot-dev/embed/bGgogyM?height=500&amp;theme-id=light&amp;default-tab=result&amp;editable=true" style="height: 300px; width: 100%; border: 0;" loading="lazy"></iframe>

<video controls>
<source src="/learn/css3/focus-2.mp4" />
</video>

## В заключение

Создание состояния фокуса, контрастирующего с состоянием элемента по умолчанию, невероятно важно. Стили браузера по умолчанию уже делают это за вас, но если вы хотите изменить это поведение, помните следующее:

-   Избегайте использования `outline: none` для элементов, которые могут получать фокус клавиатуры.
-   Не заменяйте стили `outline` на `box-shadow`, поскольку они не отображаются в режиме высокой контрастности Windows.
-   Устанавливайте положительное значение `tabindex` для HTML-элемента только в случае крайней необходимости.
-   Убедитесь, что состояние фокуса очень четко отличается от состояния по умолчанию.

:information_source: Источник &mdash; [Focus](https://web.dev/learn/css/focus/)