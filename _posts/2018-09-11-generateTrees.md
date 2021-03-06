---
layout: post
title:  "95. 不同的二叉搜索树 II"
categories: 算法
tags: leetcode 动态规划
---

* content
{:toc}

<!--more-->

给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。

示例:

```
输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

解：

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n <= 0) {
            return new ArrayList<TreeNode>();
        }
        return generateSubTree(1, n);
    }

    public ArrayList<TreeNode> generateSubTree(int start, int end) {
        ArrayList<TreeNode> result = new ArrayList<TreeNode>();
        if (start > end) {
            result.add(null);
            return result;
        }
        for (int rootVal = start; rootVal <= end; rootVal++) {
            for (TreeNode leftSubTreeRoot : generateSubTree(start, rootVal - 1)) {
                for (TreeNode rightSubTreeRoot : generateSubTree(rootVal + 1, end)) {
                    TreeNode root = new TreeNode(rootVal);
                    root.left = leftSubTreeRoot;
                    root.right = rightSubTreeRoot;
                    result.add(root);
                }
            }
        }
        return result;
    }
}
```
