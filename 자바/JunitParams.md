# JUnit4에서 JUnitParams 이용해서 파라미터 테스트하기

JunitParams를 이용하기 위해 종속성 추가

``` 
<dependency>
  <groupId>pl.pragmatists</groupId>
  <artifactId>JUnitParams</artifactId>
  <version>1.1.1</version>
  <scope>test</scope>
</dependency>
```
``` 
  @RunWith(JUnitParamsRunner.class)
  public class PositiveTest {

    @Test
    @Parameters({
        "1, true",
        "2, true",
        "-1, false"
    })
    public void positive(int number, boolean isPositive) {
      // given, when
      Positive positive = new Positive(number);

      // then
      assertThat(positive.isPositive()).isEqualTo(isPositive);
    }
  }
``` 
위 방법보다 조금더 type safe 한 방법은 아래와 같이 하면된다

```
  @Test
  @Parameters(method = "parameters")
  public void positive(int number, boolean isPositive) {
    // given, when
    Positive positive = new Positive(number);

    // then
    assertThat(positive.isPositive()).isEqualTo(isPositive);
  }

private Collection<Object[]> parameters() {
    return Arrays.asList(new Object[][]{
        {1, true},
        {2, true},
        {-1, false}
    });
  }
  ```
