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
