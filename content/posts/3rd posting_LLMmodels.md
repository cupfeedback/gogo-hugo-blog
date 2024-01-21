+++
title = "LLM Models"
description = "NLP LLM Models 히스토리"
tags = [
    "LLM",
    "writing",
    "NLP",
    "LLM_Models",
]
date = "2024-01-21"
categories = [
    "DeepLearning",
    "writing",
]
menu = "main"
+++

# 2024년 1월 근황
로보틱스 관련해서 예전부터 관심이 있어서 약간의 발을 걸쳐두고 있었습니다.

LLM과 관련해서 발표도 해보고 계속 스터디도 하고 있습니다.

20-30년 정도 투자해서 로봇 연구를 키우는 건

현재 AI 발전 흐름과 관련해서 필요한 일이 아닐까 합니다

사람은 나이가 들고

아프기도 하고

사소한 거에 취약해지고

회복하려면 시간이 걸리기도 하는데

로봇은 그렇지 않으니까요.

회사 생활하면서 틈틈이 스터디에 참여하려니 

가끔 힘들다는 생각이 들기도 하는데

장기적으로 봤을 때는 필요한 일이라고 생각합니다.

그리고 이번 주에는 뭔가 모르게 일이 있었는데

어려운 문제라 하필 잘 풀리지 않아서 회사 일을 나름 풀어내려고 고심하고,

동시에 로봇틱스 관련해서 발표 준비하느라 바빴던 시간들이었습니다.

아무튼,

오늘은 LLM Models 히스토리에 대해서 한 번 글을 쓰려고 합니다.

