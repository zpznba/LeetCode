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
