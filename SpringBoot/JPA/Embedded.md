# @Embeddable 
임베디드 타입
임베디드 타입은 복합 값 타입으로 불리며 새로운 값 타입을 직접 정의해서 사용하는 JPA의 방법을 의미한다.
아래의 코드를 보면 User엔티티는 id, 이름, 이메일, 성별, 주소정보의 데이터를 갖고 있는데 주소 정보가 도시, 구, 상세주소, 우편번호 등으로 여러개의 컬럼으로 나눠져 있는 것을 볼 수 있습니다. 
-> 이렇게 상세한 데이터를 그대로 갖고 있는 것은 객체지향적이지 않으며 응집력을 떨어뜨립니다.
이럴때 임베디드 타입을 사용하면 더욱더 객체지향적인 코드를 만들 수 있습니다.
```
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @NonNull
    private String name;

    @NonNull
    private String email;


    @Enumerated(value = EnumType.STRING)
    private Gender gender;
    
    @Embedded
    private Address address;

}
```

```
@Embeddable
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Address {
    // 주소 정보
    private String city; // 도시
    private String district; // 구

    @Column(name = "address_detail")
    private String detail; // 상세 주소
    private String zipCode; // 우편번호
}
```

```
// 데이터 추가하는 방법
user.setAddress(new Address("서울시", "강남구", "강남대로 123", "16427"));
```

# @AttributeOverride : 속성명 재정의
같은 종류의 Attribute에 대해서 중복된 코드를 적을 필요 없이 간단하고 직관성있게 선언 가능하다.

```
@Entity
public class User {

.....

    @Embedded
    @AttributeOverrides({
            @AttributeOverride(name = "city", column = @Column(name = "home_city")), // city를 home_city라는 column명으로 사용
            @AttributeOverride(name = "district", column = @Column(name = "home_district")),
            @AttributeOverride(name = "detail", column = @Column(name = "home_address_detail")),
            @AttributeOverride(name = "zipCode", column = @Column(name = "home_zipCode"))
    })
    private Address homeAddress;

    @Embedded
    @AttributeOverrides({
            @AttributeOverride(name = "city", column = @Column(name = "company_city")),
            @AttributeOverride(name = "district", column = @Column(name = "company_district")),
            @AttributeOverride(name = "detail", column = @Column(name = "company_address_detail")),
            @AttributeOverride(name = "zipCode", column = @Column(name = "company_zipCode"))
    })
    private Address companyAddress; 
}
```

![image](https://github.com/jun-youngpark/note/assets/54339804/b96769ff-125d-49a6-8dc1-c5dc2f5a2296)


