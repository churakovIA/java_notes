# Работа с Zip - архивами
---
[ZipEntry][3] - класс описавающий файл в zip-архиве
```java 
ZipEntry entry = new ZipEntry("bigtext.txt");
```
---
[ZipOutputStream][2] - поток записи в zip-архив
```java
// создаем поток записи в zip-архив
try(ZipOutputStream zip = new ZipOutputStream(new FileOutputStream("archive.zip"))){
    // открываем новую запись в архиве, позиционирует на нее поток
    zip.putNextEntry(new ZipEntry("project/readme.txt")); 
    // пишем из файла в поток zip-архива
    Files.copy(Paths.get("c:/project/readme.txt"), zip); 
}
```
---
[ZipInputStream][1] - поток чтения из zip-архива
```java
//создаем поток чтения из zip
try(ZipInputStream zip = new ZipInputStream(new FileInputStream("archive.zip"))){
    ZipEntry entry;
    //последовательно получаем записи из архива
    while((entry = zip.getNextEntry()) != null){
        //пишем из zip потока в файл
        Files.copy(zip, Paths.get("e:/target/" + entry.getName()), StandardCopyOption.REPLACE_EXISTING);
    }
}
```

[1]: https://docs.oracle.com/javase/8/docs/api/java/util/zip/ZipInputStream.html
[2]: https://docs.oracle.com/javase/8/docs/api/java/util/zip/ZipOutputStream.html
[3]: https://docs.oracle.com/javase/8/docs/api/java/util/zip/ZipEntry.html