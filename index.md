### XML parsing with XPath

Parsing and extracting data from XML file with XPath.
The output displays detailed information on all books whose price is higher than 10, which were published after 2005.

***Main.java***
```java
/*
 * Goran Radosavljevic
 */
package main;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import javax.xml.xpath.XPath;
import javax.xml.xpath.XPathConstants;
import javax.xml.xpath.XPathExpression;
import javax.xml.xpath.XPathExpressionException;
import javax.xml.xpath.XPathFactory;
import org.w3c.dom.NodeList;
import org.xml.sax.InputSource;

public class Main {

    public static void main(String[] args) throws XPathExpressionException, FileNotFoundException {

        XPathFactory factory = XPathFactory.newInstance();
        XPath path = factory.newXPath();
        XPathExpression xPathExpression = path.compile("//book[price > 10 and translate(publish_date,'-','')>20050000]");

        File xmlDocument = new File("books.xml");
        InputSource inputSource = new InputSource(new FileInputStream(xmlDocument));

        Object result = xPathExpression.evaluate(inputSource, XPathConstants.NODESET);
        NodeList nodeList = (NodeList) result;

        for (int i = 0; i < nodeList.getLength(); i++) {
            System.out.println("Author: " + nodeList.item(i).getFirstChild().getNextSibling().getTextContent());
            System.out.println("Title: " + nodeList.item(i).getFirstChild().getNextSibling().getNextSibling().getNextSibling().getTextContent());
            System.out.println("Genre: " + nodeList.item(i).getFirstChild().getNextSibling().getNextSibling().getNextSibling().getNextSibling().getNextSibling().getTextContent());
            System.out.println("Price: " + nodeList.item(i).getLastChild().getPreviousSibling().getPreviousSibling().getPreviousSibling().getPreviousSibling().getPreviousSibling().getTextContent());
            System.out.println("Publish date: " + nodeList.item(i).getLastChild().getPreviousSibling().getPreviousSibling().getPreviousSibling().getTextContent());
            System.out.println("Description: " + nodeList.item(i).getLastChild().getPreviousSibling().getTextContent());
            System.out.println("");
        }

    }

}
```
***books.xml***
```xml
<!DOCTYPE catalog SYSTEM "books.dtd">
<catalog>
   <book id="bk101">
      <author>Gambardella, Matthew</author>
      <title>XML Developer's Guide</title>
      <genre>Computer</genre>
      <price>44.95</price>
      <publish_date>2000-10-01</publish_date>
      <description>An in-depth look at creating applications 
      with XML.</description>
   </book>
   <book id="bk102">
      <author>Ralls, Kim</author>
      <title>Midnight Rain</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2002-12-16</publish_date>
      <description>A former architect battles corporate zombies, 
      an evil sorceress, and her own childhood to become queen 
      of the world.</description>
   </book>
   <book id="bk103">
      <author>Corets, Eva</author>
      <title>Maeve Ascendant</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2000-11-17</publish_date>
      <description>After the collapse of a nanotechnology 
      society in England, the young survivors lay the 
      foundation for a new society.</description>
   </book>
   <book id="bk104">
      <author>Corets, Eva</author>
      <title>Oberon's Legacy</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2001-03-10</publish_date>
      <description>In post-apocalypse England, the mysterious 
      agent known only as Oberon helps to create a new life 
      for the inhabitants of London. Sequel to Maeve 
      Ascendant.</description>
   </book>
   <book id="bk105">
      <author>Corets, Eva</author>
      <title>The Sundered Grail</title>
      <genre>Fantasy</genre>
      <price>5.95</price>
      <publish_date>2001-09-10</publish_date>
      <description>The two daughters of Maeve, half-sisters, 
      battle one another for control of England. Sequel to 
      Oberon's Legacy.</description>
   </book>
   <book id="bk106">
      <author>Randall, Cynthia</author>
      <title>Lover Birds</title>
      <genre>Romance</genre>
      <price>4.95</price>
      <publish_date>2003-09-02</publish_date>
      <description>When Carla meets Paul at an ornithology 
      conference, tempers fly as feathers get ruffled.</description>
   </book>
   <book id="bk107">
      <author>Thurman, Paula</author>
      <title>Splish Splash</title>
      <genre>Romance</genre>
      <price>4.95</price>
      <publish_date>2004-11-02</publish_date>
      <description>A deep sea diver finds true love twenty 
      thousand leagues beneath the sea.</description>
   </book>
   <book id="bk108">
      <author>Knorr, Stefan</author>
      <title>Creepy Crawlies</title>
      <genre>Horror</genre>
      <price>4.95</price>
      <publish_date>2005-12-06</publish_date>
      <description>An anthology of horror stories about roaches,
      centipedes, scorpions  and other insects.</description>
   </book>
   <book id="bk109">
      <author>Kress, Peter</author>
      <title>Paradox Lost</title>
      <genre>Science Fiction</genre>
      <price>6.95</price>
      <publish_date>2006-11-02</publish_date>
      <description>After an inadvertant trip through a Heisenberg
      Uncertainty Device, James Salway discovers the problems 
      of being quantum.</description>
   </book>
   <book id="bk110">
      <author>O'Brien, Tim</author>
      <title>Microsoft .NET: The Programming Bible</title>
      <genre>Computer</genre>
      <price>36.95</price>
      <publish_date>2006-12-09</publish_date>
      <description>Microsoft's .NET initiative is explored in 
      detail in this deep programmer's reference.</description>
   </book>
   <book id="bk111">
      <author>O'Brien, Tim</author>
      <title>MSXML3: A Comprehensive Guide</title>
      <genre>Computer</genre>
      <price>36.95</price>
      <publish_date>2007-12-01</publish_date>
      <description>The Microsoft MSXML3 parser is covered in 
      detail, with attention to XML DOM interfaces, XSLT processing, 
      SAX and more.</description>
   </book>
   <book id="bk112">
      <author>Galos, Mike</author>
      <title>Visual Studio 7: A Comprehensive Guide</title>
      <genre>Computer</genre>
      <price>49.95</price>
      <publish_date>2008-04-16</publish_date>
      <description>Microsoft Visual Studio 7 is explored in depth,
      looking at how Visual Basic, Visual C++, C#, and ASP+ are 
      integrated into a comprehensive development 
      environment.</description>
   </book>
</catalog>
```
***books.dtd***
```xml
<?xml version='1.0' encoding='UTF-8'?>

<!--
    TODO define vocabulary identification
    PUBLIC ID: -//vendor//vocabulary//EN
    SYSTEM ID: http://server/path/books.dtd

-->

<!--
    An example how to use this DTD from your XML document:

    <?xml version="1.0"?>

    <!DOCTYPE catalog SYSTEM "books.dtd">

    <catalog>
    ...
    </catalog>
-->

<!--- Put your DTDDoc comment here. -->
<!ELEMENT catalog (book)*>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT book (author|title|genre|price|publish_date|description)*>
<!ATTLIST book
    id ID #IMPLIED
  >

<!--- Put your DTDDoc comment here. -->
<!ELEMENT author (#PCDATA)>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT title (#PCDATA)>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT genre (#PCDATA)>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT price (#PCDATA)>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT publish_date (#PCDATA)>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT description (#PCDATA)>
```

