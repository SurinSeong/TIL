# LLM의 구성요소와 Transformer

## Transformer in Detail

### NNLM to PLM

- RNNLM으로 Machin Translation과 같은 여러 task를 수행하기엔 성능이 부족했음.
- RNN 자체 모델의 한계 때문에, 긴 텍스트에서 성능이 떨어지고 많은 텍스트를 학습하기 힘들다.

⇒ 이를 보완하기 위해, RNN 2개를 연결하여 Encoder-Decoder 구조를 제안하고 attention 연산을 추가하여 성능을 향상시킨 기법이 등장함.

### RNN-based LM : Seq2Seq

![Image](https://github.com/user-attachments/assets/f566f5a5-889e-4da8-9692-a43d9ad74774)

- **2개의 RNN** (⇒ RNN을 조금 더 발전시킨 것 : LSTM) : Encoder - Decoder
    - **Encoder** : 무언가(text)를 코드(숫자)로 만드는 것
    - **Decoder** : 코드를 다시 무언가(text)로 만드는 것
        - **Start of sentence** (= Begin of sentence; 입력 토큰) 가 존재함. → 문장의 시작을 알 수 있음.
        - **End of sentence**가 나올 때까지 **auto-regressive** 방식을 수행한다.
    
    ⇒ 문장의 길이가 길어지면 문제가 생길 수 있음..
    

### Attention

![Image](https://github.com/user-attachments/assets/8207f8c9-189c-4214-b093-66dd0298f175)

- **Decoder가 Encoder의 어디를 확인해야 할까?**를 연산으로 정해주는 것.

⇒ 정답을 제대로 만들기 위해 Encoder의 어떤 부분을 중요해서 봐야할까를 연산으로 정해주는 것!

### Transformer : Attention is All you Need

1. RNN은 긴 문장에 취약함.
2. 연산의 비효율성 (병렬 연산이 많이 가능해질수록 많은 일을 할 수 있다.
3. 데이터를 많이 학습해도 효과가 적음

⇒ RNN을 없애고, **Attention으로 모든 연산을 구현한 최초의 모델** ⇒ paradigm SHIFT! **SCALE UP**

![Image](https://github.com/user-attachments/assets/46080e6a-24ce-4adc-8fd8-c26d9094e9a7)

- Encoder에서 dependency를 없애고, Attention 구조가 sequential 정보를 반영하지 못하는 점을 **positional encoding(디펜던시 정보 추가)**으로 해결했음.
※ RNN의 dependency = sequential한 정보의 처리
1. Encoder Self-Attention : 인코더 자체의 맥락을 파악하는 어텐션
2. **Masked** Decoder Self-Attention : 디코더는 auto-regressive해야 한다. Masked를 통해 앞의 문장만 확인할 수 있도록 해서 뒤에 어떤 단어가 나올지 예측한다.
3. Encoder-Decoder Attention : 디코더가 인코더를 살펴본다.
    
    ![Image](https://github.com/user-attachments/assets/2ccc65a3-b2f6-427b-ae1c-d700c50804b1)
    
    ![Image](https://github.com/user-attachments/assets/0c284dca-812e-43b7-b880-0e43b258f43f)
    

### Transformer가 가져온 것

- Attention을 활용한 구조로 **더 많은 데이터와 더 많은 파라미터를 사용**할 수 있게 되었음.
- RNNLM은 병렬 연산을 사용할 파트가 적었지만, Transformer는 **병렬 연산이 가능**한 구조이기 때문에 **GPU를 충분히 활용**할 수 있다.
- RNNLM보다 더 긴 문장/문서에 대해서도 **충분히 맥락을 학습**할 수 있게 되었다.

⇒ Transformer **Decoder 구조**가 모든 LLM의 근간이 됨.
텍스트를 벡터로 변환하지 않고 **데이터 자체를 바로 디코더에 넣어서 학습**할 수 있도록 한다.

## LLM 제작 프로세스

### LLM의 재료

- **Infra (= Money)**
    - Hyper Scale Cloud(AWS, GCP, Azure), Super Computing, Hyper Scale Data Center ⇒ heavy computing을 NVIDIA GPU로 해야하기 때문에 사용한다.
    - 운영 환경 (하드웨어)
    - AI + 클라우드를 중심으로 비즈니스 패러다임이 이동할 것!
- **Backbond Model (= Pretrained Model)**
    - ChatGPT의 여러 모델들도 결국 GPT3.5, GPT 4, GPT-o1 기반
    - Perplexity.ai의 Sonar 405B도 Llama 3.1 405B기반
    
    ⇒ **Pretrained LLM이 기반 모델**로 중요해짐.
    
- **Tuning** (**비용 효율적인** 백본 튜닝 기술)
    - 어떻게 **경량화**할 것인가?
    - 반도체 기술 (행렬 연산 최적화)
- **Data** (고품질 & 다량의 학습 데이터)
    - Prompt, Instruction
    - 내가 하고 싶은 것에 해당하는 내용!
- **Human Preference** (유저가 좋아하는 것)
    - 유저가 좋아하는 답변을 어떻게 정의할 것인가?
    ex) 로그, 설문조사
    - 플랫폼 + 활성화된 유저를 어떻게 모을 것인가?

### LLM을 만들기 위해 알아야 하는 것들

- Dataset
    - data 타입, 포맷 설정 + 맥락 설정
    ⇒ **Supervised FineTuning** (= SFT)
    - 나의 LLM을 어떤 방향으로 키울 것인가에 따라 사전 학습해야 하는 데이터셋이 달라진다.
    
    ![Image](https://github.com/user-attachments/assets/b153de64-5500-4128-ab14-d246055e7e64)
    
    - Data bias는 LLM에게 치명적이기 때문에 꼭 처리를 해주어야 한다.
        - 중복된 데이터, 개인정보 삭제 필수
- LLM Architecture
    - Llama 3의 대략적인 구조
        
        ![Image](https://github.com/user-attachments/assets/9079d957-4c3b-42af-a1af-7291c7b3ab19)
        
        - 어떤 연산을 쓰는가? **Group Query Attention** Block / **Rotary Positional Encoding**
        - 아웃풋?
        - 전체적인 학습 맥락?
- Pre-training : 맥락 학습
    - Large Corpus → **Self-Supervised
    ※** Self-Supervised Learning : 주어져있는 데이터 자체를 스스로 가이드를 가지고 학습할 수 있는 방법
    Supervised Learning
    Unsupervised Learning
- Post-training : Fine-Tuning

![Image](https://github.com/user-attachments/assets/02a24867-d701-4d69-8fd4-bb47666e76dd)

- Evaluation
    - LeaderBoard

## LLM의 구성요소 및 한계점

### LLM의 구성요소

- **User Input** : LLM에게 보낼 질문 또는 입력
- **Prompt** : AI 모델에게 Input 질문과 함께 제공하는 **지시사항** 혹은 답변 생성을 위해 도움을 주는 예제들
- **Output** : LLM이 생성해내는 **답변**

![Image](https://github.com/user-attachments/assets/f3ff7778-71c0-4337-b1ac-c02dda91f16f)

Prompt Engineering

### LLM의 한계

- Hallucination : 모델이 사실과 무관하거나 존재하지 않는 정보를 생성하거나, 확인할 수 없는 정보를 생성하는 현상
- Intrinsic Hallucination : Source에 있는 정보들을 사용해서 합성된 잘못된 정보가 결과로 나온 경우
- Extrinsic Hallucination : Source에서 찾을 수 없는 정보가 등장한 경우
    - Knowledge Cutoff

### 기존 한계점을 해결하는 기술 , RAG

- **RAG** (Retrieval-Augmented Generation) : **검색엔진 + LLM**
    - **Hallucination**과 **Knowledge Cutoff** 문제를 모두 완화할 수 있음!
