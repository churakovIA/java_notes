# JAXB - фреймворк для сериализации объектов java в xml

## Пример работы с JAXB

**Класс объекты которого подлежат сериализации**
```java
@XmlType(name = "cat")
@XmlRootElement
class Cat
{
 public String name;
 public int age;
 public int weight;

 Cat() { }
}
```

**Сериализация объекта в xml**
```java
public static void main(String[] args) throws JAXBException
{
 //создание объекта для сериализации в XML
 Cat cat = new Cat();
 cat.name = "Murka";
 cat.age = 5;
 cat.weight = 4;

 //писать результат сериализации будем в Writer(StringWriter)
 StringWriter writer = new StringWriter();

 //создание объекта Marshaller, который выполняет сериализацию
 JAXBContext context = JAXBContext.newInstance(Cat.class);
 Marshaller marshaller = context.createMarshaller();
 marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);
 // сама сериализация
 marshaller.marshal(cat, writer);

 //преобразовываем в строку все записанное в StringWriter
 String result = writer.toString();
 System.out.println(result);
}
```

**Результат сериализации**
```
<cat>
  <name>Murka</name>
  <age>5</age>
  <weight>4</weight>
</cat>
```

**Десериализация объекта из xml**
```java
public static void main(String[] args) throws JAXBException
{
 String xmldata = "<cat><name>Murka</name><age>5</age><weight>4</weight></cat>"";
 StringReader reader = new StringReader(xmldata);

 JAXBContext context = JAXBContext.newInstance(Cat.class);
 Unmarshaller unmarshaller = context.createUnmarshaller();

 Cat cat = (Cat) unmarshaller.unmarshal(reader);
}
```

## Аннотации

https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/annotation/package-frame.html
https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/annotation/adapters/package-frame.html

Аннотация | Применение | Описание
-- | -- | --
@XmlRootElement | class, enum | указывает на то, что этот объект может быть «корнем дерева» элементов в XML. Т.е. быть элементом самого верхнего уровня, все остальные элементы лежат в нем.
@XmlType(String name) | class, enum | указывает на то, что класс участвует в JAXB сериализации, в ней же задано имя, которое будет у XML-тега для этого класса
@XmlElements | field, metod | контейнер для нескольких @XmlElement
@XmlElement(String name) | field, metod, parameter | Поле будет представлено в XML элементом. Позволяет задать имя для тэга.
@XmlAttribute(String name) | field, metod | Поле будет представлено в XMLатрибутом. Позволяет задать имя для атрибута
@XmlElementWrapper(nillable = true) | field, metod | Позволяет задать «обрамляющий тег» для группы элементов
@XmlJavaTypeAdapter |  | Позволяет задать класс, который будет преобразовывать данные поля в строку
@XmlTransient |  | помечаются поля, которые не будут включены в маршалинг
@XmlSeeAlso |  | используется, когда в классе существует объект другого класса
@XmlEnum(Class<?>	value) |  | для перечислений
@XmlEnumValue |  | значение для полей в перечислении
@XmlAccessorType |  | что именно будет сериализовано
@XmlAnyElement |  | помечается поле-коллекция куда будут помещены при десериализации значения отсутствующие в классе
@XmlMimeType |  | mime-type для поля
@XmlMixed |  | смесь текста и тэгов

## Дополнительный материал
 - https://ru.wikipedia.org/wiki/Java_Architecture_for_XML_Binding
 - https://docs.oracle.com/javase/tutorial/jaxb/intro/
 - https://devcolibri.com/jaxb-%D0%B2%D0%B2%D0%B5%D0%B4%D0%B5%D0%BD%D0%B8%D0%B5/
 - **Java Методы программирования, 2013, (Блинов, Романчик)** Глава 14 стр.412
