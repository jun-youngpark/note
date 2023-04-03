JdbcTemplate의 update() 메서드를 사용하여 데이터베이스 테이블에서 INSERT 작업을 수행할 때 
GeneratedKeyHolder 및 update(PreparedStatementCreator psc, KeyHolder generatedKeyHolder) 메서드를 사용하여 
생성된 키(기본 키 또는 자동 증가 열)를 검색할 수 있습니다.

이 예제에서 update() 메서드는 SQL 문을 정의하고 매개 변수를 설정하는 PreparedStatementCreator 개체와 업데이트 작업이 실행된 후
생성된 키를 포함할 GeneratedKeyHolder 개체의 두 인수를 사용합니다.

PreparedStatement 개체는 삽입된 행에 대해 생성된 키를 반환하도록 데이터베이스에 지시하는 RETURN_GENERATED_KEYS 플래그로 생성됩니다.

마지막으로 생성된 키는 GeneratedKeyHolder 개체에서 검색되어 필요에 따라 사용됩니다.

``` String SQL = "INSERT INTO my_table (col1, col2) VALUES (?, ?)";

GeneratedKeyHolder keyHolder = new GeneratedKeyHolder();

jdbcTemplate.update(con -> {
    PreparedStatement ps = con.prepareStatement(SQL, Statement.RETURN_GENERATED_KEYS);
    ps.setString(1, "value1");
    ps.setString(2, "value2");
    return ps;
}, keyHolder);

Long generatedKey = keyHolder.getKey().longValue();

System.out.println("Generated key: " + generatedKey);
```
