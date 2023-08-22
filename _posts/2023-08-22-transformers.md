---
layout: post
title: "Transformer, Attention is all you need"
date: 2023-08-22 15:13:18 +0900
tags: [NLP, transformers, attention]
categories: NLP
---
Transformer는 RNN, CNN 모듈을 사용하지 않고 오직 Attention module만을 이용하여 encoder, decoder 구조를 구성한 모델입니다. Self-attention module을 통해 단어들 간의 거리에 관계없이 short-term dependency를 만들어서 기존 RNN이 갖고 있던 long-term dependency 문제를 해결했습니다. 

<p align="center"><img src="{{site.baseurl}}/images/tr1.jpeg" height="300px" width="700px"></p>

## Self-Attention module
<p align="center"><img src="{{site.baseurl}}/images/tr2.jpeg" height="300px" width="700px"></p>
Q와 K를 곱하기 때문에 두 행렬의 dimension이 같아야 한다. V의 dim은 같을 필요는 없다. 그러나 구현상으로는 편의를 위해 Q, K, V의 dim을 hidden size로 모두 동일하게 만든다. 

## Multi-head Attention module
<p align="center"><img src="{{site.baseurl}}/images/tr3.jpeg" height="300px" width="700px"></p>
Q, K, V를 head의 개수만큼 분할하고 각각에서 Z’를 구한 후 concat하고 linear layer를 통해 최종적으로 Z의 크기를 맞춰주게 됩니다. 

이렇게 하는 이유는? Single attention에서는 단어마다 서로 다른 단어와 연결되는 길이 하나밖에 없기 때문입니다.

## Transformer에서의 추가적인 요소들
### Block-Based Model
<p align="center"><img src="{{site.baseurl}}/images/tr4.jpeg" height="300px" width="200px"></p>

각 블록은 아래와 같은 두 개의 sub-layer를 갖습니다. 각 sub-layer마다 Residual connection과 layer normalization이 이루어집니다.

Layernorm(x + sublayer(x))

Layer normalization은 input 값의 분포를 평균 0, 분산 1로 바꿔줍니다. 

- Multi-head attention
- Two-layer feed-forward NN (with ReLU)

### Positional Encoding
attention block에 의하면 단어가 문장에서 어떤 위치에 있는지에 영향을 안 받는데 이를 해결하기 위하여 Embedding layer 전에 Positional encoding을 추가로 해줍니다. 아래와 같은 식을 통해 위치 정보를 구별합니다. 
<p align="center"><img src="{{site.baseurl}}/images/tr5.png" height="200px" width="400px"></p>

## Decoder
Transformer의 Decoder 부분에는 Masked Attention block과 encoder 부분의 attention과 같은 구조인 multi-headed attention block의 두 가지 블록이 있습니다. 
### Masked Self-Attention
아직 생성되지 않은 단어들은 inference 단계에서 보여지면 안 되기 때문에 masking이 필요합니다. 
### Encoder-Decoder attention
Query는 이전 decoder layer에서 받고, Key, Value는 encoder의 output으로부터 옵니다.  
<br/><br/>
정리하자면, Transformer에서는 세가지 attention이 사용됩니다. 
- Encoder self-attention
- Decoder masked multi-head attention
- Decoder self-attention

---
References
- http://nlp.seas.harvard.edu/2018/04/03/attention
- https://wikidocs.net/31379