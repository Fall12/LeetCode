# [1283. 使结果不超过阈值的最小除数](https://leetcode-cn.com/problems/find-the-smallest-divisor-given-a-threshold)

### 题意
给你一个整数数组nums和一个正整数threshold ，你需要选择一个正整数作为除数，然后将数组里每个数都除以它，并对除法结果求和。

请你找出能够使上述结果小于等于阈值 threshold 的除数中 最小 的那个。

每个数除以除数后都向上取整，比方说7/3=3，10/2=5。

题目保证一定有解。
示例 1：

输入：nums = [1,2,5,9], threshold = 6
输出：5
解释：如果除数为 1 ，我们可以得到和为 17 （1+2+5+9）。
如果除数为 4 ，我们可以得到和为 7 (1+1+2+3) 。如果除数为 5 ，和为 5 (1+1+1+2)

### 解法
二分求最右值

### 代码
```go
func smallestDivisor(nums []int, threshold int) int {
	maxNum := nums[0]
	size := len(nums)
	for i := 0; i < size; i++ {
		if nums[i] > maxNum {
			maxNum = nums[i]
		}
	}
	right := maxNum
	left := 1
	ans := left
	for  {
		if left > right {
			break
		}
		mid := (left+right)>>1
		sum := 0
		for i:=0;i < size; i++ {
			x := math.Ceil(float64(nums[i])/float64(mid))
			sum += int(x)
			if sum > threshold {
				break
			}
		}

		if sum <= threshold {
			ans = mid // 需要记录合适的解
			right = mid-1
		}else  {
			left = mid+1
		}
	}
	return ans
}

```