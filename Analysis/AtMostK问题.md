# AtMostK问题
> 母题0：求一个数组的连续子数组(索引连续)总个数(不考虑重复)。
``` python
def countSubArray(nums):
    # cnt表示以数字i为结尾的子数组个数。
    cnt = res = 0
    for i in range(len(nums)):
        cnt += 1
        res += cnt
    return res
```
> 母题1：求一个数组相邻差为 1 连续子数组的总个数，即为引差 1 的同时，值也差 1。
``` python
def countSubArray(nums):
    # cnt表示以数字i为结尾的子数组个数。
    cnt = res = 1
    for i in range(1, len(nums)):
        if nums[i] - nums[i-1] == 1:
            cnt += 1
        else:
            cnt = 1
        res += cnt
    return res
```
> 母题2：求一个数组元素不大于K连续子数组的总个数，即为AtMostK(K)。
``` python
def AtMostK(nums, K):
    # cnt表示以数字i为结尾的子数组个数。
    cnt = res = 0
    for i in range(len(nums)):
        if nums[i] <= K:
            cnt += 1
        else:
            cnt = 0
        res += cnt
    return res
```
> 母题3：求一个数组元素最大值为K连续子数组的总个数，即为AtMostK(K)-AtMostK(K-1)。
> 母题4：求一个数组元素最大值大于等于K2，小于等于K1连续子数组的总个数，即为AtMostK(K1)-AtMostK(K2-1)。