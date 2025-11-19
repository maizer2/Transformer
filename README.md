# Transformer

## 1. Transformer 공부에 필요한 배경 연구들

### (1) 수학 기초

**1) 선형대수**

* 벡터, 행렬, 행렬곱, 전치
* **내적(dot product)** → attention에서 similarity 계산할 때 핵심
* 정규화(norm), 평균, 분산 → layer normalization 이해에 필요

**2) 미분 & 최적화**

* 편미분, 체인룰
* 경사하강법(Gradient Descent) 개념
* 학습률, 모멘텀, Adam 같은 옵티마이저가 뭘 하는지 정도

**3) 확률 / 통계**

* 확률변수, 기대값, 분산
* softmax, log-likelihood, cross-entropy loss
* “모델이 다음 토큰의 확률분포를 예측한다”는 감각

---

### (2) 머신러닝 기본기

* **지도학습/비지도학습** 개념
* **훈련 / 검증 / 테스트** 데이터 나누기
* overfitting / regularization 직관
* loss function이 뭔지, optimizer가 뭔지, “학습 루프”가 어떻게 돌아가는지

---

### (3) 딥러닝 기본기

**1) 기본 신경망**

* 완전연결층(Linear / Dense layer)
* 비선형 활성함수 (ReLU, GELU 등)
* 역전파(backpropagation)의 직관

**2) 학습 안정화 기법**

* batch normalization vs layer normalization
* dropout, weight decay 같은 regularization

---

### (4) 시퀀스 모델과 RNN 계열

Transformer는 “RNN을 대체한 구조”라서, RNN을 조금이라도 알아두면
“왜 이걸 만들었는지”가 더 잘 보임.

* RNN 기본 구조 (hidden state가 순차적으로 전달됨)
* LSTM, GRU가 RNN의 어떤 한계를 개선하려 했는지
* seq2seq, encoder–decoder 구조 (입력 시퀀스를 벡터로 요약 → 다시 시퀀스로 디코딩)

> **목표**: “시퀀스 데이터를 인코딩해서 다른 시퀀스로 바꾼다”는 프레임 익히기

---

### (5) Attention 메커니즘

Transformer의 심장.

* “모든 토큰이 서로를 **얼마나 중요하게 볼지** 가중치를 계산하는 것”
* **Scaled dot-product attention**

  * Query, Key, Value의 역할
  * dot-product로 similarity 계산 → softmax로 정규화 → 가중합
* RNN + Attention (기존 seq2seq에서 decoder가 encoder의 hidden states에 주목하는 구조)

여기까지 이해되면,

> “RNN 대신 self-attention만으로 전체 시퀀스를 처리”
> 이게 Transformer의 아이디어라는 게 딱 들어온다.

---

### (6) NLP 기초

* 토큰(token), vocab, 패딩(padding)
* 임베딩(embedding): 단어/토큰을 벡터로 표현
* BPE, WordPiece 같은 서브워드 토크나이저가 왜 필요한지
* 언어모델(Language Model)

  * **Causal LM**: 다음 토큰 예측
  * **Masked LM**: 일부 토큰 가리고 맞추기 (BERT류)

---

### (7) Transformer 본체 개념

여기부터가 본게임.

* Self-Attention vs Cross-Attention
* Multi-Head Attention
* Positional Encoding (sin/cos or learned)
* Residual connection + LayerNorm
* Encoder–Decoder 구조 (원래 논문) vs Decoder-only (요즘 LLM 스타일)
* Masking (padding mask, causal mask)

**조금 더 가면 좋은 심화 주제**

* Pre-norm vs Post-norm
* 학습 스케줄 (warmup, cosine decay 등)
* Parameter sharing, weight tying
* Efficient Transformer(예: sparse attention, Performer류) – 이건 나중 단계에서
