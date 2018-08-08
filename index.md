### XML parsing with XPath

Parsing and extracting data from XML file with XPath.
The output displays detailed information on all books whose price is higher than 10, which were published after 2005.

```java
Main.java

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
```xml
books.xml

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
```xml
books.dtd

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

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/rashmans/rashmans.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
