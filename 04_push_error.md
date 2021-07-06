## push error

```bash
$ git push origin master
To https://github.com/edujustin-hphk/TIL.git
 ! [rejected]        master -> master (fetch first) # 거절됨...

# 원격 저장소로 push하는 것을 실패했음..
error: failed to push some refs to 'https://github.com/edujustin-hphk/TIL.git' 

# update가 reject되었는데 왜냐면... remote에 local 없는 어떤 변경 사항이 있음...
hint: Updates were rejected because the remote contains work that you do

# 이러한 상황은 커밋이 다른 경우에 발생하는데.. remote 저장소와 local 저장소를 일치 시켜야 할 것 같음...
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes

# 어.. git pull 한번 해볼래?? 언제?? 다시 push 하기 전에...
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```



1. 로컬 저장소(내 컴퓨터)와 원격 저장소(github)의 commit 이력을 비교해본다!
   - 이 문제는 로컬 저장소와 원격 저장소의 commit 이력이 다르기 때문에 발생하는 문제
   - 주로 집에서 push를 하고 강의장에 가서 pull하지 않은 채로 작업하고 add, commit 이후에 push를 하면 보게 되는 메시지
2. 로컬 젖아소에서 `$ git pull origin master` 를 진행한다.
3. vscode 창이 나오면 text 파일을 x 버튼을 눌러서 종료 한다.
   - 이때 vs code 창이 열리지 않는 경우도 있기 때문에 당황하지 말 것!