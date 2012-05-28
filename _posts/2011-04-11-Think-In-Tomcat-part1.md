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

What

