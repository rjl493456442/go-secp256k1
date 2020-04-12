## Field notes

### 快速进行取模运算

若模数符合 m = b^t - c，且c可以表示成l长度的b-base模式(l < t)，则可以利用以下算法快速计算

**给定输入x，求r = x mod m**

* S0: q0 = math.floor(x/b^t) 
* S1: r0 = x - q0 * b^t, r = r0
* S2: qi+1 = math.floor(qi * c / b^t)
* S3: ri+1 = qi * c - q1+1 * b^t
* S4: r = r + r1
* if qi+1 == 0, terminate, else Goto S2
* If r >= m, r = r - m

注意对于field的运算，一般来说q1=0，因此只需要进行一轮计算+最后对结果取一次模就可以完成计算。

### 乘法取模运算

首先计算两个大整数的乘法结果 f.n[9-0] * f.n'[9-0] = w[19-0]

对w[19-0]进行取模。由于在这里w[9-0]已经占据了260bits，因此原先的模需要进行一定的转换。转换后的模为2^260 - 2^4*c




### 有限域内求加法逆元

**给定输入x, 求y使得满足(x+y) mod p = 0**

y = N * prime - x (其中N为magnitude)

### 有限域内求乘法逆元

根据费马小定律，一个非零整数a与一个质数p满足a^(p-1) = 1 (mod p)。
因此若要求a的乘法逆元，即a*b = 1 (mod p), 因此b = a^(p-2)