# Ввод-вывод байтов в\из массива `byte[]`

[**ByteArrayInputStream**][1] и [**ByteArrayOutputStream**][2] читает\пишет байты из массива байт. 
Эти классы по сути чем-то похожи на StringReader и StringWriter. 
Только StringReader читал символы (char) из строки (String), а InputStream читает байты из массива байт. 
Содержит внутренний динамически расширяемый массив.

>**Конструкторы**
```java
ByteArrayInputStream(byte[] buf)

ByteArrayOutputStream()
```

>**Чтение из объекта InputStream и запись в объект OutputStream:**
```java
public static void main (String[] args) throws Exception
{
    String test = "Hi!\n My name is Richard\n I'm a photographer\n";
    InputStream inputStream = new ByteArrayInputStream(test.getBytes());

    ByteArrayOutputStream outputStream = new ByteArrayOutputStream();

    executor(inputStream, outputStream);

    String result = new String(outputStream.toByteArray());
    System.out.println("Результат: "+result);
}

public static void executor(InputStream inputStream, OutputStream outputStream) throws Exception
{
    BufferedInputStream bis = new BufferedInputStream(inputStream);
    while (bis.available() > 0)
    {
        int data = bis.read();
        outputStream.write(data);
    }
}
```

>**Преобразование строки в массив байт и обратно:**
```java
public static void main (String[] args) throws Exception
{
    String test = "Hi!\n My name is Richard\n I'm a photographer\n";
    byte[] array = test.getBytes();

    String result = new String(array);
    System.out.println("Результат: "+result);
}
```

[1]: https://docs.oracle.com/javase/8/docs/api/java/io/ByteArrayInputStream.html
[2]: https://docs.oracle.com/javase/8/docs/api/java/io/ByteArrayOutputStream.html
