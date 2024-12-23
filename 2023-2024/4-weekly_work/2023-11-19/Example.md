# MNIST
[链接](https://www.bilibili.com/video/BV16g4y1z7Qu/?spm_id_from=333.337.search-card.all.click&vd_source=6714df959b40fdf22d5fa47201de3d2c)

## 代码和解释
[链接](https://chengyong.blog.csdn.net/article/details/105846692)

# MNIST数字识别实战

本文介绍使用神经网络对MNIST数据集进行手写数字识别的完整实战流程。

## 实战流程
1. 获得数据，并将数据处理成合适的格式
2. 按照自己的设计搭建神经网络
3. 设定合适的参数训练神经网络
4. 在测试集上评价训练效果

### 一、 认识MNIST数据集
```python
from keras.utils import to_categorical
from keras import models, layers, regularizers
from keras.optimizers import RMSprop
from keras.datasets import mnist
import matplotlib.pyplot as plt

# 加载数据集
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
print(train_images.shape, test_images.shape)
print(train_images[0])
print(train_labels[0])
plt.imshow(train_images[0])
plt.show()
```

将图片由二维铺开成一维
```python
# 对训练集和测试集中的图像数据进行预处理

# train_images.reshape((60000, 28*28)) 
# 这一步将训练集中的图像数据从二维(28x28像素)重塑为一维数组。
# 每个图像都被展平成一个长度为784(28*28)的一维数组。
# 这使得图像可以被输入到全连接神经网络中。
train_images = train_images.reshape((60000, 28*28)).astype('float')

# test_images.reshape((10000, 28*28)) 
# 这一步将测试集中的图像数据也从二维重塑为一维数组，处理方法与训练集相同。
test_images = test_images.reshape((10000, 28*28)).astype('float')

# to_categorical(train_labels) 
# 将训练集的标签转换为类别编码。
# 这一步将数字标签转换为二进制的独热编码（one-hot encoding）形式。
# 独热编码是将类别标签转换为二进制数组，数组中只有一个位置的值为1，其余位置的值为0。
# 例如，标签2会被转换为一个长度为10的数组，其中第三个元素为1，其余为0。
train_labels = to_categorical(train_labels)

# to_categorical(test_labels) 
# 同样将测试集的标签转换为类别编码，处理方法与训练集标签相同。
test_labels = to_categorical(test_labels)

```

### 二、 搭建一个神经网络
```python
# 创建一个序贯模型
network = models.Sequential()

# 向模型中添加一个全连接层（Dense层）
# units=15表示这个层有15个神经元
# activation='relu'表示使用ReLU激活函数
# input_shape=(28*28,)指定输入数据的形状，这里是MNIST数据集中单个图像的大小（28x28像素）被展平成一维数组
network.add(layers.Dense(units=15, activation='relu', input_shape=(28*28,)))

# 添加另一个全连接层作为输出层
# units=10表示输出层有10个神经元，对应于10个类别的数字（0到9）
# activation='softmax'表示使用softmax激活函数，这在多类分类问题中很常见，
# 它会输出每个类别的预测概率，概率最高的类别就是模型的预测结果
network.add(layers.Dense(units=10, activation='softmax'))
```
### 三、 神经网络训练
1. 编译：确定优化器和损失函数
```
# 编译步骤
network.compile(optimizer=RMSprop(lr=0.001), loss='categorical_crossentropy', metrics=['accuracy'])
```
2. 训练网络：确定训练的数据、训练的轮数和每次训练的样本数等
```python
# 训练网络，用fit函数, epochs表示训练多少个回合，batch_size表示每次训练给多大的数据
network.fit(train_images, train_labels, epochs=20, batch_size=128, verbose=2)
```

### 四、 用训练好的模型进行预测，并在测试集上做出评价
```python
# 来在测试集上测试一下模型的性能吧
y_pre = network.predict(test_images[:5])
print(y_pre, test_labels[:5])
test_loss, test_accuracy = network.evaluate(test_images, test_labels)
print("test_loss:", test_loss, "    test_accuracy:", test_accuracy)
```
### 五、 完整代码
1. 使用全连接神经网络
```python
from keras.utils import to_categorical
from keras import models, layers, regularizers
from keras.optimizers import RMSprop
from keras.datasets import mnist
import matplotlib.pyplot as plt

# 加载数据集
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

train_images = train_images.reshape((60000, 28*28)).astype('float')
test_images = test_images.reshape((10000, 28*28)).astype('float')
train_labels = to_categorical(train_labels)
test_labels = to_categorical(test_labels)

network = models.Sequential()
network.add(layers.Dense(units=128, activation='relu', input_shape=(28*28, ),
                         kernel_regularizer=regularizers.l1(0.0001)))
network.add(layers.Dropout(0.01))
network.add(layers.Dense(units=32, activation='relu',
                         kernel_regularizer=regularizers.l1(0.0001)))
network.add(layers.Dropout(0.01))
network.add(layers.Dense(units=10, activation='softmax'))

# 编译步骤
network.compile(optimizer=RMSprop(lr=0.001), loss='categorical_crossentropy', metrics=['accuracy'])

# 训练网络，用fit函数, epochs表示训练多少个回合， batch_size表示每次训练给多大的数据
network.fit(train_images, train_labels, epochs=20, batch_size=128, verbose=2)

# 来在测试集上测试一下模型的性能吧
test_loss, test_accuracy = network.evaluate(test_images, test_labels)
print("test_loss:", test_loss, "    test_accuracy:", test_accuracy)
```
2. 使用卷积网络
```python
from keras.utils import to_categorical
from keras import models, layers
from keras.optimizers import RMSprop
from keras.datasets import mnist
# 加载数据集
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

# 搭建LeNet网络
def LeNet():
    network = models.Sequential()
    network.add(layers.Conv2D(filters=6, kernel_size=(3, 3), activation='relu', input_shape=(28, 28, 1)))
    network.add(layers.AveragePooling2D((2, 2)))
    network.add(layers.Conv2D(filters=16, kernel_size=(3, 3), activation='relu'))
    network.add(layers.AveragePooling2D((2, 2)))
    network.add(layers.Conv2D(filters=120, kernel_size=(3, 3), activation='relu'))
    network.add(layers.Flatten())
    network.add(layers.Dense(84, activation='relu'))
    network.add(layers.Dense(10, activation='softmax'))
    return network
network = LeNet()
network.compile(optimizer=RMSprop(lr=0.001), loss='categorical_crossentropy', metrics=['accuracy'])

train_images = train_images.reshape((60000, 28, 28, 1)).astype('float') / 255
test_images = test_images.reshape((10000, 28, 28, 1)).astype('float') / 255
train_labels = to_categorical(train_labels)
test_labels = to_categorical(test_labels)

# 训练网络，用fit函数, epochs表示训练多少个回合， batch_size表示每次训练给多大的数据
network.fit(train_images, train_labels, epochs=10, batch_size=128, verbose=2)
test_loss, test_accuracy = network.evaluate(test_images, test_labels)
print("test_loss:", test_loss, "    test_accuracy:", test_accuracy)
```
