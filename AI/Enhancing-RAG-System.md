# 벡터DB 검색 정확도 향상 기법

## 데이터 최적화

### Data Chunking

- Embedding의 단위가 되는 텍스트를 정하는 작업
- Retrieve 대상의 단위
- 단순히 길이를 기준으로 자르는 경우
    - 의미가 담기는 단위 : 단어/구/절/문장/문단
    - 단순히 길이를 기준으로 자르는 것은 좋지 않음
- 종류
    - **Semantic Chunker**
        - **의미가 비슷한 문장들을 묶을 수 있음**
        - Langchain의 구현체는 **Hierarchical Clustering**을 사용한다.
        - 텍스트 청킹 방식 : 임베딩 모델을 활용하여 문장을 임베딩한 후, **백분위 수, 표준편차 등의 분할 기준점에 따라** 의미가 유사한 문장들을 병합
        - 시간이 오래 걸림.
    - **Recursive Text Splitter**
        - 가장 대표적으로 사용되는 Chunking 방법론 중 하나
        - 큰 단위부터 순서대로 텍스트들을 분할해 주어진 최대 chunk_size를 넘지 않게 한다.
        - 파라미터
            - chunk_size : 하나의 chunk 크기
            - chunk_overlap : 어느 정도 겹쳐서 나눠주어서 텍스트가 부자연스럽게 나뉠 가능성을 낮춘다.

### Metadata

- 검색 대상의 external information을 추가하여 filtering이나 reranking에 활용
    - 직접적인 데이터 정보로 연관성이 있는 정보

### Preprocessing

- 원본 텍스트의 퀄리티가 Embedding 성능에 영향을 미침
- 데이터 전처리 방법론
    - 데이터 노이즈 제거 : 의미없는 특수문자, 비문 등을 제거하는 것이 좋음
    - 텍스트 정제 : 오타, 띄어쓰기 수정
    - 표현 통합 : 같은 의미를 가지지만 다르게 표현된 표현들은 하나의 형태로 통합하면 성능 향상에 도움
    - 언어 통일 : multilingual corpus의 경우, 번역기를 이용해서 하나의 언어로 통일하는 방법도 가능

### Embedding Model

- 오픈소스로 공개되어 있는 pretrained model을 사용
    - openAI, cohere, upstage
    - HuggingfaceEmbeddings → leaderboards 확인 해보기
- 선택 시 기준
    1. 해당 임베딩 모델이 어떤 텍스트를 학습했는지
    2. (특히 지원하는 언어의) 성능을 확인하는 것이 중요함.
    3. 일반적으로 임베딩 공간의 크기가 클수록 성능이 뛰어나며 대신에 inference 속도가 느림
    4. 대부분 최신에 나온 임베딩 모델일수록 성능이 높은 편
        - SOTA

※ Upstage Solar Embeddings

- 긴 텍스트와 문맥 정보를 효과적으로 처리하며, 높은 검색 정확도를 제공
- 우수한 다국어 성능 : OpenAI의 text-embedding-3-large를 능가하며, 영어, 한국어, 일본어 등 다양한 언어에서 뛰어난 성능 발휘
- 벤치마크 성과 : MTEB 및 MIRACL에서 우수한 성과 기록, 특히 까다로운 작업에서도 높은 성능 보여줌.

## 벡터DB 선택하기

### Vector Store

- 각 Vector Store (=Vector Index) 마다 지원하는 방식과 구현 상의 차이가 있음.
- 각 방식마다 개발된 목적이 다르기 때문에 **서비스 상황에 맞는 것**을 골라서 사용해야 함.
- 특히, 벡터 데이터베이스마다 지원하는 검색 알고리즘이 다름.
- 대표적인 벡터 데이터베이스 : FAISS, ChromaDB, Milvus, Pinecone, Quadrant, Redis

로컬 vs 클라우드 데이터베이스

- 로컬(Local)
    - 장점 : 데이터에 대한 완전한 제어권을 유지할 수 있고, 네트워크 의존성이 낮음.
    - 단점 : 데이터양이 많아질수록 레이턴시 증가
    
    ex) Chroma, FAISS
    
- 클라우드(Cloud)
    - 장점 : 확장성이 우수하고, 대용량 데이터에서도 빠른 성능을 제공함.
    - 단점 : 네트워크 의존성이 있음.
    
    ex) Pinecone, Weaviate
    

**FAISS**

- 2019년에 Meta에서 개발된 CPU/GPU를 지원하는 **벡터 인덱싱 기법**
- 주요 component들이 C++로 구현되어 있으며, 가장 오랫동안 개발되어 다양한 기능 제공
- 대규모 임베딩 벡터의 인덱싱용으로 개발되었으며, GPU-Acceleration을 지원하기 때문에 엄청나게 빠른 속도.
- 목적에 따라 IndexFlat2 (KNN), IndexIVFFlat, IndexHNSW (ANN), IndexPQ 등 다양한 인덱싱 기법 사용
    - FAISS 인덱싱 비교

## Retriever 최적화

### Retriever

- Sparse Retriever
    - TF-IDF : 상대 빈도
    - 키워드 위주로 사용해 메모리를 적게 사용하며 연산이 빠르지만, 문맥을 파악하기 어려워 성능이 떨어질 수 있음.
- Dense Retriever
    - SentenceBERT
        - contrastive learning : positive, negative를 구분해서 학습하도록 한다.
            - 가까울수록 similarity score가 높고, 멀수록 낮다.
    - 대부분 GPU를 필요로 하며 리소스가 더 많이 필요함.
    - 효율성을 극대화하기 위해 두 방법의 장점을 합친 모델을 생각해볼 수 있음.

### Ensemble Retriever

- Sparse과 Dense의 결과를 합치는 방식
- 단순하게 하며, 각 retriever마다 뽑은 K개의 문서들을 모두 RAG에 사용
- **reranking** 방식을 사용해 각 retriever들의 결과를 종합해서 사용

### Reranking

- 이전 검색 결과들을 질의에 적합하고 유용한 순서로 재정렬하는 방식
- 검색 결과와 metadata의 결합 등으로 기존에 정의된 계산 방식으로 score를 계산
- Learning to Rank, Neural Reranking model 등을 사용하기도 함.
- **RRF(Reciprocal Rank Fusion)**를 사용해서 재정렬 한다.

**Cross-Encoder**

- 주어진 문장들의 유사도 판정을 분류 모델로 정의하여 학습하는 방식
- 기존 Retriever는 질문과 문서를 독립적으로 활용하지만, reranker는 **질문과 문서를 동시에 분석**(self-attention)함.
- Pre-trained model을 사용해서 주어진 임의의 2개 pair가 **같은 의미인지(1) 아닌지(0)**를 학습
- Cross-Encoder의 Document A에 User Query를 넣고, Document B에 Candidate sentences를 넣어서 유사도 기준으로 reranking 한다.
