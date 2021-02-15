# TOPk元素(第k大的元素)

> 从arr[1, n]这n个数中，找出最大的k个数，这就是经典的TopK问题。

## 排序
+ 将n个数组进行排序，取出最大的K个。
+ T:O(nlogn)
``` python
sort(arr, 0, n)
return arr[0:k]
```

## 局部排序T:O(nlogn)/2

+ 不进行全局排序，每次冒泡找出一个最大值。
+ T:O(nk)

``` python
for i in range(k):
    bubble_find_max(arr, i)
return arr[0:k]
```

## 小顶堆

+ 用前K个元素形成一个小顶堆，堆顶元素就是第K大的元素。
+ 整个小顶堆就是TOPk个元素。
+ T:O(nlogk)

``` python
my_heap = heapq.heapfy(nums[0:k])
for i in range(k, n):
    heapq.heappush(my_heap, nums[i])
    while len(my_heap) < k:
        heapq.heappop(my_heap)
return my_heap
```

## 快速选择

+ 分治思想