# [JAVA/MS-SQL] JAVA에서 MS-SQL 스토어드 프로시저 사용하기
 
 
이번에 쓸 내용은 프로시저내에서 output 변수로 선언된 값을 JAVA 에서 출력해주는 부분이다.


출처 :http://pcguy7.springnote.com/pages/1044536

* CallableStatement : SQL의 스토어드프로시저(Stored Procedure)를 실행시키기 위해 사용되는 인터페이스 이다.

* 스토어드프로시저란 : query문을 하나의 파일 형태로 만들거나 데이터베이스에 저장해 놓고 함수처럼 호출해서 사용하는 것임. 이것을 이용하면 연속되는 query문에 대해서 매우 빠른 성능을 보인다.
 보안적인 장점 역시 가지고 있음.


* 호출하기에 앞서 반드시 CallableStatement인터페이스의 registerOutParameter()메서드를 호출해야 함.
 
 ```
 (CallableStatement 예제)
CallableStatementTest.java
 import java.sql.*;
public class CallableStatementTest{
   public static void main(String[] args){
     try{
         Class.forName("sun.jdbc.odbc.JdbcOdbcDriver");
         Connection con = DriverManager.getConnection("jdbc:odbc:dbdsn", "id", "password");
         CallableStatementcs = con.prepareCall("{call myStoredProcedure(?,?,?)}");
         cs.setInt(1,2);
         cs.registerOutParameter(2, java.sql.Types.VARCHAR);
         cs.registerOutParameter(3, java.sql.Types.INTEGER);
         cs.execute();
         System.out.println("*name : "+ cs.getString(2) +"*age : "+ cs.getInt(3));
         cs.close();
         con.close();
     }catch(Exception e){System.out.println(e);}
   }
}
```
