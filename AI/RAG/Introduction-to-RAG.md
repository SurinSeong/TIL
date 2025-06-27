# RAG의 기본 개념 및 동작 원리

## RAG 정의 및 구성요소

### Retrieval Augmented Generation

- 텍스트를 생성해준다는 관점에서 LLM을 사용하는 것!

### Retrieval System + LLM

- 사용자의 질문(Question)에 대한 답변을 미리 저장해둔 정보를 (Knowledge)에서 찾고 (Retrieve) 찾는 내용을 합쳐 (Augmented) LLM으로 답변을 생성하는 방법
- RAG의 성능 조건
    1. 목적에 맞는 질문(**Question**)을 잘하고
    2. 외부 Knowledge를 잘 구축하고
    3. 외부 Knowledge 중 Question에 맞는 내용을 잘 검색하고 (**Retrieve**)
    4. 이를 바탕으로 LLM이 답변을 잘 생성 (**Generation**) 해야 함.
- **Retrieval System**
    - **Knowledge**는 사용자의 질문에 대해 정확한 답변을 제공하기 위한 용도로 구축된다.
        - **knowledge cutoff를 없애고 hallucination을 줄인다.**
    - Knowledge를 구축할 때는 Database를 사용하며, 어떤 정보를 처리할 것이냐에 따라 **RDBMS or Vector Store**를 사용한다.
    - RDBMS는 테이블 데이터를 다루는 용도로 사용되며, **Text2SQL**을 거쳐서 사용된다.
    ※ Text2SQL = user query → SQL
    - Vector Store는 이미지/텍스트를 주로 다루는 용도로 사용되며, **이미지/텍스트를 embedding vector로 변환**(의미 파악을 위해)하여 저장하는 용도로 사용된다.
    - **Knowledge Base (KB)** : 검색을 위한 데이터 베이스 구축
        - Knowledge가 저장된 Database를 의미함.
        - KB를 잘 구축하여야 Retrieval의 성능이 올라간다.
            - **검색이 될 자료**가 있어야 한다.
                - 검색이 될 자료 : 도메인 특화 지식!
    - **Retriever** : 사용자 질문에 도움이 되는 정보를 찾는 검색기
        - 질문과 유사성이 높은 자료를 찾는 것이 중요하다.
        - 질문과 관련된 자료를 잘 검색해서 찾는다.
            - 질문과 **유사도가 높은 자료** 중 **top 순위를 Ranking**해서 가지고 온다.
    - 구조화될 수 있는 정형 데이터의 경우, LLM으로 SQL을 생성해서 RDBMS에 접근한다.
    - 이미지/텍스트 같은 비정형 데이터의 경우, 질문을 벡터화한 후 Vector Store에 접근해서 유사도가 높은 문서를 top-K개 추출한다.
        - 유사도가 높은 → **KNN query**
        
        ![Image](https://github.com/user-attachments/assets/bf271ec0-5b8b-45c0-9b29-419a642bdcb7)
        
    
    ※ Augmented : 기존에 있는 것에 추가하는 것
    
    기존에 있는 것 : DB에 있는 정보
    
- **LLM**
    - RAG에서 답변을 잘 생성하기 위해서는 **LLM의 pre-training 성능이 중요**하다.
    - 주로 많은 token을 학습시킨 모델의 pre-training 성능이 높은 편이다. (**SOTA**)
    - 하지만, LLM은 knowledge-cutoff 문제가 있어, 항상 최신 데이터를 학습할 수는 없다.
    (대부분의 주요 LLM들이 23년 12월에 cut-off 되어 있다)
    - 이러한 한계점을 Knowledge Base에 최신 데이터를 추가해서 극복할 수 있다.

## RAG Pipeline 소개

### RAG를 구축하는 순서 (RAG 파이프라인)

![Image](https://github.com/user-attachments/assets/413fdc60-6233-4dcb-8e6d-c27bc033065b)

1. **Document Loading**
    - KB에서 **데이터를 가져오는** 작업
        - 연관된 것을 가져오는 것이 아니라 **그냥 들고 오는 것**.
    - 파일의 종류에 따라 langchain_community.document_loaders에 존재하는 구현체가 나뉨.
2. **Text Splitting**
    - 가져온 텍스트를 **chunk**로 나누는 작업.
        - chunk : 검색 단위
    - 어떤 단위로 나누냐에 따라 여러 구현체를 사용한다.
3. **Embedding**
    - 가져온 텍스트 데이터를 **컴퓨터가 이해할 수 있는 숫자**로 변환, 즉, 벡터 공간에 이식하는 작업
    - **임베딩 모델** (pretrained Model)이 있어야 한다. ⇒ 유사한 의미의 텍스트를 잘 추출하기 위해
    ※ Constrative learning : 임베딩 모델의 학습 방법
        - 임베딩 모델의 특징에 따라 잘하는 것이 달라서 도메인 특화 임베딩 모델을 사용해도 좋음.
    - chunk를 임베딩한다.
    - **질문-지식 간의 유사성** 계산이 가능하다.
4. **Vector Store (= Indexing)**
    - 저장한 embedding vector들을 빠르게 계산하기 위해 **Index를 만드는 작업**
    - Index를 만들어두면, 매번 검색할 때, 전 탐색을 수행할 필요없이 **빠르게 필요한 영역만 탐색이 가능하**다. ⇒ **efficient search**
        - O(KN) → O(KlogN)
    - 어떤 Indexing 방식을 쓰느냐에 따라 다양한 구현체가 존재한다.
5. **Retrieving**
    - vector store에서 사용자의 질문과 유사한 자료를 검색하는 과정 = **유사한 벡터 찾기!**
        - LLM이 응답을 생성할 때 **필요한 정보를 제공**한다.
    - Retriever 유형
        1. **Sparse Retriever (키워드 검색)** 
            - 사용자의 질문을 키워드 벡터로 전환해서 **키워드 기반 검색**을 진행한다.
            - **특정 도메인 지식** 등을 검색할 때 용이하다.
            
            ⇒ 대표 알고리즘 : TF-IDF, BM25
            
        2. **Dense Retriever (의미 검색)**
            - 사용자의 질문과 관련 있는 embedding vector를 찾는 과정
            - 요청한 K개의 유사성이 높은 vector를 찾고 해당 vector의 원본 텍스트를 반환
            - **Embedding Quality**에 따라 성능이 큰 영향을 받음.
6. **Generating**
    - 추가로 찾은 텍스트와 원본 질문을 함께 미리 디자인해 둔 **System Prompt의 형태로 LLM에 입력**으로 제공
    - Retrieval된 문서가 많을수록, 문서의 길이가 길수록, input prompt가 길어지기 때문에 생성되는 답변에 큰 영향을 줌.
        - generation에 도움이 되는 R을 해야 한다.
    - 사용하는 LLM의 token length도 고려해야 함.
