# Буферизированный символьный ввод-вывод

[**BufferedReader**][1] и [**BufferedWriter**][2] представляют собой надстройку над _Reader_ и  _Writer_ позволяя сокращать количество операций ввода/вывода в источник (например, файл) которые требуют существенных затрат времени. 
Вместо этого используется промежуточный буфер для накопления данных. 
Как правило, размера буфера по умолчанию, достаточно, но при необходимости его можно задать вручную. 
Это необходимо, например, когда файл состоит из блоков фиксированного размера. 
С текстовыми файлами такое случается нечасто.

 После окончания записи у объекта _BufferedWriter_ надо вызвать метод `flush()`, чтобы он записал данные из буфера во _Writer_, которые еще не записаны, т.е. буфер не заполнен до конца.
 
 Пока буфер еще не записан во _Writer_, данные можно удалить и/или заменить на другие.
 
 >**Конструкторы**
 ```java
 BufferedReader(Reader in)
 BufferedReader(Reader in, int sz)
 
 BufferedWriter(Writer out)
 BufferedWriter(Writer out, int sz)
 ```
 
 [1]: https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html
 [2]: https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html
