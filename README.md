# JS-33
Задание 1 – Создать объект counter всеми возможными способами;
```
let counter = {count: 0};
let counter = Object({count: 0});
let counter = new Object({count: 0});
let counter = Object.create({count: 0});
let counter = Object.assign({count: 0});
```
Задание 2 – Скопировать объект counter всеми
возможными способами;
```
let newCounter = {...counter};
let newCounter = deepCopy(counter);
let newCounter = Object.assign(counter);
let newCounter = JSON.parse(JSON.strinify(counter));

const deepCopyArr = (arr) => {
    let newArr = [];
    for(let el of arr){
        if(el instanceof Array){
            newArr.push(deepCopyArr(el));
            continue;
        }
        else if (el instanceof Date) {
            newArr.push(new Date(el.getTime()));
        }
        else if(el === null || typeof el !== 'object'){
            newArr.push(el);
        }
        else if(typeof el === 'object'){
            newArr.push(deepCopy(el));
        }
    }
    return newArr;
};

const deepCopy = (obj) => {
    let newObject = {};
    for (let key of Object.keys(obj)){
        if(obj[key] instanceof Array){
            newObject[key] = deepCopyArr(obj[key]);
        }
        else if (obj[key] instanceof Date) {
            newObject[key] = new Date(obj[key].getTime());
        }
        else if(obj[key] === null || typeof obj[key] !== 'object'){
            newObject[key] = obj[key];
        }
        else if(typeof obj[key] === 'object'){
            newObject[key] = deepCopy(obj[key]);
        }
    }
    return newObject;
};

class Counter{
    constructor(count = 0){
        this.count = count;
    }

    getCount(){
        return this.count;
    }
}

Counter.prototype.copy = function(){
    return new Counter(this.getCount());
}

let counter = new Counter();
let newCounter = counter.copy();
```
Задание 3 – Создать функцию makeCounter всеми описанными и возможными способами;
```
function makeCounter(){
    return {count: 0};
}

let makeCounter = function(){
    return {count: 0};
};

let makeCounter = function makeNewCounter() { 
    return {count: 0}; 
};

let makeCounter = () => { return {count: 0}; };
```
Бонус
Задание 1 –
Написать функцию глубокого сравнения двух объектов:

```
const obj1 = { here: { is:
"on", other: "3" }, object: "Y" };

const obj2 = { here: { is:
"on", other: "2" }, object: "Y" };

const arrayEqual = (arr1, arr2) => {
    return  (arr1.length == arr2.length) && arr1.every(function(element, index){ return element === arr2[index];
    })
};

const deepEqual =
(obj1, obj2) => {
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    let result = arrayEqual(keys1.sort(), keys2.sort());
    
    for(let key of keys1){
        if(!result) { return result; }
        
        if(obj1[key] instanceof Array){
            result = result && obj2[key] instanceof Array && arrayEqual(obj1[key], obj2[key]);
            continue;
        }
        else if (obj1[key] instanceof Date) {
            result = result && obj2[key] instanceof Date && obj1[key].getTime() === obj2[key].getTime();
            continue;
        }
        else if(obj1[key] instanceof Function){
            result = result && obj2[key] instanceof Function;
            continue;
        }
        else if(typeof obj1[key] === 'object'){
            result = result && typeof obj2[key] === 'object' && deepEqual(obj1[key], obj2[key]);
            continue;
        }
        result = result && (obj1[key] === obj2[key]);
    }
    return result;
};
```

Бонус 
Задание 2 –
Развернуть строку в обратном направлении при помощи методов массивов:
```
function reverseStr(str) {
    return Array.from(str).reverse().join('');
}
```
