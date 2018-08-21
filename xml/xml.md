# XML

**[JAXB](/xml/jaxb.md)** - фреймворк для сериализации объектов java в xml.

## Пакеты

```java
import org.w3c.dom.*;
import org.xml.sax.*;
import javax.xml.bind.*;
import javax.xml.parsers.*;
import javax.xml.transform.*;
// и др.
```

## Примеры работы с xml

### Создать пустой документ DOM
```java
private static Document newDocument() {
    Document doc = null;
    try {
        DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
        DocumentBuilder builder = factory.newDocumentBuilder();
        doc = builder.newDocument();
    } catch (ParserConfigurationException e) {
        e.printStackTrace();
    }

    return doc;
}
```

### Добавить в документ DOM элемент
```java
Document doc = //...
Element element = doc.createElement("price");
//Element element = doc.createCDATASection("какой-то текст"); // - добавить секцию CDATA
//Element element = doc.createTextNode("какой-то текст"); // - добавить текст
doc.appendChild(element);
```

### Создать документ DOM из строки xml
```java
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document doc = builder.parse(new InputSource(new StringReader(xmlString)));
```

### Записать документ DOM в поток вывода

```java
public static void docToOut(Document doc, OutputStream out){
   try {
       // построить объект холостого преобразования
       Transformer t = TransformerFactory.newInstance().newTransformer();
       t.setOutputProperty(OutputKeys.INDENT, "yes"); //отступы при выводе
       t.setOutputProperty(OutputKeys.STANDALONE, "no");
       // выполнить холостое преобразование и вывести результат в файл
       t.transform(new DOMSource(doc), new StreamResult(out));
   } catch (TransformerException e) {
       e.printStackTrace();
   }
}
```
[javax.xml.transform.Transformer](https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/Transformer.html)\
[javax.xml.transform.OutputKeys](https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/OutputKeys.html)

### Сериализовать объект класса в документ DOM
```java
Marshaller marshaller = ...
Object obj = ...
Document doc = ...
marshaller.marshal(obj, doc);
```

[javax.xml.bind.Marshaller](https://docs.oracle.com/javase/8/docs/api/javax/xml/bind/Marshaller.html)

### Сериализовать объект класса в строку xml
```java
Marshaller marshaller = ...
Object obj = ...
StringWriter writer = new StringWriter();
marshaller.marshal(obj, writer);
String res = writer.toString();
```

### Сериализовать объект класса с обработкой
```java
//...
Marshaller marshaller = ...
Object obj = ...
ContentHandler handler = //...
marshaller.marshal(obj, handler);
}

private static class MyContentHandler extends DefaultHandler {
    @Override public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException {...}
    @Override public void endElement(String uri, String localName, String qName) throws SAXException {...}
    @Override public void characters(char[] ch, int start, int length) throws SAXException {...}
    //...
}
```

[org.xml.sax.ContentHandler](https://docs.oracle.com/javase/8/docs/api/org/xml/sax/ContentHandler.html)

## Дополнительный материал
 - **Java 7 Наиболее полное руководство, 2012, (Хабибуллин)** Глава 28 стр.704
 - **Java Библиотека профессионала том 2, издание 10, 2017, (Хорстманн,Корнел)** Глава 3 стр.153
 - **Java Методы программирования, 2013, (Блинов, Романчик)** Глава 14 стр.395
 - http://www.quizful.net/post/getting-started-with-xml-in-java
 - http://java-course.ru/begin/xml/
