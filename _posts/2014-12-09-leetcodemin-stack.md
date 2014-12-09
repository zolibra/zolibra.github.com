---
layout: post
title: "[leetcode]Min Stack"
description: ""
category: 
tags: [Stack, List]
---
{% include JB/setup %}

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.

pop() -- Removes the element on top of the stack.

top() -- Get the top element.

getMin() -- Retrieve the minimum element in the stack.


**Solution 1**: Using LinkedList, But validation fail with Memory Limit Exceeded but Using Stack is ok, not sure why.

	class MinStack {    
	    LinkedList<Integer> minlist = new LinkedList<Integer>();
	    LinkedList<Integer> stack = new LinkedList<Integer>();
	    public void push(int x) {
	        stack.add(0,x);
	        if(minlist.size() == 0 ||x <= minlist.getFirst().intValue()){
	            minlist.add(0, x);
	        }
	    }
	    public void pop() {
	        if(stack.size() > 0){
	            int top = stack.getFirst().intValue();
	            stack.removeFirst();
	            if(top == minlist.getFirst().intValue())minlist.removeFirst();
	        }
	    }
	
	    public int top() {
	        if(stack.size() > 0)
	            return stack.getFirst().intValue();
	        return 0;
	    }
	
	    public int getMin() {
	        if (minlist.size() > 0)
	            return minlist.getFirst().intValue();
	        return 0;
	
	    }
	
	}
	
**Solution 2**: Using Stack directly, It passed. 

	class MinStack {  
	    Stack<Integer> minlist = new Stack<Integer>();
	    Stack<Integer> stack = new Stack<Integer>();
	
	    public void push(int x) {
	        stack.push(x);
	        if(minlist.size() == 0 ||x <= minlist.peek().intValue()){
	            minlist.push(x);
	        }
	    }
	
	    public void pop() {
	        if(stack.size() > 0){
	            int top = stack.peek().intValue();
	            stack.pop();
	            if(top == minlist.peek().intValue())minlist.pop();
	        }
	    }
	
	    public int top() {
	        if(stack.size() > 0)
	            return stack.peek().intValue();
	        return 0;
	    }
	
	    public int getMin() {
	        if (minlist.size() > 0)
	            return minlist.peek().intValue();
	        return 0;
	    }
	}

Solution 3: Another Solution that using only one Stack:

	public class MinStack {
	    long min;
	    Stack<Long> stack;
	
	    public MinStack(){
	        stack=new Stack<>();
	    }
	
	    public void push(int x) {
	        if (stack.isEmpty()){
	            stack.push(0L);
	            min=x;
	        }else{
	            stack.push(x-min);//Could be negative if min value needs to change
	            if (x<min) min=x;
	        }
	    }
	
	    public void pop() {
	        if (stack.isEmpty()) return;
	
	        long pop=stack.pop();
	
	        if (pop<0)  min=min-pop;//If negative, increase the min value
	
	    }
	
	    public int top() {
	        long top=stack.peek();
	        if (top>0){
	            return (int)(top+min);
	        }else{
	           return (int)(min);
	        }
	    }
	
	    public int getMin() {
	        return (int)min;
	    }
	}
