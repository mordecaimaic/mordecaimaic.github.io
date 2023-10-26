---
layout: post
title: 数据结构-单链表分拆(更新中)
---

如何把一个单链表拆成两个单链表

其中一个链表为原链表的奇数索引，另一个为原链表的偶数索引

###### 方法一：
``` c++
#include <iostream>
using namespace std;
typedef struct node
{
    int data;
    struct node *next;
}Lnode, *LinkList;

int rear_create_link_list(LinkList &L1, int n);
int divide_link_lisk(LinkList &La, LinkList&Lb);

void out_put(LinkList &L);

int main(int argc, const char * argv[]) {
    
    LinkList La;
    LinkList Lb;
    rear_create_link_list(La, 5);
    divide_link_lisk(La, Lb);

    out_put(La);
    out_put(Lb);
    return 0;
}

int rear_create_link_list(LinkList &L, int n)
{
    L = new node;
    Lnode *r = L;
    for(int i = 0; i < n; i++)
    {
        Lnode *p = new node;
        if (p == NULL)
            return 1;
        cout << "Input the " << i << " th data: ";
        cin >> p->data;
        p->next = NULL;
        r->next = p;
        r = p;
    }
    
    return 0;
}

int divide_link_lisk(LinkList &La, LinkList&Lb)
{
    Lnode *p1 = La;
    Lnode *p3 = La->next;
    Lb = new node;
    Lnode *p2 = Lb;
    if (Lb == NULL)
        return 1;
    
    for (int i = 1; p3 != NULL; i++)
    {
        if (i % 2 == 0)
        {
            p2->next = p3;
            p2 = p3;
            p3 = p3->next;
        }
        else
        {
            p1->next = p3;
            p1 = p3;
            p3 = p3->next;
        }
    }
    p1->next = NULL;
    p2->next = NULL;
    return 0;
}

void out_put(LinkList &L)
{
    Lnode *p = L->next;
    while(p)
    {
        cout<< p->data <<' ';
        p = p->next;

    }
    cout << "\n";
}
```
