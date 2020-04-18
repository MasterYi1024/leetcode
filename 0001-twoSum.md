# 两数之和

难度：简单

## 题意

给定一个整数数组`num`和一个目标值`target`，请你在该数组中找出和为目标值的那**两个**整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

## 示例

> 给定 nums = [2, 7, 11, 15]，target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
>
> 所以返回 [0, 1]

## 题解

### 方法一------暴力法

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    int * arry = (int *)malloc(2 * sizeof(int));
    int i, j;
    for(i = 0; i < numsSize - 1; i++)
    {
        for(j = i + 1; j < numsSize; j++)
        {
            if(nums[i] + nums[j] == target)
            {
                arry[0] = i;
                arry[1] = j;
                *returnSize = 2;
                return arry;
            }
        }
    }
    return 0;
}
```

`numsSize`是数组的大小（元素个数）；`returnSize`是返回数组的元素个数（此题返回两个值，故`returnSize`为2）；

设置`numsSize`变量的作用，应该是因为在C语言中，对传入函数的数组无法确定其元素个数。（目前我能力不够，感觉是这个原因，如有说错，烦请纠正！[抱拳]）

`malloc()`函数是C语言中动态分配内存的函数，给出的代码注释中说“返回的数组必须分配内存，假设调用函数的程序会调用`free()`函数”。`free()`函数是对应释放`malloc()`函数所申请的内存的函数。

方法二和方法三是用哈希表的方法，有点高深，等我成长一段时间再补上：）