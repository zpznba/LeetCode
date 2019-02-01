# 算法思想

## 双指针

双指针主要用于遍历数组，两个指针指向不同的元素，从而协同完成任务。

**2019-01-09 有序数组的 Two Sum** 

[Leetcode ：167. Two Sum II - Input array is sorted (Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

```html
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

题目描述：在有序数组中找出两个数，使它们的和为 target。

使用双指针，一个指针指向值较小的元素，一个指针指向值较大的元素。指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。

- 如果两个指针指向元素的和 sum == target，那么得到要求的结果；
- 如果 sum > target，移动较大的元素，使 sum 变小一些；
- 如果 sum < target，移动较小的元素，使 sum 变大一些。

```C++ 代码
class Solution {
	public:
	    vector<int> twoSum(vector<int>& numbers, int target) {
	        int i=0,j=numbers.size()-1;
	        vector<int> res(2);
	        while(i<j){
	            if(numbers[i]+numbers[j]==target){
	                res[0]=i+1;
	                res[1]=j+1;
	                return res;
	            }
	            else if(numbers[i]+numbers[j]>target){
	                --j;
	            }
	            else
	                ++i;
	        }
	        return res;
	    }
	};
```
**2019-01-10 两数平方和** 

[633. Sum of Square Numbers (Easy)](https://leetcode.com/problems/sum-of-square-numbers/description/)

```html
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```

题目描述：判断一个数是否为两个数的平方和。

```C++
class Solution {
public:
    bool judgeSquareSum(int c) {
        int a = 0;
        int b = sqrt(c);
        int sum = 0;
        while(a<=b){
            sum=a*a+b*b;
            if(sum==c) return true;
            else if(sum<c) ++a;
            else
                --b;
        }
        return false;
    }
};
```
**2019-01-10 反转字符串中的元音字符** 

[345. Reverse Vowels of a String (Easy)](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

```html
Given s = "leetcode", return "leotcede".
```

使用双指针指向待反转的两个元音字符，一个指针从头向尾遍历，一个指针从尾到头遍历。

```C++
class Solution {
public:
    string reverseVowels(string s) {
        int i = 0;
        int j = s.size()-1;
        while(i<j){
            i = s.find_first_of("aeiouAEIOU",i); //在s中的i位置开始查找"aeiouAEIOU"中任何一个字符第一次出现的位置
            j = s.find_last_of("aeiouAEIOU",j);//在s中的j位置开始向前查找"aeiouAEIOU"中任何一个字符第一次出现的位置
            if(i<j)
                swap(s[i++],s[j--]);
        }
        return s;
    }
};
```
**2019-01-11 回文字符串** 

[680. Valid Palindrome II (Easy)](https://leetcode.com/problems/valid-palindrome-ii/description/)

```html
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

题目描述：可以删除一个字符，判断是否能构成回文字符串。

```C++
class Solution {
public:
    bool validPalindrome(string s) {
        int i=0,j=s.size()-1;
        while(i<j){
            if(s[i]!=s[j])
                return vaild(s,i+1,j)||vaild(s,i,j-1);
            ++i;
            --j;
        }
        return true;
    }
    bool vaild(string s,int left,int right){
        while(left<right){
            if(s[left++]!=s[right--]) return false;
        }
        return true;
    }
};
```
**2019-01-11 归并两个有序数组** 

[88. Merge Sorted Array (Easy)](https://leetcode.com/problems/merge-sorted-array/description/)

```html
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

题目描述：把归并结果存到第一个数组上。

需要从尾开始遍历，否则在 nums1 上归并得到的值会覆盖还未进行归并比较的值。

```C++ 
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i=m-1;
        int j=n-1;
        int k=m+n-1; //将最大的值存到K的位置
        while(i>=0&&j>=0){
            if(nums1[i]>nums2[j])
                nums1[k--]=nums1[i--];
            else
                nums1[k--]=nums2[j--];
        }
        while(j>=0)
            nums1[k--]=nums2[j--];
    }
};
```
**2019-01-12 移动零** 
[283.Move Zeroes(easy)](https://leetcode.com/problems/move-zeroes/)

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
```html
示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

思路：
我们让两个指针同时从0出发，只考虑快指针，当快指针指向非零元素时，我们需要交换快和慢指针指向的元素，然后推进两个指针。如果它是零元素，我们只是推进快指针，这样慢指针自然就指向了0。代码很简单如下：

```C++ 
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for(int slow=0,fast=0;fast<nums.size();++fast){
            if(nums[fast]!=0)
                swap(nums[slow++],nums[fast]);
        }
    }
};

```
**2019-01-13 判断链表是否存在环** 

[141. Linked List Cycle (Easy)](https://leetcode.com/problems/linked-list-cycle/description/)

使用双指针，一个指针每次移动一个节点，一个指针每次移动两个节点，如果存在环，那么这两个指针一定会相遇。

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(head == NULL || head -> next == NULL)    
            return false;
 
        ListNode *fast = head;
        ListNode *slow = head;
        //这里的while循环很关键，因为fast每次要走两步，所以必须检测下一步和下下步是否存在？
        while(fast -> next && fast -> next -> next){
            fast = fast -> next -> next;
            slow = slow -> next;
            if(fast == slow)
                return true;
        }
 
        return false;
    }
};
```
## 排序

### 快速选择

用于求解  **Kth Element**  问题，使用快速排序的 partition() 进行实现。

需要先打乱数组，否则最坏情况下时间复杂度为 O(N<sup>2</sup>)。

### 堆排序

用于求解  **TopK Elements**  问题，通过维护一个大小为 K 的堆，堆中的元素就是 TopK Elements。

堆排序也可以用于求解 Kth Element 问题，堆顶元素就是 Kth Element。

快速选择也可以求解 TopK Elements 问题，因为找到 Kth Element 之后，再遍历一次数组，所有小于等于 Kth Element 的元素都是 TopK Elements。

可以看到，快速选择和堆排序都可以求解 Kth Element 和 TopK Elements 问题。

**Kth Element** 

[215. Kth Largest Element in an Array (Medium)](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

题目描述：找到第 k 大的元素。

**排序** ：时间复杂度 O(NlogN)，空间复杂度 O(1)

```C++

