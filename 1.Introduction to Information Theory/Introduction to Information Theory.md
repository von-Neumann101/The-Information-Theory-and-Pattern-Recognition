# Fundamental Problem
Claude Shanon的信息论希望结局这样的问题——在不可靠信道(channel)实现可靠通信。由于噪音的存在，接收信号和发送信号不完全相同。他希望构建一个接收消息等于发送原始消息的通信方式
# Information Theory
$$
\begin{align}
&s:\text{information}\to\fbox{ENCODER}\to t:\text{coded transmission}\\&\to\fbox{Channel(plus noise $n$)}
\to r:\text{received}\to\fbox{DECODER}\to \hat s
\end{align}
$$
编码器是用于添加 **冗余(redundancy)** 的系统，解码器则是推测$n$和$s$的系统
## Binary Symmetric Channel
输入和输出都是$0,\ 1$，其中输入和输出不同的概率是$f$

**Example**($f=0.1$):
![[Pasted image 20260811211115.png|616]]
