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


[1]: https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html
