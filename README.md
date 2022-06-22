## 1linePython

Collection of one-liner Python answers on some online code challenges.

Idea of this repository came when I challenged [shinez1997](https://github.com/shinez1997) for resolving code problems on [binarysearch.com](https://binarysearch.com/) with only one line of Python code. He is better than me in every aspect of coding and this is only way I can beat him somehow.

## Rules
- Answer is on the same line with the `return`.
- No module imported except defaults by code challenge platforms.
- Must not reach TLE of code challenge platform.
- Hack, trick or whatever that fit in one line and pass the tests is accepted.

Example:
```python
# functools is imported by default
class Solution: # default by online judge
    def minAddToMakeValid(self, s: str) -> int:  # default by online judge
        # answer fit in one line
        return len(functools.reduce(lambda c1, c2: c2 if not c1 else c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2, s)) if s else len(s)
```

## Real life usages
- Just don't.
- When you hate your future self.
- When you hate your company, you are willing to leave, you want your product run but unmaintainable.

## Notes

- Many of the answers are not really 1-liner Python code, as they use functions from libraries.
- Many of the answers are not the best optimized answer. They just fit under the requirement of problem's Execute Time Limit.
- Code challenge websites usually imported some default Python libraries, but the list may vary between sites.

## Contribution

Please use this template if you want to contribute to this list:

---

## 🧩 Problem Title

**Source**: [Link](#)

**Description**:

> Description and example

**Answer**:

```python
# Code in Python
```

**Explanations**:

---

## Contributors:

- [dangsonbk](https://github.com/dangsonbk)
- [shinez1997](https://github.com/shinez1997)
- [RohitSgh](https://github.com/RohitSgh)
