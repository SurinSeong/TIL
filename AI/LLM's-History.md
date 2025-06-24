# 언어모델부터 거대언어모델의 발달과정

## 언어모델(LM)이란?

### 자연어 (Natural Language)란?

- 사람이 읽고 이해하며 일상적으로 쓰는 언어
- 이를 컴퓨터가 이해할 수 있도록 “임베딩/인코딩”하는 작업을 거쳐야 한다.

ex) “곰”과 “공”은 전혀 다른 개념이지만, 컴퓨터가 이해할 수 있도록 **인코딩** 과정을 거치면 비슷한 숫자 구성이 나온다. 이를 구분하기 위해, **벡터 임베딩** 방식을 사용해서 의미를 담고 있을 수 있도록 하였다.

### 언어모델이란?

- 자연어, 텍스트 데이터를 컴퓨터가 이해할 수 있는 **좋은 숫자로 표현**하는 것. + **맥락을 이해**하는 것.
    
    ⇒ **TF-IDF**
    각 문서가 어떤 단어를 어느 정도로 중요하게 생각하는지 알 수 있음. 하지만 단어가 많아지면 문제가 될 수 있다.
    

## LLM의 개념 및 발달과정

### SLM : Statistical Language Model

⇒ 통계적인 방법으로 단어들의 나열을 확인하자

- Markov assumption을 가정하여, **이전 단어의 등장 확률이 이후 단어의 등장 확률을 결정한다**는 방법론
ex) Where are we going?
⇒ Where 다음에 올 단어의 확률을 미리 파악한 후, 어떤 단어가 올지 결정한다.
: 조건부확률 ⇒ **문맥 파악**이 가능해질 것이다! (**Next Token Prediction**)
- **N-gram 모델**이 대표적
- 단어의 길이가 길어지면, 확률 계산이 복잡해지며, 모델의 capacity가 작음.

### NNLM : Neural Network-based Language Model

- 2013년, **word2Vec**
    1. **word vector**의 생성
    2. **vector 연산**이 의미를 가짐. ⇒ 이로써 많은 곳에서 확장이 가능해졌다.
- **RNN** (Recurrent Neural Network)
    - word2Vec을 통해 문장의 의미를 이해하자 ⇒ **word vector의 흐름**을 이해해보자!

### PLM : Pretrained Language Model

- Transformer
    - 큰 사이즈의 모델로 확장이 가능해짐.
    
    ⇒ **BERT**, **GPT** 같은 모델이 등장할 수 있는 바탕이 되었음.
    
    ![Image](https://github.com/user-attachments/assets/59cce4b9-0c25-45b0-9b63-39704574759c)
    
- BERT
    
    ![Image](https://github.com/user-attachments/assets/bdc7adff-94d2-494b-8dbe-58b633096c85)
    
    - text를 학습시켜서 context를 이해할 수 있도록 한다. ⇒ **downstream task**를 수행할 수 있도록 한다.
    ※ downstream task : pre-trained 모델로 내가 만들고 싶은 것을 task로 정의하고 수행할 수 있도록 한다. 효율적인 학습을 통해 수행할 수 있도록 한다.
- GPT
    - Hyper-Scale AI의 시대가 탄생함. **175B이나 되는 큰 사이즈의 모델을 사용하면 다양한 작업을 하나의 모델로 처리할 수 있다**는 것을 보여줌.
    - NLP의 여러 downstream task가 모두 next token prediction 문제 (**생성**)로 정의가 가능하다는 것이 입증되었지만, 성능이 애매했음.
    - 2021년 Google의 FLAN의 등장 이후, Instruction Tuning이라는 기법과 함께 **텍스트 생성 결과가 여러 downstream task 성능에 직접적인 영향을 줌**.
    - InstructGPT, Chinchilla 등의 논문들과 함께 여러 LLM의 모델들의 성능을 올리기 위한 효과적인 방법론들이 제시되기 시작
    - 2022년 말, ChatGPT의 등장으로 텍스트 생성으로 많은 작업들을 대체할 수 있는 실효성 있는 서비스가 등장하며 시장을 개혁함.

### Scaling Law

- Emergent Ability : **특정 순간**에 **갑자기** 성능이 올라간다. ⇒ **큰 사이즈 모델**을 사용하면 드라마틱한 성능 개선이 가능하다.

### Auto-Regressive Manner

- 이전 입력에 대한 출력이 다음 입력으로 새롭게 들어가는 것
ex) 먼저, “I saw a cat on a” 다음에 들어갈 단어를 예측한다. “mat”이 들어간다고 예측했다면, “I saw a cat on a mat”을 다시 넣어서 다음에 들어갈 단어를 예측한다.

⇒ 따라서 LLM은 **앞에 어떤 문장을 넣는지**가 중요하다.
⇒ **프롬프트 엔지니어링**의 중요성!!!
