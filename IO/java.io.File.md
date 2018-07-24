# Ввод и вывод. Класс [**java.io.File**](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)
Класс предназначен для манипуляции файлами и каталогами, чтения и установки атрибутов. Файлы можно создавать, удалять, переименовывать и т.п..
### Методы анализа файла
Метод | Описание
--- | ---
boolean isDirectory() | Является ли «объект файла» директорией
boolean isFile() | Является ли объект файлом
Ьoolean isHidden() | Является ли файл скрытым
long length() | Возвращает размер/длину файла в байтах.
boolean exists() | Возвращает true, если файл с таким именем существует на диске компьютера.
String getAbsolutePath() | Возвращает полный путь файла со всеми поддиректориями.
String getCanonicalPath() | Возвращает канонический путь файла. Например, преобразовывает путь «c:/dir/dir2/../a.txt» к пути «c:/dir/a.txt»
String getName() | Возвращает только имя файла, без пути.
String getParent() | Возвращает только путь (директорию) к текущему файлу, без самого имени.
File getParentFile() | Возвращает только путь (директорию) к текущему файлу как объект **File**
### Манипулирование файлами
Метод | Описание
--- | ---
boolean createNewFile() | Создает файл. Если такой файл уже был, возвращает false.
boolean delete() | Удаляет файл объекта на диске. Если объект – директория, то только, если в ней нет файлов.
void deleteOnExit() | Добавляет файл в специальный список файлов, которые будут автоматически удалены при закрытии программы.
File createTempFile(String prefix, String suffix, File directory) | Создает «временный файл» — файл с случайно сгенерированным уникальным именем – что-типа «dasd4d53sd». Дополнительные параметры – префикс к имени, суффикс (окончание). Если директория не указана, то файл создается в специальной директории ОС для временных файлов 
boolean renameTo(File) | Переименовывает файл – содержимое файла фактически получает новое имя. Т.е. можно переименовать файл «c:/dir/a.txt» в «d:/out/text/b.doc».
### Каталоги
Метод | Описание
--- | ---
boolean mkdir() | Создает директорию. Название mkdir происходит от «make directory».
boolean mkdirs() | Создает директорию и все поддиректории.
String[] list() | Возвращает массив имен файлов, которые содержатся в директории, которой является текущий объект-файл.
String[] list(FilenameFilter filter) | возвращает файлы ограниченные **filter** - функциональный интерфейс `boolean accept (File dir, String name)`
File[] listFiles() | Возвращает массив файлов, которые содержатся в директории, которой является текущий объект-файл.
File[] listFiles(FileFilter filter) | **FileFilter** - функ.интерфейс `boolean accept(File pathname)`
File[] listFiles(FilenameFilter filter) | Возвращает массив файлов, которые содержатся в директории, которой является текущий объект-файл, ограниченные **filter**
**Вывести на экран список всех файлов, которые находятся в определенной директории**
```java
File folder = new File("c:/path/");
for (File file : folder.listFiles()){
    System.out.println(file.getName());
}
```
**Вывести имена всех файлов, которые есть в той же директории, что и текущий файл**
```java
//какой-то текущий файл
File originalFile = new File("c:/path/dir2/a.txt");
//объект-директория
File folder = originalFile.getParentFile();
//печать списка файлов на экран
for (File file : folder.listFiles()){
 System.out.println(file.getName());
}
```
**Вывести только каталоги**
```java
File folder = new File("e:/oscript/");
for (File file : folder.listFiles((f -> f.isDirectory()))){
    System.out.println(file.getName());
}
```
**Вывести файлы с расширением *.txt***
```java
File folder = new File("e:/oscript/");
for (File file : folder.listFiles(((dir, name) -> name.endsWith(".txt")))){
    System.out.println(file.getName());
}
```
### Работа с разделами диска
Метод | Описание
--- | ---
long getTotalSpace() | Возвращает размер диска (количество байт) на котором расположен файл.
long getFreeSpace() | Возвращает количество свободного места (количество байт) на диске, на котором расположен файл.
static File[] listRoots() | List the available filesystem roots (C:\\, D:\ etc.)
### Прочие
Метод | Описание
--- | ---
Path toPath() | Возвращает объект Path, который соответствует текущему объекту File.