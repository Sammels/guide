# CSS

- [CSS синтаксис](#css-синтаксис)
- [Порядок объявления](#Порядок-объявления)
- [Не используйте @import](#Не-используйте-import)
- [Место для media query](#Место-для-media-query)
- [Правила с одиночными объявлениями](#Правила-с-одиночными-объявлениями)
- [Сокращенная запись](#Сокращенная-запись)
- [Селекторы](#Селекторы)
- [SASS](#SASS)
- [Организация кода](#Организация-кода)

### CSS синтаксис

- Для отступов используются 2 пробела. Исключение только для готовых проектов, где уже используется другой стандарт.  
В этом примере `∙∙` - 2 пробела, а `――――` - один отступ с табуляцией.

```css
/* Плохо */
.heading {
――――font-size: 32px;
}

/* Хорошо */
.heading {
∙∙font-size: 32px;
}
```

- Каждый селектор на отдельной строке.

```css
/* Плохо */
.header, .main, .footer {
  margin-left: auto;
  margin-right: auto;
}

/* Хорошо */
.header,
.main,
.footer {
  margin-left: auto;
  margin-right: auto;
}
```

- 1 пробел перед `{`.

```css
/* Плохо */
.heading{
  font-size: 32px;
}

/* Хорошо */
.heading {
  font-size: 32px;
}
```

- 1 перенос на новою строку перед `}`.

```css
/* Плохо */
.heading {
  font-size: 32px;}

.heading {
  font-size: 32px;
    }

/* Хорошо */
.heading {
  font-size: 32px;
}
```

- 1 перенос на новую строку после `}` и между группами объявлений.

```css
/* Плохо */
.heading {
  font-size: 32px;
}
.highlight {
  background-color: #f00;
}

/* Хорошо */
.heading {
  font-size: 32px;
}

.highlight {
  background-color: #f00;
}
```

- 1 пробел после `:`.

```css
/* Плохо */
.heading {
  font-size:32px;
}

/* Хорошо */
.heading {
  font-size: 32px;
}
```

- Все объявления завершаются с `;`.

```css
/* Плохо */
.heading {
  font-size: 32px
}

/* Хорошо */
.heading {
  font-size: 32px;
}
```

- 1 пробел после запятых в значениях свойств.

```css
/* Плохо */
.header {
  background-color: rgba(0,0,0,.5);
}

/* Хорошо */
.header {
  background-color: rgba(0, 0, 0, .5);
}
```

- Не добавляйте начальный ноль для значений.

```css
/* Плохо */
.transparent {
  opacity: 0.5;
}

/* Хорошо */
.transparent {
  opacity: .5;
}
```

- Все 16-ичные значения записывайте строчными буквами (в нижнем регистре). Строчные буквы гораздо легче различить при просмотре файла, поскольку они, как правило, имеют больше уникальных форм.

```css
/* Плохо */
.white {
  background-color: #FFF;
}

/* Хорошо */
.white {
  background-color: #fff;
}
```

- Используйте короткие 16-ичные значения.

```css
/* Плохо */
.highlight {
  color: #ffffff;
  background-color: #0088ff;
}

/* Хорошо */
.highlight {
  color: #fff;
  background-color: #08f;
}
```

- `"` для значений атрибутов внутри селектора.

```css
/* Плохо */
input[type=text] {
  /* ... */
}

/* Хорошо */
input[type="text"] {
  /* ... */
}
```

- Опускайте единицы измерения при нулевом значении.

```css
/* Плохо */
.header {
  margin-top: 0px;
}

/* Хорошо */
.header {
  margin-top: 0;
}
```



### Порядок объявления

Объявления логически связанных свойств должны быть сгруппированы в следующем порядке:

  - Позиционирование - может удалить элемент из нормального потока документа и переопределить блочную модель связанных стилей.
  - Расположение - задаются внешние и внутренние отступы.
  - Блочная модель - диктует размеры
  - Типографика - шрифты, стилизация текста
  - Отображение - цвет, фон и т.п.
  - Прочее - трансформации, поведение и т.п.

Полный список порядка свойст можно посмотреть в конфигурации [CSScomb](https://github.com/CSSSR/csssr-project-template/blob/master/.csscomb.json).

Небольшой пример:

```css
.declaration-order {
  /* Позиционирование */
  position: absolute;
  z-index: 100;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  
  /* Расположение */
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
  padding: 8px 16px;

  /* Блочная модель */
  display: block;
  float: left;
  width: 100px;
  height: 100px;
  
  /* Типографика */
  font-family: 'Helvetica Neue', sans-serif;
  font-size: 14px;
  line-height: 24px;
  text-align: center;
  
  /* Отображение */
  color: #333;
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;
  opacity: 1;
  
  /* Прочее */
  transition: .25s ease-out;
  transform: scale(.75);
}
```


### Не используйте @import

По сравнению с тегом `<link>` правило `@import` медленнее, создает дополнительные запросы и может вызвать иные непредвиденные проблемы. Избегайте это правило и используйте вместо него один из альтернативных подходов:

- Склеивайте CSS-файлы в один файл и минифицируйте.
- Компилируйте CSS-код в один файл с помощью препроцессоров, например, Stylus, Sass или Less.

Для получения дополнительной информации следует ознакомиться со [статьей Стива Соудерса](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/).

```html
<!-- Используйте тег link -->
<link rel="stylesheet" href="assets/styles/main.min.css">

<!-- Избегайте @import -->
<style>
  @import url(assets/styles/main.css);
</style>
```


### Место для media query

Помещайте медиавыражения настолько близко к соответствующим наборам правил, насколько это возможно. Не объединяйте их в отдельную таблицу стилей. Не помещайте их в конце файла, для этого можно использовать специальный сборщик в [Grunt](https://www.npmjs.org/package/grunt-combine-media-queries) или [Gulp](https://www.npmjs.org/package/gulp-combine-media-queries). В противном случае это приведет к тому, что медиавыражения будут не замечены в будущем.

Вот типичная структура:

```css
.element { /* ... */ }
.element-avatar { /* ... */ }
.element-selected { /* ... */ }

@media only screen and (min-width: 480px) {
  .element { /* ... */}
  .element-avatar { /* ... */ }
  .element-selected { /* ... */ }
}
```

### Правила с одиночными объявлениями

В случаях, когда набор правил включает в себя только одно объявление, рекомендуется оставить переносы строк, иначе в будущем при добавлении новых свойств потребуется добавлять переносы. Любой набор правил с несколькими объявлениями должен быть разделен на отдельные строки.

Ключевым фактором здесь является обнаружение ошибок — например, валидатор CSS сообщает вам, что в строке 183 есть синтаксическая ошибка. С одиночным объявлением не возникнет сложности с исправлением. В случае с несколькими объявлениями, разделенными на строки, так же проблем не возникнет. Но если несколько объявлений будут записаны в одну строку, то вам будет сложнее понять какое именно объявление вызвало синтаксическую ошибку.

```css
/* Плохо */
.sprite { display: inline-block; width: 16px; height: 16px; background-image: url(../images/sprite.png); }
.sprite-home    { background-position: 0 -20px; }
.sprite-account { background-position: 0 -40px; }

/* Хорошо */
.sprite {
  display: inline-block;
  width: 16px;
  height: 16px;
  background-image: url(../img/sprite.png);
}

.sprite-home {
  background-position: 0 -20px;
}

.sprite-account {
  background-position: 0 -40px;
}
```

### Сокращенная запись

Старайтесь ограничить использование сокращенных объявлений в тех случаях, когда необходимо явно задать все доступные значения. Наиболее часто злоупотребляют сокращением следующих свойств:
- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

Часто нам не нужно устанавливать все значения сокращенной записи свойства. Например, HTML заголовки устанавливают только отступы сверху и снизу, таким образом, в случае необходимости нужно переопределить только эти два значения. Чрезмерное использование сокращенной записи свойств часто приводит к грязному коду с ненужными переопределения и непреднамеренными побочными эффектами.

На сайте Mozilla Developer Network есть отличная статья о [сокращенной записи свойств](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) для тех кто не знаком с такой формой записи.

```css
/* Плохо */
.element {
  margin: 0 0 10px;
  background: red;
  background: url(../img/image.jpg);
  border-radius: 3px 3px 0 0;
}

/* Хорошо */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url(../img/image.jpg);
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

### Комментарии

- Пишите комментарии только по мере необходимости, передающие контекст и цель кода, а не просто повторение названия класса или компонента.
- Всё комментировать не нужно.
- Комментарии только на английском языке.

### Селекторы

- Используйте только классы вместо тегов для оптимальной производительности отображения.
- Не используйте селекторы по атрибуту (например, `[class^="..."]`) для часто встречающихся компонентов. Это негативно повлияет на производительность браузера.
- Не используйте идентификаторы.
- Не используйте каскад (вложенность селекторов).
- Вложенность селекторов допускается **только** в случае необходимости, например, когда нужно изменить свойства при наведении (`:hover`) или другом подобного псевдоселекторе, и при использовании специальных глобальных классов.

Дополнительно к прочтению:
- [Scope CSS classes with prefixes](http://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/).
- [Stop the cascade](http://markdotto.com/2012/03/02/stop-the-cascade/).

```css
/* Плохо */
span { /* ... */ }
a.link { /* ... */ }
#logo { /* ... */ }
.page-container #stream .stream-item .tweet .tweet-header .username { /* ... */ }
.user { /* ... */ }

/* Хорошо */
.link {
  /* ... */
}

.user {
  /* ... */
}

.user:hover .user__name {
  /* ... */
}
```

### SASS

Если используется прекомпилятор CSS, то используется SASS с диалектом SCSS.  
Пример использования SCSS с БЭМ-ом.

```CSS
.menu-h {
  &__list {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  &__item {
    position: relative;
    float: left;
    padding: 0;
  }

  &__text {
    display: inline-block;
    border-bottom: 1px solid #fff;
    color: #fff;
    font-weight: bold;
    font-size: 20px;
    line-height: 18px;
  }

  &__link {
    display: block;
    padding: 0 18px;
    height: 70px;
    text-decoration: none;
    line-height: 70px;

    &:hover {
      background-color: $blue-light;
    }

    &--active,
    &--active:hover {
      background-color: $green;
      color: $text-black;
    }
  }

  &__link--active &__text {
    border-bottom: 1px solid transparent;
  }
}
```

### Организация кода
Организация кода основывается на [руководстве по написанию разумного, поддерживаемого и масштабируемого Sass](https://sass-guidelin.es/ru/)
Архитектура:
```
|– base/
|   |– _reset.scss       # Reset/normalize
|   |– _typography.scss  # Типографские правила
|   …                    # и т.д.
|
|– components/
|   |– _buttons.scss     # Кнопки
|   |– _carousel.scss    # Карусель
|   |– _cover.scss       # Обложка
|   |– _dropdown.scss    # Выпадающий список
|   …                    # и т.д.
|
|– layout/
|   |– _navigation.scss  # Навигация
|   |– _grid.scss        # Сетка
|   |– _header.scss      # Шапка
|   |– _footer.scss      # Подвал
|   |– _sidebar.scss     # Боковая панель
|   |– _forms.scss       # Формы
|   …                    # и т.д.
|
|– pages/
|   |– _home.scss        # Стили, особые для главной страницы
|   |– _contact.scss     # Стили, особые для страницы контактов
|   …                    # и т.д.
|
|– themes/
|   |– _theme.scss       # Тема по умолчанию
|   |– _admin.scss       # Тема админа
|   …                    # и т.д.
|
|– utils/
|   |– _variables.scss   # Переменные Sass
|   |– _functions.scss   # Функции Sass
|   |– _mixins.scss      # Примеси Sass
|   |– _helpers.scss     # Помощники классов & placeholder’ов
|
|– vendors/
|   |– _bootstrap.scss   # Bootstrap
|   |– _jquery-ui.scss   # jQuery UI
|   …                    # и т.д.
|
|
`– main.scss             # главный файл Sass
`– _shame.scss           # файл позора
```

#### Файл Main
```SASS
@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'utils/variables';
@import 'utils/functions';
@import 'utils/mixins';
@import 'utils/placeholders';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/cover';
@import 'components/dropdown';

@import 'pages/home';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';

@import 'shame';
```
