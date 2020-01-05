# XML

文档声明：<?xml version="1.0" encoding="UTF-8"?>

encoding: 解析XML文件时使用的字符集

## XML约束

## XML解析

### DOM解析

#### DOM解析原理

    XML解析器一次性把整个XML文档加载到内存，然后构建一棵Document对象树。通过Document对象，得到树上的节点对象，通过节点对象访问（操作）XML文档内容。

常用的节点类型

|节点类型|NodeType|Named Constant|nodeName 返回值|nodeValue 返回值|
|:-:|:-:|:-:|:-:|:-:|:-:|
|Element|1|ELEMENT_NODE|element name|null|
|Attr|2|ATTRIBUTE_NODE|属性名称|属性值|
|Text|3|TEXT_NODE|#text|节点内容|

```
// JDK API
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(file);
```

```
// JDOM API
SAXBuilder builder = new SAXBuilder();
Document document = builder.build(file);
```

```
// DOM4J API
SAXReader reader = new SAXReader();
Document document = reader.read(file);
```

### SAX解析

#### 解析原理

    使用handler对文档的内容依次进行解析

```
// JDK API
SAXParserFactory factory = SAXParserFactory.newInstance();
SAXParser parser = factory.newSAXParser();
//file : 文件路径
//DefaultHandler : 处理器默认父类，该类实现了ContentHandler接口
parser.parse(file, DefaultHandler); 
```

