## 🧩 Two Sum

**Source**: [Two Sum](https://leetcode.com/problems/two-sum/)

**Description**:

> Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.
> 
> You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.
> 
> You can return the answer in any order.

**Answer**:

```python
return [(i, nums[i+1:].index(target - nums[i]) + i + 1) for i in range(len(nums)) if target - nums[i] in nums[i+1:]][0]
```

## 🧩 Roman to Integer

**Source**: [Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

**Description**:

> Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.
> 
> **Symbol**       **Value**
> I             1
> V             5
> X             10
> L             50
> C             100
> D             500
> M             1000
> 
> For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.
> 
> Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:
> 
> - `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
> - `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
> - `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.
> 
> Given a roman numeral, convert it to an integer.

**Answer**:

```python
return sum(starmap(lambda x, y: x if x >= y else -x , pairwise([p for p in map(lambda c: {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}[c], s)]))) + {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}[s[-1]]
```

**Explanations**:

- First convert all characters to numbers.
- `pairwise()` and check: if a digit smaller than the next, negative it's value, else keep it's value.
- `sum()` the returned values.
- Add the last digit.

## 🧩 Binary Prefix Divisible By 5

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

## 🧩 Minimum Add to Make Parentheses Valid

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

## 🧩 Palindrome Number

**Source**: [Palindrome Number](https://leetcode.com/problems/palindrome-number/)

**Description**:

> Given an integer `x`, return `true` if `x` is palindrome integer.
> 
> An integer is a **palindrome** when it reads the same backward as forward.
> 
> - For example, `121` is a palindrome while `123` is not.

**Answer**:

```python
return str(x) == str(x)[::-1]
```

## 🧩 Remove Palindromic Subsequences

**Source**: [Remove Palindromic Subsequences](https://leetcode.com/problems/remove-palindromic-subsequences/)

**Description**:

> You are given a string `s` consisting **only** of letters '`a`' and '`b`'. In a single step you can remove one **palindromic subsequence** from `s`.
> 
> _Return the **minimum** number of steps to make the given string empty._
> 
> A string is a **subsequence** of a given string if it is generated by deleting some characters of a given string without changing its order. Note that a subsequence does **not** necessarily need to be contiguous.
> 
> A string is called **palindrome** if is one that reads the same backward as well as forward.

**Answer**:

```python
return 2 - (s == s[::-1]) - (s == "")
```

**Explanations**:

The problem is more of a brainteaser. Since, we can remove **palindromic subsequence**. Hence, 

- If `s` is empty, answer would be **0** since we need 0 steps to make the given string empty.
- If `s` is palindrome, answer would be **1** since we can remove the entire string, since entire string is palindromic subsequence.
- If `s` isn't palindrome, we can take all `a`'s as a subsequence. This will be palindromic subsequence, remove it. At next step, we can take all `b`'s as a subesequecne, this will be a palindromic subsequence, remove it. Hence, answer would be **2**

Thus, atmost we can have minimum as `2`, we can subtract `1` from it if `s` is a palindrome, can subtract another `1` if `s` is empty. Hence, the python one-liner! 

## 🧩 Plus One

**Source**: [Plus One](https://leetcode.com/problems/plus-one/)

**Description**:

> You are given a **large integer** represented as an integer array `digits`, where each `digits[i]` is the `ith` digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading `0`'s.
> 
> Increment the large integer by one and return *the resulting array of digits*.

**Answer**:

```python
return list(str(int(''.join(map(str, digits))) + 1))
```

**Explanations**:

- Convert list of numbers to number by join()

- +1 and returns the list of intergers.

## 🧩 Valid Palindrome

**Source**: [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/submissions/)

**Description**:

> A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.
> 
> Given a string `s`, return `true` *if it is a **palindrome**, or* `false` *otherwise*.

**Answer**:

```python
return reduce(lambda p, c: p+c if c.isalpha() or c.isnumeric() else p, ' ' + s).lower().strip() == reduce(lambda p, c: p+c if c.isalpha() or c.isnumeric() else p, ' ' + s).lower()[::-1].strip()
```

**Explanations**:

- I don't know why it's not TLE lmao.

## 🧩 Squares of a Sorted Array

**Source**: [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

**Description**:

> Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

**Answer**:

```python
return sorted(map(lambda n: n*n, nums))
```

## 🧩 Sqrt(x)

**Source**: [Sqrt(x)](https://leetcode.com/problems/sqrtx/)

**Description**:

> Given a non-negative integer `x`, compute and return *the square root of* `x`.
> 
> Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.
> 
> **Note:** You are not allowed to use any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5`.

**Answer**:

```python
return next((i for i in range(0, x) if i*i > x), 2) - 1 if x > 1 else x
```

**Explanations**:

Note that the requirement is: You are not allowed to use any built-in exponent function or operator, such as `pow(x, 0.5)` or `x ** 0.5`. Without this, the solution could be as easy as: `floor(sqrt(x))`

Solution is to find the first number i that i*i > x, then minus with 1.

- If x = 2, then next() returns default value of 2, 2 - 1 = 1
- Other cases: input 0 returns 0, input 1 returns 1

## 🧩 Single Number

**Source**: [Single Number](https://leetcode.com/problems/single-number/)

**Description**:

> Given a **non-empty** array of integers `nums`, every element appears *twice* except for one. Find that single one.
> 
> You must implement a solution with a linear runtime complexity and use only constant extra space.

**Answer 1**:

```python
return sum(set(nums)) * 2 - sum(nums)
```

**Explanation**: It's just simple mathematic approach.

**Answer 2**:

```python
return reduce(lambda p, n: p ^ n, nums)
```

**Explanation**: Base on this genius solution from [leetcode](https://leetcode.com/problems/single-number/discuss/1771771/Think-it-through-oror-Time%3A-O(n)-Space%3A-O(1)-oror-Python-Explained).

**Answer 3**:

```python
return collections.Counter(nums).most_common()[-1][0]
```

**Explanation**: Simply find the least common number.

## 🧩 Reverse Bits

**Source**: [Reverse Bits](https://leetcode.com/problems/reverse-bits/)

**Description**:

> Reverse bits of a given 32 bits unsigned integer.
> 
> **Note:**
> 
> - Note that in some languages, such as Java, there is no unsigned integer type. In this case, both input and output will be given as a signed integer type. They should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
> - In Java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 2** above, the input represents the signed integer `-3` and the output represents the signed integer `-1073741825`.

**Answer**:

```python
return int(bin(n)[2:][::-1].ljust(32, '0'), 2)
```

## 🧩 Count Prefixes of a Given String

**Source**: [Count Prefixes of a Given String](https://leetcode.com/problems/count-prefixes-of-a-given-string/)

**Description**:

> You are given a string array `words` and a string `s`, where `words[i]` and `s` comprise only of **lowercase English letters**.
> 
> Return *the **number of strings** in* `words` *that are a **prefix** of* `s`.
> 
> A **prefix** of a string is a substring that occurs at the beginning of the string. A **substring** is a contiguous sequence of characters within a string.

**Answer**:

```python
return len([w for w in words if w == s[:len(w)]])
```

## 🧩 Add Two Integers

**Source**: [Add Two Integers](https://leetcode.com/problems/add-two-integers/)

**Description**:

> Given two integers `num1` and `num2`, return *the **sum** of the two integers*.

**Answer**:

```python
return num1 + num2
```

## 🧩 Find Closest Number to Zero

**Source**: [Find Closest Number to Zero](https://leetcode.com/problems/find-closest-number-to-zero)

**Description**:

> Given an integer array `nums` of size `n`, return *the number with the value **closest** to* `0` *in* `nums`. If there are multiple answers, return *the number with the **largest** value*.

**Answer**:

```python
return reduce(lambda a, n: a if abs(a) < abs(n) else max(a, n) if abs(a) == abs(n) else n, nums)
```

## 🧩 Percentage of Letter in String

**Source**: [Percentage of Letter in String](https://leetcode.com/problems/percentage-of-letter-in-string)

**Description**:

> Given a string `s` and a character `letter`, return *the **percentage** of characters in* `s` *that equal* `letter` **rounded down** to the nearest whole percent.

**Answer**:

```python
return s.count(letter) * 100 // len(s)
```

## 🧩 Largest 3-Same-Digit Number in String

**Source**: [Largest 3-Same-Digit Number in String](https://leetcode.com/problems/largest-3-same-digit-number-in-string)

**Description**:

> You are given a string `num` representing a large integer. An integer is **good** if it meets the following conditions:
> 
> - It is a **substring** of `num` with length `3`.
> - It consists of only one unique digit.
> 
> Return *the **maximum good** integer as a **string** or an empty string* `""` *if no such integer exists*.
> 
> Note:
> 
> - A **substring** is a contiguous sequence of characters within a string.
> - There may be **leading zeroes** in `num` or a good integer.

**Answer 1**:

```python
return [triple for triple in ['999','888','777','666','555','444','333','222','111','000',''] if triple in num][0]
```

**Explanations**:

- Check if each triple in inputted `num`.
- The first triple that found is the largest, so get the [0]
- As `''` always in any string, if no triple found in `num`, `[''][0]` is returned.

**Answer 2**:

```python
return next((triple for triple in ['999','888','777','666','555','444','333','222','111','000'] if triple in num), '')
```

**Explanations**:

- Use `next()` to find the first triple.

- The triple list is in decreasing order, the first triple that found is the largest.

- If no triple found, `next()` returns default value of `''`

## 🧩 Thousand Separator

**Source**: [Thousand Separator](https://leetcode.com/problems/thousand-separator)

**Description**:

> Given an integer `n`, add a dot (".") as the thousands separator and return it in string format.

**Answer**:

```python
return '.'.join([str(n)[max(0, i-3):i] for i in range(len(str(n)), 0, -3)][::-1])
```

## 🧩 Shuffle String

**Source**: [Shuffle String](https://leetcode.com/problems/shuffle-string/)

**Description**:

> You are given a string `s` and an integer array `indices` of the **same length**. The string `s` will be shuffled such that the character at the `ith` position moves to `indices[i]` in the shuffled string.
> 
> Return *the shuffled string*.

**Answer**:

```python
return ''.join([s[indices.index(i)] for i in range(len(s))])
```

## 🧩 Concatenation of Array

**Source**: [Concatenation of Array](https://leetcode.com/problems/concatenation-of-array/)

**Description**:

> Given an integer array `nums` of length `n`, you want to create an array `ans` of length `2n` where `ans[i] == nums[i]` and `ans[i + n] == nums[i]` for `0 <= i < n` (**0-indexed**).
> 
> Specifically, `ans` is the **concatenation** of two `nums` arrays.
> 
> Return *the array* `ans`.

**Answer**:

```python
return nums*2
```

## 🧩 Build Array from Permutation

**Source**: [Build Array from Permutation](https://leetcode.com/problems/build-array-from-permutation/)

**Description**:

> Given a **zero-based permutation** `nums` (**0-indexed**), build an array `ans` of the **same length** where `ans[i] = nums[nums[i]]` for each `0 <= i < nums.length` and return it.
> 
> A **zero-based permutation** `nums` is an array of **distinct** integers from `0` to `nums.length - 1` (**inclusive**).

**Answer**:

```python
return [nums[nums[i]] for i in range(0, len(nums))]
```

## 🧩 Running Sum of 1d Array

**Source**: [Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array)

**Description**:

> Given an array `nums`. We define a running sum of an array as `runningSum[i] = sum(nums[0]…nums[i])`.
> 
> Return the running sum of `nums`.

**Answer**:

```python
return accumulate(nums)
# Using reduce
return reduce(lambda p, n: p + [p[-1] + n], [[0]] + nums)[1:]
# Using list comprehension with sum()
return [sum(nums[:i]) for i in range(1, len(nums) + 1)]
```

**Bonus**:

This [answer](https://leetcode.com/problems/running-sum-of-1d-array/discuss/841274/Python-3-Multiple-One-Liners/925943) is hilarious:

```python
class Solution:
    runningSum=accumulate
```

## 🧩 Final Value of Variable After Performing Operations

**Source**: [Final Value of Variable After Performing Operations](https://leetcode.com/problems/final-value-of-variable-after-performing-operations/)

**Description**:

> There is a programming language with only **four** operations and **one** variable `X`:
> 
> - `++X` and `X++` **increments** the value of the variable `X` by `1`.
> - `--X` and `X--` **decrements** the value of the variable `X` by `1`.
> 
> Initially, the value of `X` is `0`.
> 
> Given an array of strings `operations` containing a list of operations, return *the **final** value of* `X` *after performing all the operations*.

**Answer**:

```python
return sum([-1 if "--" in op else 1 for op in operations])
```

## 🧩 Richest Customer Wealth

**Source**: [Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/)

**Description**:

> You are given an `m x n` integer grid `accounts` where `accounts[i][j]` is the amount of money the `i​​​​​​​​​​​th​​​​` customer has in the `j​​​​​​​​​​​th`​​​​ bank. Return *the **wealth** that the richest customer has.*
> 
> A customer's **wealth** is the amount of money they have in all their bank accounts. The richest customer is the customer that has the maximum **wealth**.

**Answer**:

```python
return max(map(sum, accounts))
```

## 🧩 Defanging an IP Address

**Source**: [Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/)

**Description**:

> Given a valid (IPv4) IP `address`, return a defanged version of that IP address.
> 
> A *defanged IP address* replaces every period `"."` with `"[.]"`.

**Answer**:

```python
return address.replace(".", "[.]")
```

## 🧩 Maximum Number of Words Found in Sentences

**Source**: [Maximum Number of Words Found in Sentences](https://leetcode.com/problems/maximum-number-of-words-found-in-sentences/)

**Description**:

> A **sentence** is a list of **words** that are separated by a single space with no leading or trailing spaces.
> 
> You are given an array of strings `sentences`, where each `sentences[i]` represents a single **sentence**.
> 
> Return *the **maximum number of words** that appear in a single sentence*.

**Answer**:

```python
return max(map(len, map(lambda s: s.split(), sentences)))
```

## 🧩 Shuffle the Array

**Source**: [Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)

**Description**:

> Given the array `nums` consisting of `2n` elements in the form `[x1,x2,...,xn,y1,y2,...,yn]`.
> 
> *Return the array in the form* `[x1,y1,x2,y2,...,xn,yn]`.

**Answer**:

```python
return [n for a in zip(nums[:n], nums[n:]) for n in a]
# Using chain from itertools
return chain.from_iterable([a for a in zip(nums[:n], nums[n:])])
```

## 🧩 Minimum Sum of Four Digit Number After Splitting Digits

**Source**: [Minimum Sum of Four Digit Number After Splitting Digits](https://leetcode.com/problems/minimum-sum-of-four-digit-number-after-splitting-digits/)

**Description**:

> You are given a **positive** integer `num` consisting of exactly four digits. Split `num` into two new integers `new1` and `new2` by using the **digits** found in `num`. **Leading zeros** are allowed in `new1` and `new2`, and **all** the digits found in `num` must be used.
> 
> - For example, given `num = 2932`, you have the following digits: two `2`'s, one `9` and one `3`. Some of the possible pairs `[new1, new2]` are `[22, 93]`, `[23, 92]`, `[223, 9]` and `[2, 329]`.
> 
> Return *the **minimum** possible sum of* `new1` *and* `new2`.

**Answer**:

```python
return int(''.join(compress(sorted(str(num)), [1, 0, 1, 0]))) + int(''.join(compress(sorted(str(num)), [0, 1, 0, 1])))
```

**Explanations**:

You don't have to generate all possible combinations of 4 digits. Just sort the digits in decreasing order, the minimum sum always equal: `digit_0 * 10 + digit_2 + digit_1 * 10 + digit_3`

## 🧩 Number of Good Pairs

**Source**: [Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/)

**Description**:

> Given an array of integers `nums`, return *the number of **good pairs***.
> 
> A pair `(i, j)` is called *good* if `nums[i] == nums[j]` and `i` < `j`.
> 
> - `1 <= nums.length <= 100`
> - `1 <= nums[i] <= 100`

**Answer 1**:

```python
return reduce(lambda c, n: [c[0] + c[1].count(n), c[1] + [n]], [[0, []]] + nums)[0]
```

**Explanation**:

- Feed `[count, [appearances]]` to `nums` as start of reduce.

- Each step of `reduce`:
  
  - Check if number already appeared in previous steps. Count the appearances.
  
  - Remember the counted number.

**Answer 2:**

```python
return sum(k * (k - 1) / 2 for k in collections.Counter(A).values())
```

**Explanation:**

Credit to [lee215](https://leetcode.com/problems/number-of-good-pairs/discuss/731561/JavaC%2B%2BPython-Count), please upvote him.

## 🧩 Jewels and Stones

**Source**: [Jewels and Stones](https://leetcode.com/problems/jewels-and-stones/)

**Description**:

> You're given strings `jewels` representing the types of stones that are jewels, and `stones` representing the stones you have. Each character in `stones` is a type of stone you have. You want to know how many of the stones you have are also jewels.
> 
> Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.
> 
> - `1 <= jewels.length, stones.length <= 50`
> - `jewels` and `stones` consist of only English letters.
> - All the characters of `jewels` are **unique**.

**Answer**:

```python
return sum([1 for s in stones if s in jewels])
```

## 🧩 Kids With the Greatest Number of Candies

**Source**: [Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

**Description**:

> There are `n` kids with candies. You are given an integer array `candies`, where each `candies[i]` represents the number of candies the `ith` kid has, and an integer `extraCandies`, denoting the number of extra candies that you have.
> 
> Return *a boolean array* `result` *of length* `n`*, where* `result[i]` *is* `true` *if, after giving the* `ith` *kid all the* `extraCandies`*, they will have the **greatest** number of candies among all the kids**, or* `false` *otherwise*.
> 
> Note that **multiple** kids can have the **greatest** number of candies.
> 
> - `n == candies.length`
> - `2 <= n <= 100`
> - `1 <= candies[i] <= 100`
> - `1 <= extraCandies <= 50`

**Answer**:

```python
return [k + extraCandies >= max(candies) for k in candies]
```

## 🧩 Third Maximum Number

**Source**: [Third Maximum Number](https://leetcode.com/problems/third-maximum-number/)

**Description**:

> Given an integer array `nums`, return *the **third distinct maximum** number in this array. If the third maximum does not exist, return the **maximum** number*.
> 
> - `1 <= nums.length <= 104`
> - `-231 <= nums[i] <= 231 - 1`

**Answer**:

```python
return sorted(set(nums))[-3] if len(set(nums)) > 2 else max(nums)
```

**Explanation**:

Sort the list in increasing order then get the item with index -3.

As we does not count the number with same value, convert the list with `set()`

## 🧩 Reverse Words in a String III

**Source**: [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/)

**Description**:

> Given a string `s`, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Answer**:

```python
return ' '.join([w[::-1] for w in s.split()])
```

## 🧩 Minimum Time Visiting All Points

**Source**: [Minimum Time Visiting All Points](https://leetcode.com/problems/minimum-time-visiting-all-points/)

**Description**:

> On a 2D plane, there are `n` points with integer coordinates `points[i] = [xi, yi]`. Return *the **minimum time** in seconds to visit all the points in the order given by* `points`.
> 
> You can move according to these rules:
> 
> - In `1` second, you can either:
>   - move vertically by one unit,
>   - move horizontally by one unit, or
>   - move diagonally `sqrt(2)` units (in other words, move one unit vertically then one unit horizontally in `1` second).
> - You have to visit the points in the same order as they appear in the array.
> - You are allowed to pass through points that appear later in the order, but these do not count as visits.

**Answer**:

```python
return sum([max(abs(p[1][0] - p[0][0]), abs(p[1][1] - p[0][1])) for p in pairwise(points)])
```

**Explanation**:

- Number of moves between `(x0, y0)` and `(x1, y1)` equals number of moves between `(0, 0)` and `(abs(x1-x0), abs(y1-y0))`, call it `(delta_x, delta_y)`.
  
  Assumes that `delta_y` > `delta_x`, the best path is to start from `(0, 0)` to `(delta_x, delta_x)`, then move from `(delta_x, delta_x)` to `(delta_x, delta_y)`. The first path takes `delta_x` moves, second path takes `delta_y - delta_x` moves. The total number of moves is `delta_x + delta_y - delta_x = delta_y`
  
  Vice versa it takes `delta_x` moves if `delta_x` > `delta_y`

## 🧩 Maximum 69 Number

**Source**: [Maximum 69 Number](https://leetcode.com/problems/maximum-69-number/)

**Description**:

> You are given a positive integer `num` consisting only of digits `6` and `9`.
> 
> Return *the maximum number you can get by changing **at most** one digit (*`6` *becomes* `9`*, and* `9` *becomes* `6`*)*.

**Answer**:

```python
return int(str(num).replace('6', '9', 1))
```

## 🧩 Find First Palindromic String in the Array

**Source**: [Find First Palindromic String in the Array](https://leetcode.com/problems/find-first-palindromic-string-in-the-array/)

**Description**:

> Given an array of strings `words`, return *the first **palindromic** string in the array*. If there is no such string, return *an **empty string*** `""`.
> 
> A string is **palindromic** if it reads the same forward and backward.

**Answer**:

```python
return next((w for w in words if w == w[::-1]), '')
```

## 🧩 Number Of Rectangles That Can Form The Largest Square

**Source**: [Number Of Rectangles That Can Form The Largest Square](https://leetcode.com/problems/number-of-rectangles-that-can-form-the-largest-square/)

**Description**:

> You are given an array `rectangles` where `rectangles[i] = [li, wi]` represents the `ith` rectangle of length `li` and width `wi`.
> 
> You can cut the `ith` rectangle to form a square with a side length of `k` if both `k <= li` and `k <= wi`. For example, if you have a rectangle `[4,6]`, you can cut it to get a square with a side length of at most `4`.
> 
> Let `maxLen` be the side length of the **largest** square you can obtain from any of the given rectangles.
> 
> Return *the **number** of rectangles that can make a square with a side length of* `maxLen`.

**Answer**:

```python
return [min(l) for l in rectangles].count(max([min(l) for l in rectangles]))
```

**Notice**: What a shame to write code like this. I'm sorry.

**Answer 2**:

```python
return sorted(Counter([min(l) for l in rectangles]).most_common())[-1][1]
```

**Explanation**: Sort the return of `most_common()`, get count value of largest rectangles.

## 🧩 Find the Highest Altitude

**Source**: [Find the Highest Altitude](https://leetcode.com/problems/find-the-highest-altitude/)

**Description**:

> There is a biker going on a road trip. The road trip consists of `n + 1` points at different altitudes. The biker starts his trip on point `0` with altitude equal `0`.
> 
> You are given an integer array `gain` of length `n` where `gain[i]` is the **net gain in altitude** between points `i`​​​​​​ and `i + 1` for all (`0 <= i < n)`. Return *the **highest altitude** of a point.*

**Answer**:

```python
return max(accumulate([0] + gain))
```

## 🧩 Implement strStr()

**Source**: [Implement strStr()](https://leetcode.com/problems/implement-strstr/)

**Description**:

> Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).
> 
> Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.
> 
> **Clarification:**
> 
> What should we return when `needle` is an empty string? This is a great question to ask during an interview.
> 
> For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's [strstr()](http://www.cplusplus.com/reference/cstring/strstr/) and Java's [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)).

**Answer**:

```python
return haystack.find(needle)
```

**Explanations**:
Edge cases already taken care of.

## 🧩 Contains Duplicate

**Source**: [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

**Description**:

> Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Answer**:

```python
return len(set(nums)) != len(nums)
```

**Explanations**:
`set()` deletes all duplicates. Therefore, if its length is different than the original list, at least 1 element is repeated.

## 🧩 Number of 1 Bits

**Source**: [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

**Description**:

> Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).
> 
> Note:
> 
>    Note that in some languages, such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type. It should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
>    In Java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two%27s_complement). Therefore, in **Example 3**, the input represents the signed integer. `-3`.

**Answer**:

```python
return n.bit_count()
```

**Explanations**:
Python 3.10 introduced `int.bit_count()`.

## 🧩 Valid Anagram

**Source**: [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

**Description**:

> Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.
> 
> An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Answer**:

```python
return collections.Counter(s) == collections.Counter(t)
```

**Explanations**:
`collections.Counter()` [is a dict subclass for counting hashable objects](https://docs.python.org/3/library/collections.html#collections.Counter). Simply checking if they are equal does the trick.

## 🧩 Missing Number

**Source**: [Missing Number](https://leetcode.com/problems/missing-number/)

**Description**:

> Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return *the only number in the range that is missing from the array*.

**Answer**:

```python
return sum(range(1, len(nums) + 1)) - sum(nums)
```

**Explanations**:
Taking the difference between the sum of the numbers, and the whole range, will reveal the missing number.

## 🧩 To Lower Case

**Source**: [To Lower Case](https://leetcode.com/problems/to-lower-case/)

**Description**:

> Given a string `s`, return *the string after replacing every uppercase letter with the same lowercase letter*.

**Answer(s)**:

```python
return str.lower()
return "".join(chr(ord(c) + 32) if "A" <= c <= "Z" else c for c in str)
return "".join(chr(ord(c) + 32) if 65 <= ord(c) <= 90 else c for c in str)
return ''.join(chr(ord(c) + 32*('A' <= c <= 'Z')) for c in s)
```

**Explanation**: [Python short 1 line ASCII & string method solutions](https://leetcode.com/problems/to-lower-case/discuss/148813/Python-short-1-line-ASCII-and-string-method-solutions)

## 🧩 X of a Kind in a Deck of Cards

**Source**: [X of a Kind in a Deck of Cards](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards)

**Description**:

> In a deck of cards, each card has an integer written on it.
> 
> Return `true` if and only if you can choose `X >= 2` such that it is possible to split the entire deck into 1 or more groups of cards, where:
> 
> - Each group has exactly `X` cards.
> - All the cards in each group have the same integer.

**Answer**:

```python
return reduce(gcd, Counter(deck).values()) > 1
```

## 🧩 Number of Different Integers in a String

**Source**: [Number of Different Integers in a String](https://leetcode.com/problems/number-of-different-integers-in-a-string/)

**Description**:

> You are given a string `word` that consists of digits and lowercase English letters.
> 
> You will replace every non-digit character with a space. For example, `"a123bc34d8ef34"` will become `" 123  34 8  34"`. Notice that you are left with some integers that are separated by at least one space: `"123"`, `"34"`, `"8"`, and `"34"`.
> 
> Return *the number of **different** integers after performing the replacement operations on* `word`.
> 
> Two integers are considered different if their decimal representations **without any leading zeros** are different.

**Answer**:

```python
return len(set([int(''.join(g[1])) for g in groupby(word, lambda c: c.isnumeric()) if g[0]]))
```

## 🧩 Check If N and Its Double Exist

**Source**: [Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/)

**Description**:

> Given an array `arr` of integers, check if there exists two integers `N` and `M` such that `N` is the double of `M` ( i.e. `N = 2 * M`).
> 
> More formally check if there exists two indices `i` and `j` such that :
> 
> - `i != j`
> - `0 <= i, j < arr.length`
> - `arr[i] == 2 * arr[j]`

**Answer**:

```python
return next((True for i in arr if i*2 in arr and i), False) if arr.count(0) < 2 else True
```

## 🧩 Search Insert Position

**Source**: [Search Insert Position](https://leetcode.com/problems/search-insert-position/)

**Description**:

> Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
> 
> You must write an algorithm with `O(log n)` runtime complexity.

**Answer**:

```python
return next((e[0]+1 for e in enumerate(pairwise(nums)) if target >= e[1][0] and target <= e[1][1]), len(nums)) if target > nums[0] else 0
```

**Answer 2**:

```python
return bisect.bisect_left(nums, target)
```

**Explanation**: [[Python] 2 Solutions: Oneliner and Classical BS explained](https://leetcode.com/problems/search-insert-position/discuss/679918/Python-2-Solutions%3A-Oneliner-and-Classical-BS-explained)

## 🧩 Length of Last Word

**Source**: [Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

**Description**:

> Given a string `s` consisting of words and spaces, return *the length of the **last** word in the string.*
> 
> A **word** is a maximal substring consisting of non-space characters only.

**Answer**:

```python
return len(s.split()[-1])
```

## 🧩 Number of Segments in a String

**Source**: [Number of Segments in a String](https://leetcode.com/problems/number-of-segments-in-a-string/)

**Description**:

> Given a string `s`, return *the number of segments in the string*.
> 
> A **segment** is defined to be a contiguous sequence of **non-space characters**.

**Answer**:

```python
return len(s.split())
```

## 🧩 Power of Four

**Source**: [Power of Four](https://leetcode.com/problems/power-of-four/)

**Description**:

> Given an integer `n`, return *`true` if it is a power of four. Otherwise, return `false`*.
> 
> An integer `n` is a power of four, if there exists an integer `x` such that `n == 4x`.

**Answer**:

```python
return n in (1, 4, 16, 64, 256, 1024, 4096, 16384, 65536, 262144, 1048576, 4194304, 16777216, 67108864, 268435456, 1073741824)
```

**Answer 2**:

```python
return (num > 0) && ((num & (num - 1)) == 0) && ((num & 0x55555555) == num);
```

**Explanation**:

- [O(1) one-line solution without loops](https://leetcode.com/problems/power-of-four/discuss/80456/O(1)-one-line-solution-without-loops)

- [Python one line solution with explanations](https://leetcode.com/problems/power-of-four/discuss/80461/Python-one-line-solution-with-explanations)

- [Python O(1) oneliner solution, explained](https://leetcode.com/problems/power-of-four/discuss/772269/Python-O(1)-oneliner-solution-explained)

## 🧩 Power of Three

**Source**: [Power of Three](https://leetcode.com/problems/power-of-three/)

**Description**:

> Given an integer `n`, return *`true` if it is a power of three. Otherwise, return `false`*.
> 
> An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.
> 
> **Constraints:**
> 
> - `-2**31 <= n <= 2**31 - 1`

**Answer**:

```python
return n in (1, 3, 9, 27, 81, 243, 729, 2187, 6561, 19683, 59049, 177147, 531441, 1594323, 4782969, 14348907, 43046721, 129140163, 387420489, 1162261467)
```

**Answer 2:**

```python
return n > 0 and pow(3, 19) % n == 0
```

**Explanation:**

- With constraints: `-2**31 <= n <= 2**31 - 1` then `pow(3, 19)` is enough.

## 🧩 Find Smallest Letter Greater Than Target

**Source**: [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/)

**Description**:

> Given a characters array `letters` that is sorted in **non-decreasing** order and a character `target`, return *the smallest character in the array that is larger than* `target`.
> 
> Note that the letters wrap around.
> 
> - For example, if `target == 'z'` and `letters == ['a', 'b']`, the answer is `'a'`.

**Answer**:

```python
return next((c for c in letters if c > target), letters[0])
```

## 🧩 Subtract the Product and Sum of Digits of an Integer

**Source**: [Subtract the Product and Sum of Digits of an Integer](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

**Description**:

> Given an integer number `n`, return the difference between the product of its digits and the sum of its digits.

**Answer**:

```python
return reduce(lambda a, b: a - b, reduce(lambda p, n: [p[0]*n, p[1] + n], [[1, 0]] + list(map(int, str(n)))))
```

**Explanation:**

- Seed the `reduce()` with `[1, 0]`which is `[mul, add]` results corresponding.

- The second `reduce()` is to substract two values.

**Answer 2**

```python
return eval('*'.join(str(n))) - eval('+'.join(str(n)))
```

**Explanation**:

Please upvote the author if you like it: [Python one-liner using eval function (28ms, 14MB)](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/discuss/812200/Python-one-liner-using-eval-function-(28ms-14MB)) 

## 🧩 Fibonacci Number

**Source**: [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

**Description**:

> The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,
> 
> F(0) = 0, F(1) = 1
> F(n) = F(n - 1) + F(n - 2), for n > 1.
> 
> Given `n`, calculate `F(n)`.

**Answer**:

```python
return reduce(lambda p, _: [p[1], p[0] + p[1]], range(n), [0, 1])[0]
```

## 🧩 Pascal's Triangle

**Source**: [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle)

**Description**:

> Given an integer `numRows`, return the first numRows of **Pascal's triangle**.
> 
> In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

**Answer**:

```python
return accumulate([[1]] * numRows, lambda n, _: list(map(sum, pairwise([0] + n + [0]))))
```

## 🧩 Pascal's Triangle II

**Source**: [Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)

**Description**:

> Given an integer `rowIndex`, return the `rowIndexth` (**0-indexed**) row of the **Pascal's triangle**.
> 
> In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

**Answer**:

```python
return list(accumulate([[1]] * (rowIndex + 1), lambda n, _: list(map(sum, pairwise([0] + n + [0])))))[-1]
```

## 🧩 Find Triangular Sum of an Array

**Source**: [Find Triangular Sum of an Array](https://leetcode.com/problems/find-triangular-sum-of-an-array/)

**Description**:

> You are given a **0-indexed** integer array `nums`, where `nums[i]` is a digit between `0` and `9` (**inclusive**).
> 
> The **triangular sum** of `nums` is the value of the only element present in `nums` after the following process terminates:
> 
> 1. Let `nums` comprise of `n` elements. If `n == 1`, **end** the process. Otherwise, **create** a new **0-indexed** integer array `newNums` of length `n - 1`.
> 2. For each index `i`, where `0 <= i < n - 1`, **assign** the value of `newNums[i]` as `(nums[i] + nums[i+1]) % 10`, where `%` denotes modulo operator.
> 3. **Replace** the array `nums` with `newNums`.
> 4. **Repeat** the entire process starting from step 1.
> 
> Return *the triangular sum of* `nums`.

**Answer**:

```python
return reduce(lambda p, n: list(map(lambda x: sum(x) % 10, pairwise(p))), [1] * (len(nums) - 1), nums)[0]
```

## 🧩 Convert Sorted Array to Binary Search Tree

**Source**: [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree)

**Description**:

> Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.
> A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

**Answer**: Cre: [congbk92](https://github.com/congbk92)

```python
return TreeNode(nums[len(nums)//2], self.sortedArrayToBST(nums[:len(nums)//2]), self.sortedArrayToBST(nums[len(nums)//2+1:])) if len(nums) > 0 else None
```

## 🧩 Invert Binary Tree

**Source**: [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree)

**Description**:

> Given the root of a binary tree, invert the tree, and return its root.

**Answer**: Cre: [congbk92](https://github.com/congbk92)

```python
return TreeNode(root.val, self.invertTree(root.right), self.invertTree(root.left)) if root else None
```

## 🧩 First Unique Character in a String

**Source**: [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string)

**Description**:

> Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

**Answer**:

```python
return s.find(next((s for s, c in Counter(s).items() if c == 1), "#"))
```

## 🧩 Unique Morse Code Words

**Source**: [Unique Morse Code Words](https://leetcode.com/problems/unique-morse-code-words)

**Description**:

> International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows:
> 
> 'a' maps to ".-",
> 'b' maps to "-...",
> 'c' maps to "-.-.", and so on.
> For convenience, the full table for the 26 letters of the English alphabet is given below:
> `[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]`
> 
> Given an array of strings words where each word can be written as a concatenation of the Morse code of each letter.
> 
> For example, "cab" can be written as `"-.-..--..."`, which is the concatenation of `"-.-."`, `".-"`, and `"-..."`. We will call such a concatenation the transformation of a > word.
> Return the number of different transformations among all words we have.

**Answer**:

```python
return len(set([reduce(lambda p, c: p + [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."][ord(c)-97], w, "") for w in words]))
```

## 🧩 Ransom Note

**Source**: [Ransom Note](https://leetcode.com/problems/ransom-note/)

**Description**:

> Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.
> Each letter in magazine can only be used once in ransomNote.

**Answer**:

```python
return not Counter(ransomNote) - Counter(magazine)
```

## 🧩 Longest Common Prefix

**Source**: [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

**Description**:

> Write a function to find the longest common prefix string amongst an array of strings.
> 
> If there is no common prefix, return an empty string `""`.

**Answer**:

```python
return "".join(map(lambda n: n.pop(), takewhile(lambda p: len(p) == 1, map(set, zip(*strs)))))
```

## 🧩 Is Subsequence

**Source**: [Is Subsequence](https://leetcode.com/problems/is-subsequence/submissions/)

**Description**:

> Given two strings `s` and `t`, return `true` *if* `s` *is a **subsequence** of* `t`*, or* `false` *otherwise*.
> 
> A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

**Answer**:

```python
return reduce(lambda p, n: p[1:] if p and p[0] == n else p, t, s) == ''
```

## 🧩 Find Center of Star Graph

**Source**: [Find Center of Star Graph](https://leetcode.com/problems/find-center-of-star-graph/submissions/)

**Description**:

> There is an undirected **star** graph consisting of `n` nodes labeled from `1` to `n`. A star graph is a graph where there is one **center** node and **exactly** `n - 1` edges that connect the center node with every other node.
> 
> You are given a 2D integer array `edges` where each `edges[i] = [ui, vi]` indicates that there is an edge between the nodes `ui` and `vi`. Return the center of the given star graph.

**Answer**:

```python
return set.intersection(*map(set, edges)).pop()
```

## 🧩 Sorting the Sentence

**Source**: [Sorting the Sentence](https://leetcode.com/problems/sorting-the-sentence/)

**Description**:

> A **sentence** is a list of words that are separated by a single space with no leading or trailing spaces. Each word consists of lowercase and uppercase English letters.
> 
> A sentence can be **shuffled** by appending the **1-indexed word position** to each word then rearranging the words in the sentence.
> 
> - For example, the sentence `"This is a sentence"` can be shuffled as `"sentence4 a3 is2 This1"` or `"is2 sentence4 This1 a3"`.
> 
> Given a **shuffled sentence** `s` containing no more than `9` words, reconstruct and return *the original sentence*.

**Answer**:

```python
return " ".join(map(lambda w: w[:-1], sorted(s.split(), key=lambda w: w[-1])))
```

## 🧩 Root Equals Sum of Children

**Source**: [Root Equals Sum of Children](https://leetcode.com/problems/root-equals-sum-of-children/)

**Description**:

> You are given the `root` of a **binary tree** that consists of exactly `3` nodes: the root, its left child, and its right child.
> 
> Return `true` *if the value of the root is equal to the **sum** of the values of its two children, or* `false` *otherwise*.

**Answer**:

```python
return root.val == sum((root.left.val, root.right.val))
```

## 🧩 Partitioning Into Minimum Number Of Deci-Binary Numbers

**Source**: [Partitioning Into Minimum Number Of Deci-Binary Numbers](https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/)

**Description**:

> A decimal number is called **deci-binary** if each of its digits is either `0` or `1` without any leading zeros. For example, `101` and `1100` are **deci-binary**, while `112` and `3001` are not.
> 
> Given a string `n` that represents a positive decimal integer, return *the **minimum** number of positive **deci-binary** numbers needed so that they sum up to* `n`*.*

**Answer**:

```python
return int(max(n))
```

## 🧩 How Many Numbers Are Smaller Than the Current Number

**Source**: [How Many Numbers Are Smaller Than the Current Number](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

**Description**:

> Given the array `nums`, for each `nums[i]` find out how many numbers in the array are smaller than it. That is, for each `nums[i]` you have to count the number of valid `j's` such that `j != i` **and** `nums[j] < nums[i]`.
> 
> Return the answer in an array.

**Answer**:

```python
return [len(list(filter(lambda p: p < n, nums))) for n in nums]
```

## 🧩 Goal Parser Interpretation

**Source**: [Goal Parser Interpretation](https://leetcode.com/problems/goal-parser-interpretation/)

**Description**:

> You own a **Goal Parser** that can interpret a string `command`. The `command` consists of an alphabet of `"G"`, `"()"` and/or `"(al)"` in some order. The Goal Parser will interpret `"G"` as the string `"G"`, `"()"` as the string `"o"`, and `"(al)"` as the string `"al"`. The interpreted strings are then concatenated in the original order.
> 
> Given the string `command`, return *the **Goal Parser**'s interpretation of* `command`.

**Answer**:

```python
return command.replace("(al)", "al").replace("()", "o")
```

## 🧩 Check If Two String Arrays are Equivalent

**Source**: [Check If Two String Arrays are Equivalent](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/)

**Description**:

> Given two string arrays `word1` and `word2`, return `true` *if the two arrays **represent** the same string, and* `false` *otherwise.*
> 
> A string is **represented** by an array if the array elements concatenated **in order** forms the string.
> 
> **Example:**
> 
> **Input:** word1 = ["a", "cb"], word2 = ["ab", "c"]
> **Output:** false
> 
> **Example:**
> 
> **Input:** word1  = ["abc", "d", "defg"], word2 = ["abcddefg"]
> **Output:** true

**Answer**:

```python
return "".join(word1) == "".join(word2) 
```

## 🧩 Truncate Sentence

**Source**: [Truncate Sentence](https://leetcode.com/problems/truncate-sentence/)

**Description**:

> A **sentence** is a list of words that are separated by a single space with no leading or trailing spaces. Each of the words consists of **only** uppercase and lowercase English letters (no punctuation).
> 
> - For example, `"Hello World"`, `"HELLO"`, and `"hello world hello world"` are all sentences.
> 
> You are given a sentence `s`​​​​​​ and an integer `k`​​​​​​. You want to **truncate** `s`​​​​​​ such that it contains only the **first** `k`​​​​​​ words. Return `s`​​​​*​​ after **truncating** it.*
> 
> **Example 1:**
> 
> **Input:** s = "Hello how are you Contestant", k = 4
> **Output:** "Hello how are you"
> **Explanation:**
> The words in s are ["Hello", "how" "are", "you", "Contestant"].
> The first 4 words are ["Hello", "how", "are", "you"].
> Hence, you should return "Hello how are you".

**Answer**:

```python
return " ".join(s.split()[:k])
```

## 🧩 Flipping an Image

**Source**: [Flipping an Image](https://leetcode.com/problems/flipping-an-image/)

**Description**:

> Given an `n x n` binary matrix `image`, flip the image **horizontally**, then invert it, and return *the resulting image*.
> 
> To flip an image horizontally means that each row of the image is reversed.
> 
> - For example, flipping `[1,1,0]` horizontally results in `[0,1,1]`.
> 
> To invert an image means that each `0` is replaced by `1`, and each `1` is replaced by `0`.
> 
> - For example, inverting `[0,1,1]` results in `[1,0,0]`.
> 
> **Example 1:**
> 
> **Input:** image = [[1,1,0],[1,0,1],[0,0,0]]
> **Output:** [[1,0,0],[0,1,0],[1,1,1]]
> **Explanation:** First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
> Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]

**Answer**:

```python
return map(lambda r: list(map(lambda n: n^1, r))[::-1], image)
```

## 🧩 First Letter to Appear Twice

**Source**: [First Letter to Appear Twice](https://leetcode.com/problems/first-letter-to-appear-twice/)

**Description**:

> Given a string s consisting of lowercase English letters, return the first letter to appear twice.
> 
> Note:
> 
> A letter a appears twice before another letter b if the second occurrence of a is before the second occurrence of b.
> `s` will contain at least one letter that appears twice.

**Answer**:

```python
return next((c[1] for c in enumerate(s) if c[1] in s[:c[0]]), "")
```

## 🧩 Make Array Zero by Subtracting Equal Amounts

**Source**: [Make Array Zero by Subtracting Equal Amounts](https://leetcode.com/problems/make-array-zero-by-subtracting-equal-amounts/)

**Description**:

> You are given a non-negative integer array nums. In one operation, you must:

> Choose a positive integer x such that x is less than or equal to the smallest non-zero element in nums.
> Subtract x from every positive element in nums.
> Return the minimum number of operations to make every element in nums equal to 0.

> Example 1:

> Input: nums = [1,5,0,3,5]
> Output: 3
> Explanation:
> In the first operation, choose x = 1. Now, nums = [0,4,0,2,4].
> In the second operation, choose x = 2. Now, nums = [0,2,0,0,2].
> In the third operation, choose x = 2. Now, nums = [0,0,0,0,0].

**Answer**:

```python
return len(set(nums) - {0})
```

## 🧩 Merge Similar Items

**Source**: [Merge Similar Items](https://leetcode.com/problems/merge-similar-items/)

**Description**:

> You are given two 2D integer arrays, `items1` and `items2`, representing two sets of items. Each array `items` has the following properties:
> 
> - `items[i] = [valuei, weighti]` where `valuei` represents the **value** and `weighti` represents the **weight** of the `ith` item.
> - The value of each item in `items` is **unique**.
> 
> Return *a 2D integer array* `ret` *where* `ret[i] = [valuei, weighti]`*,* *with* `weighti` *being the **sum of weights** of all items with value* `valuei`.
> 
> **Note:** `ret` should be returned in **ascending** order by value.
> 
> **Example:**
> 
> **Input:** items1 = [[1,1],[4,5],[3,8]], items2 = [[3,1],[1,5]]
> **Output:** [[1,6],[3,9],[4,5]]
> **Explanation:** 
> The item with value = 1 occurs in items1 with weight = 1 and in items2 with weight = 5, total weight = 1 + 5 = 6.
> The item with value = 3 occurs in items1 with weight = 8 and in items2 with weight = 1, total weight = 8 + 1 = 9.
> The item with value = 4 occurs in items1 with weight = 5, total weight = 5.  
> Therefore, we return [[1,6],[3,9],[4,5]].

**Answer**:

```python
return sorted((Counter(dict(items1)) + Counter(dict(items2))).items())
```

## 🧩 Number of Arithmetic Triplets

**Source**: [Number of Arithmetic Triplets](https://leetcode.com/problems/number-of-arithmetic-triplets/)

**Description**:

> You are given a **0-indexed**, **strictly increasing** integer array `nums` and a positive integer `diff`. A triplet `(i, j, k)` is an **arithmetic triplet** if the following conditions are met:
> 
> - `i < j < k`,
> - `nums[j] - nums[i] == diff`, and
> - `nums[k] - nums[j] == diff`.
> 
> Return *the number of unique **arithmetic triplets**.*

**Answer**:

```python
return len([i for i in nums if i + diff in nums and i + 2*diff in nums])
```

## 🧩 Check Distances Between Same Letters

**Source**: [Check Distances Between Same Letters](https://leetcode.com/problems/check-distances-between-same-letters/)

**Description**:

> You are given a **0-indexed** string `s` consisting of only lowercase English letters, where each letter in `s` appears **exactly** **twice**. You are also given a **0-indexed** integer array `distance` of length `26`.
> 
> Each letter in the alphabet is numbered from `0` to `25` (i.e. `'a' -> 0`, `'b' -> 1`, `'c' -> 2`, ... , `'z' -> 25`).
> 
> In a **well-spaced** string, the number of letters between the two occurrences of the `ith` letter is `distance[i]`. If the `ith` letter does not appear in `s`, then `distance[i]` can be **ignored**.
> 
> Return `true` *if* `s` *is a **well-spaced** string, otherwise return* `false`.
> 
> **Example 1:**
> 
> **Input:** s = "abaccb", distance = [1,3,0,5,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]
> **Output:** true
> **Explanation:**
> 
> - 'a' appears at indices 0 and 2 so it satisfies distance[0] = 1.
> - 'b' appears at indices 1 and 5 so it satisfies distance[1] = 3.
> - 'c' appears at indices 3 and 4 so it satisfies distance[2] = 0.
>   Note that distance[3] = 5, but since 'd' does not appear in s, it can be ignored.
>   Return true because s is a well-spaced string.

**Answer**:

```python
return all((len(s) - s[::-1].index(c) - s.index(c) - 2 == distance[ord(c)-ord("a")]) for c in set(s))
```

**Explanation:**

- Index of second appearance of character, as `index()` only returns the first appearance, calculate the index of second appearance by reverse the string: `len(s) - s[::-1].index(c) - 1`
- Index of first appearance of character: `s.index(c)`
- Distance between appearances: `second - first - 1` = `len(s) - s[::-1].index(c) - 1 - s.index(c) - 1` = `len(s) - s[::-1].index(c) - s.index(c) - 2`
- Compare with provided distance `distance[ord(c)-ord("a")]`
- Do it with all characters c in s. `for c in set(s)`

## 🧩 Find Subarrays With Equal Sum

**Source**: [Find Subarrays With Equal Sum](https://leetcode.com/problems/find-subarrays-with-equal-sum/)

**Description**:

> Given a **0-indexed** integer array `nums`, determine whether there exist **two** subarrays of length `2` with **equal** sum. Note that the two subarrays must begin at **different** indices.
> 
> Return `true` *if these subarrays exist, and* `false` *otherwise.*
> 
> A **subarray** is a contiguous non-empty sequence of elements within an array.
> 
> **Example 1:**
> 
> **Input:** nums = [4,2,4]
> **Output:** true
> **Explanation:** The subarrays with elements [4,2] and [2,4] have the same sum of 6.

**Answer**:

```python
return Counter(map(sum, pairwise(nums))).most_common(1)[0][1] >= 2
```

**Explanation:**

- `itertools.pairwise(nums)` returns all subarrays with length 2. `pairwise('ABCDEFG') --> AB BC CD DE EF FG`
- Use `map(sum, pairwise(nums))` to sum all the subarrays.
- Use `Counter.most_common()` to find if there are subarrays with same `sum()`.

## 🧩 Find the Difference

**Source**: [Find the Difference](https://leetcode.com/problems/find-the-difference/)

**Description**:

> You are given two strings s and t.
> 
> String t is generated by random shuffling string s and then add one more letter at a random position.
> 
> Return the letter that was added to t.
> 
> > Example 1:
> > Input: s = "abcd", t = "abcde"
> > Output: "e"
> Explanation: 'e' is the letter that was added.

**Answer**:

```python
return (Counter(t) - Counter(s)).most_common()[0][0]
```

## 🧩 Add Digits

**Source**: [ Add Digits](https://leetcode.com/problems/add-digits/)

**Description**:

> Given an integer num, repeatedly add all its digits until the result has only one digit, and return it.
> 
> Example 1:
> Input: num = 38
> Output: 2
> Explanation: The process is
> 38 --> 3 + 8 --> 11
> 11 --> 1 + 1 --> 2 
> Since 2 has only one digit, return it.

**Answer**:

```python
return (num - 1) % 9 + 1 if num else 0
```

## 🧩 Toeplitz Matrix

**Source**: [Toeplitz Matrix](https://leetcode.com/problems/toeplitz-matrix/)

**Description**:

> Given an m x n matrix, return true if the matrix is Toeplitz. Otherwise, return false.
> A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same elements.

**Answer**:

```python
return all(r1[:-1] == r2[1:] for r1, r2 in zip(matrix, matrix[1:]))
```
