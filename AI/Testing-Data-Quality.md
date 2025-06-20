# 데이터 선택과 볼륨

## 데이터 선택

- **데이터 선택**은 머신러닝에서 오래된 과제로, **주어진 raw data에서 특정 목표 함수에 대해 최적의 데이터셋을 설계**하는 것을 목표로 한다.
- 특히, 대규모 언어 모델 (LLM) 훈련에서 핵심적인 역할을 한다.

## LLM에서의 데이터 선택

- LLM은 방대한 데이터를 사용하기 때문에 **효율적이고 효과적인 데이터 선택**이 필수이다.
- LLM 학습에서 데이터 선택 방식은 **데이터 파이프라인의 각 단계와 학습 목적에 따라 다양하게 적용**한다.
    
    ![Image](https://github.com/user-attachments/assets/0f112e18-cfcf-45e1-bc26-b802e66ca5ab)
    
- 각 학습 단계에 따라 데이터 선택 전략이 달라진다. 각 단계에서 어떤 데이터를 선택해야 하는지 명확하게 이해해야 한다.
    1. **Pretraining (사전학습) 단계**에서의 데이터 선택
        - **Pretraining** 단계는 언어 모델 학습의 초기 단계로, 범용성 있는 모델을 구축하기 위해 다양한 데이터 선택 방법을 사용한다.
        - 방대한 양의 데이터에서 **고품질, 효율적인 데이터를 선정**하고, **불필요한 노이즈와 중복 데이터를 제거**하는 것이 핵심이다.
            
            ![Image](https://github.com/user-attachments/assets/8d76c453-b826-412b-9b6d-3b8f6d07b070)
            
        - 데이터 선택 방법
            1. **Language Filtering**
                - Language Filtering의 주요 목적
                    - 사전 학습 데이터에서 **특정 언어(자연어 또는 프로그래밍 언어)** 만 포함시키는 작업
                    - 다국어 모델의 경우, **언어 간 데이터 비율을 유지**하거나, **특정 언어를 제외**하기도 한다.
                1. **문자 n-gram 기반 분류기** : 텍스트에서 문자 n-gram (예: 2글자 또는 3글자 조합)을 사용하여 언어를 판별
                    - **langdetect** : 간단하고 빠르게 언어를 감지
                    - **cld3** : Google에서 개발한 도구로 **다국어 감지 성능 우수**
                    - **FastText** : Facebook에서 개발한 도구로, **많은 언어를 지원**하며 **속도와 정확도**가 뛰어남
                    
                    ※ n-gram : **연속된 n개의 단어** 또는 **문자 단위**로 텍스트를 나누는 방법
                    
                    - n : 몇 개의 단어 또는 문자로 묶을지 정하는 숫자.
                        - 1-gram : 단어 하나씩 묶음.
                        - 2-gram : 두 단어씩 묶음.
                        - 3-gram : 세 단어씩 묶음.
                2. **비영어 데이터 제거** : 영어 데이터만 남기고 다른 언어 데이터를 모두 제거.
                    - C4 데이터셋에서는 langdetect 분류기를 사용해 영어가 아닌 페이지를 제거 (99% 이상의 확률로 영어로 분류된 데이터만 유지)
                        
                        ※ **C4 데이터** : **Colossal Clean Crawled Corpus**의 약자, **구글의 T5 모델**을 학습하기 위해 만들어진 대규모 자연어 처리 데이터셋
                        
                        - 웹에서 **크롤링한 데이터를 정제**한 대규모 텍스트 데이터로 구성
                        - 공개 데이터셋
                3. **다국어 데이터 필터링** : 여러 언어를 포함한 데이터셋을 다룰 때, 각 언어별 임계값을 설정해 데이터를 필터링
                    - **ROOTS 코퍼스**에서는 FastText를 사용해 언어별 신뢰도 점수를 계산하고, 기준 미달 데이터를 제거
                        
                        ※ **ROOTS 코퍼스** : **BigScience** 프로젝트에서 개발한 다국어 대규모 텍스트 데이터, **Bloom 모델** (오픈소스 다국어 대규모 언어 모델) 학습을 위해 설계.
                        
                        - **다양한 언어와 도메인을 포괄**하며, **데이터 품질을 높이기 위해** 체계적인 **정제 과정을 거친 것**이 특징이다.
                4. **URL 및 도메인 기반 필터링** : **특정 국가 도메인**(.kr, .fr 등)이나 **URL 패턴**을 사용해 언어를 간접적으로 판별
                    - **도메인 확장자** (예: .kr, .fr, .de)를 사용해 특정 국가와 관련된 데이터를 필터링
                    - 낮은 자원 언어 (예: 위구르어)의 경우, 언어 분류기보다 URL 기반 필터링이 더 효과적이다.
                    - **분류기가 지원하지 않는 언어에도 적용 가능**하다.
                    - 저자원 언어 데이터를 상대적으로 **신뢰성 있게 수집 가능**하다.
                    - URL 패턴만으로 언어를 완벽히 판별하기는 어렵다는 단점이 있다.
                5. **코드 데이터 필터** : 코드 파일의 확장자 (예 : .py, .java) 또는 특정 패턴을 사용해 코드 데이터를 필터링
                    - GitHub 저장소의 스냅샷 데이터를 처리할 때 파일 확장자를 기반으로 프로그래밍 언어를 식별
                    - 간단하고 빠르게 코드 데이터를 선별 가능하다.
                    - 코드와 자연어가 섞인 문서에서는 코드 부분을 정확히 분리하기 어렵다.
            2. **Heuristic Approaches**
                1. **항목 개수를 기준**으로 필터링 : **데이터의 문장 수, 단어 수, 문자 수** 등의 통계 기준으로 필터링
                    - C4 데이터셋은 5문장 미만의 페이지를 제거
                    - **MassiveText**는 50 ~ 100,000 단어 범위를 초과하는 문서를 제거
                2. **반복성** 필터링 : **반복적으로 등장**하는 n-gram, 문장, 문단이 많은 데이터를 제거
                    - MassiveText는 문서에서 반복된 문장이 30%를 넘으면 해당 문서를 제거
                3. **특정 패턴** 또는 **블랙리스트** 필터링 : 블랙리스트 단어나 패턴이 포함된 데이터를 제거
                    - C4는 **부적절한 단어 리스트**에 포함된 단어를 가진 문서를 제거
                    - **HTML 태그, 광고 문구, 오류 메시지** 등을 제거
                - 단순한 휴리스틱은 품질을 직접 판단하지 못하며, 유용한 데이터까지 제거할 위험이 있음
                - 새로운 휴리스틱의 효과를 검증하려면 많은 시간과 비용이 소요
            3. **Data Quality** : **고품질** 데이터를 선별해 모델 성능을 높이고, 불필요한 데이터를 제거
                1. **고품질의 참조 데이터셋**과 비교 : **고품질 참조 데이터셋 (위키피디아, 책, 뉴스기사 등)**을 기준으로 **유사성 점수를 계산**해 데이터 선택
                    - **GPT-3**는 WebText와 유사한 데이터를 포함시키는 분류기를 사용
                    - **FastText, n-gram, 해시 기반 분류기**로 대규모 데이터를 빠르게 처리
                        
                        ※ 참고
                        
                        - **FastText** : Facebook에서 개발한 언어 모델로, **텍스트를 빠르게 분류**하고 **유사성을 계산**
                        - **N-gram** : 텍스트를 일정 길이로 쪼개서 참조 코퍼스와 유사도를 비교
                        - **Hash** : 텍스트를 숫자로 변환해 비교를 간단하게 만든다.
                2. **퍼플렉시티 기반** 평가
                    - **참조 데이터셋 (위키피디아, 학술논문 등)**으로 학습된 언어 모델을 사용해 데이터의 퍼플렉시티 점수를 계산
                    - 퍼플렉시티가 낮을수록 참조 도메인에 가까운 데이터로 간주
                    - **CCNet**은 **5-gram 언어 모델**로 **문단별 퍼플렉시티를 평가**해 데이터를 필터링
                        
                        ※ 퍼플렉시티 (Perplexity)
                        
                        - 언어모델의 성능을 측정하는 지표로 “**모델이 다음 언어를 얼마나 잘 추측할 수 있는지 나타내는 점수**”
                        - 모델이 얼마나 혼란스러워하는가를 숫자로 표현하는 것
                        - **값이 낮을수록 모델이 더 잘 이해하고 예측**한다는 뜻
            4. **도메인 특화** 필터링
                1. **Moore-Lewis 필터링** : 특정 분야 (도메인)에 적합한 데이터를 고르는 방법. **어떤 데이터가 내가 원하는 분야 (의학, 법률 등)에 더 잘 맞는지**를 계산하는 방식
                    - 의학, 법률, 기술 등 **특화된 주제**에 대해 모델의 성능을 높이는 것이 목표이다.
                    - **두 개의 모델을 사용**하고, 특정 분야에서 학습된 도메인 모델과 일반적인 데이터에서 학습된 일반 모델을 가지고 새로운 데이터를 두 모델에 넣고, 각 모델이 이 데이터와 얼마나 잘 맞는다고 생각하는지 점수를 계산
                    - 도메인 모델의 점수가 일반 모델보다 높다면, 이 데이터는 도메인에 적합하다고 판단
            5. **중복 제거**
                - 데이터 효율성을 높이고 과적합을 방지한다.
                - **문서, 문장, n-gram 수준**에서 중복을 감지해 데이터셋을 축소
                - **CCNet**은 동일 문장을 포함한 문서를 제거
                - 고품질 필터링 없이도 **중복 제거만으로 모델 성능을 유지한 사례 존재**
                    
                    ※ **CCNet**
                    
                    - **Common Crawl**에서 수집된 웹 데이터를 기반으로 만든 대규모 텍스트 데이터셋
                    - Common Crawl의 Raw data를 정제하고, 고품질 텍스트를 추출해 자연어 처리 모델 학습에 사용하기 위해 만들어짐
    2. **Instruction Tuning**에서의 데이터 선택
        - 모델이 **사용자 명령 (instruction)을 이해하고 수행하는 능력을 학습**시키는 과정. 모델이 다양한 작업에서 정확하고 유용한 답변을 제공하도록 **특정 데이터셋을 선택하고 사용하는 것**이 핵심. 데이터는 **instruction (명령)과 output(결과) 쌍**으로 구성
            
            ![Image](https://github.com/user-attachments/assets/bab51d26-afcf-4e29-87ac-6293d7d30900)
            
        - **Instruction Tuning** 이란?
            - **모델이 사용자 명령 (instrunction)을 이해하고 원하는 결과 (output)를 생성하도록 학습하는 방법**. 구글의 **FLAN(Finetuned Language Models are Zero-Shot Learners)** 논문에서 처음 나온 개념.
        - **Instruction** 이란?
            - **사용자가 모델에 전달하는 명령어 또는 요청**으로 task의 유형과 맥략을 제공해 모델이 무엇을 해야 하는지 이해할 수 있게 만든다.
                
                ![Image](https://github.com/user-attachments/assets/b4517bd9-9152-4f89-a491-8d2980f9dfd0)
                
        - 데이터 선택 방법
            1. **데이터 다양성 확대**
                1. 다양한 작업 포함
                    - 여러 종류의 작업을 학습시켜 모델이 다양한 작업을 처리할 수 있도록 만듦.
                    
                    | 작업 종류 | 예시 |
                    | --- | --- |
                    | 요약 작업 | 이 문서를 요약하세요. |
                    | 질문-응답 | 이 텍스트에서 “화성”에 대한 정보를 찾아주세요. |
                    | 번역 작업 | 이 문장을 영어로 번역하세요. |
                2. 질문-응답 형식 통합
                    - 다양한 작업을 질문과 답 형식으로 통일
                3. 데이터 증강
                    - HuggingFace, TensorFlow Datasets와 같은 **오픈 소스 데이터셋**에서 증강
                    
                    | 증강 방법 | 설명 |
                    | --- | --- |
                    | 번역 (Translation) | 데이터를 여러 언어로 변환해 데이터의 다양성 증가 |
                    | 입력 반전 (Input Inversion) | 입력과 출력을 뒤바꿔 새로운 데이터를 생성 |
                    | 부정 예제 (Negative Example) | 잘못된 답변을 포함시켜 모델이 오류를 학습하고 피할 수 있도록 함. |
            2. **템플릿 다양화**
                - 다양한 형식의 명령과 데이터를 학습에 포함시켜 모델이 더 많은 스타일의 요청에 적응할 수 있도록 하는 방법
                
                | 템플릿 | 설명 | 예시 |
                | --- | --- | --- |
                | Zero-Shot | 예제 없이 명령만 제공 | Translate this sentence to Korean: “The weather is nice today” |
                | Few-Shot | 명령과 몇 가지 예제를 함께 제공 | Translate the following sentences to Korean:
                - 예제 1 : I love programming. ⇒ 나는 프로그래밍을 좋아합니다.
                - 예제 2 : This is a book. ⇒ 이것은 책입니다.
                - 실제 작업 : She is reading a book. |
                | Chain of Thought | 단계별 추론 과정을 포함한 명령 | Translate this sentence to Korean **step by step**:
                ”How many apples are there if you have 5 apples and eat 2?” |
                
                ※ **Chain of Thought**
                
                - LLM의 추론 능력을 향상시키기 위한 프롬프트 기법
                - **모델이 문제를 단순히 정답만 도출하는 대신, 추론 과정을 단계별로 표현하도록 유도하는 방식**
            3. **데이터 균형 유지**
                - 특정 작업이나 대규모 데이터셋이 학습을 독점하지 않도록 조정
                    - **샘플링 제한** : 한 작업이나 데이터셋에서 사용하는 **데이터 수를 제한**
                    - **가중치 적용** : 저자원 작업 (**드문 언어나 복잡한 작업**)에 **더 높은 가중치**를 부여
                    
                    | 설명 | 데이터 | 적용 후 |
                    | --- | --- | --- |
                    | 샘플링 제한 | 데이터셋 구성:
                    - 뉴스 번역 : 100,000 문장
                    - 소설 요약 : 10,000 문장
                    - 의학 논문 번역 : 1,000 문장 | 샘플링 적용 후
                    - 뉴스 번역: 5,000개
                    - 소설 요약: 5,000개
                    - 의학 논문 번역 : 1,000개
                    **⇒ 균형 조정** |
                    | 가중치 적용 | - 일반 대화 데이터 : 80%
                    - 기술 도메인 데이터 : 20% | 가중치 적용 후
                    - 기술 도메인 데이터를 40%로 조정하여 더 자주 학습 |
    3. **Alignment**에서 데이터 선택
        - **Alignment**는 모델이 사용자 의도와 윤리적 기준에 맞춰 응답하도록 **조정, 편향, 제거, 유해 데이터 필터링** 등을 통해 안전한 서비스를 만들 수 있음.
            
            ![Image](https://github.com/user-attachments/assets/f7e57804-5630-4195-a838-4acc8b04ce75)
            
        - 데이터 선택
            1. **편향 및 유해성 데이터 필터링**
                - 사용자가 입력한 요청이 부적절하거나 위험한 경우, 이를 적절히 처리하도록 설계
                    1. **입력 필터링**
                        - 사용자가 입력한 프롬프트를 사전에 검사
                            - 예시) 욕설, 증오 표현, 비윤리적 요청 (해킹 방법 요청 등)이 포함된 프롬프트를 감지
                        - 구현 : 키워드 필터링, 금지 패턴 감지
                    2. **안전 메시지 제공**
                        - 부적절한 요청에 대해 적절히 거부하거나 안전한 메시지를 반환
                            - 예시) 프롬프트 : “폭력을 조장하는 방법을 알려줘” / 응답 : “죄송하지만, 요청하신 내용은 제공할 수 없습니다.”
            2. **사용자 피드백 시스템 구축**
                - 사용자 피드백 시스템 구축
                    1. 피드백 버튼 추가 : 사용자가 모델 응답에 대해 “유용함” 또는 “부적절함”을 표시할 수 있도록 UI 설계
                    2. 피드백 데이터 활용 : 부적절한 응답 데이터를 수집하여 프롬프트를 개선하거나, 더 나은 응답을 도출하는 규칙을 추가
                    3. 실시간 개선 : 반복적인 피드백 루프를 통해 서비스 품질을 점진적으로 향상
    4. Task-specific Fine-tuning
        - 특정 작업에 최적화된 서비스를 제작하려면 **Task-Specific Fine-Tuning 과정**에서 **관련성 높은 데이터를 신중히 선택**하고 이를 통해 **모델이 목표 작업에 최적화되도록** 해야 한다.
            
            ![Image](https://github.com/user-attachments/assets/5ab1cc4a-37be-41c6-93d9-d56cc9addc53)
            
        - 데이터 선택
            1. Task와 직접적으로 관련된 데이터를 수집
            2. 고품질의 데이터 확보
            3. 적절한 양의 데이터 필요, 너무 적거나, 너무 많으면 새로운 데이터나 테스트 데이터에 대한 성능이 떨어지는 과적합 (overfitting)이 일어남
            4. 데이터의 다양성을 높이기 위해 증강
            - GPT-4는 Fine-Tuning이 불가능하지만, GPT-3.5 Turbo는 Fine-Tuning을 지원
            - Solar Pro Preview / Solar Mini는 Huggingface에 오픈되어 있어 활용 가능하다
            - 지원하는 Fine-Tuning 기능
                - **맞춤형 응답 생성** : **도메인 특화**된 데이터 학습
                - **특정 스타일이나 템플릿**을 따르는 응답 생성
            - 활용 방법
                - 오픈소스 모델들을 활용하여 Fine-tuning 데이터를 준비하고 업로드
                - Instruction 데이터를 기반으로 Fine-Tuning 진행

## 데이터 볼륨

### 1. 데이터 볼륨의 중요성

- LLM은 방대한 데이터로 학습되며, **데이터 볼륨이 크면 더 많은 언어 패턴과 지식을 학습할 기회가 생긴다**.
- 특히, Pretraining 단계에서 **데이터 양이 클수록 모델의 기본적인 언어 이해 능력이 좋아진다**.

### 2. 데이터 볼륨이 지나치게 클 경우의 문제점

1. **노이즈 증가**
    - 데이터 볼륨이 크더라도 품질이 낮거나 노이즈가 많은 데이터가 포함되면 성능에 부정적인 영향을 미친다.
        - 예시) 잘못된 문법, 의미없는 텍스트, 편향된 데이터
2. **과도한 학습 비용**
    - 데이터가 클수록 학습에 필요한 계산 차원과 시간이 증가
    - Pretraining 데이터셋의 크기가 클 경우, 학습 비용이 기하급수적으로 상승
3. **과적합 위험**
    - 동일하거나 유사한 데이터를 지나치게 많이 학습하면 모델이 특정 데이터 분포에 과적합될 수 있음.

---

# 데이터 선택과 볼륨 간 Trade-off 사례

## 적절한 데이터 볼륨과 데이터 선택 사례

### 1. Pretraining

- 최대한 방대한 데이터셋을 사용하되, 노이즈와 중복 데이터를 철저히 제거

| GPT-3 | - 방대한 데이터를 활용하여 GPT-3를 학습
- 데이터셋 : Common Crawl, WebText, Wikipedia 등
- **노이즈 필터링 기법** : 언어 검출기 (langdetect), 휴리스틱 필터링 등을 사용해 고품질 데이터를 선택 |
| --- | --- |
| T5 | - 방대한 데이터셋 (C4)로 학습한 모델로, 데이터 정제에 중점을 둠
- C4(**Common Crawl 데이터에서 필터링한 대규모 텍스트**)를 생성하여 모델 학습 |
| BERT | - **Wikipedia와 BookCorpus 데이터**를 사용하여 학습
- 데이터 볼륨은 상대적으로 적지만, **정제된 고품질 데이터**를 사용하여 성공적인 Pretraining 수행. |
| GPT-4o | - **OpenAI**에서 개발한 최신 언어 모델로, 텍스트, 음성 비전 등 다양한 모달리티를 실시간으로 처리할 수 있는 능력을 갖추고 있음 |
| Claude 3.5 | - **Anthropic**이 2024년 6월에 출시한 최신 AI 모델로, 이전 버전인 Claude 3 Opus 보다 두 배 빠른 속도와 5분의 1의 비용으로 향상된 지능을 제공
- 코드 생성, 시각적 데이터 추출, 복잡한 추론 등 다양한 작업에서 뛰어난 성능을 발휘 |
| Solar | - **업스테이지**에서 출시한 사전 학습 LLM
- 107억 개의 파라미터가 탑재, 자연어 처리 작업에서 Llama2, mistral-7B 등 기존 모델보다 뛰어난 성능을 발휘 |
| Llama2 | - **Meta**와 **Microsoft**가 개발한 오픈소스 LLM으로, 2조 개의 토큰과 최대 700억 개의 매개변수로 학습되었으며, 뛰어난 성능과 상업적 유용성으로 주목
- **긴 컨텍스트 처리**에서 우수한 성능을 보여 GPT-4와 유사한 요약 정확도를 30배 저렴한 비용하으로 제공 |
| Mistral | - 70억 파라미터를 갖춘 고성능 오픈소스 LLM
- 주요 벤치마크에서 Llama2 7B를 앞서며, **코드, 수학, 추론 작업에서도 우수한 성능**을 보여 자연어와 코드 생성에 적합 |
| vicuna 13B | - UC 버클리의 연구팀이 **Meta**의 Llama 모델을 기반으로, 70,000건의 **ChatGPT 대화 데이터를 활용**해 미세 조정한 오픈소스 챗봇으로, ChatGPT와 유사한 수준의 응답 품질을 제공 |

### 2. Fine-Tuning

- 데이터 볼륨보다는 **목표 작업과의 관련성과 품질**이 더 중요
- 특정 도메인 (의학, 법률) 에서는 소량의 고품질 데이터가 대규모의 일반 데이터보다 더 효과적

| Legal-BERT | - 법률 도메인에 특화된 BERT 모델
- 데이터셋 : 법률 문서, 판례 데이터 등 고품질의 도메인 특화 텍스트 사용
- 소량의 도메인 데이터로 BERT를 Fine-Tuning하여 법률 작업에서 성능 극대화 |
| --- | --- |
| BioBERT | - 생의학 데이터에 측화된 BERT 모델
- 데이터셋 : PubMed, PMC 등의 생의학 텍스트
- 일반 도메인 데이터를 Pretraining한 후 생의학 데이터를 Fine-Tuning |
| GPT-3 | - Fine-Tuning을 통해 특정 기업 또는 프로젝트에 적합한 GPT-3 모델 생성
- [Fine-Tuning 가이드](https://platform.openai.com/docs/guides/fine-tuning)  |

### 3. Few-Shot 또는 In-Context Learning

- 모델이 이미 Pretraining으로 충분한 지식을 학습했다면, 소량의 샘플만으로도 성능을 크게 개선할 수 있음
- 5 ~ 10개의 잘 설계된 예제로 높은 성능을 발휘

| Chain-of-Thought (CoT) Prompting | - **Chain-of-Thought Prompting**을 통해 **In-Context Learning** 성능 향상
- 소량의 입력 데이터를 제공하며, GPT-3가 복잡한 추론 작업을 단계적으로 수행 |
| --- | --- |
| CodeX | - GPT-3 기반으로 소량의 코드 예제로 Fine-Tuning 없이도 코드 생성 및 디버깅 작업 수행
- 사례 : 5 ~ 10개의 코드 스니펫만 제공하여 새로운 코드 생성 |
