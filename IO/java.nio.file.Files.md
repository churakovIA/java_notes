# Ввод и вывод. Класс [**java.nio.file.Files**][1]

Этот класс состоит исключительно из статических методов для операций с файлами, каталогами или другими типами файлов.

**Создание файлов и каталогов**

Метод | Применение | Описание
--- | --- | ---
static Path createFile(Path path, FileAttribute<?>... attrs) | Files.createFile(path) | Создать файл  
static Path createDirectory(Path path, FileAttribute<?>... attrs) | Files.createDirectory(path) | Создать каталог  
static Path createDirectories(Path path, FileAttribute<?>... attrs) | Files.createDirectories(path) | создает также любые промежуточные каталоги
static Path createTempFile (String prefix, String suffix, FileAttribute<?>.. . attrs) | Files.createTempFile (null, " .txt") | Создать временный файл  
static Path createTempFile (Path parentDir, String prefix, String suffix, FileAttribute<?>... attrs) |  | в заданном родительском каталоге 
static Path createTempDirectory (String prefix, FileAttribute<?>. . . attrs) |  | Создать временный каталог 
static Path createTempDirectory (Path parentDir, String prefix, FileAttribute<?>.. . attrs) |  | в заданном родительском каталоге

**Копирование, перемещение и удаление файлов**

Метод | Применение | Описание
--- | --- | ---
static Path copy(Path from, Path to, CopyOption... options) | Files.copy(fromPath, toPath, StandardCopyOption.REPLACE_EXISTING, StandardCopyOption.COPY_ATTRIBUTES) | Скопировать файл
static Path move(Path from, Path to, CopyOption... options) | Files.move(fromPath, toPath, StandardCopyOption.ATOMIC_MOVE) | Переместить файл. Возвращает целевой путь.
static long copy (Inputs tream from, Path to, CopyOption... options)  |  | Копируют данные в файл из потока ввода
static long copy (Path frcm, OutputStream to, CopyOption... options) |  | Копируют данные из файла в потока ввода, возвращая количество скопированных байтов.
static void delete(Path path) | Files.delete(path) | Удаляют заданный файл или пустой каталог. Исключение, если не существует.
static boolean deletelfExists(Path path) | boolean deleted = Files.deletelfExists(path) | Вернет ложь, если не существует.
 
**Получение сведений о файлах**

 Метод | Описание
--- | ---
*Проверяют заданное свойство файла по указанному пути* | 
static boolean exists(Path path) |  
static boolean isHidden(Path path) |  
static boolean isReadable (Path path) |  
static boolean isWritable(Path path) |  
static boolean isExecutable(Path path) |  
static boolean isRegularFile(Path path) |  
static boolean isDirectory(Path path) |  
static boolean isSymbolicLink(Path path) |  
static long size(Path path) | Получает размер файла в байтах
*Читает атрибуты файла, относящиеся к типу А* | 
A readAttributes(Path path, Class<A> type, LinkOption... options) | BasicFileAttributes attributes = files.readAttributes(path, BasicFileAttributes.class);	PosixFileAttributes attributes = files.readAttributes(path, PosixFileAttributes.class); 
*Получают запрашиваемый атрибут файла* | 
FileTime creationTime() |  
FileTime lastAccessTime() |  
FileTime lastMbdifiedTime() |  
boolean isRegularFile() |  
boolean isDirectory() |  
boolean isSymbolicLink() |  
long size() |  
Object fileKey() | 

---

**Cтандартные параметры для операций с файлами** 
>[**StandardOpenOption**][2] - применяется в потоках ввода-вывода типа newBufferedWriter, newInputStream, newOutputStream для операции записи

```java
public enum StandardOpenOption extends Enum<StandardOpenOption> implements OpenOption`
```

 Метод | Применение | Описание
--- | --- | ---
 |  | 
 
 [1]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html
 [2]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardOpenOption.html