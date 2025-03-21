# База знаний

## Вопросы для подготовки к собеседованиям

1. :point_right:[Java core](Assessment/1-java-core.md)
2. :point_right:[Multithreading](Assessment/2-multithreading.md)
3. :point_right:[Databases](Assessment/3-databases.md)
4. :point_right:[Clean code, Patterns](Assessment/4-patterns.md)

[Ссылки](links.md)

## Конспекты книг

- [Программист-фанатик (*Passionate Programmer*) Чед Фаулер](/book-summaries/passionate-programmer-chad-fowler.md)
- [Чистый код - создание, анализ и рефакторинг, 2011, (Роберт Мартин)](/book-summaries/clean-code-robert-martin.md)
- [Принципы юнит-тестирования, 2021, (Хориков Владимир)](/book-summaries/principles-ut-khorikov.md)
- [Паттерны проектирования. Приемы объектно-ориентированного проектирования, (Гамма, Хелм, Джонсон, Влиссидес)](/book-summaries/patterns-gof.md)

## Java core

### Ввод / вывод

- [Иерархия классов Reader и Writer](/IO/ClassHierarchyReaderWriter.PNG)
- [Иерархия классов InputStream и OutputStream](/IO/ClassHierarchyInputStreamOutputStream.PNG)

---

- [java.io.File](/IO/java.io.File.md) - класс для манипулирования файлами, работы с каталогами и атрибутами файлов 
- [java.nio.file.Path](/IO/java.nio.file.Path.md) - интерфейс описывает путь к файлу и используется во многих методах манипулирования файлами\
- [java.nio.file.Files](/IO/java.nio.file.Files.md) - класс состоит исключительно из статических методов для операций с файлами, каталогами или другими типами файлов\
- [java.util.zip](/IO/java.util.zip.md) - классы для потокового чтения/записи в zip-архив *ZipFile*, *ZipEntry*, *ZipOutputStream*, *ZipInputStream*

---

- [java.io.StringReader(Writer)](/IO/java.io.StringReaderWriter.md) - классы для потокового чтения/записи символов из строки

- [java.io.BufferedReader(Writer)](/IO/java.io.BufferedReaderWriter.md) - буферизированный ввод-вывод символов  

- [java.io.RandomAccessFile](/IO/java.io.RandomAccessFile.md) - класс с поддержкой запросов на позиционирование, что позволяет установить указатель файла на любой позиции в пределах этого файла  

- [java.io.ByteArrayInput(Output)Stream](/IO/java.io.ByteArrayByteArrayInputOutputStream.md) - ввод-вывод байтов в\из массива byte[]  

- [java.io.PrintStream](/IO/java.io.PrintStream.md) - форматированный вывод  

---

- [java.lang.reflect](/java.lang.reflect.md) - рефлексия. Прокси-классы  

- [java.util.Properties](java.util.Properties.md) - класс сохранения и загрузки настроек программы  

- [RMI](/RMI.md) - удаленный вызов процедур

## JavaScript

[Основы синтаксиса javascript](javascript/jsSyntax.md)  
[Nashorn - интерпритатор javascript](javascript/Nashorn.md)