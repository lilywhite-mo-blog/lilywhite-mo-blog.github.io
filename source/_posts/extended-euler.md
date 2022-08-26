---
title: LSMO 数论题解答（扩展 Euler）
mathjax: true
---

** 全文转自 OI Wiki **

定义 $\varphi(x)$ 为 $x$ 的欧拉函数。对于任意满足 $b\ge\varphi(m)$ 的正整数 $a,b,m$，证明：

$$
a^b \equiv a^{b \bmod \varphi(m)+\varphi(m)}\qquad (\bmod\space m)
$$

### 证明

 1. **引理**：$a$ 的从 $0$ 次，$1$ 次到 $b$ 次幂模 $m$ 构成的序列中，存在 $r$ 和 $s$，使得前 $r$ 个数（即从 $a^0 \bmod m$ 到 $a^{r-1} \bmod m$) 互不相同，从第 $r$ 个数开始，每 $s$ 个数就循环一次。

	   **证明**：

	   -   由鸽巢定理易证。

	        我们把 $r$ 称为 $a$ 幂次模 $m$ 的循环起始点，$s$ 称为循环长度。（注意：$r$ 可以为 $0$）

	        用公式表述为：$\forall i \ge r, a^i \equiv a^{i+s} \pmod{m}$

2.  **命题**：$a$ 为素数的情况，该式成立。

    **证明**：

    - **若模 $m$ 不能被 $a$ 整除**，而因为 $a$ 是一个素数，那么 $\gcd(a, m) = 1$ 成立，根据欧拉定理，容易证明该式成立。

    -   **若模 $m$ 能被 $a$ 整除**，那么存在 $r$ 和 $m'$ 使得 $m = a^r m'$，且 $\gcd(a, m')=1$ 成立。所以根据欧拉定理有 $a^{\varphi(m')} \equiv 1 \pmod{m'}$。

        又由于 $\gcd(a^r, m')=1$，所以根据欧拉函数的求值规则，容易得到：$\varphi(m) = \varphi(m') \times (a-1)a^{r-1}$，即我们有：$\varphi(m') \mid \varphi(m)$。

        所以 $a^{\varphi(m')} \equiv 1 \pmod {m'}, \varphi(m') \mid \varphi(m) \Rightarrow a^{\varphi(m)} \equiv 1 \pmod {m'}$，即 $a^{\varphi(m)}=km'+1$，两边同时乘以 $a^r$，得 $a^{r+\varphi(m)} = km + a^r$（因为 $m = a^r m'$）

        所以对于 $m$ 中素因子 $a$ 的次数 $r$ 满足：$a^r \equiv a^{r+\varphi(m)} \pmod m$。我们可以简单变换形式，得到 **推论**：

        $$
        b > r \implies a^b \equiv a^{r + ((b-r) \bmod \varphi(m))} \pmod {m}
        $$

        又由于 $m = a^r m'$，所以 $\varphi(m) = \varphi(a^r) \varphi(m') \ge \varphi(a^r)=a^{r-1}(a-1) \ge r$（tips：$a$ 是素数，最小是 $2$，而 $r \ge 1$）。

        所以因为 $\varphi(m) \ge r$，故有：

        $$
        a^r \equiv a^{r+\varphi(m)} \equiv a^{r \bmod \varphi(m)+\varphi(m)} \pmod m
        $$

        所以

        $$
        \begin{aligned}
            a^b &\equiv a^{r+(b-r) \bmod \varphi(m)} \\
                &\equiv a^{r \bmod \varphi(m) + \varphi(m) + (b-r) \bmod \varphi(m)} \\
                &\equiv a^{\varphi(m) + b \bmod \varphi(m)}
        \end{aligned} \pmod m
        $$

        即 $a^b\equiv a^{b \bmod \varphi(m)+\varphi(m)}\pmod m$。

3.  **命题**：$a$ 为素数的幂的情况，该式成立。

    **证明**：

    -   不妨令 $a = p^k$，是否依然有 $\forall r, a^{r} \equiv a^{r+\varphi(m)} \pmod m$？

        答案是肯定的，由命题 1 可知存在 $s$ 使得 $a^s\equiv 1 \pmod m$，所以 $p^{\mathrm{lcm}(s,k)} \equiv 1 \pmod {m}$，所以令 $s'=\frac{s}{\gcd(s,k)}$ 时，我们能有 $p^{s'k} \equiv 1 \pmod {m}$。

        此时有关系：$s' \mid s$ 且 $s \mid \varphi(m)$，且 $r'= \lceil \frac{r}{k}\rceil \le r \le \varphi(m)$，由 $r',s'$ 与 $\varphi(m)$ 的关系，依然可以得到 $a^b\equiv a^{b \bmod \varphi(m)+\varphi(m)}\pmod m$。

4.  **合数**：$a$ 为合数的情况，该式成立。

    **证明**：

    -   只证 $a$ 拆成两个素数的幂的情况，大于两个的用数学归纳法可证。

        设 $a=a_1a_2$，其中 $a_i=p_i^{k_i}$，而 $a_i$ 的循环长度为 $s_i$；

        则 $s \mid lcm(s_1,s_2)$，由于 $s_1 \mid \varphi(m),s_2 \mid \varphi(m)$，那么 $lcm(s_1,s_2) \mid \varphi(m)$，所以 $s \mid \varphi(m)$，$r=\max(\lceil \frac{r_i}{k_i} \rceil) \le \max(r_i) \le \varphi(m)$；

        由 $r,s$ 与 $\varphi(m)$ 的关系，依然可以得到 $a^b \equiv a^{b \bmod \varphi(m)+\varphi(m)}\pmod m$。

        证毕。
