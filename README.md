1)
```js
let promiseTwo = new Promise((resolve, reject) => {
   resolve("a");
});

promiseTwo
.then((res) => {
   return res + "b";
})
.then((res) => {
   return res + "с";
})
.finally((res) => {
   return res + "!!!!!!!";
})
.catch((res) => {
   return res + "d";
})
.then((res) => {
   console.log(res); // abc
});
```
2)
```js
function doSmth() {
   return Promise.resolve("123");
}

doSmth()
.then(function (a) {
   console.log("1", a); // 1 123
   return a;
})
.then(function (b) {
   console.log("2", b); // 2 123
   return Promise.reject("321");
})
.catch(function (err) {
   console.log("3", err); // 3 321
})
.then(function (c) {
   console.log("4", c); // 4 undefined
return c;
});
```
3) Напишите функцию, которая будет проходить через массив целых чисел и выводить индекс каждого элемента с задержкой в 3 секунды.
Входные данные: [10, 12, 15, 21]
```js
const delyLog = (arr) => {
    for (let i in arr) {
        setTimeout(() => console.log(i), 3000 + 3000 * i);
    }
}
```
4) Прочитать про Top Level Await (можно ли использовать await вне функции async)

await можно использовать вне функции async в ES-модулях.
Например, можно использовать при импорте модуля с динамическим путем
```js
const strings = await import(`/i18n/${navigator.language}`);
```
Для инициализации ресурсов
```js
const connection = await dbConnector();
```
Для загрузки зависимости с реализацией запасного варианта
```js
let jquery;

try {
  jquery = await import('https://my-server.com/api/jquery.js');
} catch {
  jquery = await import('https://unpkg.com/jquery@3.3.1/dist/jquery.js');
}

const $ = jquery.default;
```

БОНУС ЗАДАНИЕ 
/* Необходимо реализовать функцию fetchUrl, которая будет использоваться следующим образом.
Внутри fetchUrl можно использовать условный метод fetch, который просто возвращает
Promise с содержимым страницы или вызывает reject */
fetchUrl('https://google/com&#39;)
.then(...)
.catch(...) // сatch должен сработать только после 5 неудачных попыток
получить содержимое страницы внутри fetchUrl
```js
function fetchUrl(url, attempts = 5) {
    return fetch(url)
        .then(response => response.text())
        .catch(error => {
            if (attempts) {
                return fetchUrl(url, attempts - 1);
            }
            return Promise.reject(error)
        });
}
```