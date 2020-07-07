## 66.[加一](https://leetcode-cn.com/problems/plus-one)
### 题目
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。
你可以假设除了整数 0 之外，这个整数不会以零开头。
### 示例 1:
```
 输入: [1,2,3]
 输出: [1,2,4]
 解释: 输入数组表示数字 123。
```
### 示例 2:
```
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。
```
### 答案
```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for(int i=digits.size()-1;i>=0;i--)
        {
            digits[i]++;              
            if(digits[i]==10)     //判断是否有进位
                digits[i]=0;
            else return digits;  //没有进位直接返回
        }
        if(digits[0]==0)         //判断特殊情况[9,9,9]
            digits.insert(digits.begin(),1);  //在vector头部插入1
        return digits;
    }
};
```

## 380. [常数时间插入、删除和获取随机元素](https://leetcode-cn.com/problems/insert-delete-getrandom-o1/)
### 题目
设计一个支持在平均 时间复杂度 O(1) 下，执行以下操作的数据结构。

insert(val)：当元素 val 不存在时，向集合中插入该项。

remove(val)：元素 val 存在时，从集合中移除该项。

getRandom：随机返回现有集合中的一项。每个元素应该有相同的概率被返回。
### 示例 
```c++
// 初始化一个空的集合。
RandomizedSet randomSet = new RandomizedSet();

// 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomSet.insert(1);

// 返回 false ，表示集合中不存在 2 。
randomSet.remove(2);

// 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomSet.insert(2);

// getRandom 应随机返回 1 或 2 。
randomSet.getRandom();

// 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomSet.remove(1);

// 2 已在集合中，所以返回 false 。
randomSet.insert(2);

// 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
randomSet.getRandom();
```
### 答案
```c++
class RandomizedSet {
public:
    /** Initialize your data structure here. */
    vector<int> v;
    unordered_map<int,int> m;
    RandomizedSet() {
            
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {
        if(m.find(val)!=m.end()) return false;
        v.push_back(val);  //vector存放数组的值
        m.insert(make_pair(val,v.size()-1)); //hashmap存放数组的值与索引
        return true;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {
        if(m.find(val)==m.end()) return false;
        v[m[val]]=v.back();  //将待删除的值放到数组末尾
        m[v.back()]=m[val];  //把map中最后一个数对应的位置改为删除的那个数的位置,即为null
        v.pop_back();
        m.erase(val);
        return true;
    }
    
    /** Get a random element from the set. */
    int getRandom() {
        return v[rand()%v.size()];
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```
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

### 答案
```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        //sort(nums.begin(),nums.end());
       //计数排序法，两趟扫描
       int count[3]={0};
        for(int a : nums)
        {
            count[a]+=1;
        }
        for(int i=0,j=0;i<3;i++)
        {
            int num=count[i];
            while(num--)
            {   
                nums[j]=i;
                j++;
            }
        }
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
## 1381.[设计一个支持增量操作的栈](https://leetcode-cn.com/problems/design-a-stack-with-increment-operation/)
### 题目
请你设计一个支持下述操作的栈。
实现自定义栈类 **CustomStack** ：
- CustomStack(int maxSize)：用 maxSize 初始化对象，maxSize 是栈中最多能容纳的元素数量，栈在增长到 maxSize 之后则不支持 push 操作。
- void push(int x)：如果栈还未增长到 maxSize ，就将 x 添加到栈顶。
- int pop()：弹出栈顶元素，并返回栈顶的值，或栈为空时返回 -1 。
- void inc(int k, int val)：栈底的 k 个元素的值都增加 val 。如果栈中元素总数小于 k ，则栈中的所有元素都增加 val 。


### 示例:
```
输入：
["CustomStack","push","push","pop","push","push","push","increment","increment","pop","pop","pop","pop"]
[[3],[1],[2],[],[2],[3],[4],[5,100],[2,100],[],[],[],[]]
输出：
[null,null,null,2,null,null,null,null,null,103,202,201,-1]
解释：
CustomStack customStack = new CustomStack(3); // 栈是空的 []
customStack.push(1);                          // 栈变为 [1]
customStack.push(2);                          // 栈变为 [1, 2]
customStack.pop();                            // 返回 2 --> 返回栈顶值 2，栈变为 [1]
customStack.push(2);                          // 栈变为 [1, 2]
customStack.push(3);                          // 栈变为 [1, 2, 3]
customStack.push(4);                          // 栈仍然是 [1, 2, 3]，不能添加其他元素使栈大小变为 4
customStack.increment(5, 100);                // 栈变为 [101, 102, 103]
customStack.increment(2, 100);                // 栈变为 [201, 202, 103]
customStack.pop();                            // 返回 103 --> 返回栈顶值 103，栈变为 [201, 202]
customStack.pop();                            // 返回 202 --> 返回栈顶值 202，栈变为 [201]
customStack.pop();                            // 返回 201 --> 返回栈顶值 201，栈变为 []
customStack.pop();                            // 返回 -1 --> 栈为空，返回 -1


```
### 提示
- 1 <= maxSize <= 1000
- 1 <= x <= 1000
- 1 <= k <= 1000
- 0 <= val <= 100
- 每种方法 increment，push 以及 pop 分别最多调用 1000 次

### 答案
```c++
class CustomStack {
public:
    vector<int> stack;
    int max,top=0;
    CustomStack(int maxSize) {
        max=maxSize;
    }
    
    void push(int x) {
        if(top<max) 
        {
            stack[top]=x;
            top++;
        }
    }
    
    int pop() {
        if(top>=1) 
        {
            return stack[--top];
        }
        else return -1;
    }
    
    void increment(int k, int val) {
        int n=k>top?top:k;
        for(int j=0;j<n;j++)
        {
            stack[j]+=val;
        }
    }
};

/**
 * Your CustomStack object will be instantiated and called as such:
 * CustomStack* obj = new CustomStack(maxSize);
 * obj->push(x);
 * int param_2 = obj->pop();
 * obj->increment(k,val);
 */
```

## 394. [字符串解码](https://leetcode-cn.com/problems/decode-string/)
### 题目
给定一个经过编码的字符串，返回它解码后的字符串。
编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。
你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。
此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

### 示例 1:
```
s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".

```

### 答案
```c++
class Solution {
public:
    string decodeString(string s) {
        stack<int> nums;
        stack<string> strs;
        string res="";
        int num=0,len=s.size();
        for(int i=0;i<len;i++)
        {
            if(s[i]>='0'&&s[i]<='9')
            {
                num=num*10+s[i]-'0';   //*10表示进位
            }
            else if((s[i]>='a'&&s[i]<='z')||(s[i]>='A'&&s[i]<='Z'))
            {
                res=res+s[i];    //字符串拼接
            }
            else if(s[i]=='[')
            {
                nums.push(num);
                strs.push(res);
                num=0; 
                res="";
            }
            else{
                int times=nums.top();
                nums.pop();
                for(int j=0;j<times;j++)
                {
                    strs.top()+=res;
                }
                res=strs.top();
                strs.pop();
            }
        }
        return res;
    }
};
```






