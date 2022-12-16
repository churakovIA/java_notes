# Вызов обработчика при создании бина спринг

Можно вызывать метод после того как бин будет проинициализирован.
Метод без аргументов. Может быть статическим и возвращать значения, 
но они игнорируются.

**XML**

*XML (атрибут init-method дескриптора <bean>):*
```
<bean class="com.apress.prospring5.ch4.Singer" init-method="init"/>

class Singer{
	void init(){/*тут что-то делаем*/}
}
```

Задать метод для всех бинов в xml файле конфигурации:
атрибут default-init-method="init" дескриптора <beans>
```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	...
	default-init-method="init">
```

Ленивая загрузка бинов: <beans ... default-lazy-init="true">

**Интерфейс _InitializingBean_**

Вызывается метод afterPropertiesSet() после инициализации бина.
```
public class SingerWithInterface implements InitializingBean {
    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("Initializing bean");
	}
}
```

**@PostConstruct по спецификации ]SR-250**

- Имя метода произвольное.
- Метод может быть приватным.

```
public class SingerWithJSR250 {
    @PostConstruct
    private void init() throws Exception {
        System.out.println("Initializing bean");
	}
}
```

**Java config**

 - Метод инициализации в аннотации @Bean(initMethod = "init")
 - @Lazy - ленивая инициализация бина

```
@Configuration
static class SingerConfig{
	@Lazy
	@Bean(initMethod = "init")
	Singer singerOne() {
		Singer singerOne = 	new Singer();
		singerOne.setName("John Mayer");
		singerOne.setAge(39);
		return singerOne;
	}
}
```

Spring сначала вызывает метод, снабженный аннотацией @PostConstruct, 
затем метод afterPropertiesSet(),
а далее - метод инициализации, указанный в файле конфигурации.