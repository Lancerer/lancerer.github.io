---
layout: post
title: "数据结构之循环队列"
date: 2018-10-24 18:47
categories: Queue
tags: 数据结构，队列
mathjax: true
---

* content
{:toc}



### 介绍队列这个数据结构
```html
   队列（先进先出）：队列也是一种线性数据结构，他只能从一端添加数据（队尾），只能从另一端（队首）取出元素
         分类：
            链式队列：使用链表实现
            静态队列：使用数组实现， 静态队列通常都必须是循环队列
                循环队列：
                    1.静态队列为什么必须是循环队列
                    2.循环队列需要几个参数来确定
                        (1).队列初始化：front和rear的值都是零
                        (2).队列非空：front表示队列的第一个元素，rear代表的是队列的最后一个有效元素的后一个元素
                        (3).队列为空:front和rear的值相等，但是不一定等于零
                    3.循环队列各个参数的含义
                    4.循环队列入队操作：
                        (1).将值存入rear所代表的位置中
                        (2).错误：r=r+1  正确：r=（r+1）%数组长度
                   5. 循环队列出队操作：
                        f=（f+1）%数组长度
                   6.如何判断循环队列是否为空：
                        如果front与rear的值相等，则该队列一定为空
                   7.如何判断循环队列是否已满：
                        两种方式：
                            1.多添加一个标志位参数，记录循环队列中的元素
                            2.少用一个元素，如果rear在front相邻的位置时就表示队列已满
                                if（（rear+1）%数组长度==f）
                                        已满
                                else
                                        不满
```

### 循环队列的数据结构(使用数组实现)

```c
typedef struct Queue
{
    int * pBase;//等价于定义一个动态数组
    int front;//指向对首的下标
    int rear;//指向队尾的下标
} QUEUE;

```

### 循环列表的初始化
```c

void init_queue(QUEUE * pq)
{
    //这里假定数组长度为6
    pq->pBase=(int *)malloc(sizeof(int) *6);
    pq->front=0;
    pq->rear=0;
}

```
![image](http://phcabd9ew.bkt.clouddn.com/staticQueue_loopQueue.png)

### 循环队列是否为空
```c

/**
*循环队列在初始化时即空列时对首和队尾的两个坐标是相等的
*/
bool isEmpty_queue(QUEUE *pq)
{
    if(pq->front==pq->rear)
        return true;
    else
        return false;
}

```

### 循环队列是否已满
```c
/**
*循环队列规定当队尾rear在靠近队首front时就表示队列已满
*这样虽然浪费了一个位置，但是很好的和初始化区分开来了
*/

bool full_queue(QUEUE *pq)
{
    if((pq->rear+1)%6==pq->front)
        return true;
    else
        return false;
}

```

### 循环队列的入队操作
```c
/**
*当队列满时返回false，当队列没满时向队列加入元素，并且队尾向前移动一位
*/
bool en_queue(QUEUE * pq,int val)
{
    if(full_queue(pq))
    {
        return false;
    }
    else
    {
        pq->pBase[pb->rear]=val;
        pq->rear=(pq->rear+1)%6;
        return true;
    }
}
```

### 循环队列的出队操作
```c
/**
*当队列为空时出队操作失败，当队列不为空时从对首删除元素，同时对首向前移动一位
*同时可以返回出队的元素
*/
bool out_queue(QUEUE * pq,int *val)
{
    if(isEmpty_queue(pq))
    {
        printf("出队失败");
        return false;    
    }
    else
    {
        *val=pq->pBase[pq->front];
        pq->front=(pq->front+1)%6;
        return true;
    }
}

```

### 循环队列的遍历
```c
void traverse_queue(QUEUE *pq)
{
    int i=pq->front;
    while(i!=pq->rear)
    {
        printf("%d  ",pq->pBase[i]);
        i=(i+1)%6;
    }
    return;

}

```

### 测试代码
```c
int main()
{
    QUEUE q;
    int val;
    initQueue(&q);
    en_queue(&q,1);
    en_queue(&q,2);
    en_queue(&q,3);
    en_queue(&q,4);
    en_queue(&q,5);
    en_queue(&q,6);
    en_queue(&q,7);
    traverse_queue(&q);

    if(out_queue(&q,&val))
        printf("出队成功出队元素是%d\n",val);
        
     traverse_queue(&q);

    return 0;
}

控制台输出：
1  2  3  4  5  出队成功出队元素是1
2  3  4  5
```