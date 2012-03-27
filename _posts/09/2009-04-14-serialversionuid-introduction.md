--- 
layout: post
title: "serialVersionUID\xE4\xBB\x8B\xE7\xBB\x8D"
published: true
meta: {}

tags: 
- IT
- Java
type: post
status: publish
---
<h2>What is serialVersionUID?</h2>
serialVersionUID是Serializable类的验证器。也就是说，在序列化时，通过判断serialVersionUID来验证版本的一致性。如果没有匹配，将会抛出<tt><a href="http://java.sun.com/javase/6/docs/api/java/io/InvalidClassException.html">InvalidClassException</a>异常。</tt>
<h2>Guidelines for serialVersionUID</h2>
serialVersionUID的几条注意事项
<ul>
	<li>在类中要加入serialVersionUID字段，即使这是该类的第一个版本</li>
	<li>在未来的版本中不要去修改serialVersionUID的值，除非你了解修改以后将导致新旧版本不兼容</li>
	<li>即使保持serialVersionUID的值不变，序列化类的新版本也有可能与旧版本不兼容</li>
</ul>
<h2>Generate serialVersionUID using Eclipse</h2>
<p style="text-align: center;"><img class="aligncenter" src="http://farm4.static.flickr.com/3340/3440486099_d67cb84e27_o.png" alt="" width="700" height="194" /></p>

这里有两种添加方式：
默认的serialVersionUID和生成serialVersionUID。
选择默认的话将设为private static final long serialVersionUID = 1L;
而生成的话将生成一个随机值（其实是根据类名、接口名、成员方法及属性等来生成一个64位的哈希字段）
<h2>Summary</h2>
Java序列化是一个简单而又高深的部分，在实践中要慢慢学习。
