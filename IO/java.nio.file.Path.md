# ���� � �����. ��������� [**java.nio.file.Path**](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html)
��������� `Path` ��������� ���� � ����� � ������������ �� ������ ������� ��������������� �������.
��� ��������� ������� ���� `Path` �� ������ ���������� ����������� ����� `static Path get(String first, String... more)` ������ [java.nio.file.Paths](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Paths.html)
```java
Path path = Paths.get("e:/Short-term storage/temp.png");
//���
Path path = Paths.get("e:","Short-term storage","temp.png");
```
### ������
����� | ��������
--- | ---
boolean isAbsolute() | ���������� true, ���� ���� � ����������.
Path getRoot() | ���������� ������ �������� ���� � ���������� ������ �������� ������.
Path getFileName() | ���������� ��� ����� �� �������� ����.
Path getParent() | ���������� ���������� �� �������� ����.
Path getName(int index) | ���������� ������ ���� Path, ���������� ��� �������� ���� �� ���������� � ���������� �������. ��������� � ����.
int	 getNameCount() | ���������� ���������� ��������� (����� ���������) � ���������� ������� ���� Path
boolean startsWith(Path other) | ���������, ��� ������� ���� ���������� � ����������� ����.
boolean endsWith(Path other) | ���������, ��� ������� ���� ������������� �� ���������� ����.
Path normalize() | ����������� ������� ����. ��������, �������� ���� �c:/dir/dir2/../a.txt� � ���� �c:/dir/a.txt�. ������� �� ���� ���������� ������������, ��������, ����� . � ...
Path relativize(Path other) | ��������� ������������� ���� ���� ����� � �������� �����
Path resolve(String other) | ��������������� ���������� ���� �� �������� � ��������������.
Path resolveSibling(String other) | ���� �������� other �������� ���������� ����, �� ������������ ���� other, � ����� � ����, ���������� � ���������� ����������� ������������� ���� this � ��������� ���� other.
URI toUri() | ���������� URI �������� ����/�����.
Path toAbsolutePath() | �������� ���� � �����������, ���� ��� �������������.
File toFile() | ���������� ������ File, ������� ������������� �������� ������� Path.

**�������:**
```java
Path workPath = basePath.resolve("work"); // basePath - "c:\" ��������� ����� - "c:\work"
Path tempPath = workPath.resolveSibling("temp"); // ���, ���� /opt/myapp/ work � ���� � �������� ��������, �� � ���������� ���������� ������ ���������� ���� /opt/myapp/temp: 
Path � = Paths.get("/home", "fred", "myprog.properties"); 
Path parent = p.getParent(); // ���� /home/fred 
Path file = p.getFileName(); // ���� myprog.properties 
Path root = p.getRoot(); 	 // ���� /
```