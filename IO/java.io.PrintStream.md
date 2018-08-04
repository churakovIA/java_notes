# Форматированный вывод
[**PrintStream**][1] - класс для вывода данных в поток. Символы преобразуются в байты используя кодировку по-умолчанию для платформы. 
В отличие от других потоков вывода, PrintStream никогда не генерирует исключение IOException, 
вместо этого исключительные ситуации просто устанавливают внутренний флаг, который может быть протестирован с помощью метода checkError.
Класс PrintStream - это именно тот класс, который используется для вывода на консоль. System.out – это статическая переменная класса System типа PrintStream.
Он практически весь состоит из методов print и println.

>**Конструкторы**
```java
PrintStream(File file)
PrintStream(File file, String csn)
PrintStream(OutputStream out)
PrintStream(OutputStream out, boolean autoFlush)
PrintStream(OutputStream out, boolean autoFlush, String encoding)
PrintStream(String fileName)
PrintStream(String fileName, String csn)
```

Метод | Метод
--- | ---
void print(boolean b) | void println(boolean b)
void print(char c) | void println(char c)
void print(int c) | void println(int c)
void print(long c) | void println(long c)
void print(float c) | void println(float c)
void print(double c) | void println(double c)
void print(char[] c) | void println(char[] c)
void print(String c) | void println(String c)
void print(Object obj) | void println(Object obj)
void println() | 
**Форматирование** | 
PrintStream format (String format, Object ... args) | 
PrintStream format (Locale l, String format, Object ... args) | 

>**Примеры**
```java
System.out.write('s');
System.out.write('\n');

System.out.printf("%s = %8.2f\n", "Result: ", 1000.0/3.0); // Result:  =   333,33
System.out.printf("Я %1$s %1$s %2$s %2$s", "два раза", "не повторяю"); // Я два раза два раза не повторяю не повторяю
```

[1]: https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html
