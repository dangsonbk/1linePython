## binarysearch.com easy problems

---

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

## ⚠Binary Matrix Leftmost One

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Binary-Matrix-Leftmost-One)

**Description**:

> You are given a two-dimensional list of integers `matrix` which contains `1`s and `0`s. Given that each row is sorted in ascending order with `0`s coming before `1`s, return the leftmost column index with the value of `1`. If there's no row with a `1`, return `-1`.
> 
> Can you solve it faster than O(nm).

**Answer**:

```python
return -1 if not len([matrix[i].index(1) for i in range(len(matrix)) if 1 in matrix[i]]) else min([matrix[i].index(1) for i in range(len(matrix)) if 1 in matrix[i]])
```

**Explanations**:

Actually it should be:

```python
left_most = [matrix[i].index(1) for i in range(len(matrix)) if 1 in matrix[i]]
return -1 if not len(left_most) else min(left_most)
```

But the answer still fits under time limitation.

## ⚠Submajority Vote

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Submajority-Vote)

**Description**:

> You are given a list of integers `nums` where each number represents a vote to a candidate.
> 
> Return the ids of the candidates that have greater than ⌊3n​⌋ votes, in ascending order.
> 
> Bonus: solve in O(1) space.

**Answer**:

```python
return sorted(list(c for c in Counter(nums) if Counter(nums)[c] > len(nums)/3))
```

## ⚠Airplane Seat Shuffling

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Airplane-Seat-Shuffling)

**Description**:

> You are given an integer `n` representing the number of seats in an airplane. The first person has lost their ticket, so they pick a random seat. Everyone else still has their ticket, but if their seat is already taken, they will also randomly pick an available seat.
> 
> Return the probability that the last person gets their assigned seat.

**Answer**:

```python
return 0.5 if n != 1 else 1
```

**Explanations**:

This is just a tricky question.

## 1linePython

Collection of 1-line Python answers on some online code challenges.

## ⚠Demo

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Dropped-Sensor-Metric)

**Description**:

> You are given two lists of integers `a` and `b` representing sensor metrics. Each list contains unique integers and `a ≠ b`. One of the lists contains accurate sensor metrics but the other one is faulty. In the faulty list one number that wasn't the last number was dropped and a fake value was appended to the end of the list. Return the number that was dropped.
> 
> **Input**
> 
> a = [1, 2, 3]
> 
> b = [2, 3, 5]
> 
> **Output**
> 
> 1

**Answer**:

```python
return set(a).difference(set(b)).pop() if set(b).difference(set(a)).pop() == b[-1] else set(b).difference(set(a)).pop()
```

**Explanations**:

Long version:

```python
class Solution:
    def solve(self, a, b):
        _a = set(a)
        _b = set(b)
        __a = _a.difference(_b)
        __b = _b.difference(_a)
        x = __b.pop()
        if x == b[-1]:
            return __a.pop()
        else:
            return x
        print(__a, __b)
```
