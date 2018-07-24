# Ввод и вывод. Интерфейс [**java.nio.file.Path**](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html)
Интерфейс `Path` описывает путь к файлу и используется во многих методах манипулирования файлами.
Для получения объекта типа `Path` из строки существует статический метод `static Path get(String first, String... more)` класса [java.nio.file.Paths](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Paths.html)
```java
Path path = Paths.get("e:/Short-term storage/temp.png");
//или
Path path = Paths.get("e:","Short-term storage","temp.png");
```
### Методы
Метод | Описание
--- | ---
boolean isAbsolute() | Возвращает true, если путь – абсолютный.
Path getRoot() | Возвращает корень текущего пути – директорию самого верхнего уровня.
Path getFileName() | Возвращает имя файла из текущего пути.
Path getParent() | Возвращает директорию из текущего пути.
Path getName(int index) | Возвращает объект типа Path, содержащий имя элемента пуги по указанному в вызывающем объекте. Нумерация с нуля.
int	 getNameCount() | Возвращает количество элементов (кроме корневого) в вызывающем объекте типа Path
boolean startsWith(Path other) | Проверяет, что текущий путь начинается с переданного пути.
boolean endsWith(Path other) | Проверяет, что текущий путь заканчивается на переданный путь.
Path normalize() | Нормализует текущий путь. Например, приводит путь «c:/dir/dir2/../a.txt» к пути «c:/dir/a.txt». Удаляет из пути избыточные составляющие, например, знаки . и ...
Path relativize(Path other) | Вычисляет относительный путь двух путей – «разницу путей»
Path resolve(String other) | Восстанавливает абсолютный путь по текущему и относительному.
Path resolveSibling(String other) | Если параметр other содержит абсолютный путь, то возвращается путь other, а иначе — путь, получаемый в результате объединения родительского пути this и заданного пути other.
URI toUri() | Возвращает URI текущего пути/файла.
Path toAbsolutePath() | Приводит путь к абсолютному, если был относительный.
File toFile() | Возвращает объект File, который соответствует текущему объекту Path.

**ПРИМЕРЫ:**
```java
Path workPath = basePath.resolve("work"); // basePath - "c:\" результат будет - "c:\work"
Path tempPath = workPath.resolveSibling("temp"); // Так, если /opt/myapp/ work — путь к рабочему каталогу, то в результате следующего вызова образуется путь /opt/myapp/temp: 
Path р = Paths.get("/home", "fred", "myprog.properties"); 
Path parent = p.getParent(); // путь /home/fred 
Path file = p.getFileName(); // путь myprog.properties 
Path root = p.getRoot(); 	 // путь /
```