[TOC]



# 简介

第14天学习笔记



# XML

可拓展标签，后缀建议.xml

## 文档声明

必须第一行

1.0 版本，本文档utf-8编码

```xml
<?xml version="1.0" encoding="UTF-8" ?>
```

## 标签规则

只有一个根标签。

成对出现。`<name></name>`

特殊标签可以是单标签，但是必须又结束符，如`<br/>`

定义属性，属性名和标签空格隔开，属性值必须用引号引起来`<strudent id="1"></name>`

## 注释

```
<!-- 这是注释 -->
```

## 特殊字符处理

例如<  >   等符号需要使用特殊符号组合`&lt;  &gt;`转义

不用刻意去记，可以使用如下包裹住，就可以直接写特殊字符。

```xml
<![CDATA[
                select * from student where age < 18 && age > 10 ;
            ]]>
```

## 文档约束

限制xml里面文件标签及属性应该怎么写。

**DTD了解**

编写约束文件.dtd

```dtd
<!ELEMENT 书架 (书+)>
<!ELEMENT 书 (书名,作者,售价)>
<!ELEMENT 书名 (#PCDATA)>
<!ELEMENT 作者 (#PCDATA)>
<!ELEMENT 售价 (#PCDATA)>
```

在xml中导入文档约束

```xml
<!DOCTYPE 书架 SYSTEM "data.dtd">
```

缺点：不能约束具体类型

**Schema了解**

可以约束具体类型。

本身是一个xml文件，可以被其他约束文件约束。

编写约束文件，后缀.xsd

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<schema xmlns="http://www.w3.org/2001/XMLSchema"
        targetNamespace="http://www.zxh.cn"
        elementFormDefault="qualified" >
    <!-- targetNamespace:申明约束文档的地址（命名空间）-->
    <element name='书架'>
        <!-- 写子元素 -->
        <complexType>
            <!-- maxOccurs='unbounded': 书架下的子元素可以有任意多个！-->
            <sequence maxOccurs='unbounded'>
                <element name='书'>
                    <!-- 写子元素 -->
                    <complexType>
                        <sequence>
                            <element name='书名' type='string'/>
                            <element name='作者' type='string'/>
                            <element name='售价' type='double'/>
                        </sequence>
                    </complexType>
                </element>
            </sequence>
        </complexType>
    </element>
</schema>
```

在xml中导入

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<书架 xmlns="http://www.zxh.cn"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.zxh.cn data.xsd">
    <!-- xmlns="http://www.zxh.cn"  基本位置
         xsi:schemaLocation="http://www.zxh.cn books02.xsd" 具体的位置 -->
    <书>
        <书名>web从入门到精通</书名>
        <作者>dlei</作者>
        <售价>9.9</售价>
    </书>

  <!--  <书>
        <书名>web从入门到精通</书名>
        <作者>dlei</作者>
        <售价>很便宜</售价>
    </书> -->

</书架>
```





# XML 解析

使用dom4j解析xml文件

