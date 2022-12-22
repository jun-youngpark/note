# 1. 기본 명령어
$git init
새로운 local repository 생성
$git add
새로운 repository에 저장
$git commit
새로운 local repository 생성
$git push
local repository를 remote repository에 업로드

# 2. Github에 소스코드 올리기
1) 레파지토리 생성
Github 홈페이지에서 회원가입 후 repository를 생성

2) 업로드할 폴더로 이동
커맨더 창을 통해 깃허브에 업로드할 파일이 있는 폴더로 이동

$cd 폴더경로
3) init
커맨더창에서 아래의 명령어를 통해, 위의 폴더를 git이 추적할 수 있도록 .git폴더를 생성합니다. 즉, local repository를 생성하는 것임

$git init
4) 상태확인
git이 버전관리 대상 파일들의 상태를 파악합니다

$git status
명령어가 동작하지 않을 때 에러 확인
내가 작업한 파일 외에 다른 파일이 수정되진 않았는지 확인
5) add
버전 관리할 파일들을 추가합니다

$git add .
git add 파일 명령어는 특정 파일들을 추가하는 명령어이며, 아래의 명령어는 변경 모든 파일을 local repository에 추가하는 명령어입니다.

6) 커밋
commit 메세지를 작성합니다

$git commit -m "메세지내용"
-m 옵션은 간단하게 한줄로 메세지를 작성하기 위함이며, 긴 메세지 작성이 필요하다면 git commit 명령어만 실행하면됩니다.
7) remote 등록
remote repository를 등록합니다.

$git remote add origin {remote repository 주소}
origin은 remote repository의 별칭을 의미하며, remote repository의 주소를 입력하는 것이 귀찮으므로 origin 이라는 별칭을 사용합니다.
repository의 주소는 본인의 github 주소를 입력하면 되는데, 아래 사진처럼 HTTPS를 선택한 후, 복사를 클릭하면 주소를 복사할 수 있습니다.



8) push
commit한 내용을 remote repository에 push (업로드)합니다.

$git push origin master
master은 브랜치(branch)의 이름이며, remote repository를 생성하면 기본적으로 master 브랜치가 생성됩니다. (참고로 브랜치는 독립적인 작업 공간을 의미하며, 브랜치 덕분에 협업이 수월해지기 때문에 꼭 알아둬야하는 개념임)
master가 아닌 다른 branch로 push하고 싶으면, 아래와 같이 master를 특정 브랜치명으로 바꿔서 명령어를 실행하면 됩니다.

$git push origin{브랜치명}
