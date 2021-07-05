# 원격 저장소(Remote repository)

## 기본 설정

1. 내 로컬 컴퓨터의 폴더를 git이 관리하도록 설정한다.

```bash
$ git init
Initialized empty Git repository in C:/Users/NaEunSu/Desktop/TIL/.git/
```

2. Github Repository 생성

## 원격 저장소 등록 & 업로드 명령어

### 원격 저장소 추가

```bash
# 원격 저장소 추가
# git아 원격 저장소 좀 등록해줘(add) origin이라는 이름(별명)으로 원격 저장소 URL을
$ git remote add origin (원격 저장소 url)

# 예시
$ git remote add origin https://github.com/neSTORY/TIL.git

# 등록된 원격 저장소 확인
$ git remote -v
origin  https://github.com/neSTORY/TIL.git (fetch)
origin  https://github.com/neSTORY/TIL.git (push)

# 원격 저장소가 잘못 등록되어 삭제해야 하는 경우
$ git remote rm origin (원격 저장소 url)
```

### 원격 저장소에 나의 소스 코드 업로드

- 2.23 버전의 로그인 이슈
  - 아래 명령어를 입력하고 다시 push 작업 입력

```bash
$ git config --global cred
```

- 혹은 vscode에 git bash를 연결해서 push하면 문제 해결 가능

```bash
```

```bash
# 기본 루틴
$ git add .
$ git commit -m "커밋 메시지"
$ git push origin master # git아 
```

