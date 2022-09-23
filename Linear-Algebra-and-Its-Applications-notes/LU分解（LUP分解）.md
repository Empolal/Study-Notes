[toc]
# 为什么要拆成两步做，直接做不行吗

- 首先$L$是下三角矩阵，即对角线上方全为零
- $U$是上三角矩阵，即对角线下方全为零
- 由于$LU$的特性，求解矩阵$Ax=b$非常方便

# 法一
以下两种方便手算，这种方法适合计算机==感觉==，因为要求逆矩阵
![Snipaste_2022-02-27_14-28-32](https://gitee.com/empolal/blog-image/raw/master/stm32/Snipaste_2022-02-27_14-28-32.png)

# LU算法性能分析
$\quad$下列运算次数的计算适用于$n\times n$稠密矩阵$A$（大部分元素非零），$n$相当大，例如$n\geq 30$。
1. 计算$A$的$LU$分解大约需要$2n^{3}/3$浮算，而求$A^{-1}$大约需要$2n^{3}$浮算。
2. 解$L\mathbf{y}=\mathbf{b}$和$U\mathbf{x}=\mathbf{y}$大约需要$2n^{3}$浮算，因为任意$n\times n$三角方程组可以用大约$n^{3}$浮算解出。
3. 把$\mathbf{b}$乘以$A^{-1}$也需要$2n^{3}$浮算，但结果可能不如$L$和$U$得出的精确(由于计算$A^{-1}$及$A^{-1}\mathbf{b}$的舍入误差)。
4. 若$A$是稀疏矩阵（大部分元素为0），则$L$和$U$可能也是稀疏的，然而$A^{-1}$很可能是稠密的，显然用$LU$分解来解$A\mathbf{x}=\mathbf{b}$很可能比用$A^{-1}$快很多。 


# 法二

- 不必管证明，我们知道==U的第一行与A的第一行相同==，L的第一列等于A的第一列除以该列的==主元==，并且通常将$L$变为单位三角矩阵
- 矩阵$A$经过一系列初等行变换变成阶梯型矩阵，即$U$;
- 换的过程中在每个主元列，把主元以下的元素除以主元即为$L$在该列主元以下的元素。

## 例题

<img src="https://gitee.com/empolal/blog-image/raw/master/stm32/Snipaste_2022-02-27_13-36-19.png" alt="Snipaste_2022-02-27_13-36-19" width="578" height="420">

<img src="https://gitee.com/empolal/blog-image/raw/master/stm32/Snipaste_2022-02-27_14-07-37.png" alt="Snipaste_2022-02-27_14-07-37" width="578" height="414">

# 法三及其求解x

- U的第一行与A的第一行相同
- L的第一列等于A的第一列除以该列的主元
- 剩下的元素通过解方程组推出来

## 例题

<img src="https://gitee.com/empolal/blog-image/raw/master/stm32/Snipaste_2022-02-27_12-51-23.png" alt="Snipaste_2022-02-27_12-51-23" width="507" height="308" class="jop-noMdConv">

在求解未知数$x、y$的时候，先算0最多的那一行，然后一次递推