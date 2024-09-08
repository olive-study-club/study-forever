# 이진 트리 중위 탐색
1. 왼쪽 서브 트리를 inorder(재귀 탐색)
2. 루트 노드 방문
3. 오른쪽 서브 트리를 inorder(재귀 탐색)

## Q. 다음과 같은 트리는 전위 탐색 시 어떤 순서로 검색할까?
![inorder1](./images/image029.png)

D
![inorder2](./images/image037.png)

D-H-B
![inorder3](./images/image038.png)

D-H-B-E
![inorder4](./images/image039.png)

D-H-B-E-A
![inorder5](./images/image040.png)

D-H-B-E-A-I
![inorder6](./images/image041.png)

D-H-B-E-A-I-F
![inorder7](./images/image042.png)

D-H-B-E-A-I-F-J
![inorder8](./images/image043.png)

D-H-B-E-A-I-F-J-C
![inorder9](./images/image044.png)

D-H-B-E-A-I-F-J-C-G
![inorder10](./images/image045.png)

D-H-B-E-A-I-F-J-C-G-K
![inorder11](./images/image046.png)