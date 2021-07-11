# undoing

> 어떤 행위를 취소할 때 사용하는 명령어



**사전준비**

```bash
# git 초기화 & a.txt READ.md 파일 생성
```



## 1. 파일 상태를 Unstage로 변경하기

> Staging Area(INDEX)와 Working Directory(WA)를 넘나드는 방법

### 첫 번째 - `rm -cached`

- 따로 따로 커밋하려고 했지만 실수로 모두 `$ git add .`를 한 상황(처음으로 add를 하는 상황이라고 가정)

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        a.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add .

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage) # rm --cached를 써 ... 무대에서 내리고 싶으면..!
        new file:   README.md
        new file:   a.txt 
```

```bash
$ git rm --cached a.txt
rm 'a.txt'

$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt # 무대에서 내려옴!!
```

![](md-images/image-20210706143940012.png)

### 첫 번째와 두 번째 뭐가 다를까요?

```bash
$ touch b.txt

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md  # SA + commit이 한번이라도있었던 -> restore --staged

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in 
working directory)
        modified:   a.txt # WD + commit이 한번이라도 있었던 

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt # WD + commit이 한번도 안된 친구
```



1. `git rm --cached` <file 명>
   - 기존에 커밋이 없는 경우 SA -> WD로 내릴 때 사용

2. `git restore --staged <file 명>`
   - 기존에 커밋이 있는 경우 SA -> WD로 내릴 때 사용



## 2. Modified 된 파일 되돌리는 방법

add가 되어있지 않은(WD에 있는) + 수정된(modified) a.txt를 다시 돌려보자

- 일단 commit은 적어도 한번 있었고 수정되었음
- 하지만 SA에 올라가지 않은 상태



**주의!!!!!!!**

- 원래 파일로 돌아갔기 때문에 '절대로' 다시 되돌릴 수 없음
- 수정한 내용이 마음에 들지 않을 때만 사용해야 함(정말 마음에 안들때만 사용해야함)

```bash
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in 
working directory)
        modified:   a.txt # 이녀석을 수정 전 상태로 돌릴 예정

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```



```bash
# 기존에 a.txt에 작성된 내용이 모두 사라짐
$ git restore a.txt

# status -> 애초에 commit으로 남기지 않았기 때문에 돌릴 수 없음
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```



## 3. 완료된 커밋 수정

```bash
$ git commit --amend
```

1. 커밋 메시지를 잘 못 적은 경우 수정!!
   - 가장 최신의 commit만 수정 가능함..!
   - 역사를 바꾸려고 하면 안됨..!
2. 너무 일찍 커밋을 한 경우(무언가 빼먹고 commit을 진행한 경우)



**[주의사항]**

- 커밋 메시지를 바꾸면 커밋 해시값이 변하기 떄문에 원격 저장소에 업로드한 경우 커밋 메시지는 절대로 수정하지 말 것!



### 3.1 커밋 메시지 수정

- 수정을 진행하고 창을 닫아주시면 됩니다.

```bash
$ git add .
$ git commit -m "amend text file" # 오타가 났습니다..!
[master be49fae] amend text file
 1 file changed, 0 insertions(+), 0 deletions(-)    
 create mode 100644 a.txt
 
 # 수정 진행
 $ git commit --amend
[master 16c870a] amend text
 Date: Tue Jul 6 15:12:07 2021 +0900
 1 file changed, 0 insertions(+), 0 deletions(-)    
 create mode 100644 a.txt
 
 amend text file

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Tue Jul 6 15:12:07 2021 +0900
#
# On branch master
# Changes to be committed:
#	new file:   a.txt
#

# 수정을 진행하고 창을 닫으면 아래와 같이 정상적으로 커밋이 수정됩니다.
$ git commit --amend
[master c060efc] amend text
 Date: Tue Jul 6 15:12:07 2021 +0900
 1 file changed, 0 insertions(+), 0 deletions(-)    
 create mode 100644 a.txt
```



### 3-2. 어떠한 파일을 빼먹고 commit을 한 경우

> 다시 커밋을 하고 싶으면 수정 작업을 하고 SA에 추가한 다음 `--amend` 옵션을 사용하여 커밋 재작성

```bash
$ touch foo.txt bar.txt
$ git add foo.txt
```

```bash
# 상태 확인
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   foo.txt # SA + new file -> commit이 한번도 없었던 상태

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bar.txt # WD
```



```bash
# 실수로 bar.txt를 빼먹고 커밋을 진행함
$ git commit -m "foo & bar"
[master 4b10064] foo & bar
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 foo.txt

# log
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        bar.txt # bar는 WD에 남아있음!

nothing added to commit but untracked files present (use "git add" to track)
```



**해결하기**

```bash
$ git add bar.txt 
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   bar.txt

# 원래라면 commit을 진행하지만 이 경우는 commit --amend
# 편집기 화면에서 x 버튼을 눌러서 닫아주면 됨 (아까와 다르게 commit 메시지 자체를 잘못쓴건 아님)
foo & bar

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Tue Jul 6 15:16:33 2021 +0900
#
# On branch master
# Changes to be committed:
#	new file:   bar.txt
#	new file:   foo.txt
```

```bash
# 상태 확인
$ git status
On branch master
nothing to commit, working tree clean

# log 확인
$ git log --oneline
66dce89 (HEAD -> master) foo & bar # 새로운 커밋이 생긴게 아니라 기존 커밋에 bar.txt의 변경 사항만 추가됨
593efc0 amend text file
a2fba93 first commit
```

