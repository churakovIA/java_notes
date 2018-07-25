# ���� � �����. ����� [**java.nio.file.Files**][1]

���� ����� ������� ������������� �� ����������� ������� ��� �������� � �������, ���������� ��� ������� ������ ������.

**�������� ������ � ���������**

����� | ���������� | ��������
--- | --- | ---
static Path createFile(Path path, FileAttribute<?>... attrs) | Files.createFile(path) | ������� ����  
static Path createDirectory(Path path, FileAttribute<?>... attrs) | Files.createDirectory(path) | ������� �������  
static Path createDirectories(Path path, FileAttribute<?>... attrs) | Files.createDirectories(path) | ������� ����� ����� ������������� ��������
static Path createTempFile (String prefix, String suffix, FileAttribute<?>.. . attrs) | Files.createTempFile (null, " .txt") | ������� ��������� ����  
static Path createTempFile (Path parentDir, String prefix, String suffix, FileAttribute<?>... attrs) |  | � �������� ������������ �������� 
static Path createTempDirectory (String prefix, FileAttribute<?>. . . attrs) |  | ������� ��������� ������� 
static Path createTempDirectory (Path parentDir, String prefix, FileAttribute<?>.. . attrs) |  | � �������� ������������ ��������

**�����������, ����������� � �������� ������**

����� | ���������� | ��������
--- | --- | ---
static Path copy(Path from, Path to, CopyOption... options) | Files.copy(fromPath, toPath, StandardCopyOption.REPLACE_EXISTING, StandardCopyOption.COPY_ATTRIBUTES) | ����������� ����
static Path move(Path from, Path to, CopyOption... options) | Files.move(fromPath, toPath, StandardCopyOption.ATOMIC_MOVE) | ����������� ����. ���������� ������� ����.
static long copy (Inputs tream from, Path to, CopyOption... options)  |  | �������� ������ � ���� �� ������ �����
static long copy (Path frcm, OutputStream to, CopyOption... options) |  | �������� ������ �� ����� � ������ �����, ��������� ���������� ������������� ������.
static void delete(Path path) | Files.delete(path) | ������� �������� ���� ��� ������ �������. ����������, ���� �� ����������.
static boolean deletelfExists(Path path) | boolean deleted = Files.deletelfExists(path) | ������ ����, ���� �� ����������.
 
**��������� �������� � ������**

 ����� | ��������
--- | ---
*��������� �������� �������� ����� �� ���������� ����* | 
static boolean exists(Path path) |  
static boolean isHidden(Path path) |  
static boolean isReadable (Path path) |  
static boolean isWritable(Path path) |  
static boolean isExecutable(Path path) |  
static boolean isRegularFile(Path path) |  
static boolean isDirectory(Path path) |  
static boolean isSymbolicLink(Path path) |  
static long size(Path path) | �������� ������ ����� � ������
*������ �������� �����, ����������� � ���� �* | 
A readAttributes(Path path, Class<A> type, LinkOption... options) | BasicFileAttributes attributes = files.readAttributes(path, BasicFileAttributes.class);	PosixFileAttributes attributes = files.readAttributes(path, PosixFileAttributes.class); 
*�������� ������������� ������� �����* | 
FileTime creationTime() |  
FileTime lastAccessTime() |  
FileTime lastMbdifiedTime() |  
boolean isRegularFile() |  
boolean isDirectory() |  
boolean isSymbolicLink() |  
long size() |  
Object fileKey() | 

---

**C���������� ��������� ��� �������� � �������** 
>[**StandardOpenOption**][2] - ����������� � ������� �����-������ ���� newBufferedWriter, newInputStream, newOutputStream ��� �������� ������

```java
public enum StandardOpenOption extends Enum<StandardOpenOption> implements OpenOption`
```

 ����� | ���������� | ��������
--- | --- | ---
 |  | 
 
 [1]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html
 [2]: https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardOpenOption.html