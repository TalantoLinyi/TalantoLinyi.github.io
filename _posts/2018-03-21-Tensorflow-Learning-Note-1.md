---
layout: post
title:  "Tensorflow Learning Note 1"
date:   2018-03-21 15:00:00 +0800
categories: Tensorflow
---
### TF训练时的显存占用问题

选择单个GPU训练  所有的GPU显存都会被占满

Source: 在训练时默认占用所有的GPU显存

Solution： 

* 指定分配的显存比例
	
```
gpu_options=tf.GPUOptions(per_process_gpu_memory_fraction = 0.333)
sess=tf.Session(config=tf.ConfigProto(gpu_options=gpu_options))
```
     	
* 分配显存按需求增长

```
config = tf.ConfigProto()  
config.gpu_options.allow_growth=True  
sess = tf.Session(config=config)
```
  
* 限制可见GPU数目
		
```
export CUDA_VISIBLE_DEVICES=1

```
		  
		
	
## TF使用flags定义命令行参数
	
```
import tensorflow as tf

flags = tf.app.flags 
flags.DEFINE_string('str_name',"Linyi", "What the hell am I?")
flags.DEFINE_integer('int_age', 22, "I thought I am 18 forever")
flags.DEFINE_boolean("bool_name", True, "Am I Linyi?")

FLAGS = flags.FLAGS

def main(_):
	print('What the hell am I? I am',FLAGS.str_name)
	print("I thought I am 18 forever. No! You're", FLAGS.int_age)
	print('Are you sure?', FLAGS.bool_name)

if __name__ == '__main__':
	tf.app.run()
```

**Conduct**:

```
What the hell am I? I am Linyi
I thought I am 18 forever. No! You're 22
Are you sure? True
```

```
$ python3 TF1.py --str_name Alex

What the hell am I? I am Alex
I thought I am 18 forever. No! You're 22
Are you sure? True
```



		
	





