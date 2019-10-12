---
title:Latex
toc: true
date: 2019-10-12 22:30:06
tags: [markdown,latex]
categories:  
- 编程语言
- markdown
---

## 基础语法

### 公式的表示

行内的公式，用\$...\$显示

> 例：
>
> 这是\$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}\$公式
>
> 显示为：
>
> 这是$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$公式

单独显示的公式用\$\$...\$\$来显示

> 例：
>
> \$\$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}\$\$
>
> 显示为：
>
> $$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$$

### 公式中希腊字母

* 用\alpha,\beta,……来表示小写:$\alpha$,$\beta$;

* 用首字母大写的\Theta,\Delta,…来表示大写$\Theta$,$\Delta$

* 与英文字母一致的大写字母用大写英文字母表示. 比如用A表示.

* 有些希腊字母有一些变体. 比如\epsilon \varepsilon表示 $\epsilon$ $\varepsilon$,\phi \varphi表示$\phi$ $\varphi$

字母名称|大写|markdown|小写|markdown
-|-|-|-|-
alpha|$A$|A|$\alpha$|\alpha
beta|$B$|B|$\beta$|\beta
gamma|$\Gamma$|\Gamma|$\gamma$|\gamma
delta|$\Delta$|\Delta|$\delta$|\delta
eplison|$E$|E|$\epsilon$|\epsilon
||||$\varepsilon$|\varepsilon
eta|||$\eta$|\eta
zeta|$Z$|Z|$\zeta$|\zeta
theta|$\Theta$|\Theta|$\theta$|\theta
iota|$I$|I|$\iota$|\iota
kappa|$K$|K|$\kappa$|\kappa
lambda|$\Lambda$|\Lambda|$\lambda$|\lambda
mu|$M$|M|$\mu$|\mu
nu|$N$|N|$\nu$|\nu
xi|$\Xi$|\Xi|$\xi$|\xi
omicron|$O$|O|$\omicron$|\omicron
pi|$\Pi$|\Pi|$\pi$|\pi
rho|$P$|P|$\rho$|\rho
sigma|$\Sigma$|\Sigma|$\sigma$|\sigma
tau|$T$|T|$\tau$|\tau
upsilon|$\Upsilon$|\Upsilon|$\upsilon$|\upsilon
phi|$\Phi$|\Phi|$\phi$|\phi
chi|$X$|X|$\chi$|\chi
psi|$\Psi$|\Psi|$\psi$|\psi
omega|$\Omega$|\Omega|$\omega$|\omega

### 上下标和上下划线

上标用'^',下标用'_'

> 例：
>
> 用\$x_i^2\$表示$x_i^2$
>
> 用\$log_2 x\$表示$log_2 x$

上划线|markdown|下划线|markdown
-|-|-
$\overline{a+bi}$|\overline{a+bi}|$\underline{431}$|\underline{431}

### 括号

部分括号(),[],||,||||可以直接使用，{}需要用'\'转义(后四个是取整函数)

符号|markdown
-|-
$\langle$|\langle|
$\rangle$|\rangle|
$\lceil$|\lceil
$\rceil$|\rceil
$\lfloor$|\lfloor
$\rfloor$|\rfloor

这些括号在直接使用时不会随公式的高度的增加而上下拉伸, 因此需要用\left和\right在这些符号前来使这些符号随公式高度增加自动上下拉伸.

> 例：
>
> \$(\frac{\sqrt x}{y^3})\$ 显示为:
> 
> $$(\frac{\sqrt x}{y^3})$$
> 
>\$\left(\frac{\sqrt x}{y^3}\right)\$显示为:
>
> $$\left(\frac{\sqrt x}{y^3}\right)$$


如果需要手动拉伸,可以用\bigl和\bigr在这些符号前

> 例：
> 
> \$\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)\$显示为:
> 
> $$\biggl(\Bigl(\bigl((x)\bigr)\Bigr)\biggr)$$

### 空格与换行

LaTex默认是省略空格，要输入空格就得自己输入命令，mu是一个数学单位。

效果|说明|语法
-|-|-
$a\quad b$|空格宽度是当前字宽(18mu)|\quad
$a\, b$|空格宽度是3mu|\\,
$a\: b$|空格宽度是4mu|\:
$a\; b$|空格宽度是5mu|\;
$a\! b$|空格宽度是-3mu(向左缩)|\!
$a\ b$|空格宽度是标准空格键效|在\后面敲一个空格
$a\qquad b$|空格宽度是36mu|\qquad

