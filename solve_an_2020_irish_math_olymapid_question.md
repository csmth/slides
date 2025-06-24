# The question shown
- Given a, b, c > 0, Prove that
```math
(\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7} + (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7} + (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7} \geq 3
```
![Alt the question in image](olympiad_irish_math_2020.jpg)
- Refer to [LaTex-like formula markdown syntax here](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
- Refer to [AM-GM inequality](https://en.wikipedia.org/wiki/AM%E2%80%93GM_inequality). This question involves AM-GM inequality.

# An answer
- Divide both side by 3, and trying to apply AM-GM inequality, it is sufficient to prove that:

```math
((\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7}  (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7}  (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7}) ^ \frac{1}{3} \geq 1
```
```math
(\frac{a}{b+c} + \frac{b}{c+a})  (\frac{b}{c+a} + \frac{c}{a+b}) (\frac{c}{a+b} + \frac{a}{b+c}) \geq (1 ^ 3) ^ 7 = 1
```

## Tricky part $`\frac{a}{b+c} + \frac{b}{c+a}`$
- Let u, v, w be `a+b`, `b+c` and `c+a` respectively. They are all positive. That results in `a=(u-v+w)/2`, `b=(v-w+u)/2`, `c=(w-u+v)/2`.
- Formula (1) holds due to AM >= GM
```math
\frac{1}{2} ( \frac{v}{w} + \frac{w}{v}) \geq \sqrt{ (\frac{v}{w} \frac{w}{v}) } = 1 
```
- Formula (2) holds also due to AM >= GM
```math
\frac{1}{2} (\frac{u}{w} + \frac{u}{v}) \geq \frac{u}{\sqrt{vw}}
```
- Adding Formula (1) and (2) results is:

```math
\frac{1}{2} (\frac{v+u}{w}) + \frac{1}{2} (\frac{w+u}{v}) \geq 1 + \frac{u}{\sqrt{vw}}
```
```math
\frac{1}{2} (\frac{v+u}{w} -1) + \frac{1}{2} (\frac{w+u}{v} -1) = \frac{v+u-w}{w} + \frac{w+u-v}{v} \geq \frac{u}{\sqrt{vw}}
```
```math
\frac{b}{w} + \frac{a}{v} \geq \frac{u}{\sqrt{vw}} = \frac{a+b}{\sqrt{(b+c)(c+a)}}
```
- Similar cases to handle tricky part of $`(b/w) + (c/u)`$ and $`(c/u) + (a/v)`$

## Back to the question
- Return to the inequality to be proven:
```math
(\frac{a}{b+c} + \frac{b}{c+a})  (\frac{b}{c+a} + \frac{c}{a+b}) (\frac{c}{a+b} + \frac{a}{b+c}) \geq 1
```
- It is sufficient to prove that:
```math
(\frac{a+b}{\sqrt{(b+c)(c+a)}})  (\frac{b+c}{\sqrt{(c+a)(a+b)}})  (\frac{c+a}{\sqrt{(b+c)(a+b)}}) \geq 1
```

- But it is equal now. The denominator is:
```math
\sqrt{(b+c)(c+a)} \sqrt{(c+a)(a+b)} \sqrt{(b+c)(a+b)} = (a+b)(b+c)(c+a) 
```

## Summary
- The whole proof is:
```math
\frac{ (\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7} + (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7} + (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7} }{3}
\geq ((\frac{a}{b+c} + \frac{b}{c+a}) (\frac{b}{c+a} + \frac{c}{a+b}) (\frac{c}{a+b} + \frac{a}{b+c})) ^ \frac{1}{21}
\geq ((\frac{a+b}{\sqrt{(b+c)(c+a)}})  (\frac{b+c}{\sqrt{(c+a)(a+b)}}) (\frac{c+a}{\sqrt{(b+c)(a+b)}})) ^ \frac{1}{21}
```

- The number 7 in the question can be replaced by any positive number, as 1 to the power of anything is 1.
