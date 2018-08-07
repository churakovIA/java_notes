# Hashorn - интерпритатор языка javascript
 - Является преемником Rhino. 
 - Позволяет интегрировать java с javascript.
 - Является удобной средой для экспериментирования с Java API
 - Выполняет сценарии javascript по команде jjs или из кода java
 
 ## Выполнение из командной строки в режиме REPL (чтение-вычисление-печать)
 ```bash
 $ jjs
 jjs> str = "Hello"
 Hello
 jjs> str.length
 5
 ```
 
 ## Использование Java API
 ```bash
 jjs> JMath = java.lang.Math
 [JavaClass java.lang.Math]
 jjs> d = JMath.random()
 0.24107227541890053
 ```
 
 ## Варианты получения ссылки на класс java
 ```bash
 jjs> JMath = java.lang.Math
 jjs> JMath = Java.type("java.lang.Math")
 ```
 
 ## Запуск скрипта
 ```bash
 $ jjs script.js
 ```
 
 ## Выход из интерпретатора
 ```bash
 jjs> quit()
 ``` 

## Выполнение javascript из java
```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class NashornExample1 {

    public static void main(String[] args) throws ScriptException {
        ScriptEngineManager manager = new ScriptEngineManager();
        ScriptEngine nashorn = manager.getEngineByName("nashorn");
        Integer eval = (Integer) nashorn.eval("10 + 20");
        System.out.println(eval);
    }
}
```
   
 ## Дополнительная информация
  - Java SE 8 Вводный курс, 2014, (Хорстманн) Глава 7
  - https://github.com/shekhargulati/java8-the-missing-tutorial/blob/master/10-nashorn.md
  - https://docs.oracle.com/javase/8/docs/technotes/guides/scripting/nashorn/intro.html
  - https://docs.oracle.com/javase/8/docs/technotes/tools/windows/jjs.html