换行：

```
\\ 
```

### 求和、极限和微积分等

符号|markdown
-|-
$\sum$|\$\sum\$
$\int$|\$\int\$
$\oint$|\$oint\$|
$\prod$|\$\prod\$
$\bigcup$|\$\bigcup\$
$\bigcap$|\$\bigcap\$
$\iint$|\$\iint\$
$\iiint$|\$\iiint\$

以上符号在使用时以上下标来表示上下线(参考前面的上标和下标部分)

符号|语法
-|-
$\sum_{i=0}^\infty i^2$|\sum_{i=0}^\infty i^2
$\lim_{x \to -\infty}$|\lim_{x \to -\infty}
$\frac{d}{dx}\left(x^2\right) = 2x$|\frac{d}{dx}\left(x^2\right) = 2x
$\int 2x\,dx = x^2+C$|\int 2x\,dx = x^2+C
$\frac{\partial^2U}{\partial x^2} + \frac{\partial^2U}{\partial y^2}$|\frac{\partial^2U}{\partial x^2} + \frac{\partial^2U}{\partial y^2}

**如果上下限超过一个字符记得加{}**

### 分数

1.用\frac，多个字母要用{}

两种尺寸：frac和dfrac

尺寸较小|因此适合打印|尺寸适中|用于显示器展示
-|-|-|-
符号|语法|符号|语法
$\frac{1+\frac{1}{x}}{3x + 2}$|\frac{1+\frac{1}{x}}{3x + 2}|$\dfrac{1+\frac{1}{x}}{3x + 2}$|\dfrac{1+\frac{1}{x}}{3x + 2}

2.用\over，用于较复杂的分子分母

> 例：
> 
> \${a+1\over b+1}\$表示${a+1\over b+1}$

### 字体

markdown|字体|示例
-|-|-
\mathbb|Blackboard bold|$\mathbb A$
\Bbb|Balckboard Bold|$\Bbb A$
\mathbf|boldface|$\mathbf A$
\mathtt|typewriter|$\mathtt A$
\mathrm|roman font|$\mathrm A$
\mathsf|san-serif|$\mathsf A$
\mathcal|calligraphic|$\mathcal A$
\mathscr|script letters|$\mathscr A$

### 根号
用\sqrt显示根号

> 例：
> 
> \$\sqrt{x^3}\$表示$\sqrt{x^3}$
> 
> \$\sqrt\[3\]{\frac xy}\$表示$\sqrt[3]{\frac xy}$

如果是更复杂的开方,最好用指数形式{…}^a

> 例：
> 
> \$({\frac xy})^{1/2}\$表示$({\frac xy})^{1/2}$


## 矩阵的输入

### 简单矩阵

用

```
$$
\begin{matrix}
……
……
\end{matrix} \tag{n}
$$
```

表示矩阵，其中，数字与数字之间用&分隔，行与行之间用\\分隔，不用$$$$声明也是可以的！

如：

```
$$
  \begin{matrix}
   1 & 2 & 3 \\
   4 & 5 & 6 \\
   7 & 8 & 9
  \end{matrix} \tag{1}
$$
```

$$
  \begin{matrix}
   1 & 2 & 3 \\
   4 & 5 & 6 \\
   7 & 8 & 9
  \end{matrix} \tag{1}
$$

其中，`matrix`可修改为`pmatrix`、`bmatrix`、`Bmatrix`、`vmatrix`、`Vmatrix`等，分别代表(),[],{},||,||||型矩阵

\tag{n}表示该矩阵的编号，当然可以去掉，也可以换成任意数字

### 带省略符号的Matrix

如果矩阵元素太多，可以使用`\cdots` ⋯ `\ddots` ⋱  `\vdots `⋮ 等省略符号来定义矩阵。
如：

```
$$
\begin{bmatrix}
 1      & 2      & \cdots & 4      \\
 7      & 6      & \cdots & 5      \\
 \vdots & \vdots & \ddots & \vdots \\
 8      & 9      & \cdots & 0      \\
\end{bmatrix}
$$
```

