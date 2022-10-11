# 리눅스 그륩 관련
 
useradd
- 사용자 계정을 생성할때 사용한다.
- 형식 useradd [OPTIONS] 계정이름
 
이미지
 
useradd -g 옵션으로 계정의 기본 그룹을 babo로 지정해 주었습니다.
지정해주지 않았다면 nana겠죠.
 
이미지
 
useradd -c 옵션으로 사용자의 계정에 설명을 부여해줬습니다.
기본값은 NULL 입니다.
 
이미지
 
useradd -d 옵션으로 사용자의 계정의 기본 홈 디렉토리를 /home/nana/ 에서 /home/unknown/ 으로 바꿔주었습니다.
 
usermod
- 사용자의 계정을 수정할 때 사용한다.
- 형식 usermod [OPTIONS] 계정이름
 
usermod -g 는 useradd -g 와 같은 옵션이다.
usermod -c 는 useradd -c 와 같은 옵션이다.
usermod -d 는 useradd -d 와 같은 옵션이다.
 
이미지
usermod -p 옵션으로 5000 으로 nana의 비밀번호를 수정하고,
usermod -G 옵션으로 babo 그룹에 nana를 추가시켰습니다.
 
userdel
- 사용자의 계정을 삭제할 때 사용한다.
- 형식 userdel [OPTIONS] 계정이름
 
이미지
 
nana로 tty2번창에서 로그인한 후, 강제로 삭제시키고, 그와 관련된 모든 파일을 삭제했습니다.
usermod -r 는 계정과 연관된 모든 파일 삭제.
usermod -f 는 로그인 되어있거나, 이 사용자의 계정을 다른 이가 사용하고 있을때 강제로 삭제.
 
* skill -KILL/STOP [사용자이름/터미널창(tty1~6)] : 특정 터미널에 접속한 사용자 & 특정 사용자 강제 종료 / 정지
 
passwd
- 사용자의 계정에 암호를 부여 / 삭제할 때 사용한다.
- 형식 passwd [OPTIONS] 계정이름
 
이미지
 
passwd -d 옵션으로 test의 비밀번호를 NULL 값으로 만들었습니다.
 
groupadd
- 그룹을 생성할때 쓰인다.
- 형식 groupadd [OPTIONS] 그룹이름
 
딱히, 이걸 설명할 필요는 없을 것 같습니다.
 
groupmod
- 그룹이름 변경 말고는 잘 안쓴다.
- 형식 groupmod [OPTIONS] [ARGUMENT] 그룹이름
 
groupmod -n 바꿀이름 그룹이름
 
groupdel
- 그룹을 제거할때 쓰인다.
- 형식 groupdel 그룹이름
 
옵션은 없다.
 
계정 설정 파일
 
/etc/passwd/ : 사용자의 계정 정보를 담아두고 있는 파일
 
이미지
사용자 계정명 : nana
부여된 비밀번호 : x (원래 x가 있는 자리에 MD5 형식으로 비밀번호가 있었지만, 현재는 취약점 떄문에 shadow 파일에 쓰여져 있다.)
UID : 511
GID : 514
null : 계정의 대한 설명이 쓰이는 자리
/home/nana : 홈 디렉토리
/bin/bash : 사용하는 쉘
 
/etc/shadow/ : 사용자의 계정 정보를 담아두고 있지만, 더 보안이 철저한 파일.
 
이미지
사용자 계정명 : nana
부여된 비밀번호 : $1$rTcCtJuZ$m5acBrZqTtQc6tUgPFsbk.
암호 생성일자 : 15652 (기준은 1970년 1월 1일이다. 왜 1970년 1월 1일이냐면 UNIX 운영체제가 만들어진 때가 1970년도여서)
암호 변경 최소기간 : 0
암호 변경없이 사용가능한 유효기간 : 99999
계정 만료 경고일수 : 7
계정 만료일자 : null
계정 만료일 : null
 
/etc/group/ : 그룹의 기본 정보
 
이미지
그룹 이름 : babo2
그룹 패스워드 : x
GID : 513
구성원 이름 : nana
 
/etc/gshadow/ : 그룹 암호 정보
 
계정의 기본 값을 정하는 파일 / 디렉토리
 
/etc/login.defs/            : 패스워드 세부 설정, 유마스크, UID, GID 범위, 메일 경로
/etc/default/useradd/    : passwd 에 들어가는 기본 값
/etc/skel/                    : 계정 생성시 사용자의 홈 디렉토리에 자동으로 생성 될 파일
