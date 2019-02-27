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
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
class Solution {
public:
    static bool cmp(const Interval &a,const Interval &b){
        return a.end < b.end;
    }
    int eraseOverlapIntervals(vector<Interval>& intervals) {
        int len = intervals.size();
        if(len == 0 || len == 1)
            return 0;
        sort(intervals.begin(),intervals.end(),cmp);
        int count = 1;
        int end = intervals[0].end;
        for(int i = 1;i<len;++i){
            if(end > intervals[i].start)
                continue;
            end = intervals[i].end;
            ++count;
        }
        return len-count;
    }
};
```
**投飞镖刺破气球** 

[452. Minimum Number of Arrows to Burst Balloons (Medium)](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/)

```
Input:
[[10,16], [2,8], [1,6], [7,12]]

Output:
2
```

题目描述：气球在一个水平数轴上摆放，可以重叠，飞镖垂直投向坐标轴，使得路径上的气球都会刺破。求解最小的投飞镖次数使所有气球都被刺破。

也是计算不重叠的区间个数，不过和 Non-overlapping Intervals 的区别在于，[1, 2] 和 [2, 3] 在本题中算是重叠区间。

```C++
class Solution {
public:
    int findMinArrowShots(vector<pair<int, int>>& points) {
        if (points.empty()) return 0;
        sort(points.begin(), points.end());
        int res = 1, end = points[0].second;
        for (int i = 1; i < points.size(); ++i) {
            if (points[i].first <= end) {
                end = min(end, points[i].second);
            } else {
                ++res;
                end = points[i].second;
            }
        }
        return res;
    }
};
```
**根据身高和序号重组队列** 

[406. Queue Reconstruction by Height(Medium)](https://leetcode.com/problems/queue-reconstruction-by-height/description/)

```html
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

题目描述：一个学生用两个分量 (h, k) 描述，h 表示身高，k 表示排在前面的有 k 个学生的身高比他高或者和他一样高。

这道题给了我们一个队列，队列中的每个元素是一个pair，分别为身高和前面身高不低于当前身高的人的个数，让我们重新排列队列，使得每个pair的第二个参数都满足题意。首先我们给队列先排个序，按照身高高的排前面，如果身高相同，则第二个数小的排前面。
为什么要这样搞？？为了使插入操作不影响后续的操作，身高较高的学生应该先做插入操作，否则身高较小的学生原先正确插入的第 k 个位置可能会变成第 k+1 个位置。
然后我们新建一个空的数组，遍历之前排好序的数组，然后根据每个元素的第二个数字，将其插入到res数组中对应的位置，参见代码如下：

```C++
class Solution {
public:
    vector<pair<int, int>> reconstructQueue(vector<pair<int, int>>& people) {
        sort(people.begin(),people.end(),[](const pair<int,int>& a,const pair<int,int>& b){
            return (a.first>b.first||a.first==b.first&&a.second<b.second);
        });
        vector<pair<int,int>> res;
        for(auto a: people){
            res.insert(res.begin()+a.second,a);
        }
        return res;
    }
};
```
**分隔字符串使同种字符出现在一起** 

