---
description: Узнайте, как структурировать HTML-документы
icon: material/file-tree
---

# Структура документа

<big>Узнайте, как структурировать HTML-документы.</big>

HTML-документы включают в себя объявление типа документа и корневой элемент [`<html>`](../../html/html.md). В элемент `<html>` вложены шапка и тело документа. Хотя шапка документа не видна посетителю, она очень важна для функционирования сайта. В ней содержится вся метаинформация, в том числе информация для поисковых систем и социальных сетей, значки для вкладок браузера и ярлыка главного экрана мобильного устройства, а также поведение и представление контента. В этом разделе вы познакомитесь с компонентами, которые, хотя и не видны, присутствуют практически на каждой веб-странице.

Чтобы создать сайт MachineLearningWorkshop.com (MLW), начните с включения компонентов, которые должны считаться основными для каждой веб-страницы: тип документа, язык содержимого, кодировка и, конечно же, название или имя сайта или приложения.

## Добавьте в каждый HTML-документ

Есть несколько элементов, которые следует считать необходимыми для каждой веб-страницы. Браузеры все равно будут выдавать содержимое, если эти элементы отсутствуют, но включать их необходимо. Обязательно.

### `<!DOCTYPE html>`

Первым элементом любого HTML-документа является преамбула. Для HTML все, что вам нужно, это `<!DOCTYPE html>`. Это может выглядеть как элемент HTML, но это не так. Это специальный тип узла, называемый "doctype". Doctype указывает браузеру на использование режима стандартов. Если его не указать, браузеры будут использовать другой режим рендеринга, известный как [quirks mode](https://developer.mozilla.org/docs/Web/HTML/Quirks_Mode_and_Standards_Mode). Включение doctype позволяет предотвратить использование режима quirks.

### `<html>`

Элемент `<html>` является корневым элементом HTML-документа. Он является родителем элементов [`<head>`](../../html/head.md) и [`<body>`](../../html/body.md) и содержит все, что есть в HTML-документе, кроме `doctype`. Если его пропустить, то он будет подразумеваться, но его важно включить, так как именно в этом элементе объявляется язык содержимого документа.

### Язык содержимого {#content-language}

Атрибут языка [`lang`](../../html/uni-attr.md#lang), добавляемый к тегу `<html>`, определяет основной язык документа. Значением атрибута `lang` является двух- или трехбуквенный код языка ISO, за которым следует регион. Регион указывать необязательно, но рекомендуется, поскольку в разных регионах язык может сильно различаться. Например, французский язык сильно отличается в Канаде (`fr-CA`) и Буркина-Фасо (`fr-BF`). Такое объявление языка позволяет программам чтения с экрана, поисковым системам и службам перевода узнать язык документа.

Атрибут `lang` не ограничивается тегом `<html>`. Если на странице имеется текст на языке, отличном от основного языка документа, то атрибут `lang` должен использоваться для определения исключений из основного языка в документе. Как и в случае включения в head, атрибут `lang` в body не имеет визуального эффекта. Он лишь добавляет семантику, позволяя вспомогательным технологиям и автоматизированным службам узнавать язык содержимого, на которое оказывается воздействие.

Помимо задания языка документа и исключений из него, атрибут может использоваться в селекторах CSS. `<span lang="fr-fr">Ceci n'est pas une pipe.</span>` можно адресовать с помощью атрибута и языковых селекторов [`[lang|="fr"]`](https://developer.mozilla.org/docs/Web/CSS/Attribute_selectors#attrvalue_3) и [`:lang(fr)`](../../css/lang.md).

### `<head>`

Между открывающим и закрывающим тегами `<html>` расположены два дочерних тега: `<head>` и `<body>`:

```html
<!DOCTYPE html>
<html lang="en-US">
    <head></head>
    <body></body>
</html>
```

Шапка `<head>`, или заголовок метаданных документа, содержит все метаданные сайта или приложения. Тело содержит видимое содержимое. Остальная часть этого раздела посвящена компонентам, расположенным внутри открывающего и закрывающего `<head></head>`.

## Необходимые компоненты внутри `<head>`

Метаданные документа, включая заголовок документа, кодировку, настройки области просмотра, описание, базовый URL, ссылки на таблицу стилей и значки, находятся в элементе `<head>`. Хотя все эти функции могут и не понадобиться, всегда указывайте кодировку, заголовок и настройки области просмотра.

### Кодировка символов {#character-set}

Самым первым элементом `<head>` должно быть объявление кодировки символов `charset`. Он располагается перед заголовком, чтобы гарантировать, что браузер сможет отобразить символы этого заголовка и все остальные символы документа.

В большинстве браузеров по умолчанию используется кодировка [`windows-1252`](https://html.spec.whatwg.org/multipage/parsing.html#documentEncoding), в зависимости от локали. Однако следует использовать [`UTF-8`](https://developer.mozilla.org/docs/Glossary/UTF-8), поскольку она позволяет кодировать от одного до четырех байт все символы, даже те, о существовании которых вы даже не подозревали. Кроме того, именно этот тип кодировки требуется в HTML5.

Чтобы установить кодировку символов UTF-8, включите:

```html
<meta charset="utf-8" />
```

Объявив `UTF-8` (без учета регистра), вы можете даже включить в заголовок символы emojis (но, пожалуйста, не надо).

Кодировка символов наследуется во всем документе, даже в [`<style>`](../../html/style.md) и [`<script>`](../../html/script.md). Эта маленькая декларация означает, что вы можете включать emojis в имена классов и в selectorAPI (опять же, пожалуйста, не используйте). Если вы все же [используете emojis](https://readabilityguidelines.co.uk/images/emojis/), убедитесь, что они используются таким образом, чтобы повысить удобство использования без ущерба для доступности.

### Заголовок документа

Ваша главная страница и все дополнительные страницы должны иметь уникальный заголовок. Содержимое заголовка документа — текст между открывающим и закрывающим тегами [`<title>`](../../html/title.md) — отображается на вкладке браузера, в списке открытых окон, в истории, в результатах поиска и, если не переопределено с помощью тегов [`<meta>`](metadata.md), в карточках социальных сетей.

```html
<title>Machine Learning Workshop</title>
```

### Метаданные viewport {#viewport-metadata}

Другой метатег, который следует считать важным, — это метатег `viewport`, который способствует отзывчивости сайта, позволяя содержимому хорошо отображаться по умолчанию, независимо от ширины области просмотра. Хотя метатег [viewport](https://developer.mozilla.org/docs/Web/HTML/Viewport_meta_tag) существует с июня 2007 года, когда вышел первый iPhone, он только недавно был [задокументирован в спецификации](https://drafts.csswg.org/css-viewport/#viewport-meta). Поскольку он позволяет управлять размерами и масштабом области просмотра и предотвращает уменьшение размера содержимого сайта, чтобы вместить 960-мегапиксельный сайт на 320-мегапиксельный экран, его обязательно следует использовать.

```html
<meta name="viewport" content="width=device-width" />
```

Приведенный код означает "сделать сайт отзывчивым, начиная с того, чтобы ширина содержимого соответствовала ширине экрана". Кроме `width`, можно задать масштабирование и масштабируемость, но по умолчанию они оба имеют приемлемые значения. Если вы хотите указать это явно, включите:

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1, user-scalable=1"
/>
```

Viewport является частью Lighthouse accessibility audit; ваш сайт пройдет проверку, если он масштабируемый и не имеет заданного максимального размера.

Пока что структура нашего HTML-файла такова:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title>Machine Learning Workshop</title>
        <meta
            name="viewport"
            content="width=device-width"
        />
    </head>
    <body></body>
</html>
```

## Остальное содержимое `<head>`

В `<head>` входит еще много чего. Фактически, все метаданные. Большинство элементов, которые можно найти в `<head>`, рассмотрены здесь, а множество опций `<meta>` оставлено для следующей главы.

Вы уже познакомились с кодировкой и заголовком документа, но за пределами тегов `<meta>` есть еще много метаданных, которые могут быть указаны.

### CSS {#css}

В `<head>` содержатся стили для HTML. Существует [обучающий курс, посвященный CSS](../css3/index.md), если вы хотите узнать о стилях, но вам необходимо знать, как добавлять их в HTML-документы.

Существует три способа добавления CSS: [`<link>`](../../html/link.md), [`<style>`](../../html/style.md) и атрибут [`style`](../../html/uni-attr.md#style).

Основные два способа добавления стилей в HTML-файл — это указание внешнего ресурса с помощью элемента `<link>` с атрибутом [`rel`](../../html/link.md#rel), установленным на `stylesheet`, или добавление CSS непосредственно в шапку документа в открывающий и закрывающий теги `<style>`.

Тег `<link>` является предпочтительным методом добавления таблиц стилей. Ссылка на одну или несколько внешних таблиц стилей полезна как для разработчиков, так и для производительности сайта: вы получаете возможность поддерживать CSS в одном месте, а не распылять его повсюду, а браузеры могут кэшировать внешний файл, то есть его не нужно загружать заново при каждом переходе по странице.

Синтаксис: `<link rel="stylesheet" href="styles.css">`, где `styles.css` — это URL вашей таблицы стилей. Часто можно увидеть `type="text/css"`. Это не обязательно! Если вы добавляете стили, написанные не на CSS, то атрибут `type` необходим, но поскольку других типов не существует, то и этот атрибут не нужен. Атрибут `rel` определяет взаимосвязь: в данном случае `stylesheet`. Если его опустить, то CSS не будет подключен.

Вскоре вы узнаете о некоторых других значениях `rel`, но сначала давайте обсудим другие способы добавления CSS.

Если вы хотите, чтобы стили внешней таблицы стилей находились в каскадном слое, но у вас нет доступа к редактированию CSS-файла, чтобы поместить в него информацию о слое, вам нужно включить CSS с помощью [`@import`](../../css/import.md) внутри `<style>`:

```html
<style>
    @import 'styles.css' layer(firstLayer);
</style>
```

При использовании `@import` для импорта таблиц стилей в документ, а также в каскадные слои, утверждения `@import` должны быть первыми в вашем `<style>` или связанной таблице стилей, за пределами объявления кодировки.

Хотя каскадные слои еще достаточно новы, и вы можете не заметить `@import` в головном `<style>`, вы часто будете видеть пользовательские свойства, объявленные в головном блоке стилей:

```html
<style>
    :root {
        --theme-color: #226daa;
    }
</style>
```

!!!note ""

    Стили, т. е. презентационный слой, относятся к области CSS, а здесь мы рассматриваем, как прикрепить стили к слою содержимого, т. е. HTML. Если CSS предыдущего кода вас заинтересовал, посмотрите [cascade layers](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Cascade_layers) и [custom properties](https://developer.mozilla.org/docs/Web/CSS/Using_CSS_custom_properties).

Стили, либо через `<link>`, либо через `<style>`, либо через оба, должны располагаться в шапке. Они будут работать, если их включить в тело документа, но по соображениям производительности стили следует помещать в шапку. Это может показаться нелогичным, поскольку вы можете думать, что сначала загружается содержимое, но на самом деле вы хотите, чтобы браузер знал, как отобразить содержимое после его загрузки. Добавление стилей в первую очередь предотвращает ненужное перерисовывание, которое происходит, если стилизация элемента выполняется после его первого отображения.

Есть еще один способ включения стилей, который вы никогда не будете использовать в `<head>` документа: встроенные стили. Скорее всего, вы никогда не будете использовать встроенные стили в шапке, поскольку таблицы стилей пользовательских агентов по умолчанию скрывают шапку. Но если вы хотите сделать CSS-редактор без JavaScript, например, для тестирования пользовательских элементов страницы, вы можете сделать шапку видимой с помощью [`display: block`](../../css/display.md#значения), затем скрыть все в шапке, а затем с помощью инлайнового атрибута `style` сделать видимым блок редактируемых стилей.

```html
<style
    contenteditable
    style="display: block; font-family: monospace; white-space: pre;"
>
    head {
        display: block;
    }
    head * {
        display: none;
    }
    :root {
        --theme-color: #226daa;
    }
</style>
```

Хотя вы можете добавлять инлайновые стили в `<style>`, гораздо интереснее стилизовать свой `<style>` в своем `style`. Впрочем, я отвлекся.

### Прочие возможности использования элемента `<link>` {#other-uses-of-the-lesslinkgreater-element}

Элемент `link` используется для создания связей между HTML-документом и внешними ресурсами. Некоторые из этих ресурсов могут быть загружены, другие носят информационный характер. Тип связи определяется значением атрибута `rel`. В настоящее время существует [25 доступных значений атрибута `rel`](https://html.spec.whatwg.org/multipage/links.html#linkTypes), которые могут использоваться с `<link>`, [`<a>`](../../html/a.md) и [`<area>`](../../html/area.md), или [`<form>`](../../html/form.md), а некоторые из них могут использоваться со всеми. Желательно, чтобы те из них, которые относятся к метаинформации, находились в заголовочной части, а те, которые относятся к выполнению, — в `<body>`.

Теперь вы включите в заголовок еще три типа: `icon`, `alternate`, и `canonical`. Четвертый тип, [`rel="manifest"`, вы включите в следующем модуле](metadata.md).

#### Favicon

С помощью тега `<link>` с парой атрибутов/значений `rel="icon"` можно определить фавикон, который будет использоваться для вашего документа. Фавикон — это очень маленький значок, который отображается на вкладке браузера, как правило, слева от заголовка документа. При большом количестве открытых вкладок вкладки уменьшаются, а заголовок может исчезнуть совсем, но значок всегда остается видимым. Большинство фавиконов — это логотипы компаний или приложений.

Если вы не объявили фавикон, браузер будет искать файл с именем `favicon.ico` в каталоге верхнего уровня (корневой папке сайта). С помощью `<link>` можно использовать другое имя и расположение файла:

```html
<link
    rel="icon"
    sizes="16x16 32x32 48x48"
    type="image/png"
    href="/images/mlwicon.png"
/>
```

В предыдущем коде говорится, что "используйте `mlwicon.png` в качестве иконки в случаях, когда имеет смысл использовать `16px`, `32px` или `48px`. Атрибут `sizes` принимает значение `any` для масштабируемых иконок или список квадратных значений `widthXheight`, разделенных пробелами; если значения ширины и высоты равны `16`, `32`, `48` или больше в этой геометрической последовательности, единица измерения пикселей опускается, а `X` не зависит от регистра.

```html
<link
    rel="apple-touch-icon"
    sizes="180x180"
    href="/images/mlwicon.png"
/>
<link
    rel="mask-icon"
    href="/images/mlwicon.svg"
    color="#226DAA"
/>
```

Для браузера Safari существует два специальных нестандартных вида значков: `apple-touch-icon` для iOS-устройств и `mask-icon` для закрепленных вкладок на macOS. Иконка `apple-touch-icon` применяется только тогда, когда пользователь добавляет сайт на домашний экран: вы можете указать несколько иконок с разными `размерами` для разных устройств. `mask-icon` применяется только в том случае, если пользователь закрепляет вкладку в настольном Safari: сама иконка должна быть монохромной SVG, а атрибут `color` заливает иконку нужным цветом.

Хотя вы можете использовать `<link>` для определения совершенно разных изображений на каждой странице или даже при каждой загрузке страницы, не стоит этого делать. Для обеспечения последовательности и хорошего пользовательского опыта используйте одно изображение! Twitter использует синюю птицу: когда вы видите синюю птицу на вкладке браузера, вы знаете, что эта вкладка открыта на страницу Twitter без щелчка на вкладке. Google использует различные фавиконы для каждого из своих приложений: например, есть значок почты, значок календаря. Но все значки Google используют одну и ту же цветовую схему. Опять же, по значку можно точно определить содержимое открытой вкладки.

#### Альтернативные версии сайта {#alternate-versions-of-the-site}

Мы используем значение `alternate` атрибута `rel` для идентификации переводов, или альтернативных представлений, сайта.

Представим, что у нас есть версии сайта, переведенные на французский и бразильский португальский языки:

```html
<link
    rel="alternate"
    href="https://www.machinelearningworkshop.com/fr/"
    hreflang="fr-FR"
/>
<link
    rel="alternate"
    href="https://www.machinelearningworkshop.com/pt/"
    hreflang="pt-BR"
/>
```

При использовании `alternate` для перевода должен быть установлен атрибут `hreflang`.

Значение `alternate` используется не только для переводов. Например, атрибут `type` может определять альтернативный URI для RSS-канала, когда атрибут `type` имеет значение `application/rss+xml` или `application/atom+xml`. Давайте сделаем ссылку на условную PDF-версию сайта.

```html
<link
    rel="alternate"
    type="application/x-pdf"
    href="https://machinelearningworkshop.com/mlw.pdf"
/>
```

Если значение `rel` равно `alternate stylesheet`, то это определяет [alternate stylesheet](https://developer.mozilla.org/docs/Web/CSS/Alternative_style_sheets), а атрибут `title` должен быть задан с указанием имени этого альтернативного стиля.

#### Canonical

Если создать несколько переводов или версий Machine Learning Workshop, поисковые системы могут запутаться в том, какая из версий является основной. Для этого используйте `rel="canonical"`, чтобы определить предпочтительный URL-адрес сайта или приложения.

Укажите канонический URL на всех переведенных страницах, а также на главной странице, указав наиболее желаемый URL:

```html
<link
    rel="canonical"
    href="https://www.machinelearning.com"
/>
```

Каноническая ссылка `rel="canonical"` чаще всего используется при кросс-постинге в изданиях и блог-платформах для указания ссылки на первоисточник; при синдикации контента сайт должен включать каноническую ссылку на первоисточник.

### Скрипты

Тег [`<script>`](../../html/script.md) используется для включения, так сказать, скриптов. По умолчанию используется тип JavaScript. Если вы включаете какой-либо другой язык сценариев, включите атрибут `type` с типом mime, или `type="module"`, если это [JavaScript-модуль](https://developer.mozilla.org/docs/Web/JavaScript/Guide/Modules#applying_the_module_to_your_html). Анализируются и выполняются только JavaScript и модули JavaScript.

Теги `<script>` могут использоваться для инкапсуляции кода или для загрузки внешнего файла. В MLW нет внешнего файла сценария, поскольку, вопреки распространенному мнению, JavaScript не нужен для функционального сайта, и, кроме того, это курс изучения HTML, а не JavaScript.

Позже вы добавите немного JavaScript для создания пасхалки:

```html
<script>
    document
        .getElementById('switch')
        .addEventListener('click', function () {
            document.body.classList.toggle('black');
        });
</script>
```

Этот фрагмент создает обработчик события для элемента с идентификатором `switch`. В JavaScript нежелательно ссылаться на элемент до того, как он будет существовать. Он еще не существует, поэтому мы пока не будем его включать. Когда мы добавим элемент выключателя, мы добавим `<script>` в нижнюю часть `<body>`, а не в `<head>`. Почему? По двум причинам. Мы хотим убедиться, что элементы существуют до того, как появится сценарий, ссылающийся на них, поскольку мы не основываем этот сценарий на событии [DOMContentLoaded](https://developer.mozilla.org/docs/Web/API/Document/DOMContentLoaded_event). И, главное, JavaScript не только [блокирует рендеринг](https://developer.chrome.com/docs/lighthouse/performance/render-blocking-resources/), но и браузер останавливает загрузку всех активов при загрузке скриптов и не возобновляет загрузку других активов до тех пор, пока не будет выполнен JavaScript. По этой причине часто можно встретить запросы JavaScript в конце документа, а не в голове.

Существует два атрибута, которые могут уменьшить блокировку загрузки и выполнения JavaScript: [`defer`](../../html/script.md#defer) и [`async`](../../html/script.md#async). При использовании `defer` рендеринг HTML не блокируется во время загрузки, а JavaScript выполняется только после завершения рендеринга документа. При использовании `async` рендеринг также не блокируется во время загрузки, но после завершения загрузки скрипта рендеринг приостанавливается на время выполнения JavaScript.

![загрузка при использовании async и defer](document-structure-1.png)

Чтобы подключить JavaScript MLW из внешнего файла, можно написать:

```html
<script src="js/switch.js" defer></script>
```

Добавление атрибута `defer` откладывает выполнение скрипта до того момента, когда все будет отрисовано, не позволяя скрипту ухудшить производительность. Атрибуты `async` и `defer` действительны только для внешних скриптов.

### `<base>` {#base}

Существует еще один элемент, который встречается только в `<head>.` Не очень часто используемый, элемент [`<base>`](../../html/base.md) позволяет задать URL и цель ссылки по умолчанию. Атрибут [`href`](../../html/base.md#href) определяет базовый URL для всех относительных ссылок.

Атрибут [`target`](../../html/base.md#target), действительный для `<base>`, а также для ссылок и форм, задает, куда должны открываться эти ссылки. По умолчанию `_self` открывает связанные файлы в том же пространстве, что и текущий документ. Другие варианты включают `_blank`, который открывает каждую ссылку в новом окне, `_parent` текущего содержимого, который может быть тем же, что и `self`, если открывающий элемент не является `iframe`, или `_top`, который находится в той же вкладке браузера, но вырывается из любого пространства, занимая всю вкладку.

Большинство разработчиков добавляют атрибут `target` к тем немногим ссылкам, которые они хотят открыть в новом окне, на самих ссылках или форме, вместо того чтобы использовать `<base>`.

```html
<base
    target="_top"
    href="https://machinelearningworkshop.com"
/>
```

Если бы наш сайт оказался вложенным в `iframe` на таком сайте, как Yummly, включение элемента `<base>` означало бы, что при нажатии пользователем на любую ссылку в нашем документе ссылка будет загружаться из `iframe`, занимая все окно браузера.

Одним из недостатков этого элемента является то, что якорные ссылки обрабатываются с помощью `<base>`. `<base>` фактически преобразует ссылку `<a href="#ref">` в `<a target="_top" href="https://machinelearningworkshop.com#ref">`, вызывая HTTP-запрос к базовому URL с присоединенным фрагментом.

Еще несколько замечаний по поводу `<base>`: в документе может быть только один элемент `<base>`, и он должен находиться перед любыми относительными URL, включая возможные ссылки на скрипт или таблицу стилей.

Теперь код выглядит следующим образом:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title>Machine Learning Workshop</title>
        <meta
            name="viewport"
            content="width=device-width"
        />
        <link rel="stylesheet" src="css/styles.css" />
        <link
            rel="icon"
            type="image/png"
            href="/images/favicon.png"
        />
        <link
            rel="alternate"
            href="https://www.machinelearningworkshop.com/fr/"
            hreflang="fr-FR"
        />
        <link
            rel="alternate"
            href="https://www.machinelearningworkshop.com/pt/"
            hreflang="pt-BR"
        />
        <link
            rel="canonical"
            href="https://www.machinelearning.com"
        />
    </head>
    <body>
        <!-- <script defer src="scripts/lightswitch.js"></script>-->
    </body>
</html>
```

### HTML-комментарии

Обратите внимание, что скрипт завернут между угловыми скобками, тире и черточками. Именно так можно закомментировать HTML. Мы оставим скрипт закомментированным до тех пор, пока на странице не появится реальное содержимое. Все, что находится между `<!--` и `-->`, не будет видно и разобрано. HTML-комментарии можно размещать в любом месте страницы, включая `head` или `body`, за исключением скриптов или блоков стилей, где следует использовать JavaScript- и CSS-комментарии соответственно.

Вы рассмотрели основы того, что должно быть в `<head>`, но вы хотите узнать больше, чем просто основы. В следующих разделах мы узнаем о метатегах и о том, как управлять тем, что отображается при ссылках на ваш сайт в социальных сетях.

## Источник

-   [Document structure](https://web.dev/learn/html/document-structure/)
