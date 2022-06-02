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

```python
return ''.join(str(x) for x, _ in groupby(s))
```


