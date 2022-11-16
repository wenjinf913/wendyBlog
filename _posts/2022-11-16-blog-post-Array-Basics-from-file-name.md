## Binary Search Basics

1. Binary search has to work on _**Ordered Array**_ and _**No Repeating Elements**_ in the array. 
2. Binary search has to define _**Interval**_ - **左闭右闭 [left, right] _or_ 左闭右开 [left, right)** and stick to _**Loop Invariant Principle**_

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
2. if (nums[middle} > target) & if (nums[middle} < target) **left = middle -1** & **right = middle +1**, since nums[middle] is not the target

![binary-search_closed_interval](/wenjinfu913.github.io/_posts/post_img/binary-search_closed_interval.jpg)



















