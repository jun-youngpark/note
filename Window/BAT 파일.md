Bat파일

배치파일은 꾸준히 사용하게 되면서도 문법은 그리 많이 알고있지 않다.
이번 글을 몇 가지 자주 사용하는 문법을 정리해 두기 위해서 작성한다.

* 스크립트 위치로 이동 
pushd %~dp0




* 파일 및 폴더 확인
 if exist FN.EXT (ren FN.EXT NFN.EXT)
 if not exist DN (mkdir DN)

* FOR 루프

   for /L %%i in (1, 1, 10) do ( 
     .... 
  )

``` 
@echo off

set PR= 

set /p PR= INPUT : 

for /L %%i in (1, 1, 30) do (     

    if exist "01 (%%i).jpg" (

        if %%i LSS 10 (

            ren "01 (%%i).jpg" "%PR%00%%i.jpg"

        )else (

            ren "01 (%%i).jpg" "%PR%0%%i.jpg"

        )

    )

)

pause
``` 

경로 확인

만약 배치파일의 경로가 다음과 같은 경우

파일 경로 : C:\Test\Path1\ex1.bat 

 %0
 파일 전체 경로
 C:\Test\Path1\ex1.bat 
 %~d0
 드라이브 명
 C:
 %~p0
 경로 
 \Test\Path1\
 %~n0
 파일 명 
 ex1
 %~x0
 확장자 명
 .bat 
 %~dp0
 드라이브와 경로
 C:\Test\Path1\


키보드 입력 

 set STR= 

 set /p STR=아무 문자열이나 입력하세요:

 echo 입력받은 문자열 : %STR%


* Pause
수행 중 Pause 명령을 만나면 동작을 중지하고 아무 키를 입력받아야 이후 명령을 수행한다.
**pause**

* 창 제목 
배치 파일의 창 제목을 설정한다. 
**title** 창 제목


* 콘솔 색상 지정
* **color** 61
앞의 숫자는 배경색, 뒤의 숫자는 문자색이다.
 
