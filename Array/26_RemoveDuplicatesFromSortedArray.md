# Remove Duplicates from Sorted Array Q26

## 问题描述:

> 给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。
>
> 不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。
>

示例1

`给定数组 nums = [1,1,2],` 

`函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。` 

`你不需要考虑数组中超出新长度后面的元素。`

示例2

`给定 nums = [0,0,1,1,1,2,2,3,3,4],`

`函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。`

`你不需要考虑数组中超出新长度后面的元素.`

## 算法分析:

> 不需要考虑数组超过新长度之后的元素,可以在数组内设置两个标记位,head 和tail 用于指向当前不重复元素的位置以及遍历其余元素

- step1:如果数组初始长度大于1 ,设置head = 0 ,tail = 1 ,否则直接输出
- step2:使用while(tail<数组length)遍历数组,比较当前head 位置的元素是否和tail位置的相同,如果相同,将tail+1,否则执行下一步
- step3:否则将将head+1 之后将tail指向的元素存入head 并将tail+1
- step4:最后返回head的值加一即可



## 编写代码:

```python
class Solution(object):
    def removeDuplicates(nums):
        if nums is None:
            return 0
        if len(nums) > 1:
            head = 0
            tail = 1
            while(tail < len(nums)):
                if(nums[head] == nums[tail]):
                    tail += 1
                else:
                    head += 1
                    nums[head] = nums[tail]
                    tail += 1
            return head+1
        return 1
    if __name__ == '__main__':
        nums = [0,0,1,2,3,4,4]
        print(removeDuplicates(nums))
        print(nums)
      
```

## 过程总结:

> 开始时候没有注意head的位置 如果head和tail如果指向不同的元素需要先将head +1 再进行赋值,最后返回head+1才是真正的不重复元素个数.

