# Tree 심화

## BST 문제 제시

- BST 구조는 삽입되는 데이터의 순서에 따라 결정되기 때문에 특정 패턴으로 삽입되는 경우, 불균형이 발생

## AVL (레드블랙트리의 쉬운 버전)

- 정의
    - 균형 이진 탐색 트리의 일종
    - 모든 노드에서 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이가 최대 1이하인 자료구조

- 특징
    - 노드를 삽입하거나 삭제할 때 자동으로 균형 유지
    - O(logN)
    - **균형 인수**
        - **-1, 0, 1** 중 하나 (각 노드의 왼쪽 서브트리의 높이와 오른쪽 서브트리의 높이 차이)
            - 범위를 벗어나면 **회전 연산**을 통해 균형 복원
         
- 단일 회전
    - 불균형이 한쪽 서브트리에 집중되어 있을 때 사용

    - LL 회전
        - 왼쪽 자식이 왼쪽 서브트리로 인해 불균형이 발생한 경우
        - 오른쪽으로 회전하여 불균형을 해결한다.
        - 부모 노드의 균형인수: +2, 왼쪽 자식 노드의 균형 인수 : +1 또는 0

    - RR 회전
        - 오른쪽 자식이 오른쪽 서브트리로 인해 불균형이 발생한 경우
        - 오른쪽으로 회전하여 불균형을 해결한다.
        - 부모 노드의 균형인수: -2, 오른쪽 자식 노드의 균형 인수 : -1 또는 0

- 이중 회전

    - LR 회전
        - 왼쪽 자식이 오른쪽 서브트리로 인해 불균형이 발생한 경우
        - 왼쪽 자식에 대해 왼쪽으로 회전한 다음, 자신에 대해 오른쪽으로 회전
        - 부모 노드의 균형인수: +2, 왼쪽 자식 노드의 균형 인수 : -1
    - RL 회전
        - 오른쪽 자식이 왼쪽 서브트리로 인해 불균형이 발생한 경우
        - 오른쪽 자식에 대해 오른쪽으로 회전한 다음, 자신에 대해 왼쪽으로 회전
        - 부모 노드의 균형인수: -2, 왼쪽 자식 노드의 균형 인수 : +1

### 주요 연산

- 삽입
    - BST 규칙에 따라 노드를 삽입한다.
    - 균형인수 확인한다. (아래 -> 위)
    - 맞지 않으면 회전한다.


### 정리

- 회전을 이용해 균형을 유지한다.
- 삽입, 삭제, 탐색 시간을 logN으로 유지한다.

## 레드블랙트리

- 회전 사용
- 레드, 블랙을 사용해 회전 횟수를 줄인다.
- 균형인수를 엄격하게 검사하지 않는다. (유연함)
- 실무에서 많이 쓰인다.

## B Tree

- 하나의 노드가 여러 자식(둘 이상)을 가지고 있음
- 실제 쓰는 데이터는 리프 노드에서 관리한다.

## B+ Tree

- 실제 데이터 베이스가 데이터를 관리하는 원리