class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        sort(nums.begin(),nums.end());
        return nums[nums.size()-k];
    }
};
```

**堆排序** ：时间复杂度 O(NlogK)，空间复杂度 O(K)。

```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        for(auto num :nums){
            q.push(num);
            if(q.size()>k)
                q.pop();
        }
        return q.top();
    }
private:
    priority_queue<int,vector<int>,greater<int> >q;//小顶堆
};
```

**快速选择** ：时间复杂度 O(N)，空间复杂度 O(1)

```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int l=0,r=nums.size()-1;
        k=nums.size()-k;
        while(l<=r){
            int index = partition(nums,l,r);
            if(index==k)
                return nums[index];
            else if(index<k)
                l = index+1;
            else
                r = index-1;
        }
        return 0;
    }
    int partition(vector<int>& nums, int start, int end)
    {
        if(start==end)
            return start;
        int pivot = nums[end];
        while(start<end){
            while(start<end && nums[start]<=pivot) ++start;
            nums[end]=nums[start];
            while(start<end && nums[end]>=pivot) --end;
            nums[start]=nums[end];
        }
        nums[end]=pivot;
        return end;
    }
};
```
### 桶排序

**出现频率最多的 k 个数** 

[347. Top K Frequent Elements (Medium)](https://leetcode.com/problems/top-k-frequent-elements/description/)

关于这道题可以看我的博客：https://blog.csdn.net/zpznba/article/details/86550839

```html
Given [1,1,1,2,2,3] and k = 2, return [1,2].
```

设置若干个桶，每个桶存储出现频率相同的数，并且桶的下标代表桶中数出现的频率，即第 i 个桶中存储的数出现的频率为 i。

把数都放到桶之后，从后向前遍历桶，最先得到的 k 个数就是出现频率最多的的 k 个数。

```C++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> m;
        for (int num : nums)
            ++m[num];
        
        vector<vector<int>> buckets(nums.size() + 1); 
        for (auto p : m)
            buckets[p.second].push_back(p.first);
        
        vector<int> ans;
        for (int i = buckets.size() - 1; i >= 0 && ans.size() < k; --i) {
            for (int num : buckets[i]) {
                ans.push_back(num);
                if (ans.size() == k)
                    break;
            }
        }
        return ans;
    }
};
```
当然也可以用之前的堆排序来做:

```C++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int,int> tmp;
        vector<int> res;
        priority_queue<pair<int,int>> q;
        for(auto c : nums){
            tmp[c]++;
        }
        for(auto it : tmp){
            q.push({it.second,it.first});
        }
        for(int i=0;i<k;++i){
            res.push_back(q.top().second);
            q.pop();
        }
        return res;
    }
};
```
**2019-01-21-按照字符出现次数对字符串排序** 

[451. Sort Characters By Frequency (Medium)](https://leetcode.com/problems/sort-characters-by-frequency/description/)

```html
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```
1.堆排序
```C++
class Solution {
public:
    string frequencySort(string s) {
        string res = "";
        unordered_map<char, int> m;
        priority_queue<pair<int,char> > q;
        for (char c : s) ++m[c];
        for(auto a : m)
            q.push({a.second,a.first});
        while(!q.empty()){
            res.append(q.top().first,q.top().second);
            q.pop();
        }
        return res; 
    }  
};
```
2.桶排序
```C++
class Solution {
public:
    string frequencySort(string s) {
        string res;
        unordered_map<char, int> m;
        vector<string> bucket(s.size()+1,"");
        for (char c : s) ++m[c];
        for(auto it : m){
            int n = it.second;
            char c = it.first;
            bucket[n].append(n,c);
        }
        for(int i= s.size();i>0;--i){
            if(!bucket[i].empty())
                res.append(bucket[i]);
        }
        return res; 
    }  
};
```
### 荷兰国旗问题

荷兰国旗包含三种颜色：红、白、蓝。

有三种颜色的球，算法的目标是将这三种球按颜色顺序正确地排列。

它其实是三向切分快速排序的一种变种，在三向切分快速排序中，每次切分都将数组分成三个区间：小于切分元素、等于切分元素、大于切分元素，而该算法是将数组分成三个区间：等于红色、等于白色、等于蓝色。

<div align="center"> <img src="pics/3b49dd67-2c40-4b81-8ad2-7bbb1fe2fcbd.png"/> </div><br>

**按颜色进行排序** 

[75. Sort Colors (Medium)](https://leetcode.com/problems/sort-colors/description/)

```html
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

