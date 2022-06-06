## binarysearch.com easy problems

---

## ⚠Minimum Bracket Addition

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Minimum-Bracket-Addition)

**Description**:

> Given a string `s` containing brackets `(` and `)`, return the minimum number of brackets that can be inserted so that the brackets are balanced.
> 
> **Input**: s = ")))(("
> 
> **Output**: 5

**Answer**:

```python
return len(functools.reduce(lambda c1, c2: c2 if not c1 else c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2, s)) if s else 0
```

**Explanations**:

Uses Python `reduce()` on string s, whenever it has '()' in the result of `reduce()` step then remove this from string.

- Can use `''.join((c1, c2)).replace("()", "")` but the performance is pretty bad.
- `c2 if not c1 else ...`: prevent Exception on `c1[:-1]` when c1 is empty.
- `c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2`: if `c1 + c2` ends with `()`, then take `c1[:1]` only, else take `c1 + c2`.
- Not really 1 line because `reduce()` require `functools` imported.

## ⚠Large to Small Sort

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Large-to-Small-Sort)

**Description**:

> Given a list of integers `nums`, sort the list in the following way:
> 
> - First number is the maximum
> - Second number is the minimum
> - Third number is the 2nd maximum
> - Fourth number is the 2nd minimum
> - And so on.
> 
> **Input**: nums = [5, 2, 9, 3]
> 
> **Output**: [9, 2, 5, 3]

**Answer**:

```python
return [x for x in chain(*zip_longest(sorted(nums)[len(nums)//2:][::-1], sorted(nums)[:len(nums)//2])) if x is not None]
```

**Explanations**:

- Slices sorted input into two lists, reverse second list, got `[2, 3]` and `[9, 5]`.

- zip these two lists with second list first: got `(9, 2)`, `(5, 3)`

- chain them

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

## ⚠First Fit Room

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/First-Fit-Room)

**Description**:

> You are given a list of integers `rooms` and an integer `target`. Return the first integer in `rooms` that's `target` or larger. If there is no solution, return `-1`.

**Answer**:

```python
return next((r for r in rooms if r >= target), -1)
```

**Explanations**:

