# Tomcat Session 이름 변경


Tomcat 6.x 이하버전
http://tomcat.apache.org/tomcat-6.0-doc/config/systemprops.html
자바 환경변수 값에 아래 내용 추가.

-Dorg.apache.catalina.SESSION_COOKIE_NAME=MYSESSIONID
-Dorg.apache.catalina.SESSION_PARAMETER_NAME=MYSESSIONID
Tomcat 7.x 버전
Context 의 sessionCookieName attribute 로 추가되어있다.

<Context sessionCookieName="MYSESSIONID" cookies="true">
Tomcat 8.x 이상
이 방법 사용시 해당 Web Application이 Servlet 3.0 이상으로 선언되어야 함 (web.xml 참조)

WebApplication 의 web.xml 내의 session-config - cookie-config - name 속성 선언


<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://java.sun.com/xml/ns/javaee"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
  id="WebApp_ID" version="3.0">

  <display-name>LDS</display-name>

  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>

  <filter>
    <filter-name>Set Character Encoding</filter-name>
    <filter-class>filters.SetCharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <!-- <param-value>euc-kr</param-value> -->
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>

  <filter-mapping>
    <filter-name>Set Character Encoding</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <!-- 모든 항목은 반드시 순서를 맞춰서 선언하여야 한다. -->
  <session-config>
    <!-- 세션 유지시간 (분) -->
    <session-timeout>30</session-timeout>
    <!-- 쿠키 설정 -->
    <cookie-config>
      <!-- 임의의 Session Cookie Name 지정 할 경우,
           mod-jk의 session_cookie 도 같이 변경하여야 함 -->
      <name>MYSESSIONID</name>

      <!-- HttpOnly 설정 : 서버 요청이 있을 때에만 쿠키가 전송되도록 설정하며,
           임의로 다른 사용자에 의해 웹 브라우저에 출력되지 않도록 설정한다. -->
      <http-only>true</http-only>

      <!-- Secure 속성 : SSL 통신 채널 연결 시에만 쿠키를 전송하도록 설정 -->
      <!-- 
      <secure>true</secure>
      -->
    </cookie-config>

    <!-- url에 ;jsessionid 파라메터가 붙지 않도록 쿠키 사용 설정 -->
    <tracking-mode>COOKIE</tracking-mode>
  </session-config>

  <!-- Clustering context -->
  <distributable />
</web-app>
