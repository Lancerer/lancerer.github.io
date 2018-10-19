---
layout: post
title:  "数据结构之链表"
date:   2018-10-19 15:14:54
categories: linkedlist
tags: linkedlist
excerpt: 数据结构
mathjax: true
---

* content
{:toc}

### 链表的创建
``` c
PNODE create_list()
{
    int len;//存放有效节点的个数
    int i;
    int val;//存放用户输入的节点的值


    //分配一个没有存储数据的头结点
    PNODE pHead=(PNODE)malloc(sizeof(NODE));
    if(NULL==pHead)
    {
        printf("分配内存失败");
        exit(-1);
    }

    PNODE pTail=pHead;
    pTail->pNext=NULL;

    printf("请输入要创建几个节点的链表len=");
    scanf("%d",&len);

    for(i=0; i<len; i++)
    {
        printf("请输入第%d个节点的值:    ",i+1);
        scanf("%d",&val);

        PNODE pNew=(PNODE)malloc(sizeof(NODE));
        if(NULL==pNew)
        {
            printf("分配内存失败");
            exit(-1);
        }

        pNew->data=val;
        pTail->pNext=pNew;
        pNew->pNext=NULL;
        pTail=pNew;

    }

    return pHead;

}

```
![image](https://github.com/Lancerer/lancerer.github.io/blob/master/img/create_list.png)

### 链表的遍历
``` c
void show_list(PNODE pHead)
{
    PNODE p=pHead->pNext;

    while(NULL!=p)
    {
        printf("%d  ",p->data);
        p=p->pNext;//随着遍历指针也需要指向下一个节点的指针域

    }
    printf("\n");
    return;

}
```

### 链表的排序
```c
void sort_list(PNODE pHead)
{

    //采用冒牌排序

    int i, j, t;
    int len = length_list(pHead);
    PNODE p, q;//这里p表示首元素，q表示p的下一个元素

    for (i=0,p=pHead->pNext; i<len-1; ++i,p=p->pNext)
    {
        for (j=i+1,q=p->pNext; j<len; ++j,q=q->pNext)
        {
            if (p->data > q->data)  //类似于数组中的a[i]>a[j]
            {
                t = p->data;//类似于数组中的：t=a[i];
                p->data = q->data; //类似于数组中的a[i]=a[j]
                q->data = t; //类似于数组中得a[j]=t;
            }
        }
    }

    return;
}

```

### 链表的长度
``` c
int length_list(PNODE pHead)
{
    PNODE p=pHead->pNext;
    int len=0;
    while(NULL!=p)
    {
        len++;
        p=p->pNext;
    }
    return len;
}

```


### 向链表的第pos个节点之前插入一个节点
``` s
bool insert_list(PNODE pHead,int pos,int val)
{
    PNODE p=pHead;
    int j=0;//计数使用
    
    //寻找第pos-1个节点
    while(p&&j<pos-1)
    {
        p=p->pNext;
        j++;

    }
    
    //当要插入的pos大于表长就返回false
    if(!p||j>pos-1)
        return false;

    //这里就是向链表插入一个节点的操作
    PNODE q=(PNODE)malloc(sizeof(NODE));
    q->data=val;
    q->pNext=p->pNext;
    p->pNext=q;
    
    return true;

}
```
![image](https://github.com/Lancerer/lancerer.github.io/blob/master/img/insert_list.png)


### 删除第pos个节点（和插入有点类似）
``` c
int delete_list(PNODE pHead,int pos,int val)
{
    PNODE p=pHead;
    int j=0;
    while(p->pNext&&j<pos-1)
    {
        p=p->pNext;
        j++;
    }
    if(!p->pNext||j>pos-1)
        return false;

    PNODE q=p->pNext;
    val=q->data;
    p->pNext=p->pNext->pNext;
    free(q);
    return val;
}

```
![image](https://github.com/Lancerer/lancerer.github.io/blob/master/img/delete_list.png)