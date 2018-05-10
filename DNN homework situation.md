## 安装tensorflow
按照下面这个官网教程：
https://www.tensorflow.org/install/?hl=zh-cn

## 神经网络大概了解
可以大致读一读这个文章，感觉讲的很清楚`大话卷积神经网络（CNN）`
http://t.cj.sina.com.cn/articles/view/6463425165/181400a8d0010069cx?cre=tianyi&mod=pcpager_fintoutiao&loc=2&r=9&doct=0&rfunc=36&tj=none&tr=9

修改的是这个，可以看下中文注释：https://github.com/Asurada2015/TF_Cookbook/blob/master/08_Convolutional_Neural_Networks/02_Intro_to_CNN_MNIST/02_introductory_cnn.py

## 样本特征
- 训练集中共7697个样本，只有937个‘1’；
- 测试集中共265个样本，只有27个‘1’；
- onehots类型样本尺寸为72×398大小，其shape为（<个数>， 72， 398）。

## 谷歌网盘文件
- 中文名字的文件夹里面是一些资料文档论，你可以参考；
- code文件夹中的experiment开头的是我测试一些信息时候用的，可以不看；
- 那个作业的文件夹是我用来测试的，你把里面的注释删了，单看输入输出格式都是符合要求的，但是不准，**推荐看明白**；
- cnn0802这个基本是源文件，结果还是在预测0-9的手写数字检测；
- cnn0802mo这个可以没有删除准确率和损失变化的曲线，可以调参数时看参数变化对这两个值的影响，**推荐看**；
- cnn0802mo2是我修改最终要交的版本的中间版本，**推荐看明白**；
- .ckpt是保存tensorflow的模型时候生成的文件，无须理会；
- test, backward, forward, generateds.py这几个文件是那个同学写的，无法运行，但可能问题不大？


## 关于如何提高（排序分先后）
1. 减小pool_size的值，pool_size_1和2都改为2，训练一个新的模型测试一下；
2. 将输入归一化（因为目前输入只有0和1），考虑加入Batch Normalization层；单看这个介绍，感觉有可能是归一化的问题：https://morvanzhou.github.io/tutorials/machine-learning/tensorflow/5-13-BN/
3. learning_rate = 0.005，降低值，但不低于0.001
4. generations = 15，增加值，不高于500？
5. 看下样本分布不均衡的的解决办法，其中一个思路是手动删除一些为0的样本；
6. 测试时候可以手动建立测试集，测试集中0和1可以考虑尽量均衡。

## 问题

test.py文件中
`Line203： test_dict = {eval_input: eval_x, eval_target: range(len(test_names))}`
这个eval_target参数不知道怎么设置，随便设置了一个，但感觉对结果无影响，可以先不考虑。
