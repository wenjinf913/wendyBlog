# Array Questions Category



## Binary Search Basics

1. Binary search has to work on _**Ordered Array**_ and _**No Repeating Elements**_ in the array. 

2. Binary search has to define _**Interval**_ - **左闭右闭 [left, right] _or_ 左闭右开 [left, right)** and stick to _**Loop Invariant Principle**_

3. Binary search has to prevent **overflow** when performing addition of left and right index 

    [ Instead of `middle = (left+right)/2`, do `middle = left + ((right-left)/2)` ]

### 704. Binary-search

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with `O(log n)` runtime complexity.

Examples:

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

#### Binary-search first approach: 左闭右闭 [left, right]

1. While (left **<=** right) has to use **<=**, since left == right is legit in [left, right]
2. if (nums[middle} > target) & if (nums[middle} < target)  **right = middle +1** & **left = middle -1**, since nums[middle] is not the target

<p align="center">
    <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h87v39kokbj312i0o2ta9.jpg" width="50%" height="50%">
</p>



```python
class Solution(object):
    def search(self, nums, target):
        left = 0
        right = len(nums)-1 #define target in the closed interval [left,right]
        while left <= right: #when left==right, [left,right] inveral is still legal, so use <=
            middle = left + (right-left)/2 #equal to (left+right)/2, prevent overflow 
            if nums[middle] > target:
                right = middle -1 #target is in [left,middle-1]
            elif nums[middle] < target:
                left = middle +1 #target is in [middle+1,left]
            else: return middle #find target
        return -1
```

#### Binary-search second approach: 左闭右开 [left, right)

1. While (left **<** right) has to use **<**, since left == right is not legit in [left, right)
2. if (nums[middle} > target) & if (nums[middle} < target) **right = middle+1** since nums[middle] is not the target & **left = middle** since nums[middle] will not be examined in the next interval 

<p align="center">
    <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h87v4qi9m4j313g0qygnk.jpg" width="50%" height="50%">
</p>


```python
class Solution(object):
    def search(self, nums, target):
        left = 0
        right = len(nums) #define target in the closed interval [left,right]
        while left < right: #when left==right, [left,right] inveral is still legal, so use <=
            middle = left + ((right - left) >> 1) #shift right 1 bit equal to (right-left)/2
            if nums[middle] > target:
                right = middle #target is in [left,middle-1]
            elif nums[middle] < target:
                left = middle +1 #target is in [middle+1,left]
            else: return middle #find target
        return -1
```

Submission Proof

<p align="center">
    <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h87v5bc08hj31c00u00wc.jpg" width="70%" height="70%">
</p>



## 27. Remove Elements

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The relative order of the elements may be changed.

Examples:

```
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.
It does not matter what you leave beyond the returned k (hence they are underscores).

Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,4,0,3,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
Note that the five elements can be returned in any order.
It does not matter what you leave beyond the returned k (hence they are underscores).
```

Brute Force Approach: Time Complexity - O(n²) / Space Complexity - O(1)

```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        if nums is None or len(nums)==0:
          return 0
        size = len(nums)
        i = 0
        while i < size:
            if nums[i]==val: #if find the element to remove, shift the rest of array to the left
                j = i+1
                while j<len(nums):
                    nums[j-1]=nums[j]
                    j+=1
                #Because after the element is removed, the following values are moved forward by 1 digit
                #And we haven't if check nums[i] is the element to be removed.We have to cancel out the
                #effect of later i+=1
                i-=1 
                size-=1
            i+=1
        return size
```

Two Pointer Approach: Time Complexity - O(n) / Space Complexity - O(1)

```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        if nums is None or len(nums)==0:
          return 0
        slow = 0
        for fast in range(len(nums)):
            if nums[fast]!=val:
                nums[slow]=nums[fast]
                slow=slow+1
        return slow
```



Algorithm logic:

1. Fast pointer is used to get elements in array
2. Slow pointer is used to get the position in new array that needs to be updated







