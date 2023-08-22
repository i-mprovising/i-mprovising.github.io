---
layout: post
title: "Phrase Retrieval Learns Passge Retrieval, Too"
date: 2023-08-22 15:13:18 +0900
tags: [NLP, QuestionAnswering, Retriever, DensePhrases]
categories: papers
---
# Phrase Retrieval Learns Passge Retrieval, Too
## Abstract
* DPR(Dense phrase retrieval)은 output이 QA, 빈칸 채우기 등의 task에 직접적으로 사용될 수 있어서 유용함.
* phrase를 retrieve하는 것이 자연스럽게 더 큰 text block을 가져오는 것을 수반함 → 본 연구에서는 phrase retrieval이 passage, document와 같은 더 큰 단위의 retrieval의 베이스가 될 수 있을지 알아본다.

본 논문의 주 내용은 다음과 같습니다. 
1. Dense phrase-retrieval이 retraining 없이 passage retriever보다 더 나은 passage retreival 성능을 보이는 것을 확인.
2. 왜 phrase-level supervision이 passage-level보다 더 나은 fine-grained entailment를 학습하는지에 대한 해석을 제공
3. Phrase retrieval이 document-retrieval task에서 좋은 성능을 내기 위하여 개선될 수 있음을 보인다.
4. Phrase filtering, vector quantization이 index 사이즈를 줄이는 것.

## 