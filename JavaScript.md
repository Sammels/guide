# JavaScript

## Table of Contents

  1. [Переменные](#Переменные)
  1. [Объекты](#Объекты)
  1. [Массивы](#Массивы)
  1. [Строки](#Строки)
  1. [Функции](#Функции)
  1. [Итераторы и генераторы](#Итераторы-и-генераторы)
  1. [Операторы сравнения и равенства](#Операторы-сравнения-и-равенства)
  1. [Блоки](#Блоки)
  1. [Пробелы](#Пробелы)
  1. [Соглашения по именованию](#Соглашения-по-именованию)
  1. [jQuery](#jquery)

Все примеры приводятся на ES6, чтобы им пользоваться уже сейчас, используйте [Babel](https://babeljs.io/)

## Переменные

  - Используйте `const` для всех переменных; избегайте использовать `var`.

    > Почему? Это гарантирует, что вы не можете переназначить ваши переменные, которые могут привести к ошибкам и трудно понять код.

    ```javascript
    // Плохо
    var a = 1;
    var b = 2;

    // Хорошо
    const a = 1;
    const b = 2;
    ```

  - Если вы должны переназначить переменную, то используйте `let` вместо `var`.

    ```javascript
    // Плохо
    var count = 1;
    if (true) {
      count += 1;
    }

    // Хорошо
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

## Объекты

  - Используйте короткую запись создания объекта.

    ```javascript
    // Плохо
    const item = new Object();

    // Хорошо
    const item = {};
    ```

  - Используйте короткую запись метода.

    ```javascript
    // Плохо
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // Хорошо
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  - Не вызывайте методы `Object.prototype` напрямую, например, `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.

  ```javascript
  // Плохо
  console.log(object.hasOwnProperty(key));

  // Хорошо
  console.log(Object.prototype.hasOwnProperty.call(object, key));

  // Лучше
  const has = Object.prototype.hasOwnProperty; //  кешируется поиск
  /* или */
  const has = require('has');
  …
  console.log(has.call(object, key));
  ```

## Массивы

  - Используйте короткую запись создания массива.

    ```javascript
    // Плохо
    const items = new Array();

    // Хорошо
    const items = [];
    ```

  - Используйте метод push`, вместо прямого добавления элемента в массив.

    ```javascript
    const someStack = [];

    // Плохо
    someStack[someStack.length] = 'abracadabra';

    // Хорошо
    someStack.push('abracadabra');
    ```

  - Используйте `...` для копирования массива.

    ```javascript
    // Плохо
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // Хорошо
    const itemsCopy = [...items];
    ```

  - Используйте `return` в callback. Если функция состоит из одного оператора, то `return` можно опустиить.

    ```javascript
    // Хорошо
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // Хорошо
    [1, 2, 3].map(x => x + 1);

    // Плохо
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
    });

    // Хорошо
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
      return flatten;
    });

    // Плохо
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // Хорошо
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

## Строки
  - Используйте одиночные ковычки `''` для строк.

    ```javascript
    // Плохо
    const name = "Capt. Janeway";

    // Плохо
    const name = `Capt. Janeway`;

    // Хорошо
    const name = 'Capt. Janeway';
    ```

  - Никогда не используй `eval()`, это открывает слишком много уязвимостей.

## Функции

  - Правильное объявление функции в блоке.

    ```javascript
    // Плохо
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // Хорошо
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  - Используйте дефолтные аргументы, не изменяйте их.

    ```javascript
    // Очень плохо
    function handleThings(opts) {
      // Нет! Нельзя изменять входящие программисты.
      // Если opts false, то переменная изменится
      // Это может привести к тонким ошибкам.
      opts = opts || {};
      // ...
    }

    // Все еще плохо
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // Хорошо
    function handleThings(opts = {}) {
      // ...
    }
    ```

  - Избегайте побочных эффектов.

    ```javascript
    var b = 1;
    // Плохо
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  - Всегда дефолтные аргументы располагайте в конце.

    ```javascript
    // Плохо
    function handleThings(opts = {}, name) {
      // ...
    }

    // Хорошо
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  - Пробелы в функциях

    ```javascript
    // Плохо
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // Хорошо
    const x = function () {};
    const y = function a() {};
    ```

  - Никогда не переназначайте входные аргументы

    ```javascript
    // Плохо
    function f1(a) {
      a = 1;
    }

    function f2(a) {
      if (!a) { a = 1; }
    }

    // Хорошо
    function f3(a) {
      const b = a || 1;
    }

    function f4(a = 1) {
    }
    ```

## Итераторы и генераторы

  - Не используйте итераторы. Используйте функции высшего порядка `for-in` or `for-of`

    > Почему? Чистые функции уменьшаются количество побочных эффектов.

    > Используйте `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... для перебора массива, и `Object.keys()` / `Object.values()` / `Object.entries()` для перебора массива и последующего создания массива.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // Плохо
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }

    sum === 15;

    // Хорошо
    let sum = 0;
    numbers.forEach(num => sum += num);
    sum === 15;

    // Лучше
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;
    ```

  - Не используйте генераторы

  - Если вам нужно использовать генераторы, но все равно не рекомендуем.

    ```js
    // Плохо
    function * foo() {
    }

    const bar = function * () {
    }

    const baz = function *() {
    }

    const quux = function*() {
    }

    function*foo() {
    }

    function *foo() {
    }

    // Очень плохо
    function
    *
    foo() {
    }

    const wat = function
    *
    () {
    }

    // Хорошо
    function* foo() {
    }

    const foo = function* () {
    }
    ```

## Операторы сравнения и равенства

  - Используйте `===` and `!==` вместо `==` and `!=`

  - Используйте корткую запись.

    ```javascript
    // Плохо
    if (name !== '') {
      // ...stuff...
    }

    // Хорошо
    if (name) {
      // ...stuff...
    }

    // Плохо
    if (collection.length > 0) {
      // ...stuff...
    }

    // Хорошо
    if (collection.length) {
      // ...stuff...
    }
    ```

  - Тернарное выражение не должно быть вложенным.

    ```javascript
    // Плохо
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // Лучше
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // Хорошо
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  - Избегайте ненужных тернарных выражений.

    ```javascript
    // Плохо
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // Хорошо
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

## Блоки

  - Используйте фигурные скобки.

    ```javascript
    // Плохо
    if (test)
      return false;

    // Хорошо
    if (test) return false;

    // Хорошо
    if (test) {
      return false;
    }

    // Плохо
    function foo() { return false; }

    // Хорошо
    function bar() {
      return false;
    }
    ```

## Пробелы

  - Для отступа используйте 2 пробелы.

    ```javascript
    // Плохо
    function foo() {
    ∙∙∙∙const name;
    }

    // Плохо
    function bar() {
    ∙const name;
    }

    // Хорошо
    function baz() {
    ∙∙const name;
    }
    ```

  - Должен быть 1 пробел перед открывающей фигурной скобки

    ```javascript
    // Плохо
    function test(){
      console.log('test');
    }

    // Хорошо
    function test() {
      console.log('test');
    }

    // Плохо
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // Хорошо
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  - Должен быть 1 пробел перед открывающей скобкой, кроме списком аргуметнов и имени функции.

    ```javascript
    // Плохо
    if(isJedi) {
      fight ();
    }

    // Хорошо
    if (isJedi) {
      fight();
    }

    // Плохо
    function fight () {
      console.log ('Swooosh!');
    }

    // Хорошо
    function fight() {
      console.log('Swooosh!');
    }
    ```

  - Отделяйте операторы пробелом.

    ```javascript
    // Плохо
    const x=y+5;

    // Хорошо
    const x = y + 5;
    ```

  - Используйте отступы при создании цепочки методов.

    ```javascript
    // Плохо
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // Плохо
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // Хорошо
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // Плохо
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // Хорошо
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // Хорошо
    const leds = stage.selectAll('.led').data(data);
    ```

  - Оставьте пустую строку после блоков.

    ```javascript
    // Плохо
    if (foo) {
      return bar;
    }
    return baz;

    // Хорошо
    if (foo) {
      return bar;
    }

    return baz;

    // Плохо
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // Хорошо
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // Плохо
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // Хорошо
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  - Не начинайте с пустой строки в блоке.

    ```javascript
    // Плохо
    function bar() {

      console.log(foo);

    }

    // Плохо
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // Хорошо
    function bar() {
      console.log(foo);
    }

    // Хорошо
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  - Не добавляйте пробелы внутри скобок.

    ```javascript
    // Плохо
    function bar( foo ) {
      return foo;
    }

    // Хорошо
    function bar(foo) {
      return foo;
    }

    // Плохо
    if ( foo ) {
      console.log(foo);
    }

    // Хорошо
    if (foo) {
      console.log(foo);
    }

    // Плохо
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // Хорошо
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  - Добавить пробелы в фигурные скобки.
  
    ```javascript
    // Плохо
    const foo = {clark: 'kent'};

    // Хорошо
    const foo = { clark: 'kent' };
    ```

  - Избегайте строк кода, которые длиннее 100 символов (включая пробелы).

    ```javascript
    // Плохо
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // Плохо
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // Хорошо
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // Хорошо
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

## Соглашения по именованию

  - Избегайте одиночные названия букв.

    ```javascript
    // Плохо
    function q() {
      // ...stuff...
    }

    // Хорошо
    function query() {
      // ..stuff..
    }
    ```

  - Используйте CamelCase при именовании объектов, функций, а также переменных.

    ```javascript
    // Плохо
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // Хорошо
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  - Используйте PascalCase только при именовании конструкторов или классов.

    ```javascript
    // Плохо
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // Хорошо
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

## jQuery

  - Используйте префик `$` в переменных, где лежит объект jQuery.

    ```javascript
    // Плохо
    const sidebar = $('.sidebar');

    // Хорошо
    const $sidebar = $('.sidebar');

    // Хорошо
    const $sidebarBtn = $('.sidebar-btn');
    ```

  - [25.2](#jquery--cache) Cache jQuery.

    ```javascript
    // Плохо
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // Хорошо
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  - Используйте find с умом.

    ```javascript
    // Плохо
    $('ul', '.sidebar').hide();

    // Плохо
    $('.sidebar').find('ul').hide();

    // Хорошо
    $('.sidebar ul').hide();

    // Хорошо
    $('.sidebar > ul').hide();

    // Хорошо
    $sidebar.find('ul').hide();
    ```
