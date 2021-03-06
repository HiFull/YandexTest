<h1>Ответ на вопрос:</h1>

<ol><b>Примечания к происходящему</b>
  <li>У нас есть функция-конструктор Ticker.</li>
  <li>
    Мы задали prototype Ticker, чтобы при создании потомков от Ticker, они
    ссылались на прототип родительского объекта, на его метод. Таким образом мы экономим память,
    ибо у нас есть общий метод, а не отдельный у каждого потомка.
  </li>
  <li>Создали экземпляр ticker от Ticker.</li>
  <liПередали метод .tick в setInterval с интервалом в 1 секунду.</li>
  <li>
    setInterval выдаёт NaN в консоли, потому что мы передаём функцию как объект, но не её контекст,
    таким образом этот самый контекст выполнения функции теряется и программа работает некорректно.
  </li>
</ol>

<h2>Решения:</h2>
<ul>
  <li>
    Передать в setInterval функцию обёртку для ticker.tick. Произойдет замыкание и всё будет работать корректно =>
    
    ```
    setInterval(function() {
      ticker.tick();
    }, 1000);
    ```
    
  </li>
  <li>
    Встроенные средства JS позволяют привязывать контекст выполнения функции built-in методом .bind().Он привязывает контекст к функции.
    Таким образом, мы передадим в setInterval вызов метода ticker с привязкой к контексту объекта =>
  
    ```
    setInterval(ticker.tick.bind(ticker), 1000);
    ```
    
  </li>
</ul>