[python - Get the first item from an iterable that matches a condition - Stack Overflow](https://stackoverflow.com/a/2364277)

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
return "".join(str(len(list(y))) + str(x) for x, y in groupby(s))
# https://stackoverflow.com/a/59183023
return "".join(f"{sum(1 for _ in y)}{x}" for x, y in groupby(s))
```

**Explanations**:

`itertools.groupby()` then count the number of times the character appears in each group.

Note that object of type `itertools._grouper_` does not support `len()` method, so we have to use `sum(1 for _ in y)`or convert it to list.

## ⚠FizzBuzz

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/FizzBuzz)

**Description**:

> Given an integer `n`, return a list of integers from `1` to `n` as strings except for multiples of `3` use `“Fizz”` instead of the integer and for the multiples of `5` use `“Buzz”`. For integers which are multiples of both `3` and `5` use `“FizzBuzz”`.

**Answer**:

```python
return ["FizzBuzz" if not i%3 and not i%5 else "Fizz" if not i%3 else "Buzz" if not i%5 else str(i) for i in range(1, n+1)]
```

## ⚠Anagram Checks

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Anagram-Checks)

**Description**:

> Given two strings `s0` and `s1`, return whether they are anagrams of each other.

**Answer**:

```python
return sorted(s0) == sorted(s1)
```

## ⚠Square of a List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Square-of-a-List)

**Description**:

> Given a list of integers sorted in ascending order `nums`, square the elements and give the output in sorted order.

**Answer**:

```python
return sorted(map(lambda x: x*x, nums))
```

## ⚠Run-Length Decoding

**Source**:

**Description**:

> Given a string `s`, consisting of digits and lowercase alphabet characters, that's a run-length encoded string, return its decoded version.
> 
> Note: The original string is guaranteed not to have numbers in it.
> 
> **Input**: s = "4a3b2c1d2a"
> 
> **Output**: "aaaabbbccdaa"

**Answer**:

```python
return reduce(lambda p, c: (p[0] + c*p[1], int(c) if c.isnumeric() else 0), [("", 0)]+["".join(g[1]) for g in groupby(s, lambda n: n.isnumeric())])[0]
```

**Explanations**:

- `groupby` by `lambda n: n.isnumeric()`and create list of `[num, character, num, character ...]`

- `reduce`start with`("", n)`, where `n` is the number of times the next character appears.

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
# Your code took 4 milliseconds — faster than 18.41% in Python
```

**Explanation**:

Iterate through the list, `1` if invalid with requirements, then count if any `1` shown up.

**Answer 2**:

```python
return len(list(dropwhile(lambda x: ((a[2 * x + 1] <= a[x]) if (2 * x + 1) < len(a) else True) and ((a[2 * x  2] <= a[x]) if (2 * x + 2) < len(a) else True) , range(len(a))))) == 0
```

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
return "".join(i for j in zip(s0[:min([len(s0), len(s1)])], s1[:min([len(s0), len(s1)])]) for i in j) + s0[min([len(s0), len(s1)]):] + s1[min([len(s0), len(s1)]):]
```

**Explanation**:

- Slice the longer string to the length equal shorter string, zip 2 strings.

- Add the rest of longer string.

- It's fun but the answer 2 is better.

**Answer 2**:

```python
return "".join("".join(x) for x in zip_longest(s0, s1, fillvalue=''))
```

**Explanation**:

- Check this: [itertools zip_longest](https://docs.python.org/3/library/itertools.html#itertools.zip_longest)

## ⚠Reverse Sublists to Convert to Target

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Reverse-Sublists-to-Convert-to-Target)

**Description**:

> Given two lists of integers `nums`, and `target`, consider an operation where you take some sublist in `nums` and reverse it. Return whether it's possible to turn `nums` into `target`, given you can make any number of operations.
> 
> **Input**
> 
> nums = [1, 2, 3, 8, 9]
> 
> target = [3, 2, 1, 9, 8]
> 
> **Output**: True

**Answer**:

```python
return Counter(nums) == Counter(target)
```

## ⚠Greatest Common Divisor

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Greatest-Common-Divisor)

**Description**:

> Given a list of positive integers `nums`, return the largest positive integer that divides each of the integers.

**Answer**:

```python
return reduce(math.gcd, nums)
```

## ⚠Longest Alliteration

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Longest-Alliteration)

**Description**:

> Given a list of lowercase alphabet strings `words`, return the length of the longest contiguous sublist where all words share the same first letter.
> 
> **Input**: words = ["she", "sells", "seashells", "he", "sells", "clams"]
> 
> **Output**: 3

**Answer**:

```python
 return max([len(list(g[1])) for g in groupby(words, lambda x: x[0])]) if len(words) else 0
```

**Explanation:**

groupby() by first later of words then find longest group.

## ⚠Rotate List Left by K

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Rotate-List-Left-by-K)

**Description**:

> Write a function that rotates a list of numbers to the left by `k` elements. Numbers should wrap around.
> 
> Note: The list is guaranteed to have at least one element, and `k` is guaranteed to be less than or equal to the length of the list.
> 
> Bonus: Do this without creating a copy of the list. How many swap or move operations do you need?
> 
> **Input**
> 
> nums = [1, 2, 3, 4, 5, 6]
> 
> k = 2
> 
> **Output**: [3, 4, 5, 6, 1, 2]

**Answer**:

```python
return nums[k:] + nums[:k]
```

## ⚠Largest Gap

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Largest-Gap)

**Description**:

> Given a list of integers `nums`, return the largest difference of two consecutive integers in the sorted version of `nums`.

**Answer**:

```python
return max([y-x for x,y in zip(sorted(nums)[:-1], sorted(nums)[1:])])
```

## ⚠Odd Number of Digits

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Odd-Number-of-Digits)

**Description**:

> Given a list of positive integers `nums`, return the number of integers that have odd number of digits.

**Answer**:

```python
return len([c for c in nums if len(str(c))%2])
```

## ⚠Append List to Sum Target

**Source**:

**Description**:

> You are given a list of integers `nums` and integers `k` and `target`. Consider an operation where we choose an integer `-k ≤ e ≤ k` and append it to `nums`.
> 
> Return the minimum number of operations required such that the sum of `nums` equals to `target`.

**Answer**:

```python
return math.ceil(abs(sum(nums) - target) / k)
```

## ⚠In-Place Move Zeros to End of List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/In-Place-Move-Zeros-to-End-of-List)

**Description**:

> Given a list of integers `nums`, put all the zeros to the back of the list by modifying the list in-place. The relative ordering of other elements should stay the same.
> 
> Can you do it in O(1) additional space?

**Answer**:

```python
return list([n for n in nums if n != 0]) + [0]*nums.count(0)
```

## ⚠Add One to List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Add-One-to-List)

**Description**:

> You are given a list of integers `nums`, representing a decimal number and `nums[i]` is between `[0, 9]`.
> 
> For example, `[1, 3, 9]` represents the number `139`.
> 
> Return the same list in the same representation except modified so that `1` is added to the number.
> 
> **Input**: nums = [1, 9, 1]
> 
> **Output**: [1, 9, 2]

**Answer**:

```python
return list([int(c) for c in str(int(''.join([str(n) for n in nums])) + 1)])
```

## ⚠Roomba

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Roomba)

**Description**:

> A Roomba robot is currently sitting in a Cartesian plane at `(0, 0)`. You are given a list of its `moves` that it will make, containing `NORTH`, `SOUTH`, `WEST`, and `EAST`.
> 
> Return whether after its moves it will end up in the coordinate `(x, y)`.
> 
> **Input**
> 
> moves = ["NORTH", "EAST"]
> 
> x = 1
> 
> y = 1
> 
> **Output**: True

**Answer**:

```python
return ((x, y) == tuple([sum(p) for p in zip(*[{"NORTH":(0, 1),"EAST":(1, 0),"SOUTH":(0, -1),"WEST":(-1, 0)}[m] for m in moves])])) if len(moves) else (x, y) == (0, 0)
```

**Explanation:**

- Convert moves to direction map: `{"NORTH":(0, 1),"EAST":(1, 0),"SOUTH":(0, -1),"WEST":(-1, 0)`

- zip the move then we have two list of moves by x and moves by y.

- sum the moves to get final position, returns [POS_X, POS_Y], compare to provided x, y values.

## ⚠Reverse Words

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Reverse-Words)

**Description**:

> Given a string `s` of words delimited by spaces, reverse the order of words.

**Answer**:

```python
return " ".join(sentence.split()[::-1])
```

## ⚠Merging Two Sorted Lists

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Merging-Two-Sorted-Lists)

**Description**:

> Given two lists of integers `a` and `b` sorted in ascending order, merge them into one large sorted list.

**Answer**:

```python
return sorted(a + b)
```

## ⚠Sum of First N Odd Integers

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Sum-of-First-N-Odd-Integers)

**Description**:

> Given an integer `n`, return the sum of the first `n` positive odd integers.

**Answer**:

```python
return n*n
```

## ⚠Check Palindrome

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Check-Palindrome)

**Description**:

> Given a string `s`, return whether it is a palindrome.

**Answer**:

```python
return ([1 for i in range(len(s)//2) if s[i] != s[len(s) - 1 - i]].count(1) == 0)
```

## ⚠Detect the Only Duplicate in a List

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Detect-the-Only-Duplicate-in-a-List)

**Description**:

> You are given a list `nums` of length `n + 1` picked from the range `1, 2, ..., n`. By the [pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle), there must be a duplicate. Find and return it. There is guaranteed to be exactly one duplicate.
> 
> Bonus: Can you do this in O(n) time and O(1) space?

**Answer**:

```python
return sum(nums) - sum(set(nums))
```

## ⚠Minimum Initial Value for Positive Prefix Sums

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Minimum-Initial-Value-for-Positive-Prefix-Sums)

**Description**:

> You are given a list of integers nums. Return the minimum positive value we can append to the beginning of nums such that prefix sums of the resulting list contains numbers that are all greater than 0.

**Answer**:

```python
return 1 if not nums or min(accumulate(nums)) > 0  else (abs(min(accumulate(nums))) + 1)
```

## ⚠Consecutive Duplicates

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Consecutive-Duplicates)

**Description**:

> Given a string s, consisting of "X" and "Y"s, delete the minimum number of characters such that there's no consecutive "X" and no consecutive "Y".

**Answer**:

```python
return "".join(x for x,_ in groupby(s))
```

## ⚠Strictly Increasing or Strictly Decreasing

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Strictly-Increasing-or-Strictly-Decreasing)

**Description**:

> Given a list of integers nums, return whether the list is strictly increasing or strictly decreasing.

**Answer**:

```python
return len(list(dropwhile(lambda x: nums[x+1] > nums[x], range(len(nums) - 1)))) == 0 or len(list(dropwhile(lambda x: nums[x+1] < nums[x], range(len(nums) - 1)))) == 0
# Your code took 34 milliseconds — faster than 18.81% in Python
```

**Answer 2:**

```python
return abs(sum([1 if i > j else -1 if i < j else 0 for i, j in zip(nums, nums[1:])])) == len(nums) - 1 if len(nums) > 1 else True
# Your code took 26 milliseconds — faster than 32.82% in Python
```

**Explanation:**

- shift input by one and zip with original input.

- compare items in each zip, reproduce 1, -1, 0 corresponding to larger, smaller, equal

- if list is strictly increasing or strictly decreasing, then number of 1s or -1s must equal `len(input)-1`

## ⚠Shortest String

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Shortest-String)

**Description**:

> Given a string s consisting only of "1"s and "0"s, you can delete any two adjacent letters if they are different. Return the length of the smallest string that you can make if you're able to perform this operation as many times as you want.

**Answer**:

```python
return len(reduce(lambda a, b: a + b if not a or a[-1] == b else a[:-1], s)) if s else 0
```

## ⚠123 Number Flip

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/123-Number-Flip)

**Description**:

> You are given an integer `n` consisting of digits `1`, `2`, and `3` and you can flip one digit to a `3`. Return the maximum number you can make.

**Answer**:

```python
return max([int(str(n)[:i] + "3" + str(n)[i+1:]) for i in range(len(str(n)))])
```

**Explanations**:

- Convert input list to string, generate list of all possible replacements, return max.

## ⚠3-6-9

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/3-6-9)

**Description**:

> Given an integer `n`, return a list with each number from 1 to `n`, except if it's a multiple of 3 or has a 3, 6, or 9 in the number, it should be the string `"clap"`.
> 
> Note: return the number as a string.

**Answer**:

```python
return ["clap" if not i%3 else "clap" if "3" in str(i) or "6" in str(i) or "9" in str(i) else str(i) for i in range(1, n + 1)]
```

## ⚠Even-Frequency

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Even-Frequency)

**Description**:

> Given a list of integers nums, return whether all numbers appear an even number of times.

**Answer**:

```python
return len(list(filter(bool, [1 - len(list(x)) % 2 == 0 for _,x in groupby(sorted(nums))]))) == 0
```

**Answer 2:**

```python
return not any([i%2 for i in Counter(nums).values()])
```

## ⚠Minimum Cost Sort

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Minimum-Cost-Sort)

**Description**:

> Given a list of integers nums, return the minimum cost of sorting the list in ascending or descending order. The cost is defined as the sum of absolute differences between any element's old and new value.

**Answer**:

```python
return min(sum([abs(i - j) for i, j in zip(nums, sorted(nums))]), sum([abs(i - j) for i, j in zip(nums, sorted(nums)[::-1])]))## ⚠3 and 7
```

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/3-and-7)

**Description**:

> Given a positive integer `n`, determine whether you can make `n` by summing up some non-negative multiple of 3 and some non-negative multiple of 7.

**Answer**:

```python
return n > 11 or n in {3, 6, 7, 9, 10}
```

**Explanations**:

Chicken McNugget Theorem aka Postage Stamp Problem. Given any two relatively prime number a, b the greatest N that cannot be represented as ax + by = N is (a*b)–a–b where x, y both > 0.

For a = 3 and b = 7 if n > (3×7-3-7) the answer is true.

## ⚠Max Product of Two Numbers

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Max-Product-of-Two-Numbers)

**Description**:

> Given a list of integers nums, find the largest product of two distinct elements.

**Answer**:

```python
return max(reduce(lambda x, y: x * y, sorted(nums)[-2:]), reduce(lambda x, y: x * y, sorted(nums)[:2]))
```

## ⚠Equivalent Value and Frequency

**Source**: [binarysearch | Learn Algorithms Together](https://binarysearch.com/problems/Equivalent-Value-and-Frequency)

**Description**:

> Given a list of integers nums, return whether there's an integer whose frequency in the list is same as its value.

> 

**Answer**:

```python
return len(list(filter(bool, (x == len(list(y)) for x, y in groupby(sorted(nums)))))) != 0
```
