# The question shown
- Given a, b, c > 0, Prove that
```math
(\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7} + (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7} + (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7} \geq 3
```

- Readers can refer to LaTex-like formula reference here: https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions
![Alt the question in image](olympiad_irish_math_2020.jpg)

# My answer
- Divide both side by 3, and trying to apply AM > GM inequality, it is sufficient to prove that:

```math
((\frac{a}{b+c} + \frac{b}{c+a}) ^ \frac{1}{7}  (\frac{b}{c+a} + \frac{c}{a+b}) ^ \frac{1}{7}  (\frac{c}{a+b} + \frac{a}{b+c}) ^ \frac{1}{7}) ^ \frac{1}{3} \geq 1
```
- Simplified it:

```math
(\frac{a}{b+c} + \frac{b}{c+a})  (\frac{b}{c+a} + \frac{c}{a+b}) (\frac{c}{a+b} + \frac{a}{b+c}) \geq (1 ^ 7) ^ 3 = 1
```

- I don't have a good way to solve it quick. Rewrite the inequality by brute force.
```math
(\frac{a(c+a) + b(b+c)}{(b+c)(c+a)})  (\frac{b(a+b) + c(c+a)}{(c+a)(a+b)} ) (\frac{c(b+c) +a(a+b)}{(a+b)(b+c)} ) \geq 1
```

-  All denominators are positive so I can rewrite this:
```math
(a(c+a) + b(b+c)) (b(a+b) + c(c+a)) (c(b+c) +a(a+b))  \geq (b+c)(c+a)(c+a)(a+b)(a+b)(b+c) = ((b+c)(c+a)(a+b)) ^ 2
```

- Brute force rewrite gain:
```math
 2abc(c+a)(a+b)(b+c) + aba(c+a)(a+b)(a+b) + acc(c+a)(c+a)(b+c) + aca(c+a)(c+a)(a+b) + bbc(b+c)(a+b)(b+c) + bba(b+c)(a+b)(a+b) + bcc(b+c)(c+a)c(b+c) \geq ((b+c)(c+a)(a+b)) ^ 2
```
