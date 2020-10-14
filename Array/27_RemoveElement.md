# Remove Element Q27

##  问题描述:

> 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
>
> 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

## 算法分析:

> 设置两个定位变量,一个tail用于遍历当前数组,另一个head用于定位删除val元素后数组的最后一个元素位置.

- step1: 将head和tail都设为0.赋值到
- step2: 使用tail遍历数组,发现与val值不同的元素就赋值到head位置,然后,tail和head同时后移.否则执行3.
- step3: 如果,tail的值与val相同,head不变tail继续后移.
- step4: 最后输出~~head+1~~head 便是移除后数组的长度.

## 编写代码:

```python
class Solution(object):
    def removeDuplicates(nums,val):
        if nums is None:
            return 0
      	else:
            head = 0
            tail = 0
            while(tail < len(nums)):
                if(nums[tail] == val):
                    tail += 1
                else:
                    nums[head] = nums[tail]
                    head += 1
                    tail += 1
            return head
   if __name__ == '__main__':
        nums = [0,0,1,2,3,4,4]
        print(removeDuplicates(nums,0))
        print(nums)
      
```

## 过程总结:



> 开始时没注意head 每次都指向移除后数组的后一位,所以不用加一.

