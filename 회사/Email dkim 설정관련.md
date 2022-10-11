# DKIM 설정
## Dkim은 구글에서 사용하는 gmail 스팸 정책, dkim을 설정할 경우 스팸으로 수신될 확률을 줄일 수 있습니다.

1.openssl설치(http://www.openssl.org/source/)
> tar xvzfp openssl-1.0.0d.tar.gz
> yum -y install gcc
> ./config
> make
> make install

2. 개인, 공개 키 생성
1) 홈페이지 서버에서 생성하면 됨(210.181.236.2)
2) 개인키 생성: /home/wise/openssl/private_key_gen.sh 도메인
- 도메인으로 시작하는 파일에 개인키를 생성함
3) 공개키 생성: /home/wise/openssl/public_key_gen.sh 도메인
- 개인키로 공개키를 생성함

3. DNS에 TXT 등록
wiseu._domainkey.mnwise.com.INTXT"v=DKIM1;g=*;k=rsa;p=MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBAM6u0U/5ZkyEE52qNP4JauJxJGplkfzwnxE2lqkxlIdMdsCuj6mUIO2Uz5ApgZr76YCRKwq/qeyj/yoYGXFAC30CAwEAAQ=="

4.DNS에DKIM공개키등록확인(도스)
C:\Users\keultae>nslookup
기본 서버: ns.dacom.co.kr
Address: 164.124.101.2

> set type=txt
> wiseu._domainkey.mnwise.com
서버: ns.dacom.co.kr
Address: 164.124.101.2

권한 없는 응답:
wiseu._domainkey.mnwise.com text =

"v=DKIM1; g=*; k=rsa; p=MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBAM6u0U/5ZkyEE52q
NP4JauJxJGplkfzwnxE2lqkxlIdMdsCuj6mUIO2Uz5ApgZr76YCRKwq/qeyj/yoYGXFAC30CAwEAAQ==
"

mnwise.com nameserver = ns1.mnwise.com
ns1.mnwise.com internet address = 210.181.236.2

5. hotmail.com
DKIM체크시SMTP프로토콜의MAILFROM을사용하지않고마임의FROM을사용함

 
  
