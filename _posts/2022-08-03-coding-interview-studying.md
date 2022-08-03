---
layout: post
title: "Coding Interview Studying"
description: "Read up on how I use UMD CS curriculum to study for my coding interviews!"
date: 2022-08-03
feature_image: images/road.jpg
tags: [tips, work]
---
Studying for the coding interview is extremely stressful. That is why I am motivating myself to make sure I really understand the problems by posting ym thought process here on problems that I think are important.

<!--more-->

## Subtree of Another Tree - LeetCode 572
**Level: Easy**

**Problem Description**: Given the roots of two binary trees `root` and `subRoot`, return true if there is a subtree of `root` with the same structure and node values of `subRoot` and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

Here is the skeleton of the class that we are given: 
```java
  class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
    }
  }
```

Usually to start these problems, I begin with thinking about the base case. 

Lets think of what would happen if the root was null. Could anything be a subtree of it? Well, in this problem, it says that there has to be at least one node. Therefore, if the root is null, then there is no chance that it could return true. 

```java
  class Solution {
      public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root == null){
          return false;
        }
      }
    }
```

Now, we know that this subtree could be the whole tree itself, within the right subtree, or the left subtree. We need to check for each root if it is possible a subtree. So, this starts sounding like recursion.

However, since we need to check every possible subtree, we basically need to use recursion to act like a double for loop (sort of). We need to see for each node if its children match the subtree entirely. So, we can have the main method `isSubtree` call another helper method that traverses through all of the nodes in the current subtree that we are on. 

```java
  class Solution {
      public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root == null){
          return false;
        }
      }

      public boolean isSubtreeHelper(TreeNode root, TreeNode subRoot){

      }
    }
```

So, let's start with **case 1**: the subtree and the root are the same! Best case scenario kind of in terms of ease of thinking. 

We basically need to check for every node, if they have the same values.

If they are entirely the same, starting at the root, you would just call our traverser helper method and check every single node. 

```java
if(isSubtreeHelper(root, subRoot)){
            return true;
}
```

Since we will be traversing both trees at the same time and we could find out at any point that they are different sizes, we should first check to see if either is null. If one is null and the other one isnt, this means it would return `false` since they should be the same. 

```java
if(root == null || subRoot == null){
  return root == subRoot;
}
```

Otherwise, if they both are not null, we want to see if their values are the same! `root.val == subRoot.val`

But, we also need to check the right and left children/subtrees of this node as well. We want `root.val == subRoot.val` **and** all the values in the right subtree to be the same **and** all the values in the left subtree to be the same.

```java
public boolean isSubtreeHelper(TreeNode root, TreeNode subRoot){
        if(root == null || subRoot == null){
            return root == subRoot;            
        }
        return root.val == subRoot.val && isSubtreeHelper(root.right, subRoot.right) && isSubtreeHelper(root.left, subRoot.left);
    }
```

Now we have a helper method that traverses through each subtree and checks if its equal to the subRoot tree.

In the other **cases 2 and 3** where the `subRoot` subtree lies inside the right or left subtrees, we have to have another recursive call for each one. It just has to be for one or the other, so:

```java
 return isSubtree(root.right, subRoot) || isSubtree(root.left, subRoot);
 ```

We are done!
```java
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root == null){
            return false;
        }
        if(isSubtreeHelper(root, subRoot)){
            return true;
        }
        return isSubtree(root.right, subRoot) || isSubtree(root.left, subRoot);
    }
    
    public boolean isSubtreeHelper(TreeNode root, TreeNode subRoot){
        if(root == null || subRoot == null){
            return root == subRoot;            
        }
        return root.val == subRoot.val && isSubtreeHelper(root.right, subRoot.right) && isSubtreeHelper(root.left, subRoot.left);
    }
}
```

You have a helper function that traverses each subtree individually to see if this condition is true. You recurse through the subtrees using your main `isSubtree` function, and rely on your helper method to do the heavy lifting.





