## ⚠Arithmetic Sequences

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/room/Is-Is-3QBtdAZ3vF)

**Description**:

> Given a list of integers `nums`, return the number of contiguous arithmetic sequences of length `≥ 3`.
> 
> **Input**: nums = [5, 7, 9, 11, 12, 13]
> 
> **Output**: 4

**Answer**:

```python
return sum(map( lambda n: n*(n-1)//2, [len(list(g)) for _, g in groupby(zip(nums[:-1], nums[1:]), lambda p: p[1] - p[0])]))
```

**Explanations**:

- `groupby(zip(nums[:-1], nums[1:])`: divide input list into pairs, groupby there differences between elements.

- output after list of groupby could be like: `[[(5, 7), (7, 9), (9, 11)], [(11, 12), (12, 13)]]`

- As given *return the number of contiguous arithmetic sequences of length `≥ 3`.* means count the number of sub-group of group with length >= 2. Calculate by `n*(n-1)//2`with n = length of group.


