## ⚠Binary Prefix Divisible By 5

**Source**: [Binary Prefix Divisible By 5](https://leetcode.com/problems/binary-prefix-divisible-by-5/submissions/)

**Description**:

> You are given a binary array `nums` (**0-indexed**).
> 
> We define `xi` as the number whose binary representation is the subarray `nums[0..i]` (from most-significant-bit to least-significant-bit).
> 
> - For example, if `nums = [1,0,1]`, then `x0 = 1`, `x1 = 2`, and `x2 = 5`.
> 
> Return *an array of booleans* `answer` *where* `answer[i]` *is* `true` *if* `xi` *is divisible by* `5`.

**Answer**:

```python
return reduce(lambda p, n: [p[0] + str(n), p[1] + [int(p[0] + str(n), 2)%5 == 0]], [["", []]] + nums)[1]
```

## ⚠Minimum Add to Make Parentheses Valid

**Source**: [Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)

**Description**:

> A parentheses string is valid if and only if:
> 
> - It is the empty string,
> - It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
> - It can be written as `(A)`, where `A` is a valid string.
> 
> You are given a parentheses string `s`. In one move, you can insert a parenthesis at any position of the string.
> 
> - For example, if `s = "()))"`, you can insert an opening parenthesis to be `"(**(**)))"` or a closing parenthesis to be `"())**)**)"`.
> 
> Return *the minimum number of moves required to make* `s` *valid*.

**Answer**:

```python
return len(functools.reduce(lambda c1, c2: c2 if not c1 else c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2, s)) if s else len(s)
```

**Explanations**:

Uses Python `reduce()` on string s, whenever it has '()' in the result of `reduce()` step then remove this from string.

- Can use `''.join((c1, c2)).replace("()", "")` but the performance is pretty bad.
- `c2 if not c1 else ...`: prevent Exception on `c1[:-1]` when c1 is empty.
- `c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2`: if `c1 + c2` ends with `()`, then take `c1[:1]` only, else take `c1 + c2`.


