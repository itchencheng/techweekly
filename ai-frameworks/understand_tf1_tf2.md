# 如何看懂tf-1.x和tf-2.x

## Python基础

```python
class DeepQNetwork(object):
    def __init__(self, a, b):
        self.a = a # 注意，这里的self.a表示成员变量，a是入参变量，不要搞混
        self.b = b
    def process(self, x):
        self.a = x
```



### tensorflow

环境

```python
#import tensorflow as tf
import tensorflow.compat.v1 as tf
tf.disable_v2_behavior()

self.sess = tf.Session() # session对象
self.sess.run(tf.global_variables_initializer()) # 执行init


```

 Tensorflow的设计理念称之为计算流图，在编写程序时，首先构筑整个系统的graph，代码并不会直接生效。

Tensorflow是一个编程系统，使用**图（graphs）来表示计算任务**，图（graphs）中的**节点称之为op（operation）**，一个op获得0个或者多个Tensor，执行计算，产生0个或多个Tensor，Tensor看作是一个n维的数组或列表。**图必须在会话（Session）里被启动。**


```python
# check to replace target parameters
if self.learn_step_counter % self.replace_target_iter == 0:
    self.sess.run(self.replace_target_op)
```





### tf.placeholder

占位，用来表示输入。

tf.placeholder(type, shape, name)，shape中的None表示该维不固定。

```python
self.s = tf.placeholder(tf.float32, [None, self.n_features], name='s')  # input
self.q_target = tf.placeholder(tf.float32, [None, self.n_actions], name='Q_target')  # for calculating loss
```

### tf.variable_scope

https://www.cnblogs.com/southtonorth/p/11060419.html

变量作用域，**Variable Scope** 这种独特的机制来共享变量。这个机制涉及两个主要函数：

```python
with tf.variable_scope('loss'):
    self.loss = tf.reduce_mean(tf.squared_difference(self.q_target, self.q_eval))
```