### RESTful Web Service

Web service for translating between two languages / Mini Fruit Dictionary

***web.xml***
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">
  <display-name>RESTFull</display-name>
 <servlet>
    <servlet-name>Jersey REST Service</servlet-name>
    <servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class>
     <!-- Register resources and providers under com.vogella.jersey.first package. -->
    <init-param>
        <param-name>jersey.config.server.provider.packages</param-name>
        <param-value>service</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>Jersey REST Service</servlet-name>
    <url-pattern>/rest/*</url-pattern>
  </servlet-mapping>
</web-app>
```
***index.html***
```html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Mini Fruit Dictionary</title>
    </head>
    <body>
        <h1>Mini Fruit Dictionary</h1>
        <form>  
            Enter the word: 
            <input type="text" name="word" id="word"/> 
            <button onclick="input()">Translate</button> 
        </form>  
        <script>
            function input() {
                url = 'http://localhost:8080/RESTfull/rest/MyRestService/' + document.getElementById("word").value;
                window.open(url, '_blank');
            }
        </script>
    </body>
</html>
```
***translator.xml***
```xml
<!DOCTYPE catalog SYSTEM "translator.dtd">
<translator>  
    <word en="apple">jabuka</word>  
    <word en="apricot">kajsija</word>  
    <word en="avocado">avokado</word>  
    <word en="banana">banana</word>  
    <word en="blackcurrant">crna ribizla</word>
    <word en="blackberry">kupina</word>  
    <word en="blueberry">borovnica</word>  
    <word en="cherry">višnja</word>  
    <word en="coconut">kokos</word>  
</translator>  
```
***MyService.java***
```java
package service;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.PathParam;
import javax.xml.xpath.XPath;
import javax.xml.xpath.XPathConstants;
import javax.xml.xpath.XPathExpression;
import javax.xml.xpath.XPathExpressionException;
import javax.xml.xpath.XPathFactory;
import org.w3c.dom.NodeList;
import org.xml.sax.InputSource;

@Path("/MyRestService/{word}")
public class MyService {

    @GET
    public String doGet(@PathParam("word") String word) throws XPathExpressionException, FileNotFoundException {
    String output = null;  
            
      XPathFactory factory = XPathFactory.newInstance();  
      XPath path = factory.newXPath();  
      XPathExpression xPathExpression = path.compile("//word[@en='"+ word.trim().toLowerCase() +"']");  
        
      File xmlDocument = new File("translator.xml");  
      InputSource inputSource = new InputSource(new FileInputStream(xmlDocument));  
        
      Object result = xPathExpression.evaluate(inputSource, XPathConstants.NODESET);  
      NodeList nodeList = (NodeList)result;  
        
      if (nodeList.getLength() < 1) {
        output = "Word " + word + " does not exist in dictionary";
      } else {  
        for (int i = 0; i < nodeList.getLength(); i++) {  
          output = "Word " + word + " translates as: " + nodeList.item(i).getTextContent();  
        }  
      }         
      return output;       
    }

}
```
***translator.dtd***
```xml
<?xml version='1.0' encoding='UTF-8'?>

<!--
    TODO define vocabulary identification
    PUBLIC ID: -//vendor//vocabulary//EN
    SYSTEM ID: http://server/path/translator.dtd

-->

<!--
    An example how to use this DTD from your XML document:

    <?xml version="1.0"?>

    <!DOCTYPE translator SYSTEM "translator.dtd">

    <translator>
    ...
    </translator>
-->

<!--- Put your DTDDoc comment here. -->
<!ELEMENT translator (word)*>

<!--- Put your DTDDoc comment here. -->
<!ELEMENT word (#PCDATA)>
<!ATTLIST word
    en CDATA #IMPLIED
  >
```

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
