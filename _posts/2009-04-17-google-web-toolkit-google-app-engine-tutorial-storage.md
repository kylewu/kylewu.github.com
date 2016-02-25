---
layout: post
title: Google Web Toolkit 和 Google App Engine 综合教程 存储篇
date: 2009-04-17 00:00:00.000000000 +02:00
published: true
categories:
- 编程技术
tags:
- eclipse
- gae
- google
- gwt
- java
---
前面已经向同学们简要介绍了Google Web Toolkit 和 Google App Engine ，并且做出了一个初步的界面。在这篇教程里，我们将一起学习如何使用Google App Engine 的数据库。

## 简单介绍Google App Engine 的数据库

Google App Engine 的数据库提供了健壮的可扩展的分布式数据存储，我们不必考虑连接哪一个数据库，也不需要配置连接参数。我们需要做的是调用简单的API来进行各种操作。

Google App Engine 的数据库提供了两套API ： 标准API和底层API。标准API是与App Engine解耦的，所以使用标准API你可以很方便的将你的应用移植到其他环境中；而是用底层API，你可以让你的应用拥有更好的性能。

Google App Engine 支持两种连接数据库的标准： Java Data Objects (JDO) 和 Java Persistence API (JPA)。从Google App Engine 的网站中可以看到，它们都是由[DataNucleus Access Platform](http://www.datanucleus.org/)提供的，不过我没有细看，有兴趣的同学可以自己点进去学习。

## 什么是JDO ?

Java Data Objects (JDO) 是存储对象的标准接口。使用了JDO的应用程序不需要关心数据库类型，不论是关系数据库，层次数据库还是对象数据库，这样在我们更换数据源的时候会非常的方便。

要在Google App Engine项目中支持JDO，需要进行配置，不过Eclipse的插件已经帮我们做好了，再次请有兴趣的同学移步[这里](http://code.google.com/appengine/docs/java/datastore/usingjdo.html#Setting_Up_JDO)仔细学习。

Java Persistence API (JPA) 和JDO的作用相似，我现在使用的JDO，所以就不多做介绍了，[链接](http://code.google.com/appengine/docs/java/datastore/usingjpa.html)补上。

## 建立数据库的POJO类

前面进行了简单介绍，下面来实际操作一下。新建一个net.kylewu.idea.db.dataobject.Idea类。

    package net.kylewu.idea.server;
    import java.io.Serializable;
    import javax.jdo.annotations.IdGeneratorStrategy;
    import javax.jdo.annotations.IdentityType;
    import javax.jdo.annotations.PersistenceCapable;
    import javax.jdo.annotations.Persistent;
    import javax.jdo.annotations.PrimaryKey;

    @PersistenceCapable(identityType = IdentityType.APPLICATION)
    public class Idea implements Serializable {

        /**
         *
         */
        private static final long serialVersionUID = 1083036616443527590L;

        @PrimaryKey
        @Persistent(valueStrategy = IdGeneratorStrategy.IDENTITY)
        private Long id;
        @Persistent
        private String subject;
        @Persistent
        private String detail;
        @Persistent
        private String progress;
        @Persistent
        private String date;

        public Idea(Long id, String subject, String detail, String progress,
                String date) {
            super();
            this.id = id;
            this.subject = subject;
            this.detail = detail;
            this.progress = progress;
            this.date = date;
        }

        public Idea(String subject, String detail, String progress, String date) {
            this.subject = subject;
            this.detail = detail;
            this.progress = progress;
            this.date = date;
        }

        public Long getId() {
            return id;
        }

        public void setId(Long id) {
            this.id = id;
        }

        public String getSubject() {
            return subject;
        }

        public void setSubject(String subject) {
            this.subject = subject;
        }

        public String getDetail() {
            return detail;
        }

        public void setDetail(String detail) {
            this.detail = detail;
        }

        public String getProgress() {
            return progress;
        }

        public void setProgress(String progress) {
            this.progress = progress;
        }

        public String getDate() {
            return date;
        }

        public void setDate(String date) {
            this.date = date;
        }

        public String toString(){
            return String.valueOf(id)+"|"+subject+"|"+detail+"|"+progress+"|"+date;
        }
}

JDO使用annotations来表示数据如何在数据库中存储。这里我们把id设置为主键。

与数据库交互需要用到PersistenceManager对象，它是由PersistenceManagerFactory中获得的，为了免去重复创建factory的开销，使用singleton模式来实现这个类。Google App Engine 上提供了一个很好的例子，我直接拿来用了。

    package net.kylewu.idea.db;
    import javax.jdo.JDOHelper;
    import javax.jdo.PersistenceManagerFactory;

    public final class PMF {
        private static final PersistenceManagerFactory pmfInstance = JDOHelper
        .getPersistenceManagerFactory("transactions-optional");

        private PMF() {
        }

        public static PersistenceManagerFactory get() {
            return pmfInstance;
        }
    }

好了，这样就可以get到PersistenceManager对象了，那么该如何存储查询对象呢？代码很简单。

    Idea idea = new Idea ("Kylewu Idea", "This is Kyle Wu's idea.", "75%", "");
    PersistenceManager pm = PMF.get().getPersistenceManager();
    pm.makePersistent(idea);
    String query = "select from " + Idea.class.getName();
    (List) list = pm.newQuery(query).execute();

同学们要问了，我们怎么让他跑起来呢？这个涉及到Google Web Toolkit 与服务器端的交互了，下一篇教程将详细介绍。
