## Git 명령어 정리
### Git 파일 설정, 해제
```
git init - git 파일로 설정
rm -r .git  - git init 취소

.gitignore  - 이 파일에 적은 파일명들은 git에서 관리하지 않음
(push를 해도 원격레포지토리에 올라가지 않음)
```
### Git 원격 설정
```
git branch -M main   - branch 명을 main으로 바꿈
git remote add origin github주소    - github와 git을 동기화 시킴

git remote remove origin  - ↑위에서 등록한 원격 삭제
git remote -v    - 원격 리스트 출력
git remote set-url origin github주소  - 원격 주소 변경
git remote update origin --prune    -바뀐 주소를 remote 서버와 동기화
```
### GitHub에 파일 올리기
```
git status  - git이 관리하는 폴더 변화 확인
git add 파일이름.확장자명  - commit 준비 (add ., * : modified 된 파일이나 untracked 된 파일 모두 add)
git commit -m "메모할 내용"  - git에 올림
git push -u origin main  -commit 내용을 github에 올림

git reset   -git add로 올린 파일 취소
```
### Git 기록, 설정 보기
```
git log  - commit 된 기록들을 보여줌
(git log --oneline   -commit된 기록들을 짧게 보여줌)
git checkout (commit 16진수)   - 예전 기록으로 돌아감
(git checkout -, branch name    - 현재 상태로 돌아옴)

git config --list    - 저장소별 설정 정보 조회 (연결된 원격 주소, 계정 등 알 수 있음)
git config --global --list  - 전역 설정 정보 조회 
```
### 원격과 로컬이 다를 때
```
git fetch  - 원격 저장소에 변경사항이 있는지 확인
git pull  - 원격과 로컬을 동기화함
```
### Github에서 파일 가져오기
```
git clone github주소 .  - 파일 복제(복사한 파일이 저장되는 폴더는 비어있어야함)
```
### Git conflict , merge
```
1)
git pull origin main
git merge --continue                    장점 : 한 번의 merge로 해결 가능
git push origin 작업브랜치              단점 : merge commit이 생겨 깔끔하지 않음 

2)
git checkout 작업브랜치
git pull --rebase origin main              장점 : merge commit 없음
git rebase --continue                      단점 : conflict 건이 많으면 다 고쳐야함
충돌을 해결해 나가면서, 계속 rebase를 진행
git rebase --abort
git push -f origin 작업브랜치  
```
### Git push한 파일 내리기?
```
$ git rm --cached 파일명/폴더명
```



