# 香农噪声信道编码定理
## 噪音打字机
![[Pasted image 20260928143620.png|120]]
27个字符到对应字符和相邻两个字符的概率均为 $\dfrac13$
对于该信道，其容量为
$$
C=\operatorname*{max}_{P_x}I(X;Y)=\operatorname*{max}_{P_x}H(Y)-\log3=\log27-\log 3=\log9\text{ bits}
$$
$P_x^*=\{\frac1{27},\frac1{27},...,\frac1{27}\}=\{0,\frac19,0,0,\frac19,0,0...\}$
第二种方式叫做**输入的非混淆子集**。也就是说，对于一个信道的输出，他的输入唯一
![[Pasted image 20260928153312.png|120]]
## 二进制对称信道拓展
对一个 $N$ 长二进制序列使用 $N$ 次 BSC，我们就能对每一位进行翻转（信道只是针对一个位来说的，对于长序列，我们要说“N 次使用信道”）
输入的二进制序列的长度为 $N$，那么有 $2^N$ 个输入和输出。每一个输入都会有一个**典型集**，大小是 $N\cdot f\pm \sqrt N$（当 $N$ 很大的时候），相邻的（汉明距离为 1）输入的典型集有相当的重叠

所有典型集的并的大小约为 $2^{NH(Y)}$，每一个典型集的大小约为 $2^{NH(Y|X)}$

我们如果把典型集看做**近似的输入非混淆子集**，我们能得到类似噪声打字机的情况——为了保证尽可能的非混淆，输入字符的个数应该为：
$$
\frac{2^{NH(Y)}}{2^{NH(Y|X)}}=2^{NI(X;Y)}\le2^{NC}
$$
等号成立当且仅当 $P_x=P_x^*$

或者可以说，使用 $n$ 次信道可以发送 $nC \text{ bits}$

**定理**：对于翻转概率为 $f$ 的 BSC，其信道容量为 $C=1-H_2(f)$
$\forall \varepsilon>0,R<C$，存在一个充分大的 $N$（使用信道的次数），总存在一个具有 $N$ 长且速率大于等于 $R$ 的编码和一组使得分组错误率小于 $\varepsilon$ 编码、解码器

[[Introduction to Information Theory#^7a95f4|7,4-Hamming Code]] 的码率是 $4/7$，其错误率是 $\Theta(f^2)$
用矩阵表示这个纠错码
$$
H=
\begin{bmatrix}
1 & 1 & 1 & 0 & 1 & 0 & 0\\
0 & 1 & 1 & 1 & 0 & 1 & 0\\
1 & 0 & 1 & 1 & 0 & 0 & 1
\end{bmatrix}=\begin{bmatrix}
K&I
\end{bmatrix}
$$
有效的传输 $t$ 满足：
$$
Ht\equiv
\begin{bmatrix}
0\\
0\\
0
\end{bmatrix}
\pmod 2
$$

我们收到的向量视为 $r=t+n\bmod 2$，那么伴随式 $z=Hr=Hn$
例如 $t=0000000$，$r=0100000$. 那么 $z=(1,1,0)$
我们对 $n(噪音)$ 的估计为 $\hat n=z$ 

**推广**：定义 $H$ 为 $M\times N$ 的矩阵，令 $K=N-M$，那么其码率 $R$ 大约为 $\dfrac KN$

**定理**：对于足够大的码长，一定能找到一个**线性码** $H$ 使得码率**任意接近** BSC 信道容量并且使得错误率**任意小**

以 [[Source coding theorem, bent coin lottery#Example The Bent Coin Lottery|Bent coin 彩票]] 为例，和之前不同是——我们不在彩票后面写上某种标记，而是写那个彩票的伴随式 $Hn$（$n$ 指的是彩票的二进制序列）
用户需要设定 $t_1,...,t_k$，而 $t_{k+1},...,t_{m}$ 由 $Ht\equiv 0\pmod 2$ 得到
错误率由两部分组成：**中奖票不在袋子里+中奖票在袋子里，但是有多个相同伴随式的彩票**
错误率依赖于 $H$，前一个部分和 $H$ 无关（这是典型集的取法，和概率分布有关），后一部分显然和 $H$ 有关（存在 $H\tilde n=z$）
$$
\text{Probabilities of error}(H)=P_I+P_{II}(H)
$$
前一项当 $N$ 充分大时趋于 0（多拿一些彩票）
$$
\begin{align}
P_{II}(H)&=\sum_{n\in\text{bag}}P(n)\mathbb 1(\exists \tilde n:n\ne n,\tilde n\in\text{bag},H(n-\tilde n)=0)\\
&\le \sum_n P(n)\underbrace{\sum_{\tilde n\ne n,\tilde n\in\text{bag}}\mathbb 1[H(n-\tilde n)=0]}_{\text{总的冲突次数}}
\end{align}
$$
为了证明总的冲突次数很小（对于任意一个 $H$，这非常难证），我们尝试求**平均**：
$$
\begin{align}
\langle P_{II}\rangle_H=\sum_H P(H)\sum_n P(n){\sum_{\tilde n\ne n,\tilde n\in\text{bag}}\mathbb 1[Hx=0]}\quad (x=n-\tilde n\ne 0)
\end{align}
$$
交换求和顺序：
$$
\sum_{n\in \text{bag}}P(n)\sum_{\tilde n\ne n,\tilde n\in\text{bag}}\sum_HP(H)\mathbb 1[Hx=0]\quad(x\ne 0)
$$
设 $h_1,...,h_M$ 为矩阵 $H$ 的行，那么满足 $\forall i,h_i\cdot x\equiv0\pmod 2$ 的概率为多少？
由于 $x,h_i$ 是任意二进制序列，那么点积为偶数的概率为 $0.5$
所以 $P(H)\mathbb 1[Hx=0]=\frac1{2^M}$：
$$
\sum_{n\in \text{bag}}P(n)\sum_{\tilde n\ne n,\tilde n\in\text{bag}}\frac1{2^M}\le1\times2^{NH_2(f)^+}\times\frac1{2^M}
$$
所以，错误率上界为：
$$
P_I+\dfrac{1}{2^{M-NH(f)^+}}
$$
注意到，当 $\dfrac MN>H_2(f)\Longleftrightarrow 1-\dfrac MN<1-H_2(f)\Longleftrightarrow R<C$，第二项趋于 $0$
