# 리눅스 그륩 관련
 
* useradd
- 사용자 계정을 생성할때 사용한다.
- 형식 useradd [OPTIONS] 계정이름
 
  
* usermod
- 사용자의 계정을 수정할 때 사용한다.
- 형식 usermod [OPTIONS] 계정이름
 
* userdel
- 사용자의 계정을 삭제할 때 사용한다.
- 형식 userdel [OPTIONS] 계정이름 
  
usermod -r 는 계정과 연관된 모든 파일 삭제.
usermod -f 는 로그인 되어있거나, 이 사용자의 계정을 다른 이가 사용하고 있을때 강제로 삭제.
 
* skill -KILL/STOP [사용자이름/터미널창(tty1~6)] : 특정 터미널에 접속한 사용자 & 특정 사용자 강제 종료 / 정지
 
* passwd
- 사용자의 계정에 암호를 부여 / 삭제할 때 사용한다.
- 형식 passwd [OPTIONS] 계정이름
 
 passwd -d 옵션으로 비밀번호를 NULL 초기화
 
* groupadd
- 그룹을 생성할때 쓰인다.
- 형식 groupadd [OPTIONS] 그룹이름
 
* groupmod
- 그룹이름 변경 말고는 잘 안쓴다.
- 형식 groupmod [OPTIONS] [ARGUMENT] 그룹이름
 
* groupmod -n 바꿀이름 그룹이름
 
* groupdel
- 그룹을 제거할때 쓰인다.
- 형식 groupdel 그룹이름
 
 
 
* 계정 설정 파일
 
* /etc/passwd/ : 사용자의 계정 정보를 담아두고 있는 파일
 
* /etc/shadow/ : 사용자의 계정 정보를 담아두고 있지만, 더 보안이 철저한 파일.
 
아래 정보들 표시됩니다.
 
사용자 계정명 : nana
부여된 비밀번호 : $1$rTcCtJuZ$m5acBrZqTtQc6tUgPFsbk.
암호 생성일자 : 15652 (기준은 1970년 1월 1일이다. 왜 1970년 1월 1일이냐면 UNIX 운영체제가 만들어진 때가 1970년도여서)
암호 변경 최소기간 : 0
암호 변경없이 사용가능한 유효기간 : 99999
계정 만료 경고일수 : 7
계정 만료일자 : null
계정 만료일 : null
 
* /etc/group/ : 그룹의 기본 정보
 
아래 정보들 표시됩니다.

그룹 이름 : babo2
그룹 패스워드 : x
GID : 513
구성원 이름 : nana
 
* /etc/gshadow/ : 그룹 암호 정보
 
계정의 기본 값을 정하는 파일 / 디렉토리
 
* /etc/login.defs/            : 패스워드 세부 설정, 유마스크, UID, GID 범위, 메일 경로
* /etc/default/useradd/    : passwd 에 들어가는 기본 값
* /etc/skel/                    : 계정 생성시 사용자의 홈 디렉토리에 자동으로 생성 될 파일
