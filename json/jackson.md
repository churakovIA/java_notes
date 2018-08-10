# Jackson - фрейворк для работы с json
Класс [ObjectMapper (com.fasterxml.jackson.databind.ObjectMapper)][2] обеспечивает сериализация/десериализацию json.
```java
ObjectMapper mapper = new ObjectMapper();
```

## Пример класса для сериализации в json
- поля должны быть видимые: или public или иметь getter’ы и setter’ы
- должен быть конструктор по умолчанию (без параметров)
```java
// Note: can use getters/setters as well; here we just use public fields directly:
public class MyValue {
  public String name;
  public int age;
  // NOTE: if using getters/setters, can keep fields `protected` or `private`
}
```

## Десериализация JSON

### Десериализация объекта из файла
```java
public static <T> T convertFromJsonToNormal(String fileName, Class<T> clazz) throws IOException {
    ObjectMapper mapper = new ObjectMapper();
    return mapper.readValue(new File(fileName), clazz);
}
```

### Десериализация из разных источников
```java
MyValue value = mapper.readValue(new File("data.json"), MyValue.class);
// or:
value = mapper.readValue(new URL("http://some.com/api/entry.json"), MyValue.class);
// or:
value = mapper.readValue("{\"name\":\"Bob\", \"age\":13}", MyValue.class);
```

## Сериализация json
```java
mapper.writeValue(new File("result.json"), myResultObject);
// or:
byte[] jsonBytes = mapper.writeValueAsBytes(myResultObject);
// or:
String jsonString = mapper.writeValueAsString(myResultObject);
// or:
StringWriter writer = new StringWriter();
mapper.writeValue(writer, myResultObject);
```

### Форматировать выходной json
```java
System.out.println(mapper.writerWithDefaultPrettyPrinter().writeValueAsString(raceBike));
//{
//    "name" : "Simba",
//    "owner" : "Peter",
//    "age" : 2
//}
```

---

## Аннотации

[Полный список jackson аннотаций][4]\
[Простые примеры jackson аннотаций][5]\
[Javadocs 2.9][6]


Аннотация | Описание
--- | ---
@JsonAutoDetect | Ставится перед классом. | Помечает класс как готовый к сериализациив JSON.
@JsonIgnore | Ставится перед свойством. Свойство игнорируется при сериализации.
@JsonProperty | Ставится перед свойством или getter’ом или setter’ом. Позволяет задать другое имя поля при сериализации.
@JsonWriteNullProperties | Ставится перед классом. Поля объекта, которые равны null не будет игнорироваться.
@JsonPropertyOrder | Ставится перед классом. Позволяет задать порядок полей для сериализации.

### Пример с аннотациями 
```java
@JsonAutoDetect
class Cat{
    @JsonProperty("alias")
    public String name;
    public int age;
    @JsonIgnore
    public int weight;

    Cat() {}
}
```

### Указываем тип для десериализации 
```java
@JsonAutoDetect
class Cat{
    public String name;
    @JsonDeserialize(as = ArrayList.class, contentAs = Cat.class)
    // для map "keyAs" вместо "contentAs": @JsonDeserialize(keyAs=KeyTypeImpl.class)
    public List<Cat> cats = new ArrayList<>();
    Cat() {}
}
```

### @JsonFormat
Используется для указания способа форматирования полей и/или свойств для вывода JSON.
В частности, эта аннотация позволяет указать, как форматировать значения даты и календаря в соответствии с форматом `SimpleDateFormat`.
```java
@JsonFormat(pattern = "dd-MM-yyyy hh:mm:ss")
public Date eventDate;
//"eventDate" : "10-08-2018 13:04:46"
```

### @JsonAnyGetter
Этой аннотацией помечается геттер возвращающий `map`, чтобы ее элементы возвращались как свойства объекта.
```java
@JsonAnyGetter
public Map<String, Object> getAdditionalMap() {
    return additionalMap;
}
//без аннотации: 
//{
//  "id" : 1,
//  "name" : "first",
//  "additionalMap" : {
//    "KEY#1" : "VALUE#1",
//    "KEY#3" : "VALUE#3",
//    "KEY#2" : "VALUE#2"
//  }
//}
//с аннотацией:
//{
//    "id" : 1,
//    "name" : "first",
//    "KEY#1" : "VALUE#1",
//    "KEY#3" : "VALUE#3",
//    "KEY#2" : "VALUE#2"
//}
```

### Пример аннотации, которая позволяет управлять процессом «полиморфной десериализации»
```java
@JsonTypeInfo(use = JsonTypeInfo.Id.NAME, property="type")
@JsonSubTypes({
        @JsonSubTypes.Type(value=Cat.class, name="cat"),
        @JsonSubTypes.Type(value=Dog.class, name="dog")
})
class Pet{
    public String name;
}

class Cat extends Pet{
    public int age;
}

class Dog extends Pet{
    public int age;
    public String owner;
}

class House
{
    public List<Pet> pets = new ArrayList<>();
}
```

### Отключить использование аннотаций
```java
mapper.disable(MapperFeature.USE_ANNOTATIONS);
```
---

## Дополнительный материал
[Главная страница на GitHub (jackson-databind)][3] много хороших примеров\
[Javadocs (jackson-databind)][1]


[1]: https://github.com/FasterXML/jackson-databind/wiki
[2]: http://fasterxml.github.io/jackson-databind/javadoc/2.9/com/fasterxml/jackson/databind/ObjectMapper.html
[3]: https://github.com/FasterXML/jackson-databind
[4]: https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations
[5]: https://github.com/FasterXML/jackson-annotations
[6]: http://fasterxml.github.io/jackson-annotations/javadoc/2.9
