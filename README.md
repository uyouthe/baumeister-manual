# Введение

В данном руководстве речь пойдет о создании полноценных модульных сайтов, которые легко расширять, поддерживать и изменять. Для достижения наших целей мы будем использовать [Baumeister](#baumeister) — генератор шаблонов сайтов, использующий [Sass](https://sass-scss.ru/), [Bootstrap](https://getbootstrap.com/) и [Handlebars](http://handlebarsjs.com/).

## Bootstrap

[Bootstrap](https://getbootstrap.com/) — это фреймворк, позволяющий быстро создавать адаптивные веб-страницы, используя набор готовых компонентов.

Разработка сайтов с нуля влечет за собой слишком большую дополнительную ответственность. Как правильно организовать код? Как добиться отсутствия конфликтов различных CSS-правил? Как сделать код пригодным для повторного использования? Как не забыть о тысяче мелочей, требующихся для нормального отображения сайта разных браузерах, в том числе в старых IE? Для начинающего разработчика создание сайта с учетом всех нюансов может оказаться попросту невозможным, а опытному разработчику ни к чему раз за разом повторять одни и те же тривиальные действия.

Bootstrap позволяет не задумываться об этих проблемах, предлагая устоявшуюся, стандартизованную систему организации компонентов.

Помимо этого, существуют типовые задачи, такие как, например, создание сетки, которые давно уже были решены, и решать их заново нет никакой необходимости \(если вы, конечно, не создаете _нестандартный_ сайт, в таком случае, вы сами знаете, что делать\).

Bootstrap заточен на решение типовых задач и позволяет справляться с ними очень быстро. В набор компонентов входят:

* Адаптивная сетка
* Кнопки
* Карусели
* Модальные окна
* Формы
* Множество других компонентов.

С полным списком компонентов и руководством пользователя можно ознакомиться на [официальном сайте](https://getbootstrap.com/).

У [Хекслета](https://ru.hexlet.io/) есть замечательное [краткое руководство по Bootstrap](https://hexletguides.github.io/bootstrap/).

### Темы

Хотя Bootstrap и предоставляет пользователю набор базовых компонентов, вряд ли их внешний вид нас устроит. Мы будем создавать сайты для разных целей, очевидно, что они не должны выглядеть абсолютно одинаково.

Bootstrap достаточно сложен, чтобы каждый раз модифицировать его исходный код, чтобы заставить компоненты выглядеть так, как нам нужно. Создатели Bootstrap понимали это. Они постарались, и теперь для того, чтобы изменить внешний вид встроенных компонентов, нужно всего лишь создать свою собственную **тему**.

Тема для Bootstrap — это файл стилей, содержащий описание внешнего вида компонентов. Процесс создания темы описан в разделе «[Рабочий процесс](/rabochii-protsess.md)».

## Препроцессоры

Bootstrap использует препроцессор [Sass](https://sass-scss.ru/) вместо обычного CSS. Препроцессор позволяет добиться более оптимального повторного использования кода при помощи миксинов и функций, а так же позволяет не задумываться о правильном слиянии стилей многочисленных компонентов в один CSS-файл, вендорных префиксах, минификации и прочих тривиальных вещах.

У Sass существует два синтаксиса: собственно Sass и SCSS, более близкий к обычному CSS. Мы будем использовать SCSS.

Любой правильно написанный CSS-код является правильным SCSS-кодом. Если вы никогда раньше не использовали Sass, вы можете писать обычный CSS в SCSS-файлах, все будет работать. Постепенно добавляя в CSS все больше Sass, вы сможете полностью перейти на него.

Подробнее о Sass можно почитать в [официальном руководстве](https://sass-scss.ru/guide/).

Если Sass-код кажется вам непонятным, используйте [Sassmeister](https://www.sassmeister.com/) для отладки и преобразования Sass в привычный CSS прямо в браузере.

## Шаблонизация

Предположим, перед нами стоит задача разработать верстку интернет-магазина. В каталоге находится множество различных товаров, предположим, на одной странице их 12. Мы верстаем одну карточку товара, копируем ее и вставляем еще 11 таких же. Теперь у нас появилась серьезная проблема.

Если нужно будет _немного изменить_ верстку карточки, придется внести одни и те же изменения 12 раз. А если карточек нужно 50? Копирование одного и того же кода создает большие проблемы для дальнейшей поддержки.

Помимо этого, вас возненавидит бэкенд-разработчик — ему придется потратить много времени, чтобы разобраться в огромном, повторяющемся коде.

Намного разумнее было бы написать код один раз, создав компонент и явно указав, какие части кода повторяются, а какие являются уникальными для каждого из экземпляров компонента. Например, верстка карточки товара окажется абсолютно одинаковой, а значения, такие как цена товара, картинка и название, окажутся разными для каждой из карточек.

Помимо очевидных преимуществ для нас, бэкенд-разработчик сможет потратить намного меньше времени, подключая нашу верстку к бэкенду, потому что все повторяющиеся элементы окажутся описаны в удобной для шаблонизации форме. В отдельных случаях, бэкенд-разработчику _вообще_ не придется выполнять шаблонизацию вручную, достаточно будет скопировать созданные нами компоненты.

Шаблонизаторы позволяют создавать компоненты, пригодные для повторного использования. Мы будем использовать шаблонизатор [Handlebars](http://handlebarsjs.com/).

## БЭМ

Одним из главных принципов CSS является наследование стилей. Иными словами, некоторые свойства, применяемые к родительским элементам, применяются так же и к дочерним. Например:

```css
body {
    font-size: 16px;
}
```

Код, указанный выше, установит размер шрифта в `16px` для тела html-документа, а так же для всех его потомков, если не найдется более специфичного правила, устанавливающего иной размер шрифта.

Наследование стилей может быть полезным, однако, оно в большинстве случаев делает невозможным написание компонентов, пригодных для повторного использования, особенно, если эти компоненты нужно будет перенести в другой проект и использовать там. Рассмотрим пример:

```css
body div:first-child .card > div ul li {
    font-size: 22px;
    color: hotpink;
}
```

Код, указанный выше, может быть и работает, но, помимо того, что он уже выглядит очень сложным и противным, работать он будет только в данном конкретном случае. Стоит лишь вынести элемент с классом `card` из первого `div` в `body` куда-то в другое место, и верстка сломается.

Проблем, описанных выше, можно избежать, если мыслить в терминах компонентов. Будет удобно, если можно будет написать стили для отдельно взятого компонента, и эти стили будут работать всегда и везде, вне зависимости от других компонентов или родительских элементов. Именно для этих целей служит методология БЭМ.

БЭМ определяет три ключевых понятия:

* **Блок**: повторяющийся компонент страницы. Например, шапка или навигационная панель.
* **Элемент**: составная часть блока. Например, одна из ссылок навигационной панели.
* **Модификатор**: выражение, отображающее изменение поведения или внешнего вида блока или элемента. Например, навигационная панель может быть отображена в виде списка или в виде вкладок.

О том, как именно обозначать блоки, элементы и модификаторы, можно прочитать в [официальной документации](https://ru.bem.info/methodology/quick-start/).

Преимущества БЭМ:

* Можно вкладывать элементы и блоки друг в друга в любом порядке: верстка не развалится.
* Верстка _вообще _теперь практически никогда не развалится.
* Можно использовать семантические теги на полную катушку, так как все стили применяются через имена классов, совершенно неважно, к чему их применять: к `nav` или к `footer`.
* Можно забыть о проблемах со специфичностью.
* Можно переносить компоненты между проектами: правильное использование БЭМ позволяет гарантировать, что все стили, относящиеся к компоненту, находятся в одном месте.
* Можно описать все возможные варианты отображения элемента при помощи модификаторов и безболезненно переключать их при помощи JavaScript. Элегантное решение часто возникающей задачи.

БЭМ отлично сочетается с компонентным подходом к созданию сайтов, упрощает поддержку, внесение изменений и рекомендуется к использованию[^1].

Более подробно с методологией можно ознакомиться на [официальном сайте](https://ru.bem.info/) или в [этой статье](https://habrahabr.ru/company/yandex/blog/276035/).

## Baumeister {#baumeister-description}

Неразумно было бы каждый раз при создании типового сайта с одним и тем же набором инструментов заново устанавливать все необходимые пакеты, вспоминая их названия, создавать файлы конфигурации, настраивать сборку всего проекта. Намного проще и быстрее было бы начать с уже созданного проекта-шаблона, который можно легко изменить. Еще лучше, если нам не придется вручную прописывать в конфигурационных файлах такие вещи, как имя проекта, название темы Bootstrap, тип лицензии и т.д. Было бы идеально, если наш инструмент сам спросил все нужные вещи у нас.

Именно таким инструментом является [Baumeister ](https://baumeister.io/)— генератор шаблонов, генерирующий проекты с уже настроенным Bootstrap, созданной темой, компонентами Handlebars, оптимизатором изображений, линтером и многими другими инструментами. Именно его мы и будем использовать в работе.



[^1]: Строго говоря, использование Bootstrap является отходом от БЭМ, потому что компоненты начинают зависеть не только от соответствующих им стилей, но и от стилей Bootstrap. Однако, Bootstrap является достаточно популярным и легким в установке, чтобы этой проблемой можно было пренебречь.