[763. Partition Labels (Medium)](https://leetcode.com/problems/partition-labels/description/)

```html
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```
这道题给了我们一个字符串S，然我们将其尽可能多的分割为子字符串，条件是每种字符最多只能出现在一个子串中。比如题目汇总的例子，字符串S中有多个a，这些a必须只能在第一个子串中，再比如所有的字母e值出现在了第二个子串中。那么这道题的难点就是如何找到字符串的断点，即拆分成为子串的位置。我们仔细观察题目中的例子，可以发现一旦某个字母多次出现了，那么其最后一个出现位置必须要在当前子串中，字母a，e，和j，分别是三个子串中的结束字母。所以我们关注的是每个字母最后的出现位置，我们可以使用一个HashMap来建立字母和其最后出现位置之间的映射，那么对于题目中的例子来说，我们可以得到如下映射：

a -> 8
b -> 5
c -> 7
d -> 14
e -> 15
f -> 11
g -> 13
h -> 19
i -> 22
j -> 23
k -> 20
l -> 21

建立好映射之后，就需要开始遍历字符串S了，我们维护一个start变量，是当前子串的起始位置，还有一个last变量，是当前子串的结束位置，每当我们遍历到一个字母，我们需要在HashMap中提取出其最后一个位置，因为一旦当前子串包含了一个字母，其必须包含所有的相同字母，所以我们要不停的用当前字母的最后一个位置来更新last变量，只有当i和last相同了，即当i = 8时，当前子串包含了所有已出现过的字母的最后一个位置，即之后的字符串里不会有之前出现过的字母了，此时就应该是断开的位置，我们将长度9加入结果res中，同理类推，我们可以找出之后的断开的位置，参见代码如下：
```C++
class Solution {
public:
    vector<int> partitionLabels(string S) {
        vector<int> res;
        int n = S.size();
        int start = 0;
        int last = 0;
        unordered_map<char,int> m;
        for(int i = 0;i<n;++i) m[S[i]]=i;
        for(int i = 0;i<n;++i){
            last = max(last,m[S[i]]);
            if(i==last){
                res.push_back(last-start+1);
                start = last + 1;
            }
        } 
        return res;
    }
};
```
**种植花朵** 

[605. Can Place Flowers (Easy)](https://leetcode.com/problems/can-place-flowers/description/)

```html
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True
```

题目描述：花朵之间至少需要一个单位的间隔，求解是否能种下 n 朵花。


我们遍历花床，如果某个位置为0，我们就看其前面一个和后面一个位置的值，注意处理首位置和末位置的情况.由于首位置和末位置的特殊性（只用看一侧，另一侧则可以视作是0），所以我们干脆直接先在首尾各加了一个0，然后就三个三个的来遍历，如果找到了三个连续的0，那么n自减1，i自增1，这样相当于i一下向后跨了两步，可以自行带例子检验，最后还是看n是否小于等于0，参见代码如下：
```C++
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        if(n == 0)
            return true;
        flowerbed.push_back(0);
        flowerbed.insert(flowerbed.begin(),0);
        for(int i = 1;i<flowerbed.size()-1;++i){
            if(flowerbed[i-1]+flowerbed[i]+flowerbed[i+1] == 0){
                --n;
                ++i;
            }   
        }
        return n<=0;
    }
};
```
**判断是否为子序列** 

[392. Is Subsequence (Medium)](https://leetcode.com/problems/is-subsequence/description/)

```html
s = "abc", t = "ahbgdc"
Return true.
```
很简单的双指针问题： 

```C++
class Solution {
public:
    bool isSubsequence(string s, string t) {
        if(s.empty())
            return true;
        int i = 0,j = 0;
        while(i<s.size() && j<t.size()){
            if(s[i] == t[j]) ++i;
            ++j;
        }
        return i==s.size();
    }
};
```
**修改一个数成为非递减数组** 

[665. Non-decreasing Array (Easy)](https://leetcode.com/problems/non-decreasing-array/description/)

```html
Input: [4,2,3]
Output: True
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```

题目描述：判断一个数组能不能只修改一个数就成为非递减数组。

在出现 nums[i] < nums[i - 1] 时，需要考虑的是应该修改数组的哪个数，使得本次修改能使 i 之前的数组成为非递减数组，并且  **不影响后续的操作** 。优先考虑令 nums[i - 1] = nums[i]，因为如果修改 nums[i] = nums[i - 1] 的话，那么 nums[i] 这个数会变大，就有可能比 nums[i + 1] 大，从而影响了后续操作。还有一个比较特别的情况就是 nums[i] < nums[i - 2]，只修改 nums[i - 1] = nums[i] 不能使数组成为非递减数组，只能修改 nums[i] = nums[i - 1]。

```C++
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
        int cnt = 0;
        for(int i=1;i<nums.size()&&cnt<2;++i){
            if(nums[i]>=nums[i-1])
                continue;
            cnt++;
            if(i-2>=0 && nums[i-2]>nums[i])
                nums[i] = nums[i-1];
            else
                nums[i-1] = nums[i];
        }
        return cnt<=1;
    }
};
```
**股票的最大收益** 

[122. Best Time to Buy and Sell Stock II (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)

题目描述：一次股票交易包含买入和卖出，多个交易之间不能交叉进行。

对于 [a, b, c, d]，如果有 a <= b <= c <= d ，那么最大收益为 d - a。而 d - a = (d - c) + (c - b) + (b - a) ，因此当访问到一个 prices[i] 且 prices[i] - prices[i-1] > 0，那么就把 prices[i] - prices[i-1] 添加到收益中，从而在局部最优的情况下也保证全局最优。

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res=0;
        if(prices.empty())
            return 0;
        for(int i=0;i<prices.size()-1;++i)
        {
            if(prices[i]<prices[i+1])
            {
                res+=prices[i+1]-prices[i];
            }
        }
        return res;
    }
};
```
**子数组最大的和** 

[53. Maximum Subarray (Easy)](https://leetcode.com/problems/maximum-subarray/description/)

```html
For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.
```
求数组中最大子序列的和，可以遍历每一个数组元素，找到以这个元素结尾的最大子序列，然后就变成了n个数求最大值，比当前max大的再更新。那么问题就在于怎么求每个元素的结尾的最大子序列。每个元素结尾的子序列要么是它本身，以及加上它前面的子序列们。我们只需要找到之前子序列中的最大的，如果是负数或0那当前最大子序列就是元素本身，如果是正数，那就是加上它成为当前下标的最大子序列。然后不断向前推进。
```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int>::iterator it = nums.begin();
        int maxsum =*it;
        int cursum =*it;
        
        for(it=it+1;it!=nums.end();++it){
            cursum = max(cursum + *it, *it);
            
            if(cursum>maxsum)
                maxsum = cursum;
        }
        return maxsum;
    }
};
```
**买入和售出股票最大的收益** 

[121. Best Time to Buy and Sell Stock (Easy)](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

题目描述：只进行一次交易。

只要记录前面的最小价格，将这个最小价格作为买入价格，然后将当前的价格作为售出价格，查看当前收益是不是最大收益。

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty()) return 0;
        vector<int>::iterator it = prices.begin();
        int curmin = *it;//记录到目前为止的最小价格
        int resmax = 0;//收益初始化
        for(it=it+1;it!=prices.end();++it){
            resmax = max(*it - curmin,resmax); 
            curmin = curmin <= *it ? curmin : *it;
        }
        return resmax;//返回最终收益
};
```
## 二分查找
**求开方** 

[69. Sqrt(x) (Easy)](https://leetcode.com/problems/sqrtx/description/)

```html
Input: 4
Output: 2

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be truncated.
```

一个数 x 的开方 sqrt 一定在 0 \~ x 之间，并且满足 sqrt == x / sqrt。可以利用二分查找在 0 \~ x 之间查找 sqrt。

对于 x = 8，它的开方是 2.82842...，最后应该返回 2 而不是 3。在循环条件为 l <= h 并且循环退出时，h 总是比 l 小 1，也就是说 h = 2，l = 3，因此最后的返回值应该为 h 而不是 l。

```C++
class Solution {
public:
    int mySqrt(int x) {
        if (x <= 1) return x;
        int left = 0, right = x;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (x / mid >= mid) left = mid + 1;
            else right = mid;
        }
        return right - 1;
    }
};
```
**大于给定元素的最小元素** 

[744. Find Smallest Letter Greater Than Target (Easy)](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)

```html
Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

题目描述：给定一个有序的字符数组 letters 和一个字符 target，要求找出 letters 中大于 target 的最小字符，如果找不到就返回第 1 个字符。

```C++
class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {
        if(target >= letters.back()) return letters[0];
        int l = 0;
        int r = letters.size();
        while(l < r){
            int mid = l + (r - l)/2;
            if(letters[mid] <= target) l=mid+1;
            else r = mid;
        }
        return letters[r];
    }
};
```
**有序数组的 Single Element** 

[540. Single Element in a Sorted Array (Medium)](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)

```html
Input: [1, 1, 2, 3, 3, 4, 4, 8, 8]
Output: 2
```

题目描述：一个有序数组只有一个数不出现两次，找出这个数。要求以 O(logN) 时间复杂度进行求解。

可以把数组中的元素两两一组编组，如0、1为一组，2、3为一组.....这样每次看Mid和它同组的小伙伴是否相等？（mid为奇数，则看mid和mid+1;mid为偶数，则看mid和mid-1）如果相等了，说明落单数在右边，如果不等，说明在左边.

```C++
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int l = 0 ;
        int r =nums.size()-1;
        while(l < r){
            int mid = l + (r - l)/2;
            if(nums[mid] == nums[mid ^ 1]) l = mid + 1;
            else r = mid;
        }
        return nums[l];
    }
};
```
**第一个错误的版本** 

[278. First Bad Version (Easy)](https://leetcode.com/problems/first-bad-version/description/)

题目描述：给定一个元素 n 代表有 [1, 2, ..., n] 版本，可以调用 isBadVersion(int x) 知道某个版本是否错误，要求找到第一个错误的版本。

如果第 m 个版本出错，则表示第一个错误的版本在 [l, m] 之间，令 h = m；否则第一个错误的版本在 [m + 1, h] 之间，令 l = m + 1。

因为 h 的赋值表达式为 h = m，因此循环条件为 l < h。

```C++
class Solution {
public:
    int firstBadVersion(int n) {
        int l = 1;
        int r = n;
        while(l < r){
            int mid = l + (r - l)/2;
            if(isBadVersion(mid))
                r = mid;
            else
                l = mid+1;
        }
        return l;
    }
};
```
**旋转数组的最小数字** 

[153. Find Minimum in Rotated Sorted Array (Medium)](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

```html
Input: [3,4,5,1,2],
Output: 1
```

```C++
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l = 0;
        int r = nums.size()-1;
        while(l < r){
            int mid = l + (r - l)/2;
            if(nums[mid] <= nums[r])
                r = mid;
            else
                l = mid + 1;
        }
        return nums[l];
    }
};
```




   
























        