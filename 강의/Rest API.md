## 현재의 RESTAPI는 아래 두가지를 잘 지키지 못하는경우가 많다.

1. Self-descriptive message
메시지 스스로 메시지에 대한 설명이 가능해야 한다.
서버가 변해서 메시지가 변해도 클라이언트는 그 메시지를 보고 해석이 가능해야한다.
확장 가능한 커뮤니케이션

2. HATEOAS
하이퍼미디어(링크)를 통해 애플리케이션 상태 변화가 가능해야 한다.
링크 정보를 동적으로 바꿀 수 있다. 버저닝 할 필요가 없음(v1,v2,v3)


# Domain 만들기
@data를 사용할 경우 순환 참조 문제가 발생할수 있으므로 id값만 equals , hashcode 할수있도록 
id값만 equals 가능하도록 한다.
```
@EqualsAndHashCode(of = "id")
```

# Enum entity 만들때 주의사항
EnumType의 기본은 ORDINAL인데, ORDINAL은 열거체 상수 숫자값을 반환한다.
중간에 순서가 바뀌면 버그가 유발될수 있으므로 String형을 사용한다

```
  @Enumerated(**EnumType.STRING**)
    private EventStatus eventStatus = EventStatus.DRAFT;
```

# ModelMapper
DTO - > 도메인 객체로 복사 해주는 라이브러리
https://modelmapper.org/getting-started/
```
 ModelMapper modelMapper = new ModelMapper();
 OrderDTO orderDTO = modelMapper.map(order, OrderDTO.class);
```
 

