# JavaScript - основы синтаксиса

## Объяление функции
```javascript
function min(a, b) {
    return a < b ? a : b;
}

function main() {
    var s = 3;
    var t = 5;
    var min = min(s, t);
}
```

## Динамическая типизация
```javascript
function main() {
    var s = "Bender";
    var k = 1;
    var n = s.length;
}
```

## Циклы, условия if, for, while
```javascript
function main() {
    var s = "Bender";

    var result = "";

    for (var i = 0; i < s.length; i++) {
        result += s[i] + "";
    }
    if (result.length > 10) {
        alert(result);
    } else {
        while (result.length <= 10) {
            result += " ";
        }
        alert(result);
    }
}
```

## Исключения try-catch-finally
```javascript
function main() {
    try {
        var s = null;
        var n = s.length;
    } catch (e) {
        alert(e);
    }
}
```

## Массивы 
Массивы могут динамически растягиваться, при добавлении новых элементов и уменьшаться при их удалении. 
```javascript
function main() {
    var m = [1, 3, 18, 45, 'c', "roma", null];
    alert(m.length);
    //7

    m.push("end");
    alert(m.length);
    //8

    for (var i = 0; i < m.length; i++) {
        alert(m[i]);
    }
}
```

## Пустой массив
```javascript
var m = [];
```

## Объявление объектов. 
Чтобы создать новый объект достаточно написать две фигурные скобки «{}». 
Внутри скобок можно указать данные объекта в формате «ключ, двоеточие, значение, запятая». 
```javascript
function main() {
    var m = {
        first_name: "Bill",
        last_name: "Gates",
        age: 54,
        weight: 67,
        children: ["Emma", "Catrin"],
        wife: {
            first_name: "Melinda",
            last_name: "Gates",
            age: 45,
        }
    };

    alert(m.first_name);
    // Bill
    alert(m.age);
    // 54
    alert(m.wife.first_name);
    // Melinda

    m.age = 45;
    m.age++;
    m["first_name"] = "Stive";
    m["wife"] = null;
}
```

## К полям объекта можно обращаться двумя способами: 
Если указанного поля нет, оно создается.
```javascript
m.age = 45;
m[“age”] = 45;
```



