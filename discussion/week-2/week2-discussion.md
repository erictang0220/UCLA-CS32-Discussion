# Discussion Session Week 2
By Licheng Guo and Devyan Biswas

- Git
- Binary Search

## Basic Introduction to Git

- Git is a version control tool
- You can have many "snapshot" of the current status of your project
- You could see the latest modification compared to your last checkpoint.
- You could go back to your last checkpoint if you somehow mess up your code.
- Help you colloborate with others to work on the same project

### Basic Commands

- `git init` 
  - Creates a new git repository

- `git status`
  - Show the lastest status of your git repo

- `git add`
  - Tell git to start tracking a file.

- `git commit`
  - Tell git to make a checkpoint of the current status of your project

- `git diff [FILE NAME]`
  - Show the modification done to this file compared to its contents in the last checkpoint

- `git log`
  - Show the history of checkpoints

## Recommended Tool
- VSCode + Remote SSH
- MobaXTerm (for Windows)
- VNCViewer / VNCserver
- Vim
- Tmux 

## Binary Search

### 1. Search in Sorted Array

Given an array of integers `nums` sorted in **ascending** order, find the position of a given `target` value. If `target` is not found in the array, return `-1`. Solve the problem in `log(n)` time.

- Example 1
<pre>
<b>Input</b>: nums = [5,6,7,8,9,10], target = 9
<b>Output</b>: 4
</pre>

- Example 2
<pre>
<b>Input</b>: nums = [5,6,7,8,9,11,12], target = 10
<b>Output</b>: -1
</pre>

- Example 3
<pre>
<b>Input</b>: nums = [], target = 0
<b>Output</b>: -1
</pre>

```c++
1  int searchNum(int[] nums, int size, int target) {
2    int lo = 0;
3    int hi = size-1; // pay attention to the -1
4  
5    while (lo <= hi) { // pay attention to <= or <
6      int mid = (lo + hi) / 2; // pay attention whether +1
7  
8      if (nums[mid] == target) { 
9        return mid;
10     }
11     else if (nums[mid] < target ) { 
12       lo = mid + 1;
13     }
14     else {
15       hi = mid - 1;
16     }
17   }
18    
19   return -1; // pay attention if final checking is needed
20 }
```

Lesson learned:

- When you made a "typo", it is likely that you will make this "typo" again. Every "typo" is a fundamentally bug/error.
- Keep a record of what you have written. Write comments where you have made mistakes.
- Potential Errors in this example:
  - `size` vs `size-1`
  - `while(lo < hi)` vs `while (lo <= hi)`
  - `lo = mid` vs `lo = mid + 1`
  - Whether to change `lo` or `hi` (e.g., when `nums[mid] < target`)
  - double-check whether you can directly return `-1` outside the loop.
  - `mid = (lo + hi) / 2` vs `mid = (lo + hi) / 2`
  - Diversity your test cases.

- Follow-up questions:
  - What if we write `lo = mid;` instead?

```c++
1  int searchNum(int[] nums, int size, int target) {
2    int lo = 0;
3    int hi = size-1; // pay attention to the -1
4  
5    while (lo < hi) { 
6      // int mid = (lo + hi) / 2;
6      int mid = (lo + hi) / 2 + 1;
7  
8      if (nums[mid] == target) { 
9        return mid;
10     }
11     else if (nums[mid] < target ) { 
12       lo = mid;
13     }
14     else {
15       hi = mid - 1;
16     }
17   }
18    
19   if (nums[lo] == target) return lo;
20   else return -1;
21 }
```

## More Follow-up Questions Not Discussed Yet

The key point here is that it may not be obvious that you can use binary search to solve things. You could check the solution on Leetcode by yourself.

### 2. Search in Sorted Array with Repetition (Leetcode 34)

Given an array of integers `nums` sorted in **non-descending** order, find the starting and ending position of a given `target` value. If `target` is not found in the array, return `[-1, -1]`.

- Example 1
<pre>
<b>Input</b>: nums = [5,7,7,8,8,10], target = 8
<b>Output</b>: [3, 4]
</pre>

- Example 2
<pre>
<b>Input</b>: nums = [5,7,7,8,8,10], target = 6
<b>Output</b>: [-1, -1]
</pre>

- Example 3
<pre>
<b>Input</b>: nums = [], target = 0
<b>Output</b>: [-1, -1]
</pre>

- Hint
  - First use binary search to find where is the "rotation pivot"

### 3. Search in Rotated Sorted Array (Leetcode 33)

You are given an integer array `nums` sorted in ascending order (with distinct values), and an integer `target`. Suppose that `nums` is rotated at some pivot unknown to you beforehand (i.e., `[0,1,2,4,5,6,7]` might become `[4,5,6,7,0,1,2]`). If `target` is found in the array return its index, otherwise, return `-1`.

- Example 1
<pre>
<b>Input</b>: nums = [4,5,6,7,0,1,2], target = 0
<b>Output</b>: 4
</pre>

- Example 2
<pre>
<b>Input</b>: nums = [4,5,6,7,0,1,2], target = 3
<b>Output</b>: -1
</pre>

- Example 3
<pre>
<b>Input</b>: nums = [1], target = 0
<b>Output</b>: -1
</pre>

- Hint
  - Use binary search to find the left and right boundary of the group of targets.