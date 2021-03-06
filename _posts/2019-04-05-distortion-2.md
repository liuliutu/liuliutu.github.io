# 畸变如何校正(2)

写了半天(1)，发现参考博客说的太简略了，还是回头翻[维基百科Distortion (optics)](https://en.wikipedia.org/wiki/Distortion_(optics))比较权威。  
不才我连翻译带查，搬砖搬过来了。

> # Distortion (optics) 畸变   
> 
> 不要与球面像差相混淆，球面镜片表面会导致图像清晰度下降。  
> 在几何光学中，畸变是与直线投影的偏差; 投影，其中场景中的直线在图像中保持笔直。 它是光学像差的一种形式。  
> 
> #### Radial distortion 径向畸变  
> 
> 尽管变形可以是不规则的或遵循许多图案，但是最常见的变形是径向对称的，或者大致如此，这是由于摄影镜头的对称性引起的。 这些径向畸变通常可归类为桶形失真或枕形失真。见van Walree。[1]   
> - 桶形畸变  
    在桶形失真中，图像放大率随着距光轴的距离而减小。 明显的效果是已经围绕球体（或桶）映射的图像。 采用半球形视图的鱼眼镜头利用这种类型的失真作为将无限宽物体平面映射到有限图像区域的方式。 在变焦镜头镜筒中，失真出现在镜头焦距范围的中间，并且在该范围的广角端最差。[2]  
> 
> - 枕形畸变  
    在枕形失真中，图像放大率随着距光轴的距离而增加。 可见效果是，没有穿过图像中心的线条向内弯曲，朝向图像的中心，如枕形。
> 
> - 胡子畸变  
    两种类型的混合物，有时称为胡子畸变或复杂畸变，不常见但不罕见。 它开始于靠近图像中心的桶形失真，并逐渐变成朝向图像周边的枕形失真，使得框架上半部分的水平线看起来像八字胡须。
> 
> 在数学上，桶形和枕形畸变是二次的，这意味着它们随着距中心的距离的平方而增加。 在胡须畸变中，四次项很重要：在中心，二次的桶形失真占主导地位，而在边缘处，枕形方向的4度失真占主导地位。 其他扭曲原则上是可能的 - 边缘处的中心和镜筒中的枕形，或者更高阶的扭曲（6度，8度） - 但实际镜片中通常不会发生扭曲，相对于主镜筒和枕形，高阶扭曲很小效果。
> 

上述描述理解不上去，只好验一下： 

假设系统中只存在径向畸变，不存在平移旋转之类复杂情况，则公式简化为ru=rd×(k1+k2×rd^2+k3×rd^4+k4×rd^6)，其中几乎所有文献均将k1默认为1，此问题过后讨论。我们先预设两种畸变情况，桶形畸变公式系数k1=1.0，k2=1.89e-3，k3=-3.39e-6，k4=4.14e-8，则畸变校正前后的形状对比如下：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061315.jpg)  
    （觉不觉得边缘好像吃掉了半格宽度？后面讨论）  
    
枕形畸变公式系数k1=1.0，k2=-1.89e-3，k3=3.39e-6，k4=-4.14e-8，就是把上面枕形的k2到k4反号，校正前后形状对比如下：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061518%E6%A0%A1%E6%AD%A3%E5%89%8D%E5%90%8E%E5%9B%BE%E7%89%87.jpg)    
不知道为什么枕形畸变的边缘过校了，明明按照原公式求解的，此处暂时忽略。  

现在，我们来做一下改系数的实验，看看有什么变化？  

- 系数k1~k4，除了k1=1，其余全为0，则畸变实际上不存在，ru=rd；  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061348%E6%A0%A1%E6%AD%A3%E5%89%8D%E5%90%8E%E5%9B%BE%E7%89%87.jpg)
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061348rurd%E6%9B%B2%E7%BA%BF.jpg)  
    
- 系数k1=1，k2=1.89e-3，其余全为0，如下图所示，桶形畸变得到了极大的校正，说明预设畸变公式中，二次项权重对桶形畸变的影响较大；  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061407%E6%A0%A1%E6%AD%A3%E5%89%8D%E5%90%8E%E5%9B%BE%E7%89%87.jpg)
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061407rurd%E6%9B%B2%E7%BA%BF.jpg)  

- 系数k1=1，把k2变负号，即k2=-1.89e-3，感觉应该是对枕形畸变的校正，如下图所示：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061622%E6%A0%A1%E6%AD%A3%E5%89%8D%E5%90%8E%E5%9B%BE%E7%89%87.jpg)
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061622rurd%E6%9B%B2%E7%BA%BF.jpg)  
    
    ru-rd曲线出现了断层，且后半段出现了负值，为解析这种情况，将像高取值范围扩大如下：  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061422%E6%A1%B6%E5%BD%A2%E6%9E%95%E5%BD%A2%E6%9B%B2%E7%BA%BF%E5%B7%AE%E5%BC%82.jpg)   
    
    图中桶形畸变曲线和枕形畸变曲线分别位于等高线上下方，与直观感受一致，但由于枕形畸变曲线在大范围处出现拐点，另整个曲线非单调，因此前一幅图片出现了两段曲线。  
    
    之所以出现断层，应该是我的畸变图片像高r_d是我根据r_u反向求取出来的，因为非单调性导致r_u减小到一定范围后，r_d存在三个解，我程序中默认取一个，因此r_d坐标出现断层。  
    
    实际r_d是连续的像高图像，对应的r_u虽然非单调，但始终存在唯一的r_u对应r_d；非单调性会导致不同r_d的图像重合在相同的r_u位置，这种现象不知道物理上如何解释，是否存在，有待各位的指导。  

- 系数k1=1，k2=1.89e-3，k3=-3.39e-6，k4=0，如下图所示，桶形畸变校正得不如只有二阶项好，可见并不是阶数越高校正越好；  
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061628I.jpg)   
    ![](https://github.com/liuliutu/liuliutu.github.io/blob/master/img/201904061628rurd.jpg)   
    

    







