---
layout: post
title:  "TensorFlow: A First Taste"
---
## Why TensorFlow?

There are a lot of good machine learning/deep learning frameworks out there: Caffe, Theano, Torch... but none of them had the same attention level when it first came out as Google's [TensorFlow][tensorflow].

I have been using Caffe for a few months, and I can hardly complain. However, the extensibility of Caffe is arguably weak. Besides, I'd like to try out some fun stuff using LSTM, which is not supported well by Caffe. Theano or Torch? I hear mostly good things about them, but TensorFlow is the fast rising star here.

(By the way there is this very recent [arxiv paper][compare] comparing popular machine learning/deep learning frameworks, TensorFlow not included.)

## Three Things to Note Before Installation

The official guide for TensorFlow installation is not bad. Specifically, I do find `virtualenv` easy to use and useful. However, since TensorFlow is still at a very early stage, I wish someone pointed out these three things before installation:

1. Only supports Python 2.7.X

   This is mentioned in the [Binary Installation][install] section.

2. Only supports protobuf >= 3.0.0

   You can check the version of your protoc using `protoc -V` and the version of your protobuf using `pip show protobuf`. Personally I upgraded both protoc and protobuf to 3.0.0.

   Specifically, I installed `protobuf-3.0.0-beta-1` from source, and upgraded protobuf using `pip uninstall protobuf` and `pip install 'protobuf>=3.0.0a3'` following [this page][protobufissue].

3. Only supports CUDA toolkit 7.0 and cuDNN 6.5 V2 

   No matter you have a higher or lower CUDA toolkit version, it's no good. The version number `7.0` is hard-cored in the current TensorFlow scripts.

   When installing CUDA 7.0, I recommend using `runfile` over `deb`. The interactive installation is very clear and allows you to keep your old toolkit. If `nvidia-smi` fails after installation, don't panic. Remember to reboot.

I am sure there will be an elegant official fix for the Python requirement and CUDA+cuDNN requirement in a few months. But if you want to try out TensorFlow **NOW**, this is what you have to pay ;)

## Try MNIST!

If you are reading this post, then you probably want to try the [MNIST for Experts][experts] instead of for beginners.

Note that in order to run the first line, make sure `tensorflow/tensorflow/g3doc/tutorials/mnist` is in your `$PYTHONPATH`.

Here is just all of the codes on [MNIST for Experts][experts] put together, in case you want to run everything at once:

{% highlight python %}
import input_data # make sure tensorflow/tensorflow/g3doc/tutorials/mnist is in $PYTHONPATH
mnist = input_data.read_data_sets('MNIST_data', one_hot=True)

import tensorflow as tf
sess = tf.InteractiveSession()

x = tf.placeholder("float", shape=[None, 784])
y_ = tf.placeholder("float", shape=[None, 10])

W = tf.Variable(tf.zeros([784,10]))
b = tf.Variable(tf.zeros([10]))

sess.run(tf.initialize_all_variables())

y = tf.nn.softmax(tf.matmul(x,W) + b)

cross_entropy = -tf.reduce_sum(y_*tf.log(y))

train_step = tf.train.GradientDescentOptimizer(0.01).minimize(cross_entropy)

for i in range(1000):
  batch = mnist.train.next_batch(50)
  train_step.run(feed_dict={x: batch[0], y_: batch[1]})

correct_prediction = tf.equal(tf.argmax(y,1), tf.argmax(y_,1))

accuracy = tf.reduce_mean(tf.cast(correct_prediction, "float"))

print accuracy.eval(feed_dict={x: mnist.test.images, y_: mnist.test.labels})

# CNN START

def weight_variable(shape):
  initial = tf.truncated_normal(shape, stddev=0.1)
  return tf.Variable(initial)

def bias_variable(shape):
  initial = tf.constant(0.1, shape=shape)
  return tf.Variable(initial)

def conv2d(x, W):
  return tf.nn.conv2d(x, W, strides=[1, 1, 1, 1], padding='SAME')

def max_pool_2x2(x):
  return tf.nn.max_pool(x, ksize=[1, 2, 2, 1],
                        strides=[1, 2, 2, 1], padding='SAME')

W_conv1 = weight_variable([5, 5, 1, 32])
b_conv1 = bias_variable([32])

x_image = tf.reshape(x, [-1,28,28,1])

h_conv1 = tf.nn.relu(conv2d(x_image, W_conv1) + b_conv1)
h_pool1 = max_pool_2x2(h_conv1)

W_conv2 = weight_variable([5, 5, 32, 64])
b_conv2 = bias_variable([64])

h_conv2 = tf.nn.relu(conv2d(h_pool1, W_conv2) + b_conv2)
h_pool2 = max_pool_2x2(h_conv2)

W_fc1 = weight_variable([7 * 7 * 64, 1024])
b_fc1 = bias_variable([1024])

h_pool2_flat = tf.reshape(h_pool2, [-1, 7*7*64])
h_fc1 = tf.nn.relu(tf.matmul(h_pool2_flat, W_fc1) + b_fc1)

keep_prob = tf.placeholder("float")
h_fc1_drop = tf.nn.dropout(h_fc1, keep_prob)

W_fc2 = weight_variable([1024, 10])
b_fc2 = bias_variable([10])

y_conv=tf.nn.softmax(tf.matmul(h_fc1_drop, W_fc2) + b_fc2)

cross_entropy = -tf.reduce_sum(y_*tf.log(y_conv))
train_step = tf.train.AdamOptimizer(1e-4).minimize(cross_entropy)
correct_prediction = tf.equal(tf.argmax(y_conv,1), tf.argmax(y_,1))
accuracy = tf.reduce_mean(tf.cast(correct_prediction, "float"))
sess.run(tf.initialize_all_variables())
for i in range(20000):
  batch = mnist.train.next_batch(50)
  if i%100 == 0:
    train_accuracy = accuracy.eval(feed_dict={
        x:batch[0], y_: batch[1], keep_prob: 1.0})
    print "step %d, training accuracy %g"%(i, train_accuracy)
  train_step.run(feed_dict={x: batch[0], y_: batch[1], keep_prob: 0.5})

print "test accuracy %g"%accuracy.eval(feed_dict={
    x: mnist.test.images, y_: mnist.test.labels, keep_prob: 1.0})
{% endhighlight %}

## Conclusion

This post is for those who are trying out TensorFlow for the first time. Hopefully with my words, you will save some time during setup. 

As of today, judging from the installation process, TensorFlow seems far from mature. If you prefer to use a *stable release* kind of thing, maybe it's better to wait a few months.

Happy Thanksgiving!


[install]: http://www.tensorflow.org/get_started/os_setup.html#binary-installation
[compare]: http://arxiv.org/abs/1511.06435
[tensorflow]: http://www.tensorflow.org
[experts]: http://www.tensorflow.org/tutorials/mnist/pros/index.html
[protobufissue]: https://github.com/tensorflow/tensorflow/issues/11