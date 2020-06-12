## 双指针模板
### 1. 快慢指针
```c++
l = 0
r = 0
while 没有遍历完
  if 一定条件
    l += 1
  r += 1
return 合适的值
```
**题目推荐**
- [26.Remove Duplicates from Sorted Array（Easy）](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array)
- [141.Linked List Cycle (Easy)](https://leetcode-cn.com/problems/linked-list-cycle)
- [142.Linked List Cycle II（Medium）](https://leetcode-cn.com/problems/linked-list-cycle-ii)
- [287.Find the Duplicate Number（Medium）](https://leetcode-cn.com/problems/find-the-duplicate-number)
- [202.Happy Number (Easy)](https://leetcode-cn.com/problems/happy-number)
### 2. 左右端点指针
```c++
l = 0
r = n - 1
while l < r
  if 找到了
    return 找到的值
  if 一定条件1
    l += 1
  else if  一定条件2
    r -= 1
return 没找到
```
**题目推荐**
- [16.3Sum Closest (Medium)](https://leetcode-cn.com/problems/3sum-closest)
- [713.Subarray Product Less Than K (Medium)](https://leetcode-cn.com/problems/subarray-product-less-than-k)
- [977.Squares of a Sorted Array (Easy)](https://leetcode-cn.com/problems/squares-of-a-sorted-array)
--- 
下面是二分类型
- [33.Search in Rotated Sorted Array (Medium)](https://leetcode-cn.com/problems/search-in-rotated-sorted-array)
- [875.Koko Eating Bananas（Medium）](https://leetcode-cn.com/problems/koko-eating-bananas)
- [881.Boats to Save People（Medium）](https://leetcode-cn.com/problems/boats-to-save-people)
### 3. 固定间距指针
```c++
l = 0
r = k
while 没有遍历完
  自定义逻辑
  l += 1
  r += 1
return 合适的值
```
**题目推荐**
- [456.Maximum Number of Vowels in a Substring of Given Length（Medium）](https://leetcode-cn.com/problems/132-pattern)
