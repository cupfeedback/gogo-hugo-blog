+++
title = "일반신경망_분류"
description = "기본 신경망 작성하기"
tags = [
    "NeuralNetwork",
    "writing",
    "Classification",
    "DeepLearning",
]
date = "2023-12-24"
categories = [
    "DeepLearning",
    "writing",
]
menu = "main"
+++

# Intro
Neural Network 를 sklearn이나 pytorch, tensorflow 등 라이브러리 활용해서 짜는 것도 있지만 직접 A부터 Z까지 짜는 과정에 대해서 기록합니다.
요즘에는 Andrew Ng 교수님 Deep Learning 과정을 듣고 있습니다. 
퀴즈나 과제 풀고 제출해야 하는 과정인데 주말마다 듣고 있습니다. 
인상깊었던 부분은 tensorflow를 구글에서 만드셔서 그런지 과제도 전부 직접 만드는 걸 내주십니다. 
python을 몰랐던 때 이것저것 해보다가 과제 푼 것 중에 set 클래스 구현하는 게 있었는데 그 때 생각나기도 합니다.
데이터는 따로 없지만 sudo 코드로 어떻게 분류 과제를 neural network로 구현하는지 기록하겠습니다.

# 1. 라이브러리 및 Dataset
Dataset을 불러옵니다.
라이브러리는 간단하게 numpy 정도?

  import numpy as np
  import copy

  X, Y = load_dataset() # 해당되는 데이터셋트 불러오기

그리고 형태를 확인
  X.shape
  Y.shape


# 2. Neural Network Model
  For one example $x^{(i)}$:
  $$z^{[1] (i)} =  W^{[1]} x^{(i)} + b^{[1]}\tag{1}$$ 
  $$a^{[1] (i)} = \tanh(z^{[1] (i)})\tag{2}$$
  $$z^{[2] (i)} = W^{[2]} a^{[1] (i)} + b^{[2]}\tag{3}$$
  $$\hat{y}^{(i)} = a^{[2] (i)} = \sigma(z^{ [2] (i)})\tag{4}$$
  $$y^{(i)}_{prediction} = \begin{cases} 1 & \mbox{if } a^{[2](i)} > 0.5 \\ 0 & \mbox{otherwise } \end{cases}\tag{5}$$
  
  Given the predictions on all the examples, you can also compute the cost $J$ as follows: 
  $$J = - \frac{1}{m} \sum\limits_{i = 0}^{m} \large\left(\small y^{(i)}\log\left(a^{[2] (i)}\right) + (1-y^{(i)})\log\left(1- a^{[2] (i)}\right)  \large  \right) \small \tag{6}$$

