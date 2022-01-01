---
layout: post
title: Prefix Sum Polynomial
---

Consider the \\(n\\) degree polynomial \\(P(x) = \sum_{i=0}^n p_ix^i\\). I call the polynomial \\(Q(x)\\) it's "prefix sum polynomial" if it satisfies the following condition:

$$Q(x) = \sum_{y=0}^x P(y)$$

Essentially, \\(Q(x)\\) is a prefix sum on the values of \\(P(x)\\). So,

$$
\begin{align}
Q(x) &= \sum_{y=0}^x P(y) \\
     &= \sum_{y=0}^x \sum_{i=0}^n p_i y^i \\
     &= \sum_{i=0}^n p_i \sum_{y=0}^x y^i
\end{align}
$$

Now, all we need is a formula for the prefix sum of \(y^i\). This is given by [Faulhaber's Formula](https://en.wikipedia.org/wiki/Faulhaber%27s_formula):

$$
\sum_{y=0}^x y^i = \frac{1}{i+1} \sum_{j=0}^i \binom{i+1}{j} B_j x^{i+1-j}
$$

where \\(B_j\\) is the \\(j\\)th [Bernoulli number](https://en.wikipedia.org/wiki/Bernoulli_number). The formula only applies for positive values of \\(i\\), so we have to handle \\([x^0]P(x)\\) separately. Moreover, we can tell from this formula that the degree of \\(Q(x)\\) will be \\(n+1\\).

Just using the formula above is enough to find \\(Q(x)\\) in \\(O(n^2)\\), but let us go further. From what we know so far, the coefficients of \\(Q(x)\\) would be:

$$
\begin{align}
[x^i]Q(x) &= \sum_{j=i-1}^n \frac{p_j}{j+1} B_{j+1-i} \binom{j+1}{j+1-i} \\
&= \sum_{j=i-1}^n \frac{p_j}{j+1} B_{j+1-i} \frac{(j+1)!}{i! \cdot (j+1-i)!} \\
&= \frac{1}{i!} \sum_{j=i-1}^n (p_j j!) \cdot \frac{B_{j+1-i}}{(j+1-i)!} \\
\end{align}
$$

This looks suspiciously like a convolution. Let us define \\(A(x)\\) and \\(B(x)\\) as:

$$
A(x) = \sum_{i=0}^n \frac{B_{n-i}}{(n-i)!} x^i
$$

$$
B(x) = \sum_{i=1}^n (p_i \cdot i!)x^i
$$

Then,

$$
[x^i] Q(x) = \frac{[x^{i+n-1}](A \cdot B)}{i!}
$$

We can include the contribution of \\([x^0]P(x)\\) after this by adding it to \\([x^0]Q(x)\\) and \\([x^1]Q(x)\\). This way, we can calculate \\(Q(x)\\) in \\(O(n \log n)\\) using FFT.

Finally, we need to tackle the problem of calculating the Bernoulli numbers. We could use the recursive formula on the Wikipedia page, but that's \\(O(n^2)\\). Instead, we can use the exponential generating function of the Bernoulli numbers:

$$
\frac{x}{e^x-1} = \left(\sum_i \frac{x^i}{(i+1)!} \right)^{-1}
$$

Now, we can solve the entire problem in \\(O(n \log{n})\\).

This post and some related discussion can also seen on [my Codeforces blog](https://codeforces.com/blog/entry/98563).
