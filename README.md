# JS-33
1) Какие бывают алгоритмы сортировок ?

- Сортировка пузырьком - О(n^2);
- Быстрая сортировка   - O(n*log n);
- Сортировка вставками - O(n^2);
- Соритровка слиянием  - O(n*log n); 


2) Прочитать про "Операторы и выражения, циклы в JS"
3) Создать объект Person несколькими способами, после создать объект Person2, чтобы в нём были доступны методы объекта Person. Добавить метод logInfo чтоб он был доступен всем объектам.

```js
function Person(name){
    this.name = name;
};

const person0 = new Person('Gleb');
const person1 = Object.create(Person.prototype);
const person2 = {};
Object.setPrototypeOf(person2, Person.prototype);

person1.name = 'Max';
person2.name = 'Ben';

Person.prototype.logInfo = function(){
    console.log(this.name);
};

person0.logInfo(); // Gleb
person1.logInfo(); // Max
person2.logInfo(); // Ben
```

4) Создать класс PersonThree c get и set для поля name и конструктором, сделать класс наследник от класса Person.

```js
class Person{
    constructor(name){
        this.name = name;
    }

    getName(){
        return this.name;
    }

    setName(newName){
        this.name = newName;
    }
};

class PersonThree extends Person{
    constructor(name){
        super(name);
    }
}

const person = new PersonThree('Gleb');

console.log(person.getName()); // Gleb
person.setName('Max');
console.log(person.getName()); // Max
```

БОНУС: 
1) Написать функцию, которая вернет массив с первой парой чисел, сумма которых равна total:
```js
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
total = 13;
//result = [4, 9]

const firstSum = (arr, total) => {
    let l = 0, r = arr.length - 1;
    while(l != r){
        let sum = arr[l] + arr[r];
        if(sum === total){
            return [arr[l], arr[r]];
        }

        if (sum > total){
            r--;
        }
        else if (sum < total){
            l++;
        }
    }
    return [];
}

firstSum(arr,total)
```
2) Какая сложность у вашего алгоритма ?

O(n)