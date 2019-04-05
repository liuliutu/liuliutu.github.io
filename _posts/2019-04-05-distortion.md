# 写在前面的话

第一次写技术博客，好不容易会了一点Markdown，但是编辑水平实在太烂，就直接上图了，见谅……toc

# VR畸变如何校正

畸变校正离不开坐标系的转换，我们先来灌一桶基础知识。

#### 坐标系的转换

- 二维坐标系的旋转  

    一个二维坐标系Oxy，顺时针旋转α，变为Ox'y'坐标系，公式如下：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904051436.JPG "二维坐标系旋转矩阵表达式")  
    
- 三维坐标系的旋转

    一个三维坐标系Oxyz，可以参考[此处博客](https://blog.csdn.net/humanking7/article/details/44756073)，但里面讲到三维旋转的时候，不知为什么举的例子都是逆时针（当转轴垂直纸面向外的时候），此处手动推导先绕Oz顺时针旋转α，再绕Oy顺时针旋转β，最后绕Ox顺时针旋转γ，所得的旋转矩阵R的表达式为：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20190405155108.jpg "三维旋转矩阵R的表达式")  
    
    

# END
