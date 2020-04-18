# 两数相加

难度：中等

## 题意

给出两个**非空**的链表用来表示两个非负的整数。其中，它们各自的位数是按照**逆序**的方式存储的，并且它们的每个节点只能存储**一位**数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字0之外，这两个数都不会以0开头。

## 示例

> 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
>
> 输出：7 -> 0 -> 8
>
> 原因：342 + 465 = 807

## 题解

这道题我用的方法是读出这两个由链表组成的数，然后相加，但是提交之后总是不能通过全部例子，后来发现最后几个例子很长，现有的数据类型容纳不了。参考题解了解到这个题是模拟加法运算，两个加数位，一个进位位，知道这个思想后就是写代码了。这个思想通信电子专业的同学可能也接触过，在数电模电课上做加法器之类的应该会用到，只是那个是电路，这个是代码。

### 方法一------迭代法

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    int c = 0;	//进位位
    struct ListNode *head, *cur, *next;
    head = (struct ListNode *)malloc(sizeof(struct ListNode));
    head->next = NULL;	//生成一个新链表
    cur = head;
    while(l1 != NULL || l2 != NULL || c)
    {
        next = (struct ListNode *)malloc(sizeof(struct ListNode));	//创建一个新的节点
        next->next = NULL;
        cur->next = next;	//把next放在cur和null之间，尾插法
        cur = next;
        (l1 != NULL) ? (c += l1->val, l1 = l1->next) : (c += 0);	//l1(l2)不为空，进位位c
        (l2 != NULL) ? (c += l2->val, l2 = l2->next) : (c += 0);	//加上l1(l2)，为空则加0
        cur->val = c % 10;	//此时c位三位总和，该步保存个位值
        c = c / 10;	//该步保存进位值
    }
    struct ListNode *del = head;
    head = head->next;
    free(del);	//释放空间
    return head;
}
```

### 方法二------递归法

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

int c = 0;
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    if(l1 == NULL && l2 == NULL && c == 0)
        return NULL;
    (l1 != NULL) ? (c += l1->val, l1 = l1->next) : (c += 0);
    (l2 != NULL) ? (c += l2->val, l2 = l2->next) : (c += 0);
    struct ListNode *cur = (struct ListNode *)malloc(sizeof(struct ListNode));
    cur->val = c % 10;
    c = c / 10;
    cur->next = addTwoNumbers(l1, l2);
    return cur;
}
```

## 参考

[1].[leetcode题解](https://leetcode-cn.com/problems/add-two-numbers/solution/zui-jian-xie-fa-by-baal-3/)

