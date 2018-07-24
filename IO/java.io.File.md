# ���� � �����. ����� [**java.io.File**](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)
����� ������������ ��� ����������� ������� � ����������, ������ � ��������� ���������. ����� ����� ���������, �������, ��������������� � �.�..
### ������ ������� �����
����� | ��������
--- | ---
boolean isDirectory() | �������� �� ������� ����� �����������
boolean isFile() | �������� �� ������ ������
�oolean isHidden() | �������� �� ���� �������
long length() | ���������� ������/����� ����� � ������.
boolean exists() | ���������� true, ���� ���� � ����� ������ ���������� �� ����� ����������.
String getAbsolutePath() | ���������� ������ ���� ����� �� ����� ���������������.
String getCanonicalPath() | ���������� ������������ ���� �����. ��������, ��������������� ���� �c:/dir/dir2/../a.txt� � ���� �c:/dir/a.txt�
String getName() | ���������� ������ ��� �����, ��� ����.
String getParent() | ���������� ������ ���� (����������) � �������� �����, ��� ������ �����.
File getParentFile() | ���������� ������ ���� (����������) � �������� ����� ��� ������ **File**
### ��������������� �������
����� | ��������
--- | ---
boolean createNewFile() | ������� ����. ���� ����� ���� ��� ���, ���������� false.
boolean delete() | ������� ���� ������� �� �����. ���� ������ � ����������, �� ������, ���� � ��� ��� ������.
void deleteOnExit() | ��������� ���� � ����������� ������ ������, ������� ����� ������������� ������� ��� �������� ���������.
File createTempFile(String prefix, String suffix, File directory) | ������� ���������� ���� � ���� � �������� ��������������� ���������� ������ � ���-���� �dasd4d53sd�. �������������� ��������� � ������� � �����, ������� (���������). ���� ���������� �� �������, �� ���� ��������� � ����������� ���������� �� ��� ��������� ������ 
boolean renameTo(File) | ��������������� ���� � ���������� ����� ���������� �������� ����� ���. �.�. ����� ������������� ���� �c:/dir/a.txt� � �d:/out/text/b.doc�.
### ��������
����� | ��������
--- | ---
boolean mkdir() | ������� ����������. �������� mkdir ���������� �� �make directory�.
boolean mkdirs() | ������� ���������� � ��� �������������.
String[] list() | ���������� ������ ���� ������, ������� ���������� � ����������, ������� �������� ������� ������-����.
String[] list(FilenameFilter filter) | ���������� ����� ������������ **filter** - �������������� ��������� `boolean accept (File dir, String name)`
File[] listFiles() | ���������� ������ ������, ������� ���������� � ����������, ������� �������� ������� ������-����.
File[] listFiles(FileFilter filter) | **FileFilter** - ����.��������� `boolean accept(File pathname)`
File[] listFiles(FilenameFilter filter) | ���������� ������ ������, ������� ���������� � ����������, ������� �������� ������� ������-����, ������������ **filter**
**������� �� ����� ������ ���� ������, ������� ��������� � ������������ ����������**
```java
File folder = new File("c:/path/");
for (File file : folder.listFiles()){
    System.out.println(file.getName());
}
```
**������� ����� ���� ������, ������� ���� � ��� �� ����������, ��� � ������� ����**
```java
//�����-�� ������� ����
File originalFile = new File("c:/path/dir2/a.txt");
//������-����������
File folder = originalFile.getParentFile();
//������ ������ ������ �� �����
for (File file : folder.listFiles()){
 System.out.println(file.getName());
}
```
**������� ������ ��������**
```java
File folder = new File("e:/oscript/");
for (File file : folder.listFiles((f -> f.isDirectory()))){
    System.out.println(file.getName());
}
```
**������� ����� � ����������� *.txt***
```java
File folder = new File("e:/oscript/");
for (File file : folder.listFiles(((dir, name) -> name.endsWith(".txt")))){
    System.out.println(file.getName());
}
```
### ������ � ��������� �����
����� | ��������
--- | ---
long getTotalSpace() | ���������� ������ ����� (���������� ����) �� ������� ���������� ����.
long getFreeSpace() | ���������� ���������� ���������� ����� (���������� ����) �� �����, �� ������� ���������� ����.
static File[] listRoots() | List the available filesystem roots (C:\\, D:\ etc.)
### ������
����� | ��������
--- | ---
Path toPath() | ���������� ������ Path, ������� ������������� �������� ������� File.