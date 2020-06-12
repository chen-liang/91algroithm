## 75.[颜色分类](https://leetcode-cn.com/problems/sort-colors/)
### 题目
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。
此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

**注意:**
不能使用代码库中的排序函数来解决这道题。

### 示例 
```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```
### 进阶
- 一个直观的解决方案是使用计数排序的两趟扫描算法。首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
- 你能想出一个仅使用常数空间的一趟扫描算法吗？

### 方法1
#### 代码思路
通过提示使用计数排序的两趟扫描法，本质上有点类似桶排序。因为只有三种元素，且已知大小，所以只需要三个桶，建立一个长度为3的数组。
遍历所给的数组，完成桶的构造。最后遍历桶中元素值，按照0,1,2元素的个数给数组赋值。
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
       //计数排序法，两趟扫描
       int count[3]={0};
        for(int a : nums)   //构造桶
        {
            count[a]+=1;
        }
        for(int i=0,j=0;i<3;i++)  //遍历桶，给原有数组重新赋值
        {
            int num=count[i];
            while(num--)
            {   
                nums[j]=i;
                j++;
            }
        }
     }
};
```
#### 复杂度分析
- 时间复杂度：两次扫描花费时间相同。O(n)+O(n)=O(n).
- 空间复杂度:O(1)
### 方法2
#### 代码思路
采用双（3）指针思想，用i遍历数组，将0全部放到数组左边，2全部放到数组右边。left指向已排序完数组0的右端点，right指向1的左端点。
在区间[0,left)都是0，区间(right,len]全部为2.
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {        
        //双指针，一趟扫描
        int i=0,left=0,right=nums.size()-1;
        
        while(i!=right+1)
        {
            int cur=nums[i];
            if(cur==0)
            {
                swap(nums[left],nums[i]);
                left++;i++;
            }
            else if(cur==1)
            {
                i++;
            }
            else 
            {
                swap(nums[right],nums[i]);
                right--;
            }
        }
    }
};
```

## 142.[环形链表||](https://leetcode-cn.com/problems/linked-list-cycle-ii/)
### 题目
为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。
说明：不允许修改给定的链表。

### 示例 1：
```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```
### 示例 2：
```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```
### 示例 3：
```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```
### 进阶：
- 你是否可以不用额外空间解决此题？


### 代码思路
使用快慢指针方法。慢指针每次走1步，快指针每次走2布，同时从起点出发，那么快指针所走路程是慢指针的两倍。假设链表有环，链表起点到环路入口距离为x,相遇点距离环入口为y，d，那么环路长度c=y+d。设快指针走了n圈环路。则2(x+y)=x+y+n* c，化简得，x=d+(n-1)* c，那么慢指针从头指针开始走x个距离与快指针从相遇点走d+(n-1)* c距离相等，即两指针会在环路入口相遇。

![](https://media.giphy.com/media/ekSKZLVnEYOuKmkEQq/giphy.gif#pic_center)

```c++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow=head;      
        ListNode *fast=head;
        while(fast!=NULL&&fast->next!=NULL)   //没有环的退出条件。fast->next!=NULL是为了fast->next->next存在
        {
            slow=slow->next;
            fast=fast->next->next;      
            if(slow==fast)                    //找到相遇点
            {
                slow=head;                    
                while(slow!=fast)             //找到入环点
                
                {
                    slow=slow->next;
                    fast=fast->next;           
                }
                return slow;
            }        
        }
        return NULL;
    }
};
```
#### 复杂度分析
- 时间复杂度：O(n),取决于x与c的大小。若x>>c，则为O(n^2)
- 空间复杂度:O(1)


