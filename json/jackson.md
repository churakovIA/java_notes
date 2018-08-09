# Jackson - фрейворк для работы с json
Класс [ObjectMapper (com.fasterxml.jackson.databind.ObjectMapper)][2] обеспечивает сериализация/десериализацию json.

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
```java
MyValue value = mapper.readValue(new File("data.json"), MyValue.class);
// or:
value = mapper.readValue(new URL("http://some.com/api/entry.json"), MyValue.class);
// or:
value = mapper.readValue("{\"name\":\"Bob\", \"age\":13}", MyValue.class);
```

## Сериализация JSON
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

---

## Аннотации
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


---

## Дополнительный материал
[Главная страница на GitHub (jackson-databind)][3] много хороших примеров\
[Javadocs (jackson-databind)][1]


[1]: https://github.com/FasterXML/jackson-databind/wiki
[2]: http://fasterxml.github.io/jackson-databind/javadoc/2.9/com/fasterxml/jackson/databind/ObjectMapper.html
[3]: https://github.com/FasterXML/jackson-databind
