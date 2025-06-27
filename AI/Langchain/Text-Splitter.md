# Text Splitter

## 역할

1. 작고, 의미기반의 단위로 텍스트를 쪼갠다.
2. 사용자가 정한 특정한 크기가 될 때까지 작은 조각을 더 큰 조각으로 합친다.
3. 특정 크기가 되면, 조각을 만들고, 이전 내용을 조금 포함해서 새로운 조각을 만든다.

## 커스터마이징

1. 어떻게 텍스트가 쪼개질 것인가?
2. 어떻게 조각크기를 측정할 것인가?

## 종류

| 이름 | 클래스명 | 쪼개는 방법 | 메타데이터 추가여부 | 설명 |
| --- | --- | --- | --- | --- |
| Recursive | `RecursiveCharacterTextSplitter`,
`RecursiveJsonSplitter` | 사용자가 정한 대로 쪼갠다 | X | **텍스트 간의 연관성**을 지키기 위한 방식.
추천! |
| HTML | `HTMLHeaderTextSplitter`,
`HTMLSectionSplitter` | HTML 특화 | O | **HTML 특화 방식**으로 텍스트를 쪼갠다.
조각들이 어디 있는지에 대한 정보를 추가할 수 있음. |
| Markdown | `MarkdownHeaderTextSplitter` | Markdown 특화 | O | **Markdown 특화 방식**으로 텍스트를 쪼갠다.
조각들이 어디에 있는지에 대한 정보를 추가할 수 있다. |
| Code | many languages | Code (Python, JS) 특화 | X | **코딩 언어**에 특화된 쪼개기 방식을 사용한다.
15개의 언어를 선택할 수 있다. |
| Token | many classes | Tokens | X | 토큰으로 텍스트를 쪼갠다.
여러 토큰 측정 방식이 있다. |
| Character | `CharacterTextSplitter` | 사용자 정의 | X | 특징을 정의해서 텍스트를 쪼갠다.
가장 심플한 방법 중 하나. |
| Semantic Chunker | `SemanticChunker` | 문장 | X | 문장 단위로 자른다. 그 다음, 의미적으로 비슷한 것끼리 합친다. |
| AI21 Semantic Text Splitter | `AI21SemanticTextSplitter` |  | O | **특정 토픽**으로 나눈다. |
