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
예전에 python을 몰랐던 때 이것저것 해보다가... 과제 푼 것 중에 python의 기본 내장 set 클래스를 직접 구현해보라고 했던 과제가 있었는데, 그 과제 풀었을 때가 생각나기도 합니다.
데이터는 따로 없지만,
sudo 코드로 어떻게 분류 과제를 neural network로 구현하는지 기록하겠습니다.

# 1. 라이브러리 및 Dataset
Dataset을 불러옵니다.
라이브러리는 간단하게 numpy 정도?

  import numpy as np
  import copy

  X, Y = load_dataset() # 해당되는 데이터셋트 불러오기

그리고 형태를 확인
  X.shape
  Y.shape


# 2. Neural Network Model 시작
 다음을 구현할 예정입니다 $x^{(i)}$:
  $$z^{[1] (i)} =  W^{[1]} x^{(i)} + b^{[1]}\tag{1}$$ 
  $$a^{[1] (i)} = \tanh(z^{[1] (i)})\tag{2}$$
  $$z^{[2] (i)} = W^{[2]} a^{[1] (i)} + b^{[2]}\tag{3}$$
  $$\hat{y}^{(i)} = a^{[2] (i)} = \sigma(z^{ [2] (i)})\tag{4}$$
  
  $$y^{(i)}_{prediction} = \begin{cases} 1 & \mbox{if } a^{[2](i)} > 0.5 \\ 0 & \mbox{otherwise } \end{cases}\tag{5}$$
  
hidden 레이어에는 하이퍼볼릭탄젠트 활성화 함수를 사용하고 출력 레이어에는 시그모이드 활성화 함수를 활용해서 1과 0이 출력되는데, 그 과정의 수식은 다음과 같습니다. 

# 3. layer 구조 정하기

    def 레이어구조정하기(X, Y):
        return (입력레이어, 숨겨진레이어, 출력레이어)

입력값 X 가 만약 (2, 4000) 이면 입력 레이어 갯수는 2,
출력값 Y 가 만약 (1, 4000)이면 출력 레이어 갯수는 1 로 입력될 수 있도록 구조를 짭니다.
숨겨진 레이어 사이즈 같은 경우는 연구자 마음대로. 예를 들어 숨겨진 레이어의 갯수를 4로 하겠습니다.

# 4. parameter 초기화하기

    def 초기화값(입력, 히든, 출력):
        # W는 weight 값을 말합니다.
        W1 = 랜덤값인데 (히든, 입력) * 0.001 로 초기화를 해줍니다. (4, 2)
        # b는 bias 값입니다. 0으로 해주는데 레이어 사이즈에 맞춰서 0으로 초기화
        b1 = np.zeros((히든, 1)) 으로 하면 사이즈가 맞죠. 여기서는 (4, 1)
        W2 = (출력, 히든) * 0.001
        b2 = np.zeros((출력, 1))
        return 값은 딕셔너리 구조를 활용해서 해당 값을 리턴합니다

# 5. forward propagation

탄젠트 함수와 시그모이드 함수를 구현해서 출력값과 히든값들에 대해서 중간에 계산해주는 과정입니다.
데이터와 앞서서 초기화된 파라미터값을 집어넣습니다.

시그모이드 함수는 = 1 /  ( 1 + np.exp(-x) ) 를 참고하여 구현합니다. 
구글 검색하면 나옵니다. 그림을 집어넣기엔 시간이 촉박해서ㅋㅋㅋㅠㅠㅠ

    $$Z^{[1]} =  W^{[1]} X + b^{[1]}\tag{1}$$ 
    $$A^{[1]} = \tanh(Z^{[1]})\tag{2}$$
    $$Z^{[2]} = W^{[2]} A^{[1]} + b^{[2]}\tag{3}$$
    $$\hat{Y} = A^{[2]} = \sigma(Z^{[2]})\tag{4}$$

파이썬으로 구현하면

    def 정전파(X, parameters):
        # parameters는 이전에 딕셔너리 형태로 w1, b1, w2, b2값을 초기화했으니 해당 값을 받으면 됩니다. 
        w1, b1, w2, b2 = parameter["W1"], parameter["b1"],,, 등등

        # 이제 np.dot(w, X) + b 가 된 z값과 히든 레이어에서 탄젠트 활성화함수를 거친 a1, 그리고 마지막 출력 레이어의 시그모이드 활성화 함수를 통과한 a2값을 구하기
        Z1, A1, Z2, A2의 값을 구합니다
        Z1 = np.dot(W1, X) + b1
        A1 = np.tanh(Z1)
        Z2 = np.dot(W2, A1) + b2
        A2 = sigmoid(Z2) 값으로 이것도 역시 딕셔너리 형태로
        return 해주면 되겠네요

