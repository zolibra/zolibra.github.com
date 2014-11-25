---
layout: post
title: "[leetcode]Determine If Two Rectangles Overlap"
description: ""
category: 
tags: [algorithsm, leetcode]
---
{% include JB/setup %}

Given two axis-aligned rectangles A and B. Write a function to determine if the two rectangles overlap.


	/**
	 * Created by ray on 11/20/14.
	 */
	/*
	^
	|
	| |---------|maxPoint
	| |         |
	| |         |
	| -----------
	|minPoint
	----------------------->
	 */
	class Point{
	    int x;
	    int y;
	    public Point(int x , int y){
	        this.x = x;
	        this.y = y;
	    }
	}
	
	class Rectangle{
	    Point minPoint;
	    Point maxPoint;
	
	    public Rectangle(int x1, int y1, int x2, int y2){
	        minPoint = new Point(x1, y1);
	        maxPoint = new Point(x2, y2);
	    }
	
	}
	
	public class RectanglesOverlapCheck {
	
	    public boolean isOverlap(Rectangle a , Rectangle b){
	        if (a.minPoint.x > b.maxPoint.x)return false; //a is on the right of b
	        if (a.minPoint.y > b.maxPoint.y)return false; //a is above of b
	        if (a.maxPoint.x < b.minPoint.x)return false; //a is on the left of b
	        if (a.maxPoint.y < b.minPoint.y)return false; //a is below of b
	        return true;
	    }
	
	    public static void main(String[] args) {
	        RectanglesOverlapCheck check = new RectanglesOverlapCheck();
	
	        int[][] a = {{1,1,3,4,2,3,5,5},
	                {2,3,5,5,1,1,3,4},
	                {2,2,5,3,3,1,4,5}, // cross intersection
	                {1,1,2,2,3,3,4,4}//not overlap
	        };
	        for (int i = 0; i < a.length; i++) {
	            boolean isOverlap = check.isOverlap(new Rectangle(a[i][0],a[i][1],a[i][2],a[i][3]),
	                    new Rectangle(a[i][4],a[i][5],a[i][6],a[i][7]));
	            System.out.println(isOverlap);
	        }
	
	    }
	}


Next Question: How to detecting whether two convex polygons overlap?