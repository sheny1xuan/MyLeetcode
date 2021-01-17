# 题目分类
## 栈
<!-- 
❌
✔ -->

做题情况 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ |[7.整数反转](https://leetcode-cn.com/problems/reverse-integer/) | [👍](Solutions/7.整数反转.md) | [👉](Solutions/7.整数反转.md)
✔ |[20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/) | [👍](Solutions/20.有效的括号) | [👉](Solutions/20.有效的括号) 

## 字符串

做题情况 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ |[8.字符串转换整数(atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/) | [👍](Solutions/8.字符串转换整数.md) | [👉](Solutions/8.字符串转换整数.md)
✔ |[14.最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/) | [👍](Solutions/14.最长公共前缀.md) | [👉](Solutions/14.最长公共前缀.md) 
❌ |[415.字符串相加](https://leetcode-cn.com/problems/add-strings/) | [👍](415.字符串相加.md) | [👉](https://leetcode-cn.com/problems/multiply-strings/solution/python-zi-fu-chuan-bao-li-mo-ni-shu-shi-cheng-fa-j/)
❌ |[43.字符串相乘](https://leetcode-cn.com/problems/multiply-strings/) | [👍](Solutions/43.字符串相乘.md) | [👉]([Solutions/14.最长公共前缀.md](https://leetcode-cn.com/problems/multiply-strings/solution/python-zi-fu-chuan-bao-li-mo-ni-shu-shi-cheng-fa-j/)) 

## 双指针

双指针 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ | [9.回文数](https://leetcode-cn.com/problems/palindrome-number/) | [👍](Solutions/9.回文数.md) | [👉](Solutions/9.回文数.md)
✔ |[15.盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/) | [👍](Solutions/15.盛最多水的容器.md) | [👉](Solutions/15.盛最多水的容器.md) 
✔ |[26.删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/) | [👍](Solutions/26.删除排序数组中的重复项.md) | [👉](Solutions/26.删除排序数组中的重复项.md) 

### 二分法

二分法 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ | [11.三数之和](https://leetcode-cn.com/problems/3sum/) | [👍](Solutions/11.三数之和.md) | [👉](Solutions/11.三数之和.md)
✔ |[16.最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/) | [👍](Solutions/16.最接近的三数之和.md) | [👉](Solutions/16.最接近的三数之和.md) 
✔ |[26.删除排序数组中的重复项](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/) | [👍](Solutions/33.搜索旋转排序数组.md) | [👉](Solutions/33.搜索旋转排序数组.md) 

## 链表

做题情况 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ | [2.两数相加](https://leetcode-cn.com/problems/add-two-numbers/) | [👍](Solutions/2.两数相加.md) | [👉](Solutions/2.两数相加.md)
✔ |[21.合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/) | [👍](Solutions/21.合并两个有序链表.md) | [👉](Solutions/21.合并两个有序链表.md) 
✔ |[23.合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/) | [👍](Solutions/23.合并K个升序链表.md) | [👉](Solutions/23.合并K个升序链表.md) 

## 动态规划

做题情况 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ | [5.最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/) | [👍](Solutions/5.最长回文子串.md) | [👉](Solutions/5.最长回文子串.md)
✔ | [53.最大子序和](https://leetcode-cn.com/problems/maximum-subarray/) | [👍](Solutions/53.最大子序和.md) | [👉]([Solutions/5.最长回文子串.md](https://leetcode-cn.com/problems/maximum-subarray/solution/zui-da-zi-xu-he-cshi-xian-si-chong-jie-fa-bao-li-f/))

# 回溯算法
## 回溯算法模板

``` cpp
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```
##  排列类题目
做题情况 |题目 | 我的题解 | 参考资料
 :-: | - | :-: | :-:
✔ | [46.全排列](https://leetcode-cn.com/problems/permutations/) | [👍](Solutions/46.全排列.md) | [👉](https://leetcode-cn.com/problems/permutations/solution/46-quan-pai-lie-hui-su-suan-fa-jing-dian-ti-mu-xia/)
