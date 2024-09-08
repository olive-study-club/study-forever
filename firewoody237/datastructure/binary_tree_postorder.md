# 이진 트리 후위 탐색
1. 왼쪽 서브 트리를 inorder(재귀 탐색)
2. 오른쪽 서브 트리를 inorder(재귀 탐색)
3. 루트 노드 방문

## Q. 다음과 같은 트리는 전위 탐색 시 어떤 순서로 검색할까?
![preorder1](./images/image029.png)

H
![preorder2](./images/image047.png)

H-D
![inorder3](./images/image048.png)

H-D-E
![inorder4](./images/image049.png)

H-D-E-B
![inorder5](./images/image050.png)

H-D-E-B-I
![inorder6](./images/image051.png)

H-D-E-B-I-J
![inorder7](./images/image052.png)

H-D-E-B-I-J-F
![inorder8](./images/image053.png)

H-D-E-B-I-J-F-K
![inorder9](./images/image054.png)

H-D-E-B-I-J-F-K-G
![inorder10](./images/image055.png)

H-D-E-B-I-J-F-K-G-C
![inorder11](./images/image056.png)

H-D-E-B-I-J-F-K-G-C-A
![inorder12](./images/image057.png)