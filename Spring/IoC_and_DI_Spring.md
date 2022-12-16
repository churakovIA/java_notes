# Инверсия управления и внедрение зависимостей в Spring

## Реализации интерфейса BeanFactory

- BeanFactory - ядро контейнера DI в Spring.
- Управляет жизненным циклом и зависмостями Spring Beans
- Интерфейс BeanDefinition - внутренняя конфигурация компонентов Spring Beans
- Классы PropertiesBeanDefinitionReader, XmlBeanDefinitionReader - читают BeanDefinition

```
	DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
	XmlBeanDefinitionReader rdr = new XmlBeanDefinitionReader(factory);
	rdr.loadBeanDefinitions(new ClassPathResource("spring/xml-bean-factory-config.xml"));
```

## Интерфейс ApplicationContext

- ApplicationContext расширяет BeanFactory - транзакции и АОП, источник сообщений \
для i18n, обработка событий в приложениях и пр.
- Загружается вручную или в среде веб-контейнера через класс ContextLoaderListener
- Конфигурируется через XML или аннотации
- Включить обработку аннотаций: <context:component-scan base-package="com.apress.**.annotation"/>
- Исключающий фильтр: <context:exclude-filter type="assignable" expression="com.example.NotAService"/>
- Варианты type: annotation, regex, assignable, aspectj или custom
- expression зависит от type
- GenericXmlApplicationContext - реализация ApplicationContext

```
GenericXmlApplicationContext ctx = new GenericXmlApplicationContext();
ctx.load("classpath:spring/app-context-xml.xml");
ctx.refresh();
```

## Конфигурирование на языке Java (JavaConfig)

- @Configuration - помечается конфигурационный класс
- @Bean - помечается метод возвращающий Spring Bean
- Имя Spring Bean будет совпадает с именем метода
- AnnotationConfigApplicationContext - реализация ApplicationContext

```
ApplicationContext ctx = new AnnotationConfigApplicationContext(HelloWorldConfiguration.class);
```

- @ComponentScan - включить обработку аннотаций

```
@ComponentScan(basePackages = {"com.apress.prospring5.ch3.annotated"})
@Configuration
public class HelloWorldConfiguration {
}
```

- @ImportResource - загружает конфигурацию из XML

```
@ImportResource(locations = {"classpath:spring/app-context-xml.xml"})
@Configuration
public class HelloWorldConfiguration {
}
```

## Внедрение зависимостей через сеттер

- В XML зависимость внедряется через дескриптор `<property>` внутри `<bean>`:

```
<bean id="renderer"
class="com.apress.prospring5.ch2.decoupled.StandardOutMessageRenderer">
<property name="messageProvider" ref="provider"/>
</bean>
```

- Или тоже самое (пространство имен p):

```
<bean id="renderer"
class="com.apress.prospring5.ch2.decoupled.StandardOutMessageRenderer">
p:messageProvider-ref="provider"/>
</bean>
```

- Через аннотацию @Autowired
- Аналогично @Resource(name="messageProvider") - JSR-250
- Аналогично @Inject - JSR-299

```
@Autowired
public void setMessageProvider(MessageProvider provider) {
	this.messageProvider = provider;
}
```

## Внедрение зависимостей через конструктор

- В XML зависимость внедряется через дескриптор `<constructor-arg>` внутри `<bean>`:
- атрибут value для внедрения простого значения, ref - для бина
- атрибут index используется когда в конструкторе несколько аргументов
- атрибут type для уточнения типа аргумента

```
<bean id="messageProvider"
class="com.apress.prospring5.ch3.xml.ConfiguraЬleMessageProvider">
<constructor-arg value="I hope that someone gets ту message in а bottle"/>
</bean>

<bean id="constructorConfusion"
	class="com.apress.prospring5.ch3.xml.ConstructorConfusion">
	<constructor-arg type="int">
		<value>90</value> 
	</constructor-arg> 
</bean>
```

- Или тоже самое (пространство имен с):
- _0 индекс аргумента конструктора
- можно по имени: <bean class=... c:message=".../>

```
<bean id="message" class="java.lang.String"
	  c:_0="I hope that someone gets my message in a bottle"/>
```

- Через аннотацию @Autowired
- Применяется только к одному конструктору

## Внедрение зависимостей через поле

- Через аннотацию @Autowired
- Поле может быть приватным

```
@Service("singer")
public class Singer {
	@Autowired
	private Inspiration inspirationBean;
	...
}
```


## Наследование бинов спринг

 - задается атрибутом <bean ... parent="parent" ... />
 - наследуются аргументы конструктора и значения полей
 - можно использовать как шаблон
 - abstract="true" чтобы скрыть родительский бин в контексте 
 

```
<beans ... >
	<bean id="parent"
		class="com.apress.prospring5.ch3.xml.Singer"
		p:name="John Mayer" p:age="39" abstract="true"/>
	<bean id="child"
		class="com.apress.prospring5.ch3.xml.Singer" parent="parent" 
		p:age="O"/>
</beans>
```