# 6. Cost 구하기
cost 값은 어느 정도 될 것인지 구합니다

    
        $$J = - \frac{1}{m} \sum\limits_{i = 1}^{m} \large{(} \small y^{(i)}\log\left(a^{[2] (i)}\right) + (1-y^{(i)})\log\left(1- a^{[2] (i)}\right) \large{)} \small\tag{13}$$


    def 비용계산(A2, Y): 
        # 앞에서 마지막 출력레이어에서 시그모이드 함수를 거친 값인 A2와 실제 라벨링된 데이터 Y를 계산합니다
        m = 데이터 갯수
        logprobs = np.multiply(np.log(A2), Y) + np.multiply(np.log(1-A2), (1-Y))
        cost = -np.sum(logprobs) * 1/m
        return cost

# 7. 역전파 값 구하기
역전파는 각 단계에서 편미분한 값을 구합니다. 
gradient descent라고도 하죠. 어느 방향으로 learning rate 를 정해서 조금씩 조금씩 cost가 줄어드는 방향으로 가기 위해서 역전파 값을 구해야 합니다.

    def 역전파(초기화된 parameters, 이전에 구한 값, X, Y):
        초기화된 파라미터 W1, W2 
        활성화 값 A1, A2 
        을 활용해서
        각 단계별 편미분된 값을 구합니다.
        dz2, dw2, db2, dz1, dW1, db1 등입니다.
        dZ2 = A2-Y
        dW2 = np.dot(dZ2, A1.T) * 1/m
        db2 = 1/m * np.sum(dZ2, axis=1, keepdims=True)
        dZ1 = np.dot(W2.T, dZ2) * (1-np.power(A1, 2))
        dW1 = 1/m * np.dot(dZ1, X.T)
        db1 = 1/m * np.sum(dZ1, axis=1, keepdims=True)
        예를 들어 이렇게 구할 수 있습니다.
        그리고 dW1, db1, dW2, db2 값은 이후에 parameter 업데이트 할 때 필요하니 마찬가지로 딕셔너리 형태로 return 해주기

# 8. parameter 업데이트
        파라미터 값을 업데이트 합니다
        W1, b1, W2, b2 값은 learning_rate 를 하드 코드 값으로 받아서 업데이트할 수 있습니다. 앞에서 편미분된 dW1, db1, dW2, db2 값 등을 받아서 업데이트합니다.
        W1 -= learning_rate * dW1
        b1 -= learning_rate * db1
        W2
        b2 
        마찬가지로 return {"W1" : W1, ... } 딕셔너리 형태로 반환을 받고



# 9. 최종 모델 만들기

    최종 모델을 만듭니다.
    def nn_model(X, Y, 히든, 반복횟수, cost값 출력):
        레이어 x, y 사이즈 정하기
        파라미터 = 초기화된 파라미터 값 부르기
        for i in range 반복횟수:
            a2, 파라미터 = forward propagation 함수 호출해서 마지막 시그모이드 출력 레이어 통과한 값 과 W1, b1 등의 값 불러오기
            A2, cache = forward_propagation(X, parameters)
            cost 구하기 Y와 해당 출력 값 비교한 뒤 비용 계산
            cost = compute_cost(A2, Y)
            역전파 값 구해서 gradient descent 값 받기
            grads = backward_propagation(parameters, cache, X, Y)
            learning rate 값 넣어서 해당 파라미터 값 업데이트 하기 
            parameters = update_parameters(parameters, grads)
        

로 10000 번 정도 반복 시켜서 돌려주고 최종 업데이트된 parameters 값을 반환받습니다.

# 10. 예측하기

이제 해당 모델에서 예측합니다.
시그모이드 함수를 통과한 값이  0.5 이상이면 1, 0으로 찍어주면 예측값이 나오도록 
    def predict 함수를 짭니다.
        return 값은 numpy 값이 나오도록... 예를 들어 np.where(A2 > 0.5, 1, 0)


# 11. 마무리
sudo 코드 로 짠 Neural Network 코드로 분류 과제하기 였습니다.
모든 수학적 수식을 코드로 구현한 뒤에 굴리는 과정인데, 직접 해보면 재밌습니다. (그런데 실무에서는 라이브러리 적극 활용)
끗.



