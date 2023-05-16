## 🧩 Minimum Deletions to Make Character Frequencies Unique

**Source**: [Minimum Deletions to Make Character Frequencies Unique](https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique/)

**Description**:

> A string `s` is called **good** if there are no two different characters in `s` that have the same **frequency**.
> 
> Given a string `s`, return *the **minimum** number of characters you need to delete to make* `s` ***good**.*
> 
> The **frequency** of a character in a string is the number of times it appears in the string. For example, in the string `"aab"`, the **frequency** of `'a'` is `2`, while the **frequency** of `'b'` is `1`.
> 
> **Constraints:**
> 
> - `1 <= s.length <= 10^5`
> - `s` contains only lowercase English letters.

**Answer**:

```python
return reduce(lambda p, _: [p[1], p[0] + p[1]], range(n), [0, 1])[0]**Explanations**:
```

- Sort the frequency of letters in decreasing order.

- Seed the `reduce()` function with `[last_value, number_of_deletions] and sorted frequency`

- If any letter's frequency value is equal or larger than previous value, decrease it's value and add the same amount to the `number_of_deletions`.

## 🧩 Queue Reconstruction by Height

**Source**: [Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/)

**Description**:

> You are given an array of people, people, which are the attributes of some people in a queue (not necessarily in order). Each `people[i] = [hi, ki]` represents the `ith` person of height hi with exactly `ki` other people in front who have a height greater than or equal to hi.
> 
> Reconstruct and return the queue that is represented by the input array people. The returned queue should be formatted as an array queue, where `queue[j] = [hj, kj]` is the attributes of the `jth` person in the queue (queue[0] is the person at the front of the queue).

**Answer**:

```python
return reduce(lambda p, n: p[:n[1]] + [n] + p[n[1]:] , [[]] + sorted(people, key=lambda x: (x[0], -x[1]), reverse=True))
```

**Explanations**:

