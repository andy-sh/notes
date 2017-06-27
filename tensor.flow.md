# TensorFlow学习笔记

## 概念

TensorFlow是一个开源软件库，用于各种感知和语言理解任务的机器学习。TensorFlow最初由Google Brain团队开发，用于Google的研究和生产，于2015年11月9日在Apache 2.0开源许可证下发布。

### Tensor(张量)

#### 什么是tensor
The central unit of data in TensorFlow is the tensor.

A tensor is an array of n-dimension containing the same type of data (int32, bool, etc.)

A tensor consists of a set of primitive values shaped into an array of any number of dimensions. A tensor's rank is its number of dimensions.

#### 什么是shape
A tensor can be described with what we call a shape(形态): it is a list (or tuple) of numbers describing the size of each dimension of our tensor, for example:

- For a tensor of n dimensions: `(D_0, D_1, …, D_n-1)`
- For a tensor of size `W x H` (usually called a matrix): `(W, H)`
- For a tensor of size `W` (usually called a vector): `(W,)`
- For a simple scalar (those are equivalent): `()` or `(1,)`

**Note: (D_*, W and H are integers)**

```
3 # a rank 0 tensor; this is a scalar with shape []
[1. ,2., 3.] # a rank 1 tensor; this is a vector with shape [3]
[[1., 2., 3.], [4., 5., 6.]] # a rank 2 tensor; a matrix with shape [2, 3]
[[[1., 2., 3.]], [[7., 8., 9.]]] # a rank 3 tensor with shape [2, 1, 3]
```

Tensor in TensorFlow has 2 shapes! The static shape AND the dynamic shape.

##### The static shape

The static shape is the shape you provided when creating a tensor OR the shape inferred by TensorFlow when you define an operation resulting in a new tensor. 

It is a tuple(元组，不可改变的列表） or a list.

##### The dynamic shape

The dynamic shape is the actual one used when you run your graph. It is itself a tensor describing the shape of the original tensor.

### Computational Graph(可计算图表)
A computational graph is a series of TensorFlow operations arranged into a graph of nodes. 

### placeholders

A graph can be parameterized to accept external inputs, known as placeholders. A placeholder is a promise to provide a value later.

```
a = tf.placeholder(tf.float32)
b = tf.placeholder(tf.float32)
adder_node = a + b  # + provides a shortcut for tf.add(a, b)
```

### 编码思路

When you write math in TF, you have to think about it as an architect(设计师). You are designing operations and not calculating things. Calculus(微积分) will happens in the next phase: everything that “happens” in TF, “happens” within a **Session**. So when you “add” something in TF, you are designing an “add” operation, not actually adding anything.

All those operations are organised as a **Graph**, your Graph holds operations and tensors, not values.

## 安装

### mac os:Installing with virtualenv

1.Install pip and virtualenv

```
sudo pip3 install --upgrade virtualenv
```

2.Create a virtualenv environment

```
virtualenv --system-site-packages -p python3 ~/tensorflow
```

3.Activate the virtualenv environment

```
source ~/tensorflow/bin/activate # If using bash, sh, ksh, or zsh
```

deactivate the environment:

```
(tensorflow)$ deactivate
```

4.install TensorFlow and all the packages that TensorFlow requires into the active Virtualenv environment:

```
pip3 install --upgrade tensorflow
```

Uninstalling TensorFlow:

```
$ rm -r ~/tensorflow 
```

### mac os:Installing with native pip

```
$ pip3 install tensorflow     # Python 3.n; CPU support
```

## 基础通用知识

## 基础函数

### reduce_sum

降维求和。第二个参数为需要被降维的axis。If `axis` has no entries, all dimensions are reduced, and a tensor with a single element is returned.

```
# 'x' is [[1, 1, 1]
#         [1, 1, 1]]
tf.reduce_sum(x) ==> 6
tf.reduce_sum(x, 0) ==> [2, 2, 2]
tf.reduce_sum(x, 1) ==> [3, 3]
tf.reduce_sum(x, 1, keep_dims=True) ==> [[3], [3]]
tf.reduce_sum(x, [0, 1]) ==> 6
```

## 参考
- [TensorFlow Tutorial For Beginners](https://www.datacamp.com/community/tutorials/tensorflow-tutorial)
- [Getting Started With TensorFlow](https://www.tensorflow.org/get_started/get_started)
- [TensorFlow: Shapes and dynamic dimensions](https://blog.metaflow.fr/shapes-and-dynamic-dimensions-in-tensorflow-7b1fe79be363)
- [A simple introduction to TensorFlow](https://blog.metaflow.fr/tensorflow-a-primer-4b3fa0978be3)