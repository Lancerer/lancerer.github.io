---
layout: post
title:  "数据结构之链表"
date:   2018-10-19 15:14:54
categories: linkedlist
tags: linkedlist 算法
excerpt: 数据结构
mathjax: true
---

* content
{:toc}

### 介绍链表这个数据结构(离散存储)
```
     定义：
        n个节点离散分配，彼此使用指针相连，每个节点只有一个前驱节点和一个后续节点，首节点没有前驱节点尾节点没有后续节点
        
专业术语：
            首节点：第一个有效节点
            尾节点：最后一个有效节点
            头结点：第一个有效节点之前的节点，头结点不存放有效数据，加头结点是为了方便操作链表
            头指针：指向头结点的指针变量
            尾指针：指向尾节点的指针变量

 分类：
        单链表：
        双链表：每一个节点都有两个指针域
        *** 循环链表：能通过任何一个节点找到其他所有的节点，他和单链表的主要差异就是：当p->next
        =null时链表为空，循环链表则是当p->pnext不等于头结点链表就不为空
        非循环链表：
        
优缺点：
        优点：没有空间限制，插入删除元素很快
        缺点：存储速度很慢

如果希望通过一个函数对链表进行处理，我们只需要知道一个头指针就行，头指针中包含下一个节点的地址，然后链表又是连续的我们就可以相继的推算出所有链表的参数
```

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
![image](http://phcabd9ew.bkt.clouddn.com/create_list.png)

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
![image](http://phcabd9ew.bkt.clouddn.com/insert_list.png)


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
![image](http://phcabd9ew.bkt.clouddn.com/delete_list.png)

### 测试代码
```c
int main()
{
    PNODE pHead=NULL;

    pHead=create_list();

    show_list(pHead);

    int len=length_list(pHead);

    if(isEmpty_list(pHead))
    {
        printf("链表内容为空\n");
    }

    printf("链表的长度为：%d\n",len);

    sort_list(pHead);
    printf("排序后的链表内容：");
    show_list(pHead);

//   if(insert_list(pHead,3,555))
//    show_list(pHead);

    delete_list(pHead,2,99);
    show_list(pHead);


    return 0;
}

控制台输出：

请输入要创建几个节点的链表len=6
请输入第1个节点的值:    1
请输入第2个节点的值:    2
请输入第3个节点的值:    3
请输入第4个节点的值:    2
请输入第5个节点的值:    5
请输入第6个节点的值:    9
1  2  3  2  5  9
链表的长度为：6
排序后的链表内容：1  2  2  3  5  9
1  2  3  5  9
```

### 循环链表
```c
循环链表：能通过任何一个节点找到其他所有的节点，当他知道其中一个节点时就可以继续查找下去，不像
	单链表一样只能从头开始遍历

循环链表还可以在链表的尾部加上一个尾指针，即rear，rear->next就是头结点，rear->next->next就是链表的第一个节点

两条链表的合并
p=rearA->next ;	//保存a表的头结点
rearA->next=rearB->next->next;//将本是指向b表的第一个节点(不是head)赋值给rearA->next
rearB->next=p//将原A表的头结点赋值给rearB->next
free(p);//释放p
```
![iamge](http://phcabd9ew.bkt.clouddn.com/%E5%8D%95%E9%93%BE%E8%A1%A8%E7%9A%84%E5%90%88%E5%B9%B6.png)