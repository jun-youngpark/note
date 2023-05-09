# Spring batch database
 데이터베이스 스키마를 제공하며 spring-bath-core 라이브러리 내 /org/springframework/batch/core 하위에 데이터베이스 유형별로 제공합니다. 아래는 h2 데이터베이스 스키마 파일입니다.
  
![image](https://user-images.githubusercontent.com/54339804/236992122-7c9bef10-b0b4-4bcc-b8b4-dea35e4ec6ce.png)

자동 생성 시 spring.batch.jdbc.initialize-schema 설정은 ALWAYS, EMBEDDED, NEVER로 설정이 가능합니다.

ALWAYS: 스크립트를 항상 실행합니다. RDBMS 설정이 되어 있을 경우 내장 DB보다 우선적으로 실행됩니다.
EMBEDDED: 내장 DB일 때만 실행되며 스키마가 자동 생성됩니다. (기본값)
NEVER: 스크립트를 항상 실행하지 않습니다. 운영에서 수동으로 스크립트 생성 후 설정하는 것을 권장합니다. 내장 DB일 경우 스크립트가 생성이 안되기 때문에 오류가 발생합니다.
