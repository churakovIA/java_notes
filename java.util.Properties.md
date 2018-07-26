## [Properties][1]
Это класс сохранения и загрузки настроек программы. Унаследован от `Hashtable<Object,Object>`

**Создать _Properties_**
```java
Properties prop = new Properties();
prop.put("ArchiveName", "e:/Short-term storage/archive.zip");
prop.put("FileName", "Казначейство_УстановкаЗаместителейСогласования.epf");
```

**Записать в файл**
```java
prop.store(new FileOutputStream("my.properties"), null);
```

**Загрузить из файла**
```java
prop.load(new FileInputStream("my.properties"));
//получить значение свойства
String ArchiveName = prop.getProperty("ArchiveName");
//вывести в консоль все свойства
prop.list(System.out);
```
**Некоторые методы _Properties_**

Метод | Описание
--- | ---
void load(Reader reader) |  Загружает свойства из файла, представленного объектом Reader
void load(InputStream inStream) |  Загружает свойства из файла, представленного объектом InputStream
void loadFromXML(InputStream in) |  Загружает свойства из XML-файла
Object get(Object key) |  Возвращает значение по ключу. Метод унаследован от HashTable
String getProperty(String key) |  Возвращает значение свойства (строку) по ключу.
String getProperty(String key, String defaultValue) |  Возвращает значение свойства по ключу или defaultValue, если такого ключа нет.
Set<String> stringPropertyNames() |  Возвращает список всех ключей

[1]: https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html
