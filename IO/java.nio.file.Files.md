# Ввод и вывод. Класс [**java.nio.file.Files**][1]

Этот класс состоит исключительно из статических методов для операций с файлами, каталогами или другими типами файлов.

**Чтение и запись данных в файлы**

Метод | Применение | Описание
--- | --- | ---
*Читают содержимое файла* |  | 
static byte[] readAllBytes (Path path) | String content = new String(bytes, charset) | 
static List<String> readAllLines(Path path, Charset charset) | |
*Записывают заданное содержимое в файл и возвращают **path** как путь к нему* |  | 
static Path write(Path path, byte[] contents, OpenOption... options) | Files.write(path, content.getBytes(charset)) |   
static Path write(Path path, Iterable<? extends CharSequence> contents, OpenOption options) |  |  
*Открывают файл для чтения или записи* |  | 
static InputStream newInputStream (Path path, OpenOption.. . options) | |   
static OutputStream newOutputStream (Path path, OpenOption. . . options) | |   
static BufferedReader newBufferedReader(Path path, Charset charset) | |   
static BufferedWriter newBufferedWriter(Path path, Charset charset, OpenOption... options) | |  

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
>[**enum StandardOpenOption**][2] - применяется в потоках ввода-вывода типа `newBufferedWriter`, `newInputStream`, `newOutputStream` для операции записи

Значение | Описание
--- | ---
READ |  Открыть файл для чтения 
WRITE |  Открыть файл для записи
APPEND |  Если файл открыт для записи, присоединить данные в конце этого файла
TRUNCATE_EXISTING | Если файл открыт для записи, удалить его текущее содержимое
CREATE_NEW |  Создать новый файл, указать на неудачный исход операции, если файл уже существует 
CREATE | Создать файл атомарно, если файл не существует 
DELETE_ON_CLOSE |  Удалить файл наилучшим образом после его закрытия 
SPARSE | Указать файловой системе, что этот файл окажется разреженным
DSYNC\|SYNC |  Потребовать, чтобы при каждом обновлении файла данные и метаданные синхронно записывались на запоминающем устройстве

>[**enum StandardCopyOption**][3] - применяется в операциях копирования и перемещения

Значение | Описание
--- | ---
ATOMIC_MOVE | Переместить файл атомарно 
COPY_ATTRIBUTES | Скопировать атрибуты файла 
REPLACE_EXISTING | Заменить целевой файл, если он существует

>[**enum LinkOption**][4] - применяется во всех упомянутых выше методах, а также в методах `exists()`, `isDirectory()`, `isRegularFile()`

Значение | Описание
--- | ---
NOFOLLOW_LINKS | He следовать по символическим ссылкам FileVisitOption; применяется в методах `find()`, `walk()`, `walkFileTree()` 
FOLLOW_LINKS | Следовать по символическим ссылкам 

 [1]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html
 [2]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardOpenOption.html
 [3]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardCopyOption.html
 [4]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/LinkOption.html
 