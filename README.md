# JS-33
1) Написать ответ - почему массивы в JS являются "неправильными" и совмещают в себе несколько структур данных? Какие ?

Массив в JS позволяет изменять длину и позволяет хранить различные типы данных.
Массив совмещает в себе следущие структуры данных: стэк, очередь,
двустронняя очередь,  упорядоченный список.

2) Привязать контекст объекта к функции logger, чтобы при вызове this.item выводило - some value (Привязать через bind, call, apply)
```javascript
function logger() {
    console.log(`I output only external context: ${this.item}`);
}

const obj = { item: "some value" };

const newLogger = logger.bind(obj);
logger.call(obj);
logger.apply(obj);
newLogger();
```
Бонус задание: Реализовать полифил(собственную функцию реализующую встроенную в js) метода bind()
```js
Function.prototype.myBind = function(ctx, ...arg){
    return () => {
        return this.apply(ctx, arg);
    }
}
```