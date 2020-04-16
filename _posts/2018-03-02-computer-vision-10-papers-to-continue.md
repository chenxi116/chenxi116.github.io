---
layout: post
title:  "Computer Vision: 10 Papers to Continue"
---

It has been more than 2 years since [my last post on this topic](http://www.cs.jhu.edu/~cxliu/2015/computer-vision-10-papers-to-start.html), and a lot of exciting stuff has been going on.
Someone new to this field will probably find some papers in my previous post irrelevant, because the field has been swept by Deep Learning and is moving very fast.
In this post, I select 10 more papers that are all recent, influential, and each addressing a different problem or topic. 
Here it goes!

-  Network Training: [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167), ICML 2015

   Batch Normalization is one of the network training techniques that receives the most good words from practitioners. Networks that were difficult to train (e.g. [VGG](https://arxiv.org/abs/1409.1556)) are easily trainable after inserting BatchNorm layers.

-  Image Classification: [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385), CVPR 2016

   Residual connection is simple, well-motivated, and distinguishes itself clearly from previous convolutional neural networks for image classification.

-  Object Detection: [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497), NIPS 2015

   This work describes the current standard practice when detecting objects at instance level. Object detection is about bounding boxes, but it can be easily adapted to produce masks instead, i.e., instance segmentation.

-  Semantic Segmentation: [DeepLab: Semantic Image Segmentation with Deep Convolutional Nets, Atrous Convolution, and Fully Connected CRFs](https://arxiv.org/abs/1606.00915), PAMI 2017

   DeepLab builds on top of [FCN](https://arxiv.org/abs/1411.4038), but extends it in important ways. Atrous convolution solves the spatial reduction of classification networks naturally, and has found its way in other problems as well, like [speech synthesis](https://deepmind.com/blog/wavenet-generative-model-raw-audio/). 

-  Image Captioning: [Show, Attend and Tell: Neural Image Caption Generation with Visual Attention](https://arxiv.org/abs/1502.03044), ICML 2015

   I am selecting this image captioning paper among many, because it shows how to incorporate the attention mechanism in vision. 

-  Visual Question Answering: [Neural Module Networks](https://arxiv.org/abs/1511.02799), CVPR 2016

   I am selecting this VQA paper among many, because it offers a new perspective: that neural networks can be *dynamic* instead of static based on the input (question). The way modules are assembled has important connection to semantics. One of my favorites!

-  Dataset: [Visual Genome: Connecting Language and Vision Using Crowdsourced Dense Image Annotations](https://arxiv.org/abs/1602.07332), IJCV 2017

   This large-scale dataset is clearly more ambitious than its predecessors, because it aims at bringing in scene graph as *knowledge representation* to connect vision and language. 

-  GAN: [Generative Adversarial Networks](https://arxiv.org/abs/1406.2661), NIPS 2014

   GAN is arguably the most exciting addition to machine learning tools in the past few years. The idea is to use a discriminator to assist generator training; they are effectively "dueling", and both will become stronger over time.

-  Reinforcement Learning: [Mastering the game of Go without human knowledge](https://deepmind.com/blog/alphago-zero-learning-scratch/), Nature 2017

   Though I didn't know much about Go, I still remember watching the AlphaGo vs Lee Sedol game on YouTube with intense excitement. AlphaGo (Zero) is just one representative of increasingly many applications of Reinforcement Learning.

-  Neural Architecture Search: [Learning Transferable Architectures for Scalable Image Recognition](https://arxiv.org/abs/1707.07012), CVPR 2018

   Neural Architecture Search is one instantiation of a bigger goal: [AutoML](https://www.blog.google/topics/google-cloud/cloud-automl-making-ai-accessible-every-business/). Google has poured many human and computational resources on this task. On a personal note, my intern project at Google was also about this topic; it's [here](https://arxiv.org/abs/1712.00559) in case you are interested!
