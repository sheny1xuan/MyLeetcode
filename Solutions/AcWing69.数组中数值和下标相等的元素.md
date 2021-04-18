# [AcWing69.数组中数值和下标相等的元素](https://www.acwing.com/problem/content/65/)

## 两个数组组合二分
+ numd[i] - i >= nums[i-1] - (i-1)为递增序列。
+ 目标查找该递增序列中是否存在0.
``` cpp
class Solution {
public:
    int getNumberSameAsIndex(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] - mid == 0){
                return mid;
            }
            if(nums[mid] - mid < 0){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return -1;
    }
};
```