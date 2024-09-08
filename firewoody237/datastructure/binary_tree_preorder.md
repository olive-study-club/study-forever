# 이진 트리 전위 탐색
1. 루트 노드 방문
2. 왼쪽 서브 트리를 preorder(재귀 탐색)
3. 오른쪽 서브 트리를 preorder(재귀 탐색)

## Q. 다음과 같은 트리는 전위 탐색 시 어떤 순서로 검색할까?
![preorder1](./images/image029.png)

A-B-D
![preorder2](./images/image030.png)

A-B-D-H-E
![preorder3](./images/image031.png)
![preorder4](./images/image032.png)

A-B-D-H-E-C-F-I
![preorder5](./images/image033.png)

A-B-D-H-E-C-F-I-J
![preorder6](./images/image034.png)

A-B-D-H-E-C-F-I-J-G-K
![preorder7](./images/image035.png)
![preorder8](./images/image036.png)