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

