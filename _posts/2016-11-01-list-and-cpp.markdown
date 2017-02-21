---
layout: post
title:  "单向链表的操作"
date:   2016-11-01 20:11:00
categories: cpp
tags: cpp
---
最近在代码中需要用链表来保存用户信息，所以来复习一下单项链表的实现，巩固一下。


```C
typedef struct node{
    int data;
    node *next;
}node;

node *create() {
    int i = 0;
    node *head, *p, *q;
    int x = 0;
    head = (node*)malloc(sizeof(node));
    while(1) {
        printf("Please input int data:\n");
        scanf("%d", &x);
        if(x == 0) break;       //若输入为0，则退出
        
        p = (node *)malloc(sizeof(node));
        if(p == NULL) {
            printf("malloc node failed\n");
            return NULL;
        }
        p->data = x;
        if(++i == 1) {
            head->next = p;
        } else {
            q->next = p;        //链表尾端
        }
        
        q = p;                  //q始终指向尾端
    }
    q->next = NULL;
    return head;


/*查找链表中某一位置的node*/
node *searchNode(node *head, int pos) {
    if(pos < 0) return NULL;
    if(pos == 0) return head;
    node *p = head->next;
    
    if(p == NULL) {
        printf("Linked list is empty\n");
        return NULL;
    }
    
    while(--pos) {
        if((p = p->next) == NULL) {
            printf("incorrect position to search node\n");
            break;
        }
    }
    
    return p;
}

/*链表中pos位置插入数据为data的节点*/
node *insertNode(node *head, int pos, int data) {
    node *item = NULL;
    node *p = NULL, *tmpNode = NULL;
    item = (node *)malloc(sizeof(node));
    if(item == NULL) {
        printf("malloc node failed\n");
        return NULL;
    }
    item->data = data;
    
    if(pos == 0) {
        tmpNode = head->next;
        head->next = item;
        item->next = tmpNode;
    }
    p = searchNode(head, pos);
    if(p) {
        item->next = p->next;
        p->next = item;
    }
    return head;
    
}

void printList(node *head) {
    node *p = head->next;
    if(!p) return;
    int index = 0;
    
    while(p) {
        printf("Node[%d] = %d\n", index, p->data);
        index++;
        p = p->next;
    }
}

/*删除位置pos的节点*/
node *deleteNode(node *head, int pos)
{
    node *item = NULL;
    node *p = head->next;
    if(p == NULL) {
        printf("Linked list is empty\n");
        return NULL;
    }
    
    p = searchNode(head, pos-1);
    
    if(p != NULL && p->next != NULL) {
        item = p->next;
        p->next = item->next;
        delete item;
    }
    return head;
}

/*链表的逆置*/
node *reverse(node *head)
{
    node *p, *q, *r;
    
    if(head->next == NULL) {
        return head;
    }
    
    p = head->next;
    q = p->next;
    p->next = NULL;
    
    while(q != NULL) {
        r = q->next;
        q->next = p;
        p = q;
        q = r;
    }
    
    head->next = p;
    return head;
}

}
```