题目描述：只有 0/1/2 三种颜色。

双指针法
```C++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n=nums.size();
        int left = 0;
        int right = n-1;
        int i = 0;
        while(i <= right)
        {
            if(nums[i] == 0)
            {
                swap(nums[left], nums[i]);
                left ++;
                i ++;
            }
            else if(nums[i] == 1)
            {
                i ++;
            }    
            else
            {
                swap(nums[i], nums[right]);
                right --;
            }
        }
}
};
```
平移插入法
```C++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int i = -1,j = -1,k = -1;//注意i，j，k的含义
        int m;
        for(m = 0; m < nums.size();m++){
            if(nums[m] == 0){
                nums[++k] = 2;
                nums[++j] = 1;
                nums[++i] = 0;
            }
            else if(nums[m] == 1){
                nums[++k] = 2;
                nums[++j] = 1;
            }
            else {
                nums[++k] = 2;
            }
        }
    }
};
```
## 贪心思想

保证每次操作都是局部最优的，并且最后得到的结果是全局最优的。

**分配饼干** 

[455. Assign Cookies (Easy)](https://leetcode.com/problems/assign-cookies/description/)

```html
Input: [1,2], [1,2,3]
Output: 2

Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2.
You have 3 cookies and their sizes are big enough to gratify all of the children,
You need to output 2.
```

题目描述：每个孩子都有一个满足度，每个饼干都有一个大小，只有饼干的大小大于等于一个孩子的满足度，该孩子才会获得满足。求解最多可以获得满足的孩子数量。

给一个孩子的饼干应当尽量小又能满足该孩子，这样大饼干就能拿来给满足度比较大的孩子。因为最小的孩子最容易得到满足，所以先满足最小的孩子。

证明：假设在某次选择中，贪心策略选择给当前满足度最小的孩子分配第 m 个饼干，第 m 个饼干为可以满足该孩子的最小饼干。假设存在一种最优策略，给该孩子分配第 n 个饼干，并且 m < n。我们可以发现，经过这一轮分配，贪心策略分配后剩下的饼干一定有一个比最优策略来得大。因此在后续的分配中，贪心策略一定能满足更多的孩子。也就是说不存在比贪心策略更优的策略，即贪心策略就是最优策略。

```C++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        int res=0;
        int i=0,j=0;
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        while(i<g.size()&&j<s.size()){
            if(g[i]<=s[j]){
                ++res;
                ++i;
            }
            ++j;
        }
        return res;
    }
};
```
**不重叠的区间个数** 

[435. Non-overlapping Intervals (Medium)](https://leetcode.com/problems/non-overlapping-intervals/description/)

```html
Input: [ [1,2], [1,2], [1,2] ]

Output: 2

Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```

```html
Input: [ [1,2], [2,3] ]

Output: 0

Explanation: You don't need to remove any of the intervals since they're already non-overlapping.
```

题目描述：计算让一组区间不重叠所需要移除的区间个数。

先计算最多能组成的不重叠区间个数，然后用区间总个数减去不重叠区间的个数。

在每次选择中，区间的结尾最为重要，选择的区间结尾越小，留给后面的区间的空间越大，那么后面能够选择的区间个数也就越大。

按区间的结尾进行排序，每次选择结尾最小，并且和前一个区间不重叠的区间。

```C++
//明天做
```