$$
\begin{bmatrix}
 1      & 2      & \cdots & 4      \\
 7      & 6      & \cdots & 5      \\
 \vdots & \vdots & \ddots & \vdots \\
 8      & 9      & \cdots & 0      \\
\end{bmatrix}
$$

### 带参数的矩阵

比如写增广矩阵，可能需要最右边一列单独考虑。可以用array命令来处理（此时需要另外一种写法，在此不过多介绍，也就是加个`\left[……\right]`的问题）：

```
$$ 
\left[
    \begin{array}{cc|c}
      1 & 2 & 3 \\
      4 & 5 & 6
    \end{array}
\right] \tag{7}
$$
```

$$ 
\left[
    \begin{array}{cc|c}
      1 & 2 & 3 \\
      4 & 5 & 6
    \end{array}
\right] \tag{7}
$$

### 行间矩阵

可以使用`\bigl(\begin{smallmatrix} ... \end{smallmatrix}\bigr)`，

例如：

```
我们使用矩阵 $\bigl( \begin{smallmatrix} a & b \\ c & d \end{smallmatrix} \bigr)$ 作为因子矩阵，将其...
```

得到：

我们使用矩阵 $\bigl( \begin{smallmatrix} a & b \\ c & d \end{smallmatrix} \bigr)$ 作为因子矩阵，将其...

### 矩阵等式

先用`\begin{equation}`, `\end{equation}` 声明一下，然后在其中写就行，注意等号左右千万不能换行！

```
\begin{equation}
A=\begin{bmatrix}
c_1(w_1,w_2) \\
c_2(w_1,w_2)
\end{bmatrix} 
=\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
\begin{bmatrix}
w_1 \\
w_2
\end{bmatrix} \tag{8}
\end{equation} 
```

$$
\begin{equation}
A=\begin{bmatrix}
c_1(w_1,w_2) \\
c_2(w_1,w_2)
\end{bmatrix} 
=\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
\begin{bmatrix}
w_1 \\
w_2
\end{bmatrix} \tag{8}
\end{equation} 
$$

## 其他符号

类型|||||||||||||
-|-|-|-|-|-|-|-|-|-|-|-|-
比较|\le|$\le$|\ge|$\ge$|\ll|$\ll$|\gg|$\gg$|\neq|$\neq$|\approx|$\approx$
||\sim|$\sim$|\simeq|$\simeq$|\cong|$\cong$|\equiv|$\equiv$|\prec|$\prec$|\lhd|$\lhd$
运算|\times|$\times$|\div|$\div$|\pm|$\pm$|\mp|$\mp$  
集合|\cup|$\cup$|\cap|$\cap$|\setminus|$\setminus$|\subset|$\subset$|\subseteq|$\subseteq$|\subsetneq|$\subsetneq$
||\supset|$\supset$|\in|$\in$|\ni|$\ni$|\notin|$\notin$|\emptyset|$\emptyset$|\varnothing|$\varnothing$
头顶符号|\hat{x}|$\hat{x}$|\bar{x}|$\bar{x}$|\vec{x}|$\vec{x}$|\dot{x}|$\dot{x}$|\ddot{x}|$\ddot{x}$|
方向|\to|$\to$|\gets|$\gets$|\Rightarrow|$\Rightarrow$|\Leftarrow|$\Leftarrow$|\Leftrightarrow|$\Leftrightarrow$|\mapsto|$\mapsto$|
标识|\star|$\star$|\ast|$\ast$|\oplus|$\oplus$|\circ|$\circ$|\bullet|$\bullet$
命题|\land|$\land$|\lor|$\lor$|\lnot|$\lnot$|\forall|$\forall$|\exists|$\exists$|\top|$\top$
||\bot|$\bot$|\vdash|$\vdash$|\vDash|$\vDash$|\because|$\because$|\therefore|$\therefore$
其他|\infty|$\infty$|\triangle|$\triangle$|\angle|$\angle$|\checkmark|$\checkmark$|\nabla|$\nabla$

* {n+1 \choose 2k}or \binom{n+1}{2k}表示${n+1 \choose 2k}$
*  \cdot表示 $\cdot$ 如：$x \cdot y$ 
*  \ldots表示 $\ldots$ 如：$a_1,a_2,\ldots,a_n$
*  \cdots表示 $\cdots$ 如：$a_1+a_2+\cdots+a_n$

