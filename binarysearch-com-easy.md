## ## Demo

**Source**:

**Description**:

> Description and example

**Answer**:

```python
#
```

**Explaination**:

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

## ## Run-Length Encoding

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
