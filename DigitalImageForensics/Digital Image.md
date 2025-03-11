# MATLAB基础

## 变量与运算符

MATLAB 就是专门为矩阵运算服务的编程语言。
所以，几乎都是关于矩阵的运算。

**生成新矩阵 or 向量：**
- 正常写：`(1,2,3;4,5,6;7,8,9)`
- 冒号 `:` 生成（开始，步长，结束）
- `linespace` 、 `logspace` 去等分生成


```matlab
1:0.5:3;
x=linespace(1.2,5,4);
x=logsapce(1.2,5,4);
```

其中 `logspace(a,b,n)` 是在 `[a, b]` 范围内均匀分布的 `n` 个数。
也就是：$logspace(a,b,n)=10^{linespace(a,b,n)}$

**线性代数**

matlab的四则运算基本符合线性代数的定义。
据老师透露，对于矩阵除法求解集这种操作，自己写是不如直接用的 —— 神秘的算法优化。

矩阵（向量）加减，要求形状一样；
矩阵（向量）乘除，要求 **前列后行** 相等；
矩阵（向量）有逐个元素乘除的操作，要求形状一样（哈达马尔乘积）；
针对向量还有点乘；


## 图像读、写与画图


`load(filename);`：导入一个表格的矩阵数据
`writematrix(A,filename);`：导出一个表格的矩阵数据
`imread(filename);`
`imwrite(filename);`
`iminfo(filename);`
`image(Matrix);`：显示矩阵数据为图像
`imshow(filename/Matrix);`：显示矩阵数据为图像


`imresize()`：重定大小
`imrotate()`：旋转
`imcrop()`：裁剪
`imadjust()`：增强对比度？
`imfilter()`：使用滤波
`bwareaopen()`：去除连通小块
`edge()`：边缘检测

`figure`：创建多个图形窗口
`plot(x,y)`：画直线
`subplot(m,n,p,ax)`、`subplot(m,n,p,"replace")`：控制第p个位置的子图；ax是控制单元格合并的矩阵；replace是直接清空那个图
```matlab
subplot(2, 2, 1);  % 创建第一个子图
plot(rand(1, 10));  
title('First Plot');
subplot(2, 2, 2);  % 创建第二个子图
plot(rand(1, 25));  
title('Firster Plot');
subplot(2, 2, 3);  % 创建第三个子图
plot(rand(1, 30));  
title('Firstest Plot');

subplot(2, 2, 1, 'replace');  % 删除第一个子图，重新创建
plot(rand(1, 15));  
title('Replaced Plot');
```

`subplot('Position',[left bottom width height])` 在 pos 指定的自定义位置创建坐标区。使用此选项可定位未与网格位置对齐的子图。

<img src="images/mk-2025-03-10-20-11-18mk-.png" style="width:400px;display:block;margin:0 auto;"/>

`axis([a b c d])`:其实就是设置
`scatter()`：散点图
`surf()`：三维曲面图
`mesh()`：三维网格图

`xlabel(str)/ylabel(str)`：设置 x 轴和 y 轴标签
`title(str)`：设置标题
`suptitle(str)`：全局的title

`bar()`：条形图统计图
`histogram()`：直方图统计图
`imhist`：
`contour()`：等高线

## MATLAB代码的效果探索



# 数字图像类型

## 图像分类

首先一共有:
- 真彩色图像（真彩色是指图像中的每个像素值都分成红、绿、蓝三个基色分量）
- 索引色图像（调色板+图像每个位置上的颜色index）
- 灰度图像（0-1的浮点数 or 0-255的整数）
- 二值图像（只有两个数据，二个数值，顾名思义）
- 图像序列

互相转换的函数：
`rgb2gray(RGB)`、`gray2rgb(map)`：使用某些函数前需要转换灰度图与彩色图
`ind2rgb(X, map)`、`rgb2ind(RGB, Q)`
`gray2ind` 、 `dither`
`grayslice(I, n)`、`grayslice(I, v)`
`im2bw(I,level)`、`im2bw(X,map,level)`、`im2bw(RGB,level)`
`mat2gray(A, [amin amax])`

## 像素关系

- 4-邻接：像素相似且在四边 —— 4-连通
- 对角-邻接：像素相似且在四角 —— 
- 8-邻接：像素相似且在四边or四角 —— 8-连通
- m-邻接：像素相似且要么在四边，要么在四角 —— m-连通

