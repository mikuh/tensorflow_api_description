# tensorflow_api_description
用比官方文档更加直观的方式描述各个API的用法.

因为平时用到一些不太常用的api时总是要看文档理解半天,每次又记不住,下次遇到又得看文档小心翼翼的理解半天,于是想着,还是做个简单的笔记吧,
下次再遇见相同的api的时候方便快速查阅.

每次遇到一个就记录一个,顺序没有什么章法,等积累多了再统一整理.



### tf.gather
```python
tf.gather(params, indices, validate_indices=None, axis=None, batch_dims=0, name=None)
```
简单的说就是,根据传入的index从相应的axis抽取数据.


举个例子:
在第0个轴上先取第1个元素 再取第0个元素
params=[[1,2], [3,4]] , indices = [1, 0], axis=0  =>  [[3,4], [1,2]]
在第1个轴上先取第1个元素 再取第0个元素
params=[[1,2], [3,4]] , indices = [1, 0], axis=1  =>  [[2,1], [4,3]]


### tf.linalg.matmul / 又名 tf.matmul
```python
tf.linalg.matmul(
    a, b, transpose_a=False, transpose_b=False, adjoint_a=False, adjoint_b=False,
    a_is_sparse=False, b_is_sparse=False, name=None
)
```
就是普通的二维矩阵乘法
Args:

- a: tf.Tensor,  rank > 1.  
- b: tf.Tensor with same type and rank as a.
- transpose_a: If True, a 先转置.
- transpose_b: If True, b 先转置.
- adjoint_a: If True, a 先共轭和转置.
- adjoint_b: If True, b 先共轭和转置.
- a_is_sparse: If True, a 是一个 sparse matrix.
- b_is_sparse: If True, b 是一个 sparse matrix.
- name: Name for the operation (optional).

举几个例子:

tf.linalg.matmul([[1]], [[2,3]]) => [[2, 3]] , shape from (1,1)*(1,2) to (1,2)

tf.linalg.matmul([[[1],[2]]], [[2,3]])  =>  [[[2, 3], [4, 6]]]  shape from (1,2,1)*(1,2) to (1,2,2)

tf.linalg.matmul([[1,2]], [[1,2],[1,2]]) => [[3, 6]] shape from (1,2) *(2, 2) to (1, 2)

tf.linalg.matmul([[1,2]], [[[1,2],[2,2]],[[1,2],[2,2]]])  shape from (1,2)*(2,2,2) to (2, 1, 2)

但是这样是不行的:

tf.linalg.matmul([[[1],[2]]], [[[2],[3]]])  , (1,2,1)*(1,2,1)

从这个例子,我们很容易发现, 这个就是普通的矩阵乘法, 如果张量的rank大于2的化,就取最后的两个轴拿来计算,再拼接到原来的轴上


