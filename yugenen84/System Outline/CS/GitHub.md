- 용어정의
    - git squash 는 여러개의 commit 을 하나의 commit으로 만들 때 사용한다
    - git rebase 는 두 개의 공통 base 를 가진 브랜치에서 A브랜치의 base를 B브랜치의 최신 커밋으로 base 를 옮기는 작업을 의미함

- 여러개의 커밋을 잘못 PR하였을 경우
    1. Rebase 
        - 잘못된 커밋 전체를 Rebase 하는 명령어
        - 만약 Rebase 할 게 2개라면 __"HEAD ~2"__ 로 작성한다 
        - ```
           git rebse -i HEAD ~3
          ``` 

    2. vi 창과 같이 rebase 명령어가 실행이 된다 
        - ![](2024-10-06-07-30-26.png)
        - 1의 commit 에 2,3, 의 commit가 필요한 경우 아래와 같이 변경한다
        - ```
           pick -> S (squash)
          ```
        - ![](2024-10-06-07-33-47.png)
        - :wp 를 눌러 저장 및 종료를 한다


    3. 커밋 메시지 수정하기
        - 커밋 메시지를 수정하고 :wp를 눌러서 저장 및 종료를 한다


    4. rebase 후 PUSH하기
        - reposiory 의 원래 브랜치로 push 한다
        - ```
           git push origin -f
          ```

- Rebase Flow 
    - main에서 최신 pull을 받는다.
    - push할 브랜치로 이동한다.
    - 아래 명령어 실행
      ```
       git rebase -i master
      ```
      
    - 빔에디터가 뜨면 pick과 squash를 정하고 나간다. 그럼 commit 내역의 빔에디터가 또 나온다.
    - 글 앞에 #은 주석이다. 기존 commit 명을 전부 지워준다.
    spuash한 commit들의 이름을 적어준다.
    - ```git rebase --continue``` 로 진행 완료
    - ```git push origin 브랜치명 -f``` 로 push한다.
    - commit 명을 변경하고 싶다면 ```git rebase -i master``` 로 해당 commit을 pick → edit으로 변경하고 나와 commit 명을 수정하고 ```git commit --amend``` 로 변경사항을 저장
    - rebase 중간에 실수를 해서 rebase 이전으로 가고 싶다면 ```git rebase --abort``` 를 실행한다.

        