$D_E$：欧几里得距离
$D_4$：曼哈顿距离
$D_8$：棋盘距离
$D_m$：混合距离（下面图中哪个是呢？）

<img src="images/mk-2025-03-10-20-50-02mk-.png" style="width:400px;display:block;margin:0 auto;"/>

## 位图的格式与查看

常见的有：
> BMP、JPEG 、GIF、TIFF、PCX、PNG

他们每种都有自己独特的存储方式。

TIFF：高质量格式
GIF：最简单的动画
JPEG：有层次损失
BMP：点阵式图像文件格式，位映射存储，占用的空间很大

2个字节构成1个字；2个字构成一个双字；8个bit构成一个字节；
每个字的前一个字节是低位字节，后一个字节高位字节；每个双字的前一个字是该双字的低16位，后一个字是该字的高16位

<img src="images/mk-2025-03-10-21-34-00mk-.png" style="width:400px;display:block;margin:0 auto;"/>

学会解读 bmp 的信息头等二进制数据：

<img src="images/mk-2025-03-10-21-33-52mk-.png" style="width:400px;display:block;margin:0 auto;"/>

| 位图文件的 组成部分 | 各部分的标识名称 | 各部分的作用与用途 |
| --- | --- | --- |
| 位图文件头 | BITMAPFILEHEADER | 说明文件类型与偏移量，共14个字节。 |
| 位图信息头 | BITMAPINFORMATION | 说明位图的属性。共40个字节。 |
| 位图调色板 | RGBQUAD | 调色板数组，数组中的每个元素 是一个RGBQUAD结构，占4个字节 |
| 位图数据 | BYTE | 位图数据，位图的压缩格式影响这里，字节不限制。 |

利用MATLAB中的imfinfo函数显示.BMP格式

## 位图文件头

```cpp
typedef struct{
    WORD bfType;        \\ 文件类型
    DWORD bfSize;       \\ 文件大小
    WORD bfReserved1;   \\ 保留字1，约定0
    WORD bfReserved2;   \\ 保留字2，约定0
    DWORD bfoffBits;    \\ 位图阵列偏移量
}BITMAPFILEHEADER;
```

## 位图信息头

位图信息头可能长下面这样：

```Cpp
typedef short WORD;
typedef int DWORD;

typedef struct{
    DWORD biSize; // 信息头大小：固定为40
    DWORD biWidth; // 位图宽度，像素个数
    DWORD biHeight; // 位图高度，像素个数
    WORD biPlane; // 图像平面数，约定1

    WORD biBitCount; // 指定每个象素的位数，其值是1、4、8或24之一
    DWORD biCompression; // 指定压缩格式，0,1,2；

    DWORD biSizeImage; // 位图数据占用字节数

    DWORD biXPelsPerMeter; // 目标设备水平分辨率 单位是：像素/米
    DWORD biYPelsPerMeter; // 目标设备垂直分辨率 单位是：像素/米

    DWORD biClrUsed; // 位图中实际用到的颜色数
    DWORD biClrImportant; // 位图中重要的颜色数，为0时，则所有颜色都重要
}BITMAPINFOHEADER;
```

位图数据阵列中的每3个字节表示一个像素。
biSizeImage 用于指定实际的位图数据占用的字节数，其要求对应于位图阵列的每行的字节数必须是4的倍数。
每一行的字节数是4的倍数，不足的字节用0补齐

$$
biSizeImage =   \lfloor\frac{byte\_width+3}{4}\times 4\rfloor\times biHeight
$$

biClrUsed用于指定位图中实际用到的颜色数。当biClrUsed的值不为0时，其值即是调色板中的颜色数；当biClrUsed的值为0时，调色板中的颜色数由下面这个公式确定。

