---
layout: post
title: "[leetcode]树的遍历"
description: ""
category: 
tags: [TreeNode, java]
---
{% include JB/setup %}

###Problem 1: Binary Tree Preorder Traversal 


Given a binary tree, return the preorder traversal of its nodes' values.

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
面试大部分还是考验非递归解法，所以用Stack迭代ms更考验思维,最好把思路画在纸上

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
    
###Problem 2: Binary Tree Inorder Traversal 

中序遍历： left --> root --> right

For example:
Given binary tree {1,#,2,3},

    1
     \
      2
     /
    3
return [1,3,2].

        Vector<Integer> result = new Vector<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        while(p!=null || !stack.empty()){
            if (p!=null){
                stack.push(p);
                p = p.left;
            }else {
                p = stack.peek();
                stack.pop();
                result.add((Integer) p.val);
                p = p.right;
            }
        }
        return result;
###Problem 3: Binary Tree Postorder Traversal 
后序遍历： left --> right --> root
For example:
Given binary tree {1,#,2,3},
  
    1
     \
      2
     /
    3
return [3,2,1].
后序遍历的迭代解法需要保存一个previous指针来辅助遍历右子树

    public static List<Integer> postorderNonRecursive(TreeNode root){
        List<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        TreeNode prevNode;
        do{
            while(p!=null){
                stack.push(p);
                p = p.left;
            }
            prevNode = null;
            while (!stack.empty()){
                p = stack.peek();
                stack.pop();
                if(p.right == prevNode){
                    result.add((Integer) p.val);
                    prevNode = p;
                }else{
                    stack.push(p);
                    p = p.right;
                    break;
                }

            }
        }while (!stack.empty());
        return result;

    }