```java
/**
     目标：完成dom4j的快速入门：解析XML文件。
 */
public class Dom4jDemo1 {
    @Test
    public void parseXML() throws Exception {
        // 1、创建一个SAXReader解析器对象：代表了Dom4j框架
        SAXReader saxReader = new SAXReader();

        // 2、加载xml文件成为Document文档对象(只能在main方法下支持)
//        Document document = saxReader.read(new File("xml-app\\src\\Contacts.xml"));

        // 推荐方案：读取字节输入流(默认认为/是直接去src下寻找的)
        InputStream is = Dom4jDemo1.class.getResourceAsStream("/Contacts.xml");
        Document document = saxReader.read(is);

        // 3、文档对象的方法：可以获取根元素
        Element root = document.getRootElement();
        System.out.println(root.getName());

    }

    @Test
    public void parseXMLAllNode() throws Exception {
        // 1、创建一个SAXReader解析器对象：代表了Dom4j框架
        SAXReader saxReader = new SAXReader();
        // 2、推荐方案：读取字节输入流(默认认为/是直接去src下寻找的)
        Document document = saxReader.read(Dom4jDemo1.class.getResourceAsStream("/Contacts.xml"));
        // 3、提取根元素对象。
        Element root = document.getRootElement();

        // 4、提取根元素下的全部一级子元素
        //List<Element> elements = root.elements();
        List<Element> elements = root.elements("contact");
        for (Element element : elements) {
            System.out.println(element.getName());
        }
        // 注意：如果下面有多个子元素名称相同。默认提取第一个子元素
        Element sonEle = root.element("contact");
        System.out.println(sonEle.getName());
        System.out.println(sonEle.elementText("name"));

        // 5、如何取属性
        System.out.println(sonEle.attributeValue("id"));
        System.out.println(sonEle.attributeValue("vip"));
        // 得到属性对象
        Attribute idAttr = sonEle.attribute("id");
        System.out.println(idAttr.getName());
        System.out.println(idAttr.getValue());

        // 6、如何取文本信息
        System.out.println(sonEle.elementText("name"));
        System.out.println(sonEle.elementTextTrim("name")); // 去掉前后空格
        System.out.println(sonEle.elementText("gender"));
        System.out.println(sonEle.elementTextTrim("gender"));
        System.out.println(sonEle.elementText("email"));
        System.out.println(sonEle.elementTextTrim("email"));

        // 先得到元素对象，再提取文本值
        Element nameEle = sonEle.element("name");
        System.out.println(nameEle.getText());
        System.out.println(nameEle.getTextTrim()); // 去掉前后空格
    }

    @Test
    public void parseXMLToList() throws Exception {
        // 1、创建一个SAXReader解析器对象：代表了Dom4j框架
        SAXReader saxReader = new SAXReader();
        // 2、推荐方案：读取字节输入流(默认认为/是直接去src下寻找的)
        Document document = saxReader.read(Dom4jDemo1.class.getResourceAsStream("/Contacts.xml"));
        // 3、提取根元素对象。
        Element root = document.getRootElement();
        // 4、提取全部一级子元素
        List<Element> elements = root.elements("contact");
        // 5、定义一个ArrayList集合准备存储3个联系人对象信息
        List<Contact> contacts = new ArrayList<>();
        // 6、开始遍历每个子元素
        for (Element element : elements) {
            // 7、每个元素都是一个联系人对象：创建一个联系人对象来封装数据
            Contact contact = new Contact();
            // 8、解析数据：注入到对象中去
            contact.setId(Integer.valueOf(element.attributeValue("id")));
            contact.setVip(Boolean.valueOf(element.attributeValue("vip")));
            contact.setName(element.elementTextTrim("name"));
            contact.setSex(element.elementText("gender").charAt(0));
            contact.setEmail(element.elementTextTrim("email"));
            // 9、把联系人对象存入到集合中去
            contacts.add(contact);
        }
        // 10、遍历集合即可
        for (Contact contact : contacts) {
            System.out.println(contact);
        }

    }
}

```



# XPath

使用**路径表达式**来定位XML文档中的元素节点或属性节点

导入包

代码

