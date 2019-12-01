# 287. [寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)

思路：参考题解的想法

利用快慢指针，那么如果有重复(题目说必有重复)，意味着有环，那么快慢指针会重逢。
现在问题变为怎么找到环的入口？ 

记住，由于快指针步伐是慢指针的2倍，快指针和慢指针相逢时，假设慢指针已经走了n步，那么快指针已经走了2n步，同时，n%(环的长度c)=0()。

假设从开头到环入口的长度为m，慢指针此时在环中走的路是n-m步，那么再走m步刚好走了n步，回到环的入口，所以再来一个指针，从头也走m步，刚好和慢指针相遇。

代码：
	   
	func findDuplicate(nums []int) int {
		slow := 0
		fast := 0
		for {
			slow = nums[slow]
			fast = nums[nums[fast]]
			if nums[slow] == nums[fast] {
				find := 0
	
				for {
					find = nums[find]
					slow = nums[slow]
					if find == slow {
						return slow
					}
				}
			}
		}
	}
