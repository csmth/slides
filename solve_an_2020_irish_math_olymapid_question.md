# The question shown
- Given a, b, c > 0, Prove that
```math
(\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7} + (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7} + (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7} \geq 3
```
gain
- Readers can refer to LaTex-like formula reference here: https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions
![Alt the question in image](olympiad_irish_math_2020.jpg)

# An answer
- Divide both side by 3, and trying to apply AM >= GM inequality, it is sufficient to prove that:

```math
((\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7}  (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7}  (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7}) ^ \frac{1}{3} \geq 1
```
- Simplified it:

```math
(\frac{a}{b+c} + \frac{b}{c+a})  (\frac{b}{c+a} + \frac{c}{a+b}) (\frac{c}{a+b} + \frac{a}{b+c}) \geq (1 ^ 7) ^ 3 = 1
```

* $`\frac{a}{b+c} + \frac{b}{c+a}`$ is tricky part to handle. Want to prove that this is greater or equal to $` \frac{a+b}{\sqrt{(b+c)(c+a)}}`$:
** Test
