## branch command

```bash
$ git init
Initialized empty Git repository in C:/Users/NaEunSu/Desktop/branch_practice/.git/

$ touch a.txt
$ git add .
$ git commit -m "Finish a.txt"
[master (root-commit) dbeb5b7] Finish a.txt
 1 file changed, 0 insertions(+), 0 deletions(-)  
 create mode 100644 a.txt
```



- 브랜치 생성

  ```bash
  $ git branch 브랜치이름
  
  # 예시
  $ git branch feature
  ```

- 브랜치 목록 확인

  `*` 가 찍혀있는 것은 현재 위치한 브랜치를 의미함

  ```bash
  $ git branch
    feature
  * master
  ```

- 브랜치 이동

  ```bash
  $ git checkout 브랜치이름
  
  # 예시
  $ git checkout feature
  $ git branch
  * feature
    master
  ```

- 브랜치 생성 + 이동

  ```bash
  $ git checkout -b 브랜치명
  
  # 예시
  $ git checkout -b feature2
  Switched to a new branch 'feature2'
  
  $ git branch
    feature
  * feature2
    master
  ```

- 브랜치 병함(merge)

  - `HEAD`: 현재 브랜치의 최신 커밋

  ```bash
  # feature2 브랜치에서 b.txt 파일 생성 후 add, commit
  $ touch b.txt
  $ git add .
  $ git commit -m "Finish b.txt in feature2 branch"
  [feature2 a48ad8f] Finish b.txt in feature2 branch
   1 file changed, 0 insertions(+), 0 deletions(-)  
   create mode 100644 b.txt
   
   # master 브랜치로 이동
   $ git checkout master
  Switched to branch 'master'
  
   # merge
   $ git merge 머지할브랜치이름
  
   # 예시
   $ git merge feature2
  Updating dbeb5b7..a48ad8f
  Fast-forward
   b.txt | 0
   1 file changed, 0 insertions(+), 0 deletions(-)  
   create mode 100644 b.txt
   
   # 확인
   $ git log --oneline
  a48ad8f (HEAD -> master, feature2) Finish b.txt in feature2 branch
  dbeb5b7 (feature) Finish a.txt
  ```

- 브랜치 삭제

  ```bash
  # 
  $ git branch -d 브랜치이름
  
  # 예시
  $ git branch -d feature2
  Deleted branch feature2 (was 84a60bb).
  
  # 확인
  $ git branch
    feature
  * master
  ```

  

