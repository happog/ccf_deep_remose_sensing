# ccf_deep_remose_sensing
深度16位的图片转8位：matlab下：im2 = uint8(im1);

数据增强部分：
1.现有的代码的训练数据并没有完全用起来，很浪费。这种生成训练数据的方式比较不好。建议可以改代码，充分利用数据来训练。

1)旋转：90,180,270,360
2)加雾（雾化程度）
3)光照调整（gama）
4)噪点（高斯）
5)镜像（左右，上下）

训练部分：
1.用kaggle数据预训练，再微调
2.延长训练epoch，延长50,75看看效果


后处理部分：
1.mask总图的生成策略：可能存在某个位置的像素点同时被预测为多个类的情况。应设定合理的优先级。比如road>water>building>vegetation


可选的模型：
mask_rcnn,fcn,DenseNet,SegNet


训练数据存在不平衡问题，比如road中实际标签很少，在随机裁剪的情况下，很可能一个batch中，只有一小部分的mask是带有road的mask的，大多数mask图都是全黑的，即正样本太少，负样本太多，训练效果肯定不好。


复赛第一次提交数据：64分；对road和water采取了筛选标注的方法来防止不平衡数据的问题。并且建筑物和植被的训练长度进一步加长。现在各个loss都步入0.4以内。

接下来工作：
1.数据切割准备，1000*1000
2.数据增强：旋转，色彩扰动，高斯噪声，雾化,降低分辨率，高斯模糊
3.dropout
4.多尺度训练，多尺度预测（112*112,256*256,500*500）
5.引入新模型：mask rcnn, hed net
6.gan
