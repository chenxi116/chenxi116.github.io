---
layout: post
title:  "Computer Vision: 10 Papers to Start"
---

> "How do I know what papers to read in computer vision? There are so many. And they are so different.” Graduate Student. Xi’An. China. November, 2011.

This is a quote from an [opinion paper][core] by my advisor. Having worked on computer vision for nearly 2 years, I can absolutely resonate with the comment. The diversity of computer vision may be especially confusing for starters.

This post serves as a humble attempt to answer the opening question. Of course it is subjective, but a good starting point for sure.

This post is intended for **computer vision starters**, mostly **undergraduate students**. An important lesson is that unlike undergraduate education, when doing research, you learn primarily from reading papers, which is why I am recommending 10 to start.

Before getting to the list, it is good to know where CV papers are usually published. CV people like to publish in conferences. The three top tier CV conferences are: CVPR (each year), ICCV (odd year), ECCV (even year). Since CV is an application of machine learning, people also publish in NIPS and ICML. ICLR is new but rapidly rising to the top tier. As for journals, PAMI and IJCV are the best.

I am partitioning the 10 papers into 5 categories, and the list is loosely sorted by publication time. Here it goes!

## Features

Finding good features has always been a core problem of computer vision. A good feature can summarize the information of the image and enable the subsequent use of powerful mathematical tools. In the 2000s, a lot of feature designs were proposed.

1. [Distinctive Image Features from Scale-Invariant Keypoints][sift], IJCV 2004

   SIFT feature is designed to establish correspondence between two images. Its most important applications are in reconstruction and tracking. 

2. [Histograms of Oriented Gradients for Human Detection][hog], CVPR 2005

   HOG has the same philosophy of feature design as SIFT, but is even simpler. While SIFT is more low-level understanding, HOG is more high-level understanding.

## Reconstruction

Reconstruction is an important branch of computer vision. Since the 2000s, structure from motion (SfM) has been formalized and is still the standard practice today.

1. [Photo Tourism: Exploring Photo Collections in 3D][photo], ACM Transactions on Graphics 2006

   This paper uses SfM to reconstruct scenes from photos collected from the internet. Since then, the core pipeline remains more or less the same, and people seek improvement in, for instance, scalability and visualization. There is also an extended IJCV version later.

## Graphical Models

Graphical model is a machine learning tool that tries to capture the relationship between random variables. It is quite general in nature, and is suitable for many computer vision tasks.

1. [Structured Learning and Prediction in Computer Vision][graphical model], Foundations and Trends in Computer Graphics and Vision 2011
  
   This 180+ page paper is one of the first paper that I have read, and remains my personal favourite. It is a comprehensive overview of both theory and application of graphical models in various computer vision tasks. 

## Datasets

The advancement in computer vision can hardly live without good datasets. The evaluation on a suited and unbiased dataset is the valid proof of the proposed algorithm. Interestingly, the evolution of dataset can also reflect the progress of computer vision research.

1. [The PASCAL Visual Object Classes (VOC) Challenge][pascal], IJCV 2010

   PASCAL VOC is the standard evaluation dataset of semantic segmentation and object detection. While the annual challenge has ended, the evaluation server is still open, and the leaderboard is definitely something you want to check out to find the state-of-the-art result/algorithm. There is also a recent retrospect paper on IJCV. 

2. [ImageNet: A Large-Scale Hierarchical Image Database][imagenet], CVPR 2009

   ImageNet is the first large scale dataset, containing millions of images of 1000 categories. It is the standard evaluation dataset of classification, and is one of the driving force behind the recent success of deep convolutional neural networks. There is also a recent retrospect paper on IJCV.

3. [Microsoft COCO: Common Objects in Context][coco], ECCV 2014

   This dataset is relatively new. Similar to PASCAL VOC, it aims at instance segmentation and object detection, but the number of images is much larger. More interestingly, it contains language descriptions for each image, bridging computer vision with natural language processing.

## Deep Learning

I am sure you have heard of deep learning. It is an end-to-end hierarchical model optimized by simply chain rule and gradient descent. What makes it powerful is its billions of parameters, which enables unprecedented representation capacity. 

1. [ImageNet Classification with Deep Convolutional Neural Networks][alexnet], NIPS 2012

   This paper marks the big breakthrough of applying deep learning to computer vision. Made possible by the large ImageNet dataset and the fast GPU, the model took 1 week to train, and outperforms the traditional method on image classification by 10%.

2. [DeCAF: A Deep Convolutional Activation Feature for Generic Visual Recognition][decaf], ICML 2014

   This paper shows that while the model mentioned above is trained for image classification, its intermediate representation is a powerful feature that can transfer to other tasks. This comes back to finding good features for images. In high-level tasks, deep features consistently show superiority over traditional features. 

3. [Visualizing and Understanding Convolutional Networks][visualize], ECCV 2014

   Understanding what is indeed going on inside the deep neural network remains a challenging task. This paper is perhaps the most famous and important work towards this goal. It looks at individual neurons and uses deconvolution to visualize. However, there is still much to be done.

Again, this has been a humble attempt to address the opening question. Hope these excellent papers can kindle your enthusiasm for computer vision!

Merry Christmas!

[core]: http://www.stat.ucla.edu/~yuille/Pubs10_12/opinion_core.pdf
[sift]: https://www.cs.ubc.ca/~lowe/papers/ijcv04.pdf
[hog]: http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf
[photo]: http://phototour.cs.washington.edu/Photo_Tourism.pdf
[graphical model]: http://pub.ist.ac.at/~chl/papers/nowozin-fnt2011.pdf
[pascal]: http://host.robots.ox.ac.uk:8080/pascal/VOC/pubs/everingham10.pdf
[imagenet]: http://www.image-net.org/papers/imagenet_cvpr09.pdf
[coco]: http://arxiv.org/abs/1405.0312
[alexnet]: http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf
[decaf]: http://jmlr.org/proceedings/papers/v32/donahue14.pdf
[visualize]:https://www.cs.nyu.edu/~fergus/papers/zeilerECCV2014.pdf