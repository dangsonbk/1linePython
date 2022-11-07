## 1linePython

A collection of one-liner Python answers on some online code challenges.

The idea of this repository came when I challenged [shinez1997](https://github.com/shinez1997) to resolve code problems on [binarysearch.com](https://binarysearch.com/) with only one line of Python code. He is better than me in every aspect of coding, and this is only way I can beat him somehow.

## Rules

- The answer is on the same line with the `return`.
- No module is imported except defaults by code challenge platforms.
- Must not reach the TLE of the code challenge platform.
- Hacks, tricks, or whatever that fits in one line and pass the tests is accepted.

Example:

```python
# functools is imported by default
class Solution: # default by online judge
    def minAddToMakeValid(self, s: str) -> int:  # default by online judge
        # answer fit in one line
        return len(functools.reduce(lambda c1, c2: c2 if not c1 else c1[:-1] if c2==")" and c1[-1] == "(" else c1 + c2, s)) if s else len(s)
```

## Real life usage

- Just don't.
- When you hate your future self.
- When you hate your company, you are willing to leave, you want your product run but be unmaintainable.
- When the challenge is too simple to you, you want to make life complicate.

## Notes

- Many of the answers are not really 1-liner Python code, as they use functions from libraries.
- Many of the answers are not the best optimized answers. They just fit under the requirement of the problem's Execute Time Limit.
- Code challenge websites usually import some default Python libraries, but the list may vary between sites.

## Resources

- Found this interesting works of [finxter](https://github.com/finxter): [pythononeliners](https://pythononeliners.com/) [10 Elegant Python One-Liners That Fit in a Tweet](https://blog.finxter.com/10-python-one-liners/)

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
- [runarmod](https://github.com/runarmod)
