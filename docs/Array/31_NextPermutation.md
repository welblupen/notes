# Next Permutation Q31

##  题目描述 :

> 实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。
>
> 如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。
>
> 必须原地修改，只允许使用额外常数空间。
>
> 以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
> 1,2,3 → 1,3,2
> 3,2,1 → 1,2,3
> 1,1,5 → 1,5,1

## 算法分析 :

> 下一个更大的排列,首先想到的是做一个当前输入数组序列的全排列,然后找到位于当前数组后面的一组排列.
>
> 例如: 对于包含 1 2 3 的排列,首先将元素从小到大排序,然后使用
>
> 递归或者循环输出全排列 

```python
import math
import sys
import copy
sys.setrecursionlimit(9000000)

nums = [1,1,3]
visit = [0 for i in range( len( nums ) )]
nums.sort()
result = [[] for i in range( math.factorial( len( nums ) ) )]
data = [ 0 for i in range(len(nums))]
global count
count = 0

def dfs(path, n):
    global count
    if (path == n):
        if(data not in result):
            result[count] = copy.deepcopy(data)
            count += 1
    for i in range(n):
        if (visit[i] == 0):
            data[path] =  nums[i]
            visit[i] = 1
            dfs(path + 1, n)
            visit[i] = 0

dfs(0,len(nums))
print(result)
```

> 这种方法是获得指定序列的递增全排列组合
>
> 但是过程过于复杂而且使用递归数据量大的话,系统栈区会溢出.
>
> 其中因为事先进行过排序,使用dfs得到的全排列是字典序递增的,只需要获取同输入相同序列的下一个序列即可.
>
> 但是题目要求需要在原地修改数组,所以需要用全排列本身的特性去思考得到下一个排列的简单方法.
>
> * 分析 对比当前排列和下一个排列:(此处引用leetcode大佬的分析图片)![Next Permutation](https://pic.leetcode-cn.com/1df4ae7eb275ba4ab944521f99c84d782d17df804d5c15e249881bafcf106173-file_1555696082944)
>
> 我们可以发现对于当前排列,他如果是按逆序排列的,那么就没有比他更大的序列,反之如果他是顺序排列的,则没有比他更小的序列
>
> 从此我们可以发现,只要找到逆排列中第一个无序的元素,(这个元素后面跟着的就是当前最大的逆序子数列),因此只需将这个元素替换为逆序子序列中第一个比他大的元素,再将后面的逆序子序列逆转为顺序子序列,便得到了刚好比当前排列大的下一个排列.
>
> 这样就能在在当前数组中直接修改得到他的下一个排列.
>
> *  step1: 首先逆序遍历数组,找到第一个a[j-1]<a[j] 的 j-1 号元素,标记位 target1 ,如果没有找到:
>
>   则说明此排列为最大逆序排列只需进行逆转操作.可以标记target1 = -1 然后执行step3
>
> * step2: 接着从target1开始正向遍历,找到第一个比他小的元素, 那么此元素前面就是要交换的target2,然后交换,
>
>   如果没有找到则交换遍历到的最后一个元素.
>
> * step3: 将target之后的子序列逆转即可.
>
> 

## 编写代码 :

> ```python
> nums = [1,2,4,3]
> target1 = -1
> target2 = len(nums)-1
> for l in range(len(nums)-1,0,-1):
>  if(nums[l-1] < nums[l]):
>      target1 = l-1
>      for i in range(target1+1,len(nums)):
>          if(nums[target1] >= nums[i]):
>              target2 = i-1
>              break
>      temp = nums[target1]
>      nums[target1] = nums[target2]
>      nums[target2] = temp
>      break
> left = target1+1
> right = len(nums)-1
> while(left < right):
>     temp = nums[left]
>     nums[left] = nums[right]
>     nums[right] = temp
>     left += 1
>     right -= 1
> print(nums)
> ```
>
> 

## 过程总结 :

> dfs遍历的时候要新建一个数组,不能直接append因为在path达到终点时,count+1但是后面无法回退到添加上一层数组.而直接新建的数组还保留着上一层的数值.
>
> python 的全局变量 global 
>
> 拷贝数组值的时候要用深拷贝 copy.deepcopy()
>
> 列表切片[开始下标(能切到):结束下标(切到上一个):间隔(-1为逆)]
>
> 最后第三步逆序占用空间还是过多