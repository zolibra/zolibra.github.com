---
layout: post
title: "Think In Tomcat part1"
description: ""
category: 
tags: [Tomcat, Java, OpenSource]
---
{% include JB/setup %}

In Tomcat Class 'StandardService',there is an dynamic array implementation:


    public void addConnector(Connector connector) {
        synchronized (connectors) {
            connector.setContainer(this.container);
            connector.setService(this);
            Connector results[] = new Connector[connectors.length + 1];
            System.arraycopy(connectors, 0, results, 0, connectors.length);
            results[connectors.length] = connector;
            connectors = results;
            if (initialized) {
                try {
                    connector.initialize();
                } catch (LifecycleException e) {
                    e.printStackTrace(System.err);
                }
            }
            if (started && (connector instanceof Lifecycle)) {
                try {
                    ((Lifecycle) connector).start();
                } catch (LifecycleException e) {
                    ;
                }
            }
            support.firePropertyChange("connector", null, connector);
        }
    }

显然对Connector的随机存储要求大于add remove 操作。

在java中，什么时候用arrayList 什么时候用 linkedlist呢？
答：
当操作是在一列数据的后面添加数据而不是在前面或中间,并且需要随机地访问其中的元素时,使用ArrayList会提供比较好的性能；
当你的操作是在一列数据的前面或中间添加或删除数据,并且按照顺序访问其中的元素时,就应该使用LinkedList了

