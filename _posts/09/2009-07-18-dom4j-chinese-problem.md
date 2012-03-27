--- 
layout: post
title: !binary |
  RG9tNGog5Lit5paH6Zeu6aKY

published: true
meta: {}

tags: 
- Coding
- Java
type: post
status: publish
---
第一次使用dom4j进行xml文件的处理，使用很简单，开发很高效。

测试中中文会出现乱码，看了一下生成的文件，默认为utf-8存储，这样乱码必然会出现。

解决方法也很简单，见如下代码
<code lang="java">		OutputFormat format = OutputFormat.createPrettyPrint();
		format.setEncoding("gbk");
		XMLWriter writer = new XMLWriter(new FileWriter("commands.xml"), format);
		Document document = reader.read("commands.xml");
		writer.write(document);
		writer.close();</code>
也就是在写入文件时设置一下编码格式就可以解决乱码问题。
<p style="text-align: left;"><a href="http://farm4.static.flickr.com/3447/3728273509_6088773511_o.png"><img class="aligncenter" title="Dom4j" src="http://farm4.static.flickr.com/3447/3728273509_6088773511_o.png" alt="" width="1" height="1" /></a></p>
