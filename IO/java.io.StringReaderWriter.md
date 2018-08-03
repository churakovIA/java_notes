# Поток символов из строки

[**StringReader**][1] и [**StringWriter**][2] это простейшие реализации абстрактных классов _Reader_ и _Writer_. 
И практически аналоги _FileReader_ и _FileWriter_. Но, в отличие от них, они работают не с данными в файле на диске, а со строкой (String) находящейся в памяти Java-машины. 
StringReader – это, фактически, переходник между классом String и Reader.

>**Чтобы преобразовать строку в Reader:**
```java
String s = "data";
Reader reader = new StringReader(s);
```

>**Чтобы преобразовать StringWriter к строке:**
```java
Writer writer = new StringWriter();
/*тут пишем кучу данных во writer */
String result = writer.toString();
```

>**Чтение из объекта _Reader_. Пример как можно протестировать чтение из _Reader_:**
```java
public static void main (String[] args) throws Exception
{
    String test = "Hi!\n My name is Richard\n I'm a photographer\n";

    //это строчка – ключевая: мы «превратили» строку в Reader
    StringReader reader = new StringReader(test);

    executor(reader);
}

public static void executor(Reader reader) throws Exception
{
    BufferedReader br = new BufferedReader(reader);
    String line
    while (line = br.readLine() != null)
    {
        System.out.println(line);
    }
}
```

>**Чтение из объекта _Reader_ и запись в объект _Writer_:**
```java
public static void main (String[] args) throws Exception
{
    //эту строку должен будет прочитать Reader
    String test = "Hi!\n My name is Richard\n I'm a photographer\n";
    //заворачиваем строку в StringReader
    StringReader reader = new StringReader(test);

    //Создаем объект StringWriter
    StringWriter writer = new StringWriter();

    //переписываем строки из Reader во Writer, предварительно развернув их
    executor(reader, writer);

    //получаем текст, который был записан во Writer
    String result = writer.toString();

    //выводем полученный из Writer’а текст на экран
    System.out.println("Результат: "+result);
}

public static void executor(Reader reader, Writer writer) throws Exception
{
    BufferedReader br = new BufferedReader(reader);
    String line;

    //читаем строку из Reader’а

    while (line = br.readLine()) != null)
    {
        //разворачиваем строку задом наперед
        StringBuilder sb = new StringBuilder(line);
        String newLine = sb.reverse().toString();

        //пишем строку в Writer
        writer.write(newLine);
    }
}
```

[1]: https://docs.oracle.com/javase/8/docs/api/java/io/StringReader.html
[2]: https://docs.oracle.com/javase/8/docs/api/java/io/StringWriter.html

