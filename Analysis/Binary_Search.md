# Binary_Search

## 情况一
+ 查找某个元素是否在区间内。
``` python
def Binary_Search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) / 2
        if nums[mid] == target:
            return mid
        elif nums[mid] > target:
            right = mid - 1
        else:
            left = mid + 1
    return -1
```

## 情况二
+ 查找有序序列第一个满足某条件的元素的位置。
+ 注意三个地方：
    + left < right: 夹住满足条件的目标
    + 返回值既可能是left，也可能是right。
    + 二分上界是n
+ 例：第一个大于等于target的数
``` python
def Binary_Search(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = left + (right - left) / 2
        if nums[mid] >= target:
            right = mid
        else:
            left = mid + 1
    return left 
```
+ 模板：查找有序序列第一个满足某条件的元素的位置。
+ 解区间覆盖所有可能取值[0, n]：如果没有没有满足该条件的数返回n
+ 从左到右开始不满足条件
``` python
def Binary_Search(nums, target):
    left, right = 0, len(nums)
    while left < right:
        mid = left + (right - left) / 2
        if (满足某条件):
            right = mid
        else:
            left = mid + 1
    return left 
```

+ 模板：查找有序序列最后一个满足某条件的元素的位置。
+ 解区间覆盖所有可能取值。
+ 注意可能死循环，取中间值时应该加1
+ 从左到右开始满足条件
``` python
def Binary_Search(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        mid = left + (right - left + 1) / 2
        if (满足某条件):
            left = mid
        else:
            right = mid - 1
    return left 
```