# [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array)

### 题意
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
(例如，数组[0,1,2,4,5,6,7]可能变为[4,5,6,7,0,1,2])。
搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回-1 。
你可以假设数组中不存在重复的元素。
你的算法时间复杂度必须是O(logn)级别。

### 思路
先用二分法找出右边的最小值，然后再二分查找target

### 代码
```cgo
    int search(vector<int>& nums, int target) {
        if(nums.size() == 0 ) return -1;
        int index= findSmallest(nums);
        int left= 0,right=nums.size()-1;
        if(nums.at(right) <target && index >0) right = index-1;
        else left = index;

        return binarySearch(nums, target, left, right);
    }

    int binarySearch(vector<int>& nums, int target, int left, int right) {
        while(left<= right){
            int mid= left + (right-left)/2;
            if(nums.at(mid) == target) return mid;
            if(nums.at(mid)< target) left = mid+1;
            else right = mid-1;
        }
        return -1;
    }

    int findSmallest(vector<int>& nums) {
        int left=0, right=nums.size()-1;
        int ans =0;
        while(left<=right) {
            int mid = left + (right-left)/2;
            if(nums.at(mid)<=nums.at(nums.size()-1)) {// 1，记录下最小的右边；2，每次只要和最右值比较即可
                ans = mid;
                right = mid-1;
            } else {
                left = mid+1;
            }
        }
        return ans;
    }
```

# [154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

### 题意
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
(例如，数组[0,1,2,4,5,6,7]可能变为[4,5,6,7,0,1,2])。
请找出其中最小的元素。
注意数组中可能存在重复的元素。

### 思路
遇到相等的值的时候，`right--` 是关键

### 代码
```cgo
    int findMin(vector<int>& nums) {
        int left=0, right = nums.size()-1;
        while(left<= right) {
            int mid = left + (right-left)/2;
            if(nums[mid] > nums[right]) left = mid+1;
            else if(nums[mid]< nums[right]) right = mid;
            else right --;
        }
        return nums[left];
    }

``` 

# [81. 搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

### 题意
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
(例如，数组[0,0,1,2,2,5,6] 可能变为[2,5,6,0,0,1,2])。
编写一个函数来判断给定的目标值是否存在于数组中。若存在返回true，否则返回false。

示例1:
输入:nums=[2,5,6,0,0,1,2],target = 0
输出:true

### 思路
1. 关键是遇到相等的时候，怎么跳过  
2. 怎么确定在哪边找

### 代码
```cgo

    bool search(vector<int>& nums, int target) {
        if(nums.size() == 0 ) return false;
        int left= 0, right=nums.size()-1;
        return binarySearch(nums, target, left, right);
    }

    bool binarySearch(vector<int>& nums, int target, int left, int right) {
        while(left<= right){
            int mid= left+ (right-left)/2;
            if(nums.at(mid) == target) return true;
            if(nums[left] == nums[mid]) {
                left ++;
                continue;
            }

            //左边有序
            if(nums[left] < nums[mid]) {
                if(nums[left]<=target && nums[mid]> target) {
                    right = mid -1;
                } else {
                    left = mid+1;
                }
            } else {
                if(nums[right]>=target && nums[mid]< target)  {
                    left = mid+1;
                }else {
                    right = mid-1;
                }
            }
        }
        return false;
    }
```