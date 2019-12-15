# [26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array)

### 题意
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。
### 注意
c++的迭代器删除
### 代码
```cgo
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        for(vector<int>::iterator it=nums.begin(); it != nums.end(); ) {
           vector<int>::iterator next = it+1;
           if(next == nums.end()) {
               return nums.size();
           }
           if(*next == *it) {
               it = nums.erase(it);
           }else {
               it++;
           }
        }

        return nums.size();
    }
};
```

# [80. 删除排序数组中的重复项 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii)

### 题意
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

### 思路
迭代器it,guard，guard从0开始，it大于guard两步开始，将和guard相同的都移除。

### 代码
```cgo
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        vector<int>::iterator it=nums.begin();
        vector<int>::iterator guard=it;

        for(; guard != nums.end(); ){
            it = guard;
            if(it == nums.end() || (it+1) == nums.end()) {
                break;
            }
            it +=2;
            while(it != nums.end() && *it == *guard) {
                it = nums.erase(it);
            }
            guard ++;
        }

        return nums.size();
    }
};
```