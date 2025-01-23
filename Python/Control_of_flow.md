# Control of Flow

- **제어문 Control Statement**
  - 코드의 **실행 흐름을 제어**하는 것에 사용되는 구문
  - **조건**에 따라 코드 블록을 실행하거나 **반복**적으로 코드를 실행
  - 종류
    - 조건문 : if, elif, else
    - 반복문 : for, while
    - 반복문 제어 : break, continue, pass

---

## 조건문

- 주어진 조건식을 평가해서 해당 조건이 **참**(True)인 경우에만 코드 블록을 실행하거나 건너뜀.

### if statement

**if statement의 기본구조**
```
if 표현식:
    코드 블록

elif 표현식:
    코드 블록

else:
    코드 블록
```

---

## 반복문

- 주어진 코드 블록을 **여러 번 반복**해서 실행하는 구문

### for statement

- 임의의 시퀸스 항목들을 그 시퀸스에 들어있는 순서대로 반복

**for statement의 기본구조**
```
for 변수 in 반복 가능한 객체:
    코드 블록
```

- 반복 가능한 객체 iterable : 반복문에서 순회할 수 있는 객체 (시퀸스 객체 뿐만 아니라 dict, set 등도 포함)

### while statement

- 주어진 조건식이 참(True)인 동안 코드를 반복해서 실행 (= 조건식이 거짓이 될 때까지 반복)

**while statement의 기본구조**
```
while 조건식:
    코드 블록
```

- while문은 반드시 **종료 조건**이 필요하다.

### 반복 제어

- for 문과 while은 매 반복마다 본문 내 모든 코드를 실행하지만, 때때로 일부만 실행하는 것이 필요할 때가 있음.

1. break

  - 반복을 즉시 중지

2. continue

  - 다음 반복으로 건너뜀

3. pass

  - 아무런 동작도 수행하지 않고 넘어감

### List comprehension

- 간결하고 효율적인 리스트 생성 방법