```java
/**
    目标：XPath检索XML中的信息啊。(了解)

    引入：
        Dom4J可以用于解析整个XML的数据。
        但是如果要检索XML中的某些信息，建议使用XPath.（Xpath依赖Dom4j技术）
        Dom4J用于解析数据，Xpath用于检索数据。
    XPath使用步骤：
        1.导入dom4j框架。（XPath依赖于Dom4j技术,必须先导入dom4j框架！）
        2.导入XPath独有的框架包。jaxen-1.1.2.jar
    XPath常用API:
        List<Node> selectNodes(String var1):检索出一批节点集合。
        Node selectSingleNode(String var1)：检索出一个节点返回。
    XPath提供的四种检索数据的写法：
        1.绝对路径。
        2.相对路径。
        3.全文搜索。
        4.属性查找。
    小结：
         1.绝对路径： /根元素/子元素/子元素。
         2.相对路径： ./子元素/子元素。 (.代表了当前元素)
         3.全文搜索：
                //元素  在全文找这个元素
                //元素1/元素2  在全文找元素1下面的一级元素2
                //元素1//元素2  在全文找元素1下面的全部元素2
         4.属性查找。
                //@属性名称  在全文检索属性对象。
                //元素[@属性名称]  在全文检索包含该属性的元素对象。
                //元素[@属性名称=值]  在全文检索包含该属性的元素且属性值为该值的元素对象。
 */
public class XPathDemo {
    /**
     1.绝对路径: /根元素/子元素/子元素。
     */
    @Test
    public void parse01() throws Exception {
        // a、创建解析器对象
        SAXReader saxReader = new SAXReader();
        // b、把XML加载成Document文档对象
        Document document =
                saxReader.read(XPathDemo.class.getResourceAsStream("/Contacts2.xml"));
        // c、直接检索：
        List<Node> nodes = document.selectNodes("/contactList/contact/name");
        for (Node node : nodes) {
            Element nameEle = (Element) node;
            System.out.println(nameEle.getTextTrim());
        }
    }

    /**
      2.相对路径： ./子元素/子元素。 (.代表了当前元素)
     */
    @Test
    public void parse02() throws Exception {
        // a、创建解析器对象
        SAXReader saxReader = new SAXReader();
        // b、把XML加载成Document文档对象
        Document document =
                saxReader.read(XPathDemo.class.getResourceAsStream("/Contacts2.xml"));
        Element root = document.getRootElement();
        // c、直接检索：.代表的就是当前相对的根元素
        List<Node> nodes = root.selectNodes("./contact/name");
        for (Node node : nodes) {
            Element nameEle = (Element) node;
            System.out.println(nameEle.getTextTrim());
        }
    }

    /**
     3.全文搜索
     //元素  在全文找这个元素
     //元素1/元素2  在全文找元素1下面的一级元素2
     //元素1//元素2  在全文找元素1下面的全部元素2
     */
    @Test
    public void parse03() throws Exception {
        // a、创建解析器对象
        SAXReader saxReader = new SAXReader();
        // b、把XML加载成Document文档对象
        Document document =
                saxReader.read(XPathDemo.class.getResourceAsStream("/Contacts2.xml"));

        // c、直接检索：
        // List<Node> nodes = document.selectNodes("//name");
        // List<Node> nodes = document.selectNodes("//contact/name");
        List<Node> nodes = document.selectNodes("//contact//name");
        for (Node node : nodes) {
            Element nameEle = (Element) node;
            System.out.println(nameEle.getTextTrim());
        }
    }

    /**
     4.属性查找。
     //@属性名称  在全文检索属性对象。
     //元素[@属性名称]  在全文检索包含该属性的元素对象。
     //元素[@属性名称=值]  在全文检索包含该属性的元素且属性值为该值的元素对象。
     */
    @Test
    public void parse04() throws Exception {
        // a、创建解析器对象
        SAXReader saxReader = new SAXReader();
        // b、把XML加载成Document文档对象
        Document document =
                saxReader.read(XPathDemo.class.getResourceAsStream("/Contacts2.xml"));

        // c、检索属性信息
        List<Node> nodes = document.selectNodes("//@id");
        for (Node node : nodes) {
            Attribute attribute = (Attribute) node;
            System.out.println(attribute.getName() + "=" + attribute.getValue());
        }

        // 检索元素的
        List<Node> nodes1 = document.selectNodes("//contact[@id]");
        for (Node node : nodes1) {
            Element nameEle = (Element) node;
            System.out.println(nameEle.elementTextTrim("name"));
        }

        // 检索元素
        Node node = document.selectSingleNode("//contact[@id='3']");
        Element conEle = (Element) node;
        System.out.println(conEle.elementTextTrim("name"));
    }
}

```



# 设计模型

[十、JAVA设计模式的引出](https://blog.csdn.net/qq_38367575/article/details/120208473)





