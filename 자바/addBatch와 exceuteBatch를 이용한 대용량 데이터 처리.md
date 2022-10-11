# addBatch와 exceuteBatch를 이용한 대용량 데이터 처리



어느날 100만건이 넘는 대용량 데이터를 빠른 시간내에 처리해야 하는 이슈가 있었다.
처음에는 습관처럼 myBatis를 이용하여 데이터 insert를 처리하였는데 데이터를 insert 하는 시간이 생각보다 오래 걸렸다.

혹시나하여 myBatis를 사용하지 않고 자바 코드내에서 Connection 객체를 사용하여 insert 하였더니 소요시간이 많이 줄어들었다.
프레임웍의 일종인 myBatis를 거치면 빠른 대용량 처리시에는 부적합하다는 결론을 내리고 자바 소스내에서 처리하는것으로
개발방법을 변경하였다.

mybatis를 이용하지 않고 코드 내에서 다이렉트로 DB에 접속하여 insert 하는 방법이 속도는 더 빠르지만, 프로그램의 요구사항은 이보다 더 빠르게 처리하는게 목표였다.

그래서 오랜만에 PrepareStatement에서 제공하는 addBatch를 사용하기로 결정하였다. addBatch는 쿼리 실행을 하지 않고
쿼리 구문을 메모리에 올려두었다가, 실행 명령이 있으면 한번에 DB쪽으로 쿼리를 날린다.

아무래도 매번 쿼리를 실행할때 왔다갔다해야 하는 통신 리소스라던지, 쿼리가 실행된후 실행결과를 받는 자바 프로그램의 단계가 없이, 한번에 여러건을 실행시키니 속도는 훨씬 빠르다.

복잡하지 않고 간단하니 아래 예제를 보면 쉽게 이해가 갈것이다.
 ```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
public class TestAddBatch {
public static void main(String[] args) {
        // TODO Auto-generated method stub
        Connection con = null;
        PreparedStatement pstmt = null ;
        String sql = "Insert Into TB_test(uid, name, age) Values(?, ?, ?)" ;
            try{
                  Class.forName("com.mysql.jdbc.Driver");
                  con = DriverManager.getConnection(" jdbc:mysql://127.0.0.1:3306/TEST_DB", "test_user", "12345");
                  pstmt = con.prepareStatement(sql) ;
                  for(int i=0; i < 100000; i++){
                        int uid = 10000 + i ;
                        String name = "홍길동_" + Integer.toString(i) ;
                        int age = i ;
                        pstmt.setInt(1, uid);
                        pstmt.setString(2, name) ;
                        pstmt.setInt(3, age);
                        // addBatch에 담기
                        pstmt.addBatch();
                        // 파라미터 Clear
                        pstmt.clearParameters() ;
                        // OutOfMemory를 고려하여 만건 단위로 커밋
                        if( (i % 10000) == 0){
                            // Batch 실행
                            pstmt.executeBatch() ;
                            // Batch 초기화
                            pstmt.clearBatch();
                            // 커밋
                            con.commit() ;
                       }
                  }
              // 커밋되지 못한 나머지 구문에 대하여 커밋
              pstmt.executeBatch() ;
              con.commit() ;
        }catch(Exception e){
           e.printStackTrace();
        try {
           con.rollback() ;
        } catch (SQLException e1) {
            // TODO Auto-generated catch block
            e1.printStackTrace();
        }
        }finally{
            if (pstmt != null) try {pstmt.close();pstmt = null;} catch(SQLException ex){}
            if (con != null) try {con.close();con = null;} catch(SQLException ex){}
        }
    }
  }
```









addBatch를 통해 쿼리를 메모리에 올린다. 이후 executeBatch 명령어를 통해 쿼리를 전송한다.
여기서 주의해야 할 점은 addBatch를 통해 메모리에 올리게 되는데, 너무 많은 쿼리를 batch에 담게되면 메모리 오류가 발생한다. 그 때문에 절적한 수치를 확인하여 batch를 실행해 주어야 한다.

참고로 executeBatch를 했을경우 처리결과를 받을수도 있는데 이때는 배열로처리결과를 확인할 수 있다.
int[] result = pstmt.executeBatch() ;



