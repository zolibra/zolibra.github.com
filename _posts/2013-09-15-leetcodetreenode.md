---
layout: post
title: "[leetcode]树的遍历"
description: ""
category: 
tags: [TreeNode, java]
---
{% include JB/setup %}

###Problem 1: Binary Tree Preorder Traversal 


iven a binary tree, return the preorder traversal of its nodes' values.

For example:
Given binary tree {1,#,2,3},

    1
     \
      2
     /
    3
   
return [1,2,3].

**Solution 1: Recursive**

    public static List<Integer> preorder(TreeNode p , List<Integer> list){
        if (p != null){
            list.add((Integer)p.val);
            preorder(p.left, list);
            preorder(p.right, list);
        }
        return list;
    }
    
**Solution 2: Stack**
面试大部分还是考验非递归解法，所以用Stack迭代ms更考验思维

    public static Vector<Integer> preorderNonRecursive(TreeNode root){
        Vector<Integer> result = new Vector<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;

        if (root != null){
            stack.push(p);
        }
        while(!stack.empty()){
            p = stack.peek();
            stack.pop();
            result.add((Integer) p.val);
            if (p.right != null)stack.push(p.right);
            if (p.left != null)stack.push(p.left);
        }

        return result;

    }
