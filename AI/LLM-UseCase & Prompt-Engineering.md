# LLM Use Case Study 및 Prompt Engineering

## LLM Use Case Study

### LLM 서비스의 가치

- 기존 오픈소스 API를 가져다가 쓰기만 한다면 새로운 서비스로서의 가치를 창출하기 어려움.
    1. 서비스 관점에서 사용자가 느끼기에 편리한 UX를 제공
    2. 서비스의 **품질을 개선**
    
    ⇒ 이 중 서비스의 “품질을 개선”하기 위해서는 LLM의 한계점들을 극복해나가는 것이 중요하다.
    

### 다양한 LLM Task

- **QA** (Question Answering)
- Extraction
- Classification
- **Chatbot**
- Translation
- Comparison
- Summarization
- Code Generation

### 산업에서 적용되는 LLM 기반 서비스

- (Most Common) 도메인 특화 QA ChatBot 서비스
    - 현재까지의 질의응답 모델을 챗봇 형태로 수정
    - 담당자들끼리 소통을 할 때 생기는 딜레이나 전달 오류를 개선할 수 있음
    - LLM의 한계 중 하나인 Hallucination이 발생할 수 있기 때문에 정확한 지식 체계를 갖춰서 답변하는 것이 중요함.
    
    ⇒ RAG를 활용해서 **외부 지식을 검색해서 넣어주는 기능**이 필요함.
    
    ![Image](https://github.com/user-attachments/assets/24dbf5c5-c184-4713-86d7-1c2859e1f68a)
    
- 결론
    - 각 도메인마다 사용되는 모든 자연어 task들, 즉, **사람들이 읽는 자연어에서 패턴이 있는 대량의 지적 행동**을 대체할 수단이 된다.
    - 큰 규모로 대체되면 상당한 기술적 효용성을 가져올 수 있음.
    - 단, **LLM의 한계를 극복하고 정확한 정보를 제공하는 것**이 LLM 기반 서비스에서의 핵심이다.
    
    ![Image](https://github.com/user-attachments/assets/ff7834f1-856b-4a93-831e-79a1ca44fd0a)
    

## Prompt Engineering

### AI와 즐겁게 대화하는 법

- Prompt Engineering
    - **Prompt**란? LLM으로부터 사용자가 원하는 결과를 도출하기 위한 Input
    ⇒ AI 모델에게 내리는 지시사항이나 대화 시작의 물꼬
    - Prompt Engineering
        - LLM이 생성하는 결과물의 품질을 높일 수 있는 **Prompt 입력값들의 최적의 조합**을 찾는 작업
        
        ⇒ 거대 언어 모델을 효율적으로 사용할 수 있도록 프롬프트를 개발하고 최적화하는 방법을 연구하는 분야
        
        - LLM이 쿼리를 더 잘 이해하고 답변하도록 도와주는 역할
        - 도메인에 대해서 잘 알아야 하고, 경험이 많아야 한다.
- 절대 LLM 기반 서비스를 어렵게 대하지 말 것.
    - 질문을 완벽하게 다듬어 제출하기보다는 **빠르게 피드백을 받고 수정하는 방식**이 더 효과적이다.
1. Zero-shot Prompting
    - 그냥 바로 물어보는 것, **예시가 없는 케이스**
2. Few-shot Prompting
    - **예제 몇 개**와 함께 물어보는 것
3. **Chain of Thought (CoT)**
    - 마치 사람의 뇌가 단계적으로 계산을 하는 과정처럼 **여러 단계의 추론 과정을 LLM에게 학습시켜 LLM의 추론 능력을 향상**시키는 기법
    - 논리적 전개를 구체적으로 할 수 있을수록 답변도 정확하게 나온다!
    - **Step by Step**을 부여함.
4. Self-consistency Prompting
    - CoT Prompting을 발전시킨 방법으로, **여러 추론경로를 만들어서 일관된 답변을 채택**하는 방식.
