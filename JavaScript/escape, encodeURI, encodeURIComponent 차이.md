# escape, encodeURI, encodeURIComponent 차이
escape, encodeURI, encodeURIComponent 차이
 
 
﻿자바스크립트에서 지원하는 url encode / url decode 함수는 3가지가 있다. 
 
* escape() 는 
ABCDEFGHIJKLMNOPQRSTUVWXYZ abcdefghijklmnopqrstuvwxyz 1234567890 @*-_+./ 
위에서 열거된 문자가 아니면 모두 변환을 합니다. 1바이트문자는 %XX 형태로 2바이트 문자는 %uXXXX 식으로 변환합니다. 
(아스키문자가 아니라면 모두 유니코드 형식으로 변한)

* encodeURI()는
escape()와 비슷하지만 인터넷 주소표시에 쓰이는 특수문자들은
인코딩하지않는다. 즉, : ; / = ? & 등의 특수문자는 인코딩 되지않는다 .
보통 파라미터 전달하는 인터넷주소 전체를 인코딩할때 사용
encodeURIComponent()는
escape()와 비슷하지만 인터넷 주소표시에 쓰이는 모든 문자들을 추가로 인코딩한다.
즉, : ; / = ? & 등의 특수문자들이 추가로 인코딩이 된다.
그래서 인터넷주소 URL 을 전체로 인코딩할때는 사용할수 없고 필드 하나하나를 따로 인코딩할 때 사용된다.
 
* Java의 java.net.URLEncoder.encode 는 ?
encodeURIComponent ﻿와 비슷하지만 encodeURIComponent ﻿가 인코딩 안하는 ! ( ) 3개도 인코딩한다.

```
var url = <>;:/[]{}'">'가나다라abcd123!@#$%^&*()-=\,.<>;:/[]{}'
document.write('url : ' + url);
document.write('<br>');
document.write('1 : ' + escape(url));
document.write('<br>');
document.write('2 : ' + encodeURI(url));
document.write('<br>');
document.write('3 : ' + encodeURIComponent(url));
java.net.URLEncoder.encode("<>;:/">가나ab12!@#$%^&*()-=,.<>;:/[]{}", "utf-8")
``` 

결과
```url : 가나ab12!@#$%^&*()-=,.<>;:/[]{}
1 : %uAC00%uB098ab12%21@%23%24%25%5E%26*%28%29-%3D%2C.%3C%3E%3B%3A/%5B%5D%7B%7D
2 : %EA%B0%80%EB%82%98ab12!@#$%25%5E&*()-=,.%3C%3E;:/%5B%5D%7B%7D
3 : %EA%B0%80%EB%82%98ab12!%40%23%24%25%5E%26*()-%3D%2C.%3C%3E%3B%3A%2F%5B%5D%7B%7D
4 : %EA%B0%80%EB%82%98ab12%21%40%23%24%25%5E%26*%28%29-%3D%2C.%3C%3E%3B%3A%2F%5B%5D%7B%7D
 ```
 
결론
1. escape는 별로 쓸일이 없겠다.
   URL 전부를 인코딩할때는 encodeURI 를 사용하고
   파라미터만 인코딩 하거나 url 전체를 파라미터로 줄때는 encodeURIComponent 를 사용하면된다.
2. 자바스크립트에서 지원하는 인코딩들은 모두 utf8이다 따라서 javascript로 인코딩한뒤 파라미터를 넘기고 jsp에서 받을때 utf-8로 디코딩을 해줘야 한글이 안깨진다.
3. ajax도 utf8이기때문에 charset이 euc-kr인 페이지에서는 urlencodecomponent로 인코딩해준뒤 넘겨준다.
 
참고 : http://mtkwn.blog.me/40112707174