# LLM Models 의 히스토리
![Evolutionary Tree](https://raw.githubusercontent.com/cupfeedback/gogo-hugo-blog/main/content/posts/Evolutionary_Tree.png "Evolutionary Tree")


다음의 그림과 같이 발전했습니다. 
(markdown에 이미지 첨부하는 방법이 뭐더라.. 제대로 올라갔는지 확인 필요...)


# 특징 1. Transformer 모델 그리고 Decoder-Only 모델의 대세

그림에서 보면 Decoder-only 모델에서 훨씬 더 많은 가지들이 뻗어나온 걸 볼 수 있습니다. 

2017년 하반기 쯤에 Attention is All you Need 라는 논문이 구글에서 나왔죠. 

해당 논문에서는 Transformer 모델을 설명하고,

중요한 단어에 초점을 둘 수 있는 Attention 레이어에 대해서 설명하면서

NLP 연구의 한 획을 그었습니다.

그리고 저 Transformer 모델이 완전히 판도를 바꿉니다. chatGPT도 트랜스포머 모델 기반이니까요.

구글은 해당 논문을 소개하면서 BART라는 모델을 만듭니다. 해당 모델은 Encoder-Decoder 를 함께 쓴 모델입니다.

반대로 오픈AI는 트랜스포머 모델에서 Decoder-only 구조만 사용했죠. Auto-Regressive 라고 하죠. 

뒤에 뭐가 나올지를 예측하는 모형입니다. Q&A와 같은 데이터를 학습해서 질문을 하면 뒤에 무엇을 

무슨 단어를 내보낼지를 예측하는 모델입니다.

초기에는 Encoder-Only, Decoder-Only 보다는 Encoder-Decoder를 함께 쓰는 형태로 발전했습니다.

그런데 ChatGPT-3이 나오면서 decoder-only 가 더 핫해졌죠. 그 때 메타든 구글이든 저쪽으로 가야겠구나 해서

LLaMA, Bard 모델이 속속 제시되기 시작합니다.

Encoder-Only 모델은 사실 잘 없고,

Encoder-Decoder는 있긴 한데 대중에게는 알려져 있지 않고, 

Decoder-Only는 대중에게 정말 많이 알려져 있습니다. LLaMA, Bard, ChatGPT3.5, 4.0 등이요.



# 특징 2. Open-Source vs Closed-Source

AI, AI, AI 시대라고 해도, 사실 chatGPT가 선보이기 전까지는

이게 무슨 효과가 있을까. 과연 잘 되긴 할까 라는 의구심이 있었습니다.

텍스트 분류도, 텍스트 생성도 사실 그닥이었으니까요. 

투자하는 비용은 많은데, 성과가 잘 보이지는 않았죠. 

그래서 chatGPT3이 등장하기 전까지는 

해당 데이터를 학습시켜서 모델로 만들면 기업들이 오픈 소스로 많이 풀어주었습니다. 

생성하는 능력이나,

하이퍼파라미터 갯수가 적었지만

그래도 오픈 소스로 볼 수 있었는데,

GPT-3이 등장하면서 모든 기업에서 Closed-Source 로 변했습니다.

단, 메타는 제외입니다. Meta는 만든 모델을 모두 공개했습니다. LLaMA가 대표적이죠.

그래서 LLM 연구를 할 때 라마가 많이 언급되는 게,

소스에 접근해서 알맞은 형태로 fine-tuning을 할 수 있다는 점 때문입니다.

# 특징 3. 트랜스포머 모델 등장 전의 모델들

그럼 저기 2018년 이전의 모델을 한 번 살펴보죠. 정확하게는 트랜스포머 모델을 선보인 2017년 후반의 Attention is All you Need 
논문이 나오기 전이요.

대표적으로 볼 수 있는 건,

1. **Word2Vec (2013)**:
    - 개발자: Google
    - Word2Vec은 단어를 벡터 공간에 매핑하는 것으로, 비슷한 의미를 가진 단어들이 벡터 공간에서 서로 가까이 위치하게 됩니다.
    - 두 가지 주요 아키텍처: Continuous Bag of Words (CBOW)와 Skip-Gram. CBOW는 주변 단어들로부터 한 단어를 예측하고, Skip-Gram은 한 단어로부터 주변 단어들을 예측합니다.
    - 장점: 효율적인 학습, 단어 간의 유사성 캡처.
    - 단점: 단어의 의미가 문맥에 따라 달라지는 것을 모델링하지 못함 (즉, 동음이의어 처리 어려움).

      
2. **FastText (2016)**:
    - 개발자: Facebook Research
    - Word2Vec과 유사하지만, 단어를 더 작은 단위인 n-gram으로 나누어 이들의 벡터를 합하여 최종 단어 벡터를 얻습니다.
    - 장점: 미등록 단어(Out-Of-Vocabulary, OOV)와 단어의 형태적 변화를 더 잘 처리할 수 있음.
    - FastText는 단어의 내부 구조를 이해하는데 강점을 보여, 특히 언어의 형태학적 특성이 중요한 언어에 유용합니다.

      
3. **ELMo (Embeddings from Language Models, 2018)**:
    - 개발자: Allen Institute for AI
    - ELMo는 문맥을 고려한 단어 임베딩을 생성하는 언어 모델입니다. 이는 LSTM 기반의 양방향 언어 모델을 사용하여 단어의 벡터 표현을 생성합니다.
    - 장점: 문맥에 따라 단어의 의미가 바뀔 때 그 차이를 잘 잡아내서 단어의 벡터를 생성합니다.
    - 동음이의어와 같은 단어들도 문맥에 따라 다른 벡터 표현을 가질 수 있습니다.
  
이렇게 있습니다.

CBoW, Word2Vec, LSTM, RNN 등을 기반으로 만든 모델이죠. 초기 연구 모형이고,

사실 문제는 있었죠. 대량의 데이터를 학습하면 backpropagation에서 정보가 거의 남지 않아서 후반의 문장만 

메모리에 남는다던가 등...

# 특징 4. Transformer 이후의 Encoder-Only 소개

트랜스포머 모델이 소개가 된 다음 나온 것 중에 Bert, Electra 등의 모델이 있습니다. 

Bert는 특히 유명합니다. 양방향 문맥을 이해할 수 있는 인코더 형태를 가지고 있어서 입력 데이터에서 유용한 정보를 추출했죠.
좀 더 자세히 설명하면,


Transformer 모델은 기본적으로 encoder와 decoder 두 부분으로 구성되어 있습니다. 

이중 encoder 부분만을 사용하는 경우를 "encoder only" 모델이라고 부릅니다. 

이 모델은 입력 데이터로부터 복잡한 패턴이나 특징을 추출하고, 이를 고차원적인 표현으로 변환하는 역할을 수행합니다.

1. **BERT (Bidirectional Encoder Representations from Transformers, 2018)**:
    - 개발자: Google
    - BERT는 양방향 Transformer 인코더를 사용하여 문맥을 기반으로 단어의 임베딩을 생성합니다.
    - BERT는 'Masked Language Model' (MLM) 과 'Next Sentence Prediction' (NSP)이라는 두 가지 작업을 통해 사전 학습됩니다.
    - 장점: 문맥 기반의 단어 임베딩으로 우수한 성능을 보이며, 다양한 NLP 작업에 대해 미세 조정을 통해 적용할 수 있습니다.
    - BERT는 다양한 자연어 처리 작업에서 새로운 기준을 설정했습니다.
  
      
2. **ALBERT (A Lite BERT)**:
    - 개발자: Google Research
    - ALBERT는 BERT 모델의 경량화 버전으로 설계되었습니다. BERT와 유사한 구조를 가지고 있지만, 파라미터를 공유하고, 팩터화된 임베딩 파라미터를 사용하여 모델의 크기를 줄이고 학습 속도를 향상시켰습니다.
    - 장점: BERT에 비해 훨씬 적은 메모리를 사용하면서도 성능을 유지하거나 개선합니다.

      
3. **RoBERTa (Robustly Optimized BERT Approach)**:
    - 개발자: Facebook AI
    - RoBERTa는 BERT의 변형으로, 학습 데이터를 더 많이 사용하고, 학습 과정을 재조정하여 BERT보다 성능을 향상시킨 모델입니다.
    - 장점: 더 큰 배치 사이즈와 더 긴 학습 시간, 더 많은 데이터를 사용하여 BERT의 성능을 능가합니다.

      
4. **BERT (Bidirectional Encoder Representations from Transformers)**:
    - 개발자: Google
    - 앞서 언급했듯이, BERT는 양방향 Transformer 인코더를 사용하여 문맥 기반의 단어 임베딩을 생성합니다.
    - Masked Language Model (MLM)과 Next Sentence Prediction (NSP)을 통해 사전 학습됩니다.
  
      
5. **ELECTRA (Efficiently Learning an Encoder that Classifies Token Replacements Accurately)**:
    - 개발자: Google Research와 Stanford University
    - ELECTRA는 BERT와 유사하지만, 다른 사전 학습 방식을 사용합니다. ELECTRA는 'Replaced Token Detection' 작업을 사용하여, 실제 데이터와 생성된 데이터를 구분하는 방식으로 학습합니다.
    - 장점: 더 적은 계산 자원으로 BERT와 비슷하거나 더 나은 성능을 달성합니다.

주요 사용은 텍스트 분류, 문장 표현 등에 사용합니다. 


# 특징 5. Transformer 등장 이후 Encoder-Decoder 모델 소개
두 가지의 구조를 다 쓰는 모형으로 양방향 및 자기 회귀 트랜스포머 모델인 바트가 있습니다. 
상당히 우수한 능력을 보여주었죠. 상용화 까진 되지 않았지만, 

학습할 때 mask 된 문장에서 
단어를 복원하는 걸 학습하다보니...  문맥 이해는 바트가 상당히 뛰어났습니다. 

예를 들어, 안녕하세요. 오늘 ___ 참 좋네요. 그렇죠? 라고 중간에 비워두고 무슨 단어가 들어가는지 맞추는 과정을 
추론하도록 하는 거입니다.

1. **BART (Bidirectional and Auto-Regressive Transformers)**:
    - 개발자: Facebook AI
    - BART는 텍스트 생성 및 이해 작업을 위한 시퀀스-투-시퀀스 모델입니다.
    - Transformer 구조를 기반으로 하며, 인코더는 양방향으로,
    - 디코더는 자기 회귀적(auto-regressive)으로 작동합니다.
    - BART는 특히 텍스트 요약, 기계 번역, 질문에 대한 답변 생성과 같은 작업에서 우수한 성능을 보입니다.
    - 주요 특징은 노이즈가 주입된 문장을 원래의 문장으로 복원하는 사전 학습 과정을 통해,
    - 다양한 형태의 텍스트 변환을 이해하고 처리할 수 있다는 것입니다.


2. **T5 (Text-to-Text Transfer Transformer)**:
    - 개발자: Google Research
    - T5는 모든 NLP 작업을 텍스트-투-텍스트 문제로 변환하여 접근하는 방식을 취합니다.
    - 즉, 입력과 출력 모두 텍스트 형식을 취하며,
    - 이를 통해 다양한 작업을 하나의 일관된 프레임워크 내에서 처리할 수 있습니다.
    - T5는 사전 학습과 미세 조정 단계를 모두 포함하며,
    - 특히 미세 조정 단계에서 다양한 NLP 작업에 대해 우수한 성능을 보입니다.
    - T5는 BERT나 GPT와 같은 기존 모델들보다 더 큰 사전 학습 데이터셋과 더 광범위한 벤치마크 작업들을
    - 사용하여 학습되었습니다.


3. **GLM (Guided Language Model)**:
    - GLM은 특정한 작업을 수행하기 위해 추가적인 정보나 지침을 제공받는 언어 모델입니다.
    - GLM은 일반적으로 특정 작업에 대한 지침이나 예시를 통해 작업을 수행하는 방법을 학습합니다.
    - GLM의 구체적인 내용과 성능은 구현과 사용되는 데이터셋에 따라 다를 수 있습니다.
    - 따라서 GLM이라는 용어는 다양한 맥락에서 사용될 수 있으며,
    - 이는 문맥에 따라 특정한 방식으로 구성되고 학습된 언어 모델을 지칭할 수 있습니다.


# 특징 6. Transformer 등장 이후 Decoder 모델 소개
대망의 디코더 Only 모델. 
자기 회귀 언어 모델이라서, 이전 단어를 바탕으로 뒤에 무슨 단어가 나올지를 예측하는 겁니다.

매개 변수도 점점 더 늘어나고 있죠.
GPT1, gpt2, gpt3 은 각각 2B, 15B, 175B 개로

훈련 시키는 비용도 17억, 59억 등으로 늘어나면서

매개 변수와 비용이 모두 증가하는 모델입니다. 

투자자들 사이에서는 회수 시점을 정하기 어렵다고 합니다.

아직까지는 투자하는 만큼 더 뛰어난 성능이 나오기 때문에 끝없이 돈이 들어갑니다. 구글, OpenAI 도 몇 조 씩 투자해서 만들고 있죠.


1. **GPT-1 (Generative Pre-trained Transformer 1)**:
    - 개발자: OpenAI
    - GPT-1은 Transformer 모델을 기반으로 한 언어 생성 모델입니다.
    - Unsupervised pre-training과 supervised fine-tuning을 결합하여 다양한 NLP 작업에 적용됩니다.
    - GPT-1은 문맥을 기반으로 텍스트를 생성하는 능력을 보여주며, 다양한 작업에서 탄탄한 성능을 제공합니다.


2. **GPT-2**:
    - 개발자: OpenAI
    - GPT-2는 GPT-1의 후속 모델로, 모델 크기, 데이터셋, 그리고 학습 방법 면에서 확장되었습니다.
    - 특히, 훨씬 더 큰 데이터셋으로 학습되었고, 모델 크기도 증가했습니다.
    - GPT-2는 더 정교한 텍스트 생성 능력을 보여주며, 문맥 이해와 자연스러운 언어 생성에서 뛰어난 성능을 보입니다.


3. **GPT-3**:
    - 개발자: OpenAI
    - GPT-3는 GPT 시리즈 중 가장 큰 모델로, 매우 큰 언어 모델입니다.
    - 이는 1750억 개의 파라미터를 가지고 있으며, 이로 인해 높은 수준의 언어 이해와 생성 능력을 보여줍니다.
    - GPT-3는 광범위한 NLP 작업에 zero-shot, few-shot, 또는 fine-tuning 방식으로 적용할 수 있으며,
    - 사전 학습만으로도 상당한 성능을 나타냅니다.


4. **LLaMA (Linguistically-informed Language Model Adaptation)**:
    - LLaMA는 특정 언어적 정보나 작업에 적응할 수 있는 언어 모델입니다.
    - 이 모델은 특정 언어 구조나 패턴을 이해하고 반영할 수 있도록 설계되어 있으며,
    - 이를 통해 더 정교하고 효율적인 언어 처리가 가능합니다.
    - LLaMA는 특정 언어적 특성이나 작업에 맞게 모델을 미세 조정하는데 사용될 수 있으며,
    - 이를 통해 모델의 성능을 향상시킬 수 있습니다.


5. **Bard**:
    - Bard는 언어 모델 또는 NLP 시스템의 이름으로 사용될 수 있지만,
    - 이 문맥에서 특정한 모델이나 시스템을 가리키는 것은 아닙니다.
    - 일반적으로, Bard는 이야기나 시를 만들어내는 시스템 또는 그러한 능력을 가진 언어 모델을 의미할 수 있습니다.
    - 특정한 Bard 모델이나 시스템이 있다면,
    - 자연어 생성, 이야기 구성, 시적 표현 생성 등의 능력을 가진 모델일 수 있습니다.


# 마무리

최근 기사에서 chatGPT 5가 나온다고 합니다. 

샘 알트먼에 따르면 훨씬 더 좋은 성능이라고 합니다.

chatGPT4가 나쁜 성능이다 라고 말하는 걸 보면 얼마나 성능이 개선이 되었는지 감이 오지 않습니다.

오늘은 여기까지 쓰겠습니다.

추가로 LLaMA와 관련해서 발전된 모델 등도 써보고 싶은데, 너무 많네요. 

그리고... 아직 markdown 파일 쓰는 것에 익숙치 않으니 뭔가 불편함ㅋㅋ

그럼 20000!



