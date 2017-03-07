---
layout: post
title:  "二叉树的生成"
date:   2016-12-11 20:11:00
categories: cpp
tags: cpp
---
**问题：**输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。  
　已知二叉树的前序列表及中序列表可以确定一个二叉树，根据前序遍历的特点，可知道根节点为1，则在中序遍历列表中，{4,7,2}为节点1的左子树，{5,3,8,6}为节点1的右子树，之后节点1的左子树有前序列表{2,4,7}及后序列表{4,7,2}可以确定，递归调用。  
*定义树节点：*  
```C++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
```

```C++
class Solution {
    typedef vector<int>::iterator  vIter;
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
    
        if(pre.size()==0 || pre.size()!=vin.size()) return NULL;
        
        return ConstuctTree(pre.begin(), pre.end()-1, vin.begin(), vin.end()-1);

    }
    
    TreeNode* ConstuctTree(vIter preStart, vIter preEnd, vIter vinStart, vIter vinEnd) {
        //前序遍历第一个为根节点
        int rootVal = *preStart;
        TreeNode* rootNode = (TreeNode*)malloc(sizeof(TreeNode));
        rootNode->val = rootVal;
        rootNode->left = rootNode->right = NULL;
        
        if(preStart == preEnd) {
            if(vinStart == vinEnd && *vinStart == *vinEnd) {
                return rootNode;
            } else {
                throw std::exception();
            }
        }
        
        //中序中查找根节点，分为左右子树
        vIter rootVin = vinStart;
        
        while(*rootVin != rootVal && rootVin <= vinEnd) {
            ++rootVin;
        }
        
        int preLen = rootVin - vinStart;
        
        if(rootVin == vinEnd && *rootVin != rootVal) 
            throw std::exception();
        
        if(preLen > 0) {
            rootNode->left = ConstuctTree(preStart+1, preStart+preLen, vinStart, rootVin-1);
        }
        if(preLen < preEnd-preStart) {
            rootNode->right = ConstuctTree(preStart+preLen+1, preEnd, rootVin+1, vinEnd);
        }
        
        return rootNode;
        
    }
};
```