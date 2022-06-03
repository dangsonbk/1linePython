## binarysearch.com easy problems

## ⚠Demo

**Source**:

**Description**:

> Description and example

**Answer**:

```python
#
```

**Explanations**:

## ⚠Compress String

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Compress-String)

**Description**:

> Given a string lowercase alphabet `s`, eliminate consecutive duplicate characters from the string and return it.
> 
> That is, if a list contains repeated characters, they should be replaced with a single copy of the character. The order of the elements should not be changed.
> 
> **Input**: s = "aaaaaabbbccccaaaaddf"
> 
> **Output**: "abcadf"

**Answer:**

```python
return ''.join(str(x) for x, _ in groupby(s))
```

## ⚠Run-Length Encoding

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Run-Length-Encoding)

**Description**:

> Given a string `s`, return its run-length encoding. You can assume the string to be encoded have no digits and consists solely of alphabetic characters.
> 
> **Input**: s = "aaaabbbccdaa"
> 
> **Output**: "4a3b2c1d2a"

**Answer**:

```python
return "".join(f"{sum(1 for _ in y)}{x}" for x, y in groupby(s))
```

**Explanations**:

`itertools.groupby()` then count the number of times the character appears in each group.

Note that object of type `itertools._grouper_` does not support `len()` method, so we have to use `sum(1 for _ in y)`

## ⚠Square of a List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Square-of-a-List)

**Description**:

> Given a list of integers sorted in ascending order `nums`, square the elements and give the output in sorted order.

**Answer**:

```python
return sorted(map(lambda x: x*x, nums))
```

## ⚠Verify Max Heap

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Verify-Max-Heap)

**Description**:

> Given a list of integers `nums`, return whether it represents a max heap. That is, for every `i` we have that:
> 
> - `nums[i] ≥ nums[2*i + 1]` if `2*i + 1` is within bounds
> - `nums[i] ≥ nums[2*i + 2]` if `2*i + 2` is within bounds

**Answer**:

```python
return [1 for i in range(len(nums)) if 2*i + 1 < len(nums) and nums[i] < nums[2*i + 1]].count(1) + [1 for i in range(len(nums)) if 2*i + 2 < len(nums) and nums[i] < nums[2*i + 2]].count(1) == 0
```

**Explanation**:

Iterate through the list, `1` if invalid with requirements, then count if any `1` shown up.


## ⚠Just Average

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Just-Average)

**Description**:

> Given a list of integers nums and an integer k, return true if you can remove exactly one element from the list to make the average equal to exactly k
> 
> **Input**: nums = [1, 2, 3, 10], k = 2
> 
> **Output**: "True"

**Answer**:

```python
return (sum(nums) - k * (len(nums) - 1)) in nums
```

## ⚠Narcissistic Number

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Narcissistic-Number)

**Description**:

> Given an integer n, return whether it is equal to the sum of its own digits raised to the power of the number of digits.
> 
> **Input**: n = 153
> 
> **Output**: "True"

**Answer**:

```python
return sum(map(lambda i: i**len(str(n)), [int(d) for d in str(n)])) == n
```

## ⚠A Unique String

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/A-Unique-String)

**Description**:

> Given a lowercase alphabet string s, determine whether it has all unique characters.
> 
> **Input**: s = "abcde"
> 
> **Output**: "True"

**Answer**:

```python
return len(set(s)) == len(s)
```

## ⚠Intervals Intersecting at Point

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Intervals-Intersecting-at-Point)

**Description**:

> You are given a two-dimensional list of integers intervals and an integer point. Each element contains [start, end] represents an inclusive interval. Return the number of intervals that are intersecting at point.
> 
> **Input**: intervals = [[1, 5],[3, 9],[4, 8],[10, 13]], point = 4
> 
> **Output**: 3

**Answer**:

```python
return [1 for i in intervals if point >= i[0] and point <= i[1]].count(1)
```

## ⚠Interleaved String

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Interleaved-String)

**Description**:

> Given two strings s0 and s1, return the two strings interleaved, starting with s0. If there are leftover characters in a string they should be added to the end.
> 
> **Input**: s0 = "abc", s1 = "xyz"
> 
> **Output**: "axbycz"

**Answer**:

```python
return list("".join(str(x) for x in i) for i in zip(a, b))
```

## ⚠Verify Max Heap

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Verify-Max-Heap)

**Description**:

> Given a list of integers nums, return whether it represents a max heap. That is, for every i we have that: nums[i] ≥ nums[2*i + 1] if 2*i + 1 is within bounds nums[i] ≥ nums[2*i + 2] if 2*i + 2 is within bounds
> 
> **Input**: nums = [4, 2, 3, 0, 1]
> 
> **Output**: True

**Answer**:

```python
return len(list(dropwhile(lambda x: ((a[2 * x + 1] <= a[x]) if (2 * x + 1) < len(a) else True) and ((a[2 * x + 2] <= a[x]) if (2 * x + 2) < len(a) else True) , range(len(a))))) == 0
```