- [Visual Explanation | JAVA Greedy](https://leetcode.com/problems/queue-reconstruction-by-height/discuss/2211641/Visual-Explanation-or-JAVA-Greedy)
- [Easy concept with Python/C++/Java Solution](https://leetcode.com/problems/queue-reconstruction-by-height/discuss/89345/Easy-concept-with-PythonC%2B%2BJava-Solution)

## 🧩 Find Triangular Sum of an Array

**Source**: [Find Triangular Sum of an Array](https://leetcode.com/problems/find-triangular-sum-of-an-array/)

**Description**:

> You are given a **0-indexed** integer array `nums`, where `nums[i]` is a digit between `0` and `9` (**inclusive**).
> 
> The **triangular sum** of `nums` is the value of the only element present in `nums` after the following process terminates:
> 
> 1. Let `nums` comprise of `n` elements. If `n == 1`, **end** the process. Otherwise, **create** a new **0-indexed** integer array `newNums` of length `n - 1`.
> 2. For each index `i`, where `0 <= i < n - 1`, **assign** the value of `newNums[i]` as `(nums[i] + nums[i+1]) % 10`, where `%` denotes modulo operator.
> 3. **Replace** the array `nums` with `newNums`.
> 4. **Repeat** the entire process starting from step 1.
> 
> Return *the triangular sum of* `nums`.

**Answer**:

```python
return reduce(lambda p, n: list(map(lambda x: sum(x) % 10, pairwise(p))), [1] * (len(nums) - 1), nums)[0]
```

**Explanations**:

- Just calculate each row

## 🧩 Reduce Array Size to The Half

**Source**: [Reduce Array Size to The Half](https://leetcode.com/problems/reduce-array-size-to-the-half)

**Description**:

> You are given an integer array arr. You can choose a set of integers and remove all the occurrences of these integers in the array.
> 
> Return the minimum size of the set so that at least half of the integers of the array are removed.
> 
> Example 1:
> Input: `arr = [3,3,3,3,5,5,5,2,2,7]`
> Output: 2
> Explanation: Choosing `{3,7}` will make the new array `[5,5,5,2,2]` which has size 5 (i.e equal to half of the size of the old array).
> Possible sets of size 2 are `{3,5},{3,2},{5,2}`.
> Choosing set {2,7} is not possible as it will make the new array `[3,3,3,3,5,5,5]` which has a size greater than half of the size of the old array.
> 
> Example 2:
> Input: `arr = [7,7,7,7,7,7]`
> Output: 1
> Explanation: The only possible set you can choose is `{7}`. This will make the new array empty.

**Answer**:

```python
return len(list(takewhile(lambda x: x < len(arr)//2, accumulate(sorted(Counter(arr).values(), reverse=True))))) + 1
```

**Explanations**:

- Counter return how many times each number appears in the input array.
- Sort Counter()'s returned values, take while the sum of values less than half the length of input array, so that we have the minimum numbers of letters that need to be removed.

## 🧩 Reordered Power of 2

**Source**: [Reordered Power of 2](https://leetcode.com/problems/reordered-power-of-2/)

**Description**:

> You are given an integer n. We reorder the digits in any order (including the original order) such that the leading digit is not zero.
> Return true if and only if we can do this so that the resulting number is a power of two.

**Answer 1**:

```python
return next((True for i in range(30) if Counter(str(n)) == Counter(str(pow(2, i)))), False)
```

**Answer 2**:
```python
return sorted(str(n)) in [['1'], ['2'], ['4'], ['8'], ['1', '6'], ['2', '3'], ['4', '6'], ['1', '2', '8'], ['2', '5', '6'], ['1', '2', '5'], ['0', '1', '2', '4'], ['0', '2', '4', '8'], ['0', '4', '6', '9'], ['1', '2', '8', '9'], ['1', '3', '4', '6', '8'], ['2', '3', '6', '7', '8'], ['3', '5', '5', '6', '6'], ['0', '1', '1', '2', '3', '7'], ['1', '2', '2', '4', '4', '6'], ['2', '2', '4', '5', '8', '8'], ['0', '1', '4', '5', '6', '7', '8'], ['0', '1', '2', '2', '5', '7', '9'], ['0', '1', '3', '4', '4', '4', '9'], ['0', '3', '6', '8', '8', '8', '8'], ['1', '1', '2', '6', '6', '7', '7', '7'], ['2', '3', '3', '3', '4', '4', '5', '5'], ['0', '1', '4', '6', '6', '7', '8', '8'], ['1', '1', '2', '2', '3', '4', '7', '7', '8'], ['2', '3', '4', '4', '5', '5', '6', '6', '8'], ['0', '1', '2', '3', '5', '6', '7', '8', '9']]
```

## 🧩 Rotate Image

**Source**: [Rotate Image](https://leetcode.com/problems/rotate-image/)

**Description**:

> You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).
> You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

**Answer 1**:

```python
list(map(lambda p: setitem(matrix, p[0], p[1]), enumerate(zip(*matrix[::-1]))))
```

**Answer 2**:
[Seven Short Solutions (1 to 7 lines)](https://leetcode.com/problems/rotate-image/discuss/18884/Seven-Short-Solutions-(1-to-7-lines))

**Explanations**:
- Please check [Rotating a two-dimensional array in Python](https://stackoverflow.com/questions/8421337/rotating-a-two-dimensional-array-in-python)
- It required to modify the matrix in-place, 1st answer use `operation.setitem()`, while 2nd solution simply uses `matrix[:]`.

## 🧩 Minimum Time to Make Rope Colorful

**Source**: [Minimum Time to Make Rope Colorful](https://leetcode.com/problems/minimum-time-to-make-rope-colorful/)

**Description**:

> Alice has n balloons arranged on a rope. You are given a 0-indexed string colors where colors[i] is the color of the ith balloon.
> 
> Alice wants the rope to be colorful. She does not want two consecutive balloons to be of the same color, so she asks Bob for help. Bob can remove some balloons from > the rope to make it colorful. You are given a 0-indexed integer array neededTime where neededTime[i] is the time (in seconds) that Bob needs to remove the ith balloon from the rope.
> 
> Return the minimum time Bob needs to make the rope colorful.

**Answer**:

```python
return reduce(lambda p, n: p + n[1],(chain.from_iterable(filter(len, [sorted(list(g))[:-1] for k, g in groupby(zip(colors, neededTime), lambda n: n[0])]))), 0)
```

**Explaination**
- Groupby the zipped inputs.
- Slice the sorted groupby output by [1:]
- Sum the time by using reduce

## 🧩 Sum of Two Integers

**Source**: [Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers)

**Description**:

> Given two integers a and b, return the sum of the two integers without using the operators + and -.

**Answer**: LMAO

```python
class Solution:
    getSum = add
```

## 🧩 Count and Say

**Source**: [Count and Say](https://leetcode.com/problems/count-and-say)

**Description**:

> The count-and-say sequence is a sequence of digit strings defined by the recursive formula:
> countAndSay(1) = "1"
> countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.
> To determine how you "say" a digit string, split it into the minimal number of substrings such that each substring contains exactly one unique digit. Then for each  substring, say the number of digits, then say the digit. Finally, concatenate every said digit.

**Answer**:

```python
return reduce(lambda s, _: ''.join(str(len(list(group))) + d for d, group in groupby(s)), range(n - 1), '1')
```

## 🧩 Permutations

**Source**: [Permutations](https://leetcode.com/problems/permutations)

**Description**:

> Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

**Answer**:

```python
return permutations(nums)
```

## 🧩 Permutations II

**Source**: [Permutations II](https://leetcode.com/problems/permutations-ii)

**Description**:

> Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

**Answer**:

```python
return set(permutations(nums))
```

## 🧩 Rectangle Area

**Source**: [Rectangle Area](https://leetcode.com/problems/rectangle-area)

**Description**:

> Given the coordinates of two rectilinear rectangles in a 2D plane, return the total area covered by the two rectangles.
> The first rectangle is defined by its bottom-left corner (ax1, ay1) and its top-right corner (ax2, ay2).
> The second rectangle is defined by its bottom-left corner (bx1, by1) and its top-right corner (bx2, by2).

**Answer**: Credit to: [python3 one-liner O(1) with explanations](https://leetcode.com/problems/rectangle-area/solutions/2822228/python3-one-liner-o-1-with-explanations/), please upvote author

```python
return (ax2-ax1)*(ay2-ay1) + (bx2-bx1)*(by2-by1) - max(min(ax2,bx2)-max(ax1,bx1), 0) * max(min(ay2,by2)-max(ay1,by1), 0)
```

## 🧩 Determine if Two Strings Are Close

**Source**: [Determine if Two Strings Are Close](https://leetcode.com/problems/determine-if-two-strings-are-close)

**Description**:

> Two strings are considered close if you can attain one from the other using the following operations:
> 
> Operation 1: Swap any two existing characters.
> For example, abcde -> aecdb
> Operation 2: Transform every occurrence of one existing character into another existing character, and do the same with the other character.
> For example, aacabb -> bbcbaa (all a's turn into b's, and all b's turn into a's)
> You can use the operations on either string as many times as necessary.

> Given two strings, word1 and word2, return true if word1 and word2 are close, and false otherwise.

**Answer**:

```python
return set(word1) == set(word2) and sorted(Counter(word1).values()) == sorted(Counter(word2).values())
```
