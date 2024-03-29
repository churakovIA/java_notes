# Какие ограничения накладываются на ключ для HashMap, кроме необходимости переопределения equals и hashCode? Как сделать класс immutable?
---

## Почему нельзя использовать byte[] в качестве ключа в HashMap?

Хэш-код массива не зависит от хранимых в нем элементов, а присваивается при создании массива 
(метод вычисления хэш-кода массива не переопределен и вычисляется по стандартному Object.hashCode() на основании адреса 
массива). Так же у массивов не переопределен equals и выполняется сравнение указателей. 
Это приводит к тому, что обратиться к сохраненному с ключом-массивом элементу не получится при использовании другого 
массива такого же размера и с такими же элементами, доступ можно осуществить лишь в одном случае — при использовании 
той же самой ссылки на массив, что использовалась для сохранения элемента.

## Immutable vs Mutable class

__Изменяемый объект (mutable)__ - можно изменить состояние и поля после создания объекта. Например: `StringBuilder`, `java.util.Date` и т.д.

__Неизменяемый объект (immutable)__ - нельзя ничего изменить после создания объекта. Например: `String`, `Integer`, `Byte` и т.д.

### Как сделать класс immutable?

```
public final class Student {

    private final int id; 
    private final String name; 
    private final Address address;

    public Student(int id, String name, Address address) {
        this.id = id;
        this.name = name;
        this.address = new Address(address.getCity(), address.getStreet(), ...);
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public Address getAddress() {
        return new Address(address.getCity(), address.getStreet(), ...);
    }
}
```
* Объявляем класс как final, чтобы от него нельзя было наследоваться.
* Делаем все поля private, чтобы закрыть прямой доступ.
* Помечаем все поля final для того, чтобы их значение можно было установить только единожды;
* Не используем сеттеры, используем только конструктор;
* Для полей, которые НЕ являются примитивом или immutable классом, в геттере необходимо возвращать копию объекта, для того, 
чтобы никто извне не мог поменять его значение. То же самое в конструкторе.