$$
\text{调色板中的颜色数}=
\left\{
    \begin{align*}
        &2^{biBitCount}\qquad biBitCount=1,4,8\\
        &0 \qquad biBitCount=24
    \end{align*}
\right.
$$



## 位图调色板

每个颜色表项占1个字节

```cpp
typedef char BYTE;
typedef struct{
    BYTE rgbBlue;       \\蓝色分量
    BYTE rgbGreen;      \\绿色分量
    BYTE rgbRed;        \\红色分量
    BYTE rgbReserved;   \\保留字，约定为 0
}RGBQUAD;
```

## 查看练习


## 数字图像处理基础概念

在图像处理中，频率指单位空间内完成周期性变化的次数，即空间频率。
数字图像处理：从图像中提取信息、更适合于计算和处理的形式
图像分析：通过对图像的描述，使其更适合于计算机处理和对不同目标的分类。（机器学习里面的classification）

# 数字图像的基本运算

从严格意义上来说，图像运算仅指对图像中的**所有像素**实施了相同处理的那些运算

空间域：图像像素的简单平面
灰度变换：对单个像素进行操作
空间滤波：通过邻域的信息，处理理这个像素，最小邻域1x1

## 灰度变换
$f$一般表示输入图像，$g$一般表示输出图像。

$$g(x,y)=T(f(x,y))$$

### 灰度反转
$L$表示灰度级。256灰度级代表有0-255这256种亮度。

$$g(x,y)=L-1-f(x,y)$$

### 对数变换

$$g(x,y)=c\cdot\log(1+f(x,y))$$

1. 调高输入图像的低灰度值
2. 人的视觉感觉与进入人眼的光的强度成对数关系

## 直方图

### 灰度直方图

直方图是图像的灰度—像素个数统计图；
统计在图像中具有**该灰度值的像素出现的频数**$h(r_i)=n_i\quad(i\in\{i\in\mathbb{Z}\;|\;i\in[0,L-1]\})$，并绘制成图形
**横坐标**表示图像中像素的**灰度级**，**纵坐标**表示图像中各个灰度级像素的**数量**；灰度直方图不能表示图像中每个像素的位置(空间)信息。

灰度图像的对比度，一般用图像画面中最大的灰度值（最白）与最小的灰度值（最黑）的比值来表示。
当柱状接近分布在整个横轴上，且至少有一个峰值时，图像的对比度较好。
**归一化**直方图只是**把纵坐标上的频数换成频率**。
彩色图片的直方图（RGB）等效3个灰度直方图。

下面四个图像作为对比：

<div class="container"
    style="display: flex;
    flex-direction: column;
    /* border: 3px black solid; */
    align-items:center;
    justify-content: space-between;
    ">
    <img src="../images/mk-2025-03-11-08-40-33mk-.png" style="width:400px;">
    <img src="../images/mk-2025-03-11-08-40-45mk-.png" style="width:400px;">
    <img src="../images/mk-2025-03-11-08-40-51mk-.png" style="width:400px;">
    <img src="../images/mk-2025-03-11-08-41-00mk-.png" style="width:400px;">
</div>

## 图像的运算

### 图像相加

图像相加就是矩阵相加。

相加就是一种线性运算的关系：$g(x,y)=\alpha f_1(x,y)+(1-\alpha)f_2(x,y)$

**同一图像与其多个“副本”**的均值可以去除**加性噪声**。

首先因为：噪声是随机的，那么在无穷样本的状态下接近高斯分布 —— 任何位置都能出现。

![](../images/mk-2025-03-11-09-21-38mk-.png)

那么根据概率密度函数，大部分都分布在离中轴相当近的位置，以及他们的期望是0

也即，假设$I$是原图像真实的情况，那么对于$N$张相同照片的第$i$张图片：

$$f=I+noise_i$$

于是，我们有：

$$
E(noise)=\sum_i^N\frac{noise_i}{N}=0\\
D(g)=D(\sum_i^N\frac{noise_i}{N})=\frac{\sum_i^ND(noise)}{N^2}=\frac{ND(noise)}{N^2}=\frac{\sigma^2}{N}
$$

随着$N$的增大，噪声必然越来越小。

![](../images/mk-2025-03-11-09-23-58mk-.png)

### 图像相减

图像相减就是矩阵相减。

相减**结果小于零**时，一般都是**取零为结果值**
对于某些特殊的应用目的，也**可以取其绝对值**为结果值.
典型应用是图像的**变化检测**.

### 图像的几何变换

1. 平移

$$
\left\{
    \begin{align*}
       x^{'}&=x_0+\Delta x\\
       y^{'}&=y_0+\Delta y
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    1 & 0 & \Delta x \\ 
    0 & 1 & \Delta y \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$

2. 旋转

根据复平面上的向量内积，我们可以写出旋转公式：

$$
\left\{
    \begin{align*}
       x^{'}&=x_0\cos\beta+y_0\sin\beta\\
       y^{'}&=-x_0\sin\beta+y_0\cos\beta
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    \cos\beta & \sin\beta & 0 \\ 
    -\sin\beta & \cos\beta & 0 \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$

而由于我们图像的坐标是在左上角：
<img src="../images/mk-2025-03-11-10-45-37mk-.png" style="width:400px;display:block;margin:0 auto;"/>

所以还需要对坐标进行一步变换：

真实坐标：

$$
\left\{
    \begin{align*}
        x^{'}&=x_0\cos\beta+y_0\sin\beta\\
        y^{'}&=-x_0\sin\beta+y_0\cos\beta\\
        x_{real}^{'}&=0.5h-y^{'}\\
        y_{real}^{'}&=0.5w+x^{'}
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x_{real}^{'} \\ y_{real}^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    0 & -1 & 0.5h \\ 
    1 & 0 & 0.5w \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    \cos\beta & \sin\beta & 0 \\ 
    -\sin\beta & \cos\beta & 0 \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$

3. 水平镜像变换

$$
\left\{
    \begin{align*}
       x^{'}&=x_0\\
       y^{'}&=w-y_0
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    1 & 0 & 0 \\ 
    0 & -1 & w \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$


4. 垂直镜像变换

$$
\left\{
    \begin{align*}
       x^{'}&=h-x_0\\
       y^{'}&=y_0
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    -1 & 0 & h \\ 
    0 & 1 & 0 \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$

5. 图像的转置

$$
\left\{
    \begin{align*}
       x^{'}&=y_0\\
       y^{'}&=x_0
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    0 & 1 & 0 \\ 
    1 & 0 & 0 \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$

6. 放大缩放

$$
\left\{
    \begin{align*}
       x^{'}&=rx_0\\
       y^{'}&=ry_0
    \end{align*}
\right.\\
\Big\Downarrow\\
\begin{bmatrix} 
    x^{'} \\ y^{'} \\ 1 
\end{bmatrix} =
\begin{bmatrix} 
    r & 0 & 0 \\ 
    0 & r & 0 \\ 
    0 & 0 & 1 
\end{bmatrix}
\begin{bmatrix} 
    x_0 \\ y_0 \\ 1 
\end{bmatrix}
$$


7. 缩放算法

- 图像缩小

比如：下采样、降采样
直接去掉这个图像的奇数行偶数行

- 按整数倍放大图像的最近邻域插值法

将原图像中的每个像素原封不动地复制到放大后的每一个像素。

- 按非整数倍放大图像的最近邻域插值法

比如：映射法
新图像上的点按照比例算回旧图像，对比离哪个点最近，就取哪个点的数值。

- 双线性插值放大法

新图像上的点按照比例算回旧图像，假设在$f(x,y)$。
那么根据原图像的灰度进行两次插值计算，得到最终的结果。

# 图像的增强

图像增强就是通过对图像的某些特征，如边缘、轮廓、对比度等，进行强调或尖锐化，使之更适合于人眼的观察或机器的处理的一种技术。



## 空间域上

在图像平面中对图像的像素灰度值直接进行运算处理

### 基于点运算

逐像素点对图像进行增强

1. 对比度拉伸

<div class="container" style="display: grid;grid-template-columns: 1fr 1fr;gap:10px 0;width:100vw;align-items:center;justify-items:center;">
    <img src="../images/mk-2025-03-11-11-58-10mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-29-25mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-55-22mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-55-32mk-.png" style="max-width:200px;border:3px black dotted"/>
    <!--  -->
    <img src="../images/mk-2025-03-11-11-32-22mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-55-46mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-32-27mk-.png" style="max-width:200px;border:3px black dotted"/>
    <img src="../images/mk-2025-03-11-11-55-52mk-.png" style="max-width:200px;border:3px black dotted"/>
</div>


1. 窗切片（灰度切片）

给所关心的灰度范围指定一个较高的灰度值；其它部分指定一个较低的灰度值或0值，不管也行。

![](../images/mk-2025-03-11-11-59-20mk-.png)
![](../images/mk-2025-03-11-11-59-25mk-.png)

### 基于直方图

通过全部或局部地改变图像的对比度。

根据图表分析：当一幅图像的像素占据了所有可能的灰度级范围并呈均匀分布时，则该图像具有比较高的对比度和多变的灰度色调。

所以基于直方图的增强方法，就是从相对比较集中的某个灰度区间变成在全部灰度范围内的均匀分布，来进行图像增强的方法。

变换后的灰度保持从黑到白的单一变化顺序，且变换范围与原先一致；




### 基于空间滤波

利用模板或掩模对图像的邻域像素进行处理

## 频率域上

在图像的频率域中对图像进行增强处理

# Reference

