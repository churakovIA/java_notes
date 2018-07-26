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

### Чтение системных настроек

```java
System.getProperties().list(System.out); // вывод в консоль системных properties
String uDir = System.getProperty("user.dir"); // получить системное свойство
```

Свойство | Описание
--- | ---
user.dir |  Текущий рабочий каталог для данной виртуальной машины
user.home |  Начальный каталог пользователя
user.name |  Наименование учетной записи пользователя
java.version |  Исполняемая версия Java для данной виртуальной машины
java.home |  Начальный каталог установки Java
java.class.path |  Путь к файлу класса, с помощью которого была запущена данная виртуальная машина
java.io.tmpdir |  Каталог для хранения временных файлов [например, /tmp)
os.name |  Наименование операционной системы (например, Linux)
os.arch |  Архитектура операционной системы (например, amd64)
os.version |  Версия операционной системы (например, 3.13.0-34-generic)
file.separator |  Разделитель файлов (знак / в Unix, знак \ в Windows)
path.separator |  Разделитель путей к файлам (знак : в Unix, знак ; в Windows) |  еще: java.io.File.separator
line.separator |  Разделитель новых строк (знаки \n в Unix, знаки \r\n в Windows)


[1]: https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html
