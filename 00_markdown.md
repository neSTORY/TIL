.git 이란 파일이 있으면 git이 관리한다는 뜻( git bash에서 dr에 master라고 표시됨)

# 1. Git 초기 설정

**커밋 작성자(author) 설정**

- 최초 1회 설정하면 됨
- 만약 설정을 하지 않고 진행하면 commit 메시지를 남기는 상황에서 아래와 같은 에러 발생

```bash
$ git commit -m "Initial commit"
Author identity unknown # 이거 누가 쓴지 모르겠음

*** Please tell me who you are. # 누군지 좀 알려줘!

Run # 이거 따라하면 됨

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'NaEunSu@DESKTOP-8P8V5RH.(none)')

```

```bash
# author 설정
$ git config --global user.email "nes2376@gmail.com"
$ git config --global user.name "neSTORY"

# 설정 확인
$ git config --global --list # -l(소문자)
user.email=nes2376@gmail.com
user.name=neSTORY
```

**(추가 설정) 커밋 편집기 변경**

- 편집기 설정
- 기본 텍스트 편집기를 `vim`에서 `vscode` 로 변경하는 것

```bash
$ git config --global core.editor "code --wait"
```



# 2. Git Basic

> 주의사항!!
>
> .git 폴더가 또 다른 폴더 내부에 있으면 안됨!(git 속 git은 절대 금지!!)

### status

> 현재 git이 관리하는 폴더의 파일과 폴더 상태를 알려주는 명령어(working directory &staging area를 확인하는 명령어)

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt

nothing added to commit but untracked files present (use "git add" to track)

```

### add

> WD -> SA로 올리는 과정

```bash
$ git status
On branch master

No commits yet

Changes to be committed: # 커밋 되어질 변경 사항들
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

Untracked files: # git이 아직 변경 사항을 추적하고 있지 않은 친구들
  (use "git add <file>..." to include in what will be committed)
        b.txt

```

```bash
$ git add a.txt # 특정 파일을 WD -> SA
$ git add # 해당 디렉토리(하위 디렉토리 모두 포함)의 모든 폴더 & 파일을 SA
$ git add my-folder/ # 특정 디렉토리를 WD -> SA
```

### commit

- commit을 통해서 하나의 버전으로 기록됨
- commit 메시지는 현재의 변경 사항을
- commit 내역 확인은 $ git log 로 확인 할 수 있음

```bash
# commit 메시지의 기본구조
# -m(message)
$ git commit -m "남기고 싶은 메시지"
```

```bash
$ git commit -m "Initial commit"
[master (root-commit) a9b383d] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt

# commit 내역 확인
$ git log
commit a9b383d5a139c0ddd1c48ae7df221e995a34e8ce (HEAD -> master)
Author: neSTORY <nes2376@gmail.com>
Date:   Mon Jul 5 15:25:44 2021 +0900

    Initial commit
# commit 이력을 더 짧게
$ git log --oneline
a9b383d (HEAD -> master) Initial commit
```

퀴즈! 만약 status를 여기서 찍으면 어떤 결과가 나올까?

- 현재 b.txt 가 WD에 위치해 있기 때문에 빨간색으로 표시된다.
- `a.txt` 는 commit 명령어를 통해 하나의 버전으로 기록됨

```bash
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

