# [Langchain] RunnablePassthrough

## 1. 기본적인 RAG 구성 방법

- 일반적으로 vector store를 검색하고 그 결과를 llm으로 던져서 결과를 가져온다.
    - retriever에서 get_relevant_documents 또는 invoke를 통해 검색 후, chain을 통해 호출한다.

## 2. LCEL 방식을 사용한 호출

- chain에서 한번에 처리할 수도 있다.
- retriever를 인자로 넘길 때, 자동으로 invoke가 호출된다.

```python
chain = (
	{"context": retriever}
	| prompt
	| model
	| StrOutputParser()
)

result = chain.invoke({"input": "월드컵 경기장 근처 관광지는 어디가 유명해?"})
```

⇒ `invoke`는 str 타입을 사용해야 하기 때문에 오류 발생한다.

- input 값을 str로 바꿔주기 위해 `RunnablePassthrough`를 통해 같이 넘기는 방식을 사용한다.

```python
chain = (
	{"context": retriever, "question": RunnablePassthrough()}
	| prompt
	| model
	| StrOutputParser()
)

result = chain.invoke("월드컵 경기장 근처 관광지는 어디가 유명해?")
```

⇒  `retriever`는 `Runnable` 타입이기 때문에 `invoke`가 자동으로 호출되고,
`RunnablePassthrough`는 `chain.invoke`에 입력된 파라미터가 전달된다.

- prompt의 문서를 format하고 싶으면 `format_docs` 함수를 추가해서 사용한다.

```python
def format_docs(docs):
	return "\n\n".join(doc.page_content for doc in docs)

chain = (
	{"context": retriever | format_docs,
	 "question": RunnablePassthrough()}
	| prompt
	| model
	| StrOutputParser()
)
```

⇒ 문서의 내용만 llm에게 전달

## 3. prompt에 파라미터를 추가하는 경우

- prompt에 현재 시간을 추가적으로 넘기는 경우

```python
template = \
"""
Answer the question based only on the following context:
{context}

current date: {current_date}
Question: {question}
"""
```

⇒ 기존 prompt에 `current_date` 추가 → `RunnablePassthrough.assign`을 통해 사용

```python
def current_date():
	return "2024-09-22"
	

chain = (
	{
		"context": retriever | format_docs,
		"question": RunnablePassthrough(),
	}
	| RunnablePassthrough.assign(current_date=lambda x: current_date())
	| prompt
	| model
	| StrOutputParser()
)
```

⇒ 기존 context, question 외에 current_date 가 파라미터로 넘어감. `current_date()`를 함수로 정의하고 `RunnablePassthrough.assign`를 통해 함수의 결과를 리턴하도록 하면 된다.

- `RunnablePassthrough.assign`의 역할

```python
rag_chain_from_docs = (
	RunnablePassthrough.assign(context=(lambda x: format_docs(x["context"])))
	| prompt
	| model
	| StrOutputParser()
)
```

⇒ `RunnablePassthrough.assign`을 사용해서 입력 데이터에서 “context”키에 해당하는 값을 가공해 `format_docs` 함수로 변환한 후, 새롭게 “context” 필드에 할당한다. 이 변환된 값은 이후의 체인(`prompt`, `model`, `StrOutputParser`)으로 전달

→ `RunnablePassthrough.assign`은 Langchain에서 제공하는 `Runnable` 인터페이스 중 하나, **입력 데이터를 그대로 전달**하거나, **입력 데이터에 새로운 값을 추가해서 출력**을 생성하는 것에 사용됨.

→ `RunnablePassthrough`는 주로 **입력을 수정하지 않고 그대로 전달할** 때 유용, 여기에 `.assign` 메소드를 사용하면 **입력 데이터에 추가적인 키-값 쌍을 쉽게 할당**할 수 있음.

- `RunnablePassthrough.assign`의 작동 방식
    - **입력 그대로 전달** : `RunnablePassthrough`는 **입력 데이터를 가공하지 않고 그대로 전달**하는 역할을 함.
    - **키-값 쌍 추가** : `.assign` 메소드를 사용하면 **입력 데이터를 유지하면서 추가적으로 지정된 값들을 입력에 할당**함. ex) 딕셔너리 형태의 입력에 새로운 키-값을 추가하고 싶을 때 유용함.
