## binarysearch.com easy problems

## Demo

**Source**:

**Description**:

> Description and example

**Answer**:

```python
#
```

**Explanations**:

## Compress String

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Compress-String)

**Description**:

> Given a string lowercase alphabet `s`, eliminate consecutive duplicate characters from the string and return it.
> 
> That is, if a list contains repeated characters, they should be replaced with a single copy of the character. The order of the elements should not be changed.
> 
> #### Input
> 
> s = "aaaaaabbbccccaaaaddf"
> 
> #### Output
> 
> "abcadf"

**Answer:**

```python
return ''.join(str(x) for x, _ in groupby(s))
```

## Run-Length Encoding

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Run-Length-Encoding)

**Description**:

> Given a string `s`, return its run-length encoding. You can assume the string to be encoded have no digits and consists solely of alphabetic characters.
> 
> #### **Input**
> 
> s = "aaaabbbccdaa"
> 
> #### **Output**
> 
> "4a3b2c1d2a"

**Answer**:

```python
return "".join(f"{sum(1 for _ in y)}{x}" for x, y in groupby(s))
```

## Square of a List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Square-of-a-List)

**Description**:

> Given a list of integers sorted in ascending order `nums`, square the elements and give the output in sorted order.

**Answer**:

```python
return sorted(map(lambda x: x*x, nums))
```

## Verify Max Heap

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


