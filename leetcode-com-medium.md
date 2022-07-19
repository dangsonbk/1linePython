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
