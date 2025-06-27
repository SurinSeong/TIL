# Advanced Text Chunking

- RAG를 위한 벡터 검색의 성능을 향상시키기 위한 효과적인 전략 중 **하나는 데이터를 작은 chunk로 나누는 것**
    - LLM은 **context 창의 크기가 제한**되어 있어 정보 입력을 무한정으로 할 수 없고, **필요하지 않은 정보**가 들어가면 output의 품질도 낮아지며, 컨텍스트가 **너무 길면 중간 부분의 컨텍스트를 제대로 반영하지 못**하는 현상이 있기 때문이다.

⇒ 언어 모델에 **필요한 정보만 제공**하고, **필요 이상의 정보를 배제**하는 것이 중요함.

## 간편하게 사용할 수 있는 chunking 방법

### 1. Character Text Splitter

- 문자 단위로 **특정 문자 개수 만큼**의 청크 크기로 분할함.
- **overlap**을 통해 맥락이 끊기는 문제를 완화할 수 있음

### 2. Recursive Text Splitter

- 특정 separator 문자에 우선순위를 두고, **청크 크기 내에서 separator 문자를 탐색**해 **우선순위에 따라 분할** 지점을 찾는다
    
    ※ 우선순위 : [”\n\n”, “\n”, “ “, “.”, “,”]
    

### 3. Document Specific Splitter

- PDF, HTML, Markdown 등의 문서 형식에 따라 적합한 splitter가 따로 있을 수 있음.

## 조금 더 발전된 방법들

### 1. Semantic Chunking

- 일단, **문장 단위**로 쪼갠 후, **문장 임베딩 간의 거리 관계**를 통해 문장을 클러스터링한 후, **chunk**로 묶는 방법.
    - **방향성 1.** 문장 간의 Embedding을 비교해서 hiearachical clustering을 하고, **positional reward**를 도입하는 방법.
    Hieararchical clustering을 하게 되면, **유사한 맥락의 문장이 여러 조각**으로 동떨어져 있어도, **하나의 chunk에 함께 묶일 수 있음**. 긴 문장 이후에 짧은 문장이 오는 경우가 있어서, 이 경우 의미가 망가질 수 있는데, positional reward가 이를 완화한다.
    - 방향성 2. 문장의 embedding sequence에서, **embedding간의 거리 sequence**를 만드는 방법
    기존의 순서를 온전히 보존한다. 먼저 document를 문장 시퀀스로 바꾼 후 각 문장을 임베딩하고, **전/후 문장 간의 임베딩 거리를 계산**해 **거리 시퀸스**를 만든다. 그런 후, **threshold**를 기준으로 분할할 지점을 찾는다.

### 2. Agentic Chunking

- chunking 작업 자체를 LLM에게 맡기는 방법
    - 프롬프팅으로 어떻게 작업해야하는지 알려준다.

### 3. SubDocument RAG

- 기존 RAG
    
    문서가 평균 m개의 chunk로 분할된다고 했을 때, n개의 문서가 있다면 총 n*m개의 데이터 포인프에 대해 벡터 검색을 해야 한다.
    
    ⇒ 검색 퀄리티와 속도 측면에서 비효율적..
    
- BM25와 vector search를 단계적으로 사용하는 시나리오
    1. **document summary**를 chunk의 **metadata**에 추가하고 요약된 문서로 먼저 벡터 검색을 수행한 후, 임베딩을 통한 검색을 나중에 수행하는 방법.
        
        ⇒ 이를 통해, global/local context를 모두 반영할 수 있다. 하지만, 요약문이 chunk를 설명하기에 지나치게 광범위한 내용을 담고 있다면, 두 번째 단계로, document를 sub-document, sub-document를 chunk로 나누는 방법이 있음.
        
    2. document를 sub-document, sub-document를 chunk로 나누는 방법.
        
        ⇒ chunk의 metadata에는 document가 아닌 **sub-document의 요약**이 들어가게 된다.
