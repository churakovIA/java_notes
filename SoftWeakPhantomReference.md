# Soft [Weak | Phantom] Reference

 - _SoftReference_ – мягкая ссылка.
 - _WeakReference_ – слабая ссылка.
 - _PhantomReference_ – призрачная ссылка

Используются для более эффективной работы с памятью. Сборщик мусора по-разному влияет на объекты имеющие такие ссылки.

## [SoftReference](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/SoftReference.html)
Если на объект существуют только мягкие ссылки, то он продолжает жить и называется «мягкодостижимым».
Но! Объект, на который ссылаются только мягкие ссылки, может быть удален сборщиком мусора, если программе не хватает памяти. 
Если программе вдруг не хватает памяти, прежде чем выкинуть `OutOfMemoryException`, сборщик мусора удалит все объекты, 
на которые ссылаются мягкие ссылки и попробует выделить программе память еще раз.
Эти ссылки были специально придуманы для кэширования, хотя их можно использовать и для других целей.

```java
//создание объекта Cat
Cat cat = new Cat();
//создание мягкой ссылки на объект Cat
SoftReference<Cat> catRef = new SoftReference<Cat>(cat);
//теперь на объект ссылается только мягкая ссылка catRef.
cat = null;
//теперь на объект ссылается еще и обычная переменная cat
cat = catRef.get();
//очищаем мягкую ссылку
catRef.clear();
```

## [WeakReference ](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/WeakReference.html)

Если на объект не осталось обычных ссылок и мягких ссылок, а только слабые ссылки, то этот объект является живым, 
но он будет уничтожен при ближайшей сборке мусора.

```java
//создание объекта Cat
Cat cat = new Cat();

//создание слабой ссылки на объект Cat
WeakReference<Cat> catRef = new WeakReference<Cat>(cat);

//теперь на объект ссылается только слабая ссылка catRef.
cat = null;

//теперь на объект ссылается еще и обычная переменная cat
cat = catRef.get();

//очищаем слабую ссылку
catRef.clear();
```

[WeakHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/WeakHashMap.html) – это HashMap, у которого ключи – это слабые ссылки – WeakReference.
Пока на объекты, которые ты хранишь в WeakHashMap в качестве ключей есть обычные (сильные или мягкие) ссылки, эти объекты будут живы.
Когда объекты, используемые в качестве ключей, станут слабодостижимыми, они уничтожатся при ближайшей сборке мусора. 
А значит, из WeakHashMap автоматически удалятся и их значения.\
В `WeakHashMap` очень удобно хранить дополнительную информацию к каким-то объектам.

```java
//создаем объект для хранения дополнительной информации о пользователе
WeakHashMap<User, StatisticInfo> userStatistics = new WeakHashMap<User, StatisticInfo>();

//кладем информацию о пользователе в userStatistics
User user = session.getUser();
userStatistics.put(user, new StatisticInfo (…));

//получаем информацию о пользователе из userStatistics
User user = session.getUser();
StatisticInfo statistics = userStatistics.get(user);

//удаление любой информации о пользователе из userStatistics
User user = session.getUser();
userStatistics.remove(user);
```

## [PhantomReference](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/PhantomReference.html)
Призрачные(Phantom) ссылки – это самые слабые ссылки из всех. 
Только если на объект не остаётся никаких ссылок вообще, кроме призрачных, их механизм вступает в действие.

```java
//специальная очередь для призрачных объектов
ReferenceQueue<Integer> queue = new ReferenceQueue<Integer>();

//список призрачных ссылок
ArrayList<PhantomReference<Integer>> list = new ArrayList<PhantomReference<Integer>>();

//создаем 10 объектов и добавляем их в список через призрачные ссылки
for ( int i = 0; i < 10; i++)
{
 Integer x = new Integer(i);
 list.add(new PhantomReference<Integer>(x, queue));
}
```

[ReferenceQueue](https://docs.oracle.com/javase/8/docs/api/java/lang/ref/ReferenceQueue.html) - очередь призрачных ссылок

При уничтожении объекта, удерживаемого призрачной ссылкой, он уничтожается, но не удаляется из памяти!

Если на объект остаются только призрачные ссылки, то вот что его ждет:
1. Во время ближайшей сборки мусора у объекта будет вызван метод `finalize()`. Но, если метод `finalize()` не был переопределен, этот шаг пропускается, а выполнится сразу шаг 2.
2. Во время следующей сборки мусора, объект будет помещен в специальную очередь призрачных объектов, из которой будет удален, когда у `PhantomReference` вызовут метод `clear()`.

Метод `get()` у `PhantomReference` всегда возвращает `null`.

**Эта нить будет следить за призрачной очередью и удалять оттуда объекты**
```java
Thread referenceThread = new Thread(){
 public void run() {
  while (true)  {
   try   {
    //получаем новый объект из очереди, если объекта нет - ждем!
    PhantomInteger ref = (PhantomInteger)queue.remove();
    //вызвваем у него метод close
    ref.close();
    ref.clear();
   }
   catch (Exception ex)   {
    // пишем в лог ошибки
   }
  }
 }
};
//запускаем поток в служебном режиме.
referenceThread.setDaemon(true);
referenceThread.start();
```

**Это класс, унаследованный от PhantomReference, у него есть метод close()**
```java
static class PhantomInteger extends PhantomReference<Integer>{
 PhantomInteger(Integer referent, ReferenceQueue<? super Integer> queue) {
  super(referent, queue);
 }

 private void close() {
  System.out.println("Bad Integer totally destroyed!");
 }
}
```
