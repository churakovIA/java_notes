# RMI - удаленный вызов процедур

RMI расшифровывается Remote Method Invokation – удаленный вызов методов. 
Или другими словами RMI – это механизм, который позволяет объекту в одной Java-машине вызывать методы объекта в другой Java-машине, даже если они находятся на разных компьютерах.

![](https://javarush.ru/images/lectures/image-ru-32-01.png)

**Чтобы программы могли взаимодействовать через интернет, необходимы настройки в правах Java-машины**

В Java удаленно можно вызывать только методы интерфейсов, но не классов.

---
>**Интерфейс для межпрограммного взаимодействия**
```java
interface Reverse extends Remote // Remote - маркерный интерфейс
{
 public String reverse(String str) throws RemoteException;
}
```

>**Класс реализующий интерфейс**
```java
class ReverseImpl implements Reverse
{
 public String reverse(String str) throws RemoteException
 {
  return new StringBuffer(str).reverse().toString();
 }
}
```

>**Код сервера. На порту 2099, сервер создаёт и запускает RMI реестр.**
```java
public static final String UNIC_BINDING_NAME = "server.reverse";

public static void main(String[] args) throws Exception
{
 //создание объекта для удаленного доступа
 final ReverseImpl service = new ReverseImpl();

 //создание реестра расшареных объетов
 final Registry registry = LocateRegistry.createRegistry(2099);
 //создание "заглушки" – приемника удаленных вызовов
 Remote stub = UnicastRemoteObject.exportObject(service, 0);
 //регистрация "заглушки" в реесте
 registry.bind(UNIC_BINDING_NAME, stub);

 //усыпляем главный поток, иначе программа завершится
 while (true) {
			Thread.sleep(Integer.MAX_VALUE);
 }
}
```

>**Работа с удаленным объектом. Код клиента**
```java
public static final String UNIC_BINDING_NAME = "server.reverse";

public static void main(String[] args) throws Exception
{
 //получение реестра расшареных объетов
 Registry registry = LocateRegistry.getRegistry("localhost", 2099);

 //получаем объект (на самом деле это proxy-объект)
 Reverse service = (Reverse) registry.lookup(UNIC_BINDING_NAME);

 //Вызываем удаленный метод
 String result = service.reverse("Home sweet home.");
}
```

---

>**Дополнительный материал** \
https://javatalks.ru/topics/8059 \
https://habr.com/post/74639/ \
http://javatutor.net/books/tiej/rmi \
http://java-online.ru/java-rmi.xhtml \
https://www.intuit.ru/studies/courses/633/489/lecture/11079 \
https://javarush.ru/quests/lectures/questcollections.level02.lecture09
