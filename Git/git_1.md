### 리눅스 명령어 정리
'''
touch 파일명 - 파일생성
echo "내용" >> 파일명.확장자명 -- 파일생성

cd 폴더명 - 이동하려는 폴더로 이동
cd .. - 상위 폴더로 이동

ls - 선택한 폴더안 파일 확인
(ls -a : 숨겨진 파일 확인)

rm 파일명 - 파일삭제
(rm -rf 파일명 : 파일 강제 삭제)
(rm -r .git : git init 취소)

* - all (ex rm *.txt) -- .txt 로된 파일 모두 삭제
clear - 커널화면 정리

cat 파일이름.파일형태 - 파일 내용 출력 (텍스트 파일 내용 보기?)
'''
### GIT 명령어 정리
'''
git init - git 파일로 설정
git branch -M main  - branch 명을 main으로 변경
git remote add [origin] github주소 - github와 git을 동기화 시킴
(git remote remove [origin] : 원격삭제제)
git remote -v (원격 리스트 출력)
git remote set-url origin github주소 - 주소변경
git remote update origin --prune - 바뀐 주소를 remote 서버와 동기화
git status - git이 관리하는 폴더 변화 확인
git add 파일이름.확장자명 - commit 준비
(git add . , * : modified 된 파일이나 untracked 된 파일 모두 add)
git reset - git add로 올린 파일 취소소
git commit -m "메모할 내용" - git에 올림
git push (-u origin main) - commit 내용을 github에 올림

git log - commit 된 기록들을 보여줌
git checkout commit 16진수 - 예전 기록으로 돌아감
(git checkout - : 다시 현재상태로 돌아옴)

git fetch - 원격 저장소에 변경사항이 있는지 확인
git pull - 원격과 로컬을 동기화함

.gitignore - 이 파일에 적은 파일명들은 git에서 관리하지 않음(push를 해도 원격 레포지토리에 올라가지 않음)

git config --list - 저장소별 설정 정보 조회
git config --global --list - 전역 설정 정보 조회

git clone 주소 . - 파일 복제(복사한 파일이 저장되는 폴더는 비어있어야함)
'''
