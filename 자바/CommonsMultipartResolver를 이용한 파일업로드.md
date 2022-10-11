# CommonsMultipartResolver를 이용한 파일업로드
CommonsMultipartResolver를 이용한 파일업로드

- CommonsMultipartResolver 빈을 설정하여 파일 업로드를 처리할 수 있다.
- MultipartFile클래스를 이용하여 업로드한 파일정보를 얻어온다.
- JSP파일의 enctype을 multipart/form-data로 설정해야 한다.
- commons-fileupload, commons-io jar 파일이 있어야 한다.

pom.xml 확인

- commons-fileupload, commons-io가 있는지 확인한다.
pom.xml
```
<dependency>
    <groupId>commons-fileupload</groupId>
    <artifactId>commons-fileupload</artifactId>
    <version>1.2.1</version>
</dependency>  

<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>1.4</version>
</dependency>

```

multipart/form-data 설정

- form.jsp에 enctype="multipart/form-data"를 추가한다.
- file type의 inputbox도 추가한다.
/WEB-INF/pages/emp/form.jsp
```
<%@ page language="java" isELIgnored="false" contentType="text/html; charset=UTF-8"%>
<%@ taglib prefix="c"   uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html lang="ko">
<head>
<meta http-equiv="Content-type" content="text/html; charset=UTF-8">
<style>
.error {
    color: #ff0000;
}
.errorblock{
    color: #000;
    background-color: #ffEEEE;
    border: 3px solid #ff0000;
    padding:8px;
    margin:16px;
}
</style>
<script type="text/javascript" language="JavaScript">
        function showMessage(msg){
            if(msg != ''){
                alert(msg); 
            }   
        }

    function insertAct(){    
        var f = document.form;        
        if (!!f.empno.value && !!f.ename.value && !!f.job.value) {
            f.action = "/emp/register.ok";
            f.submit();            
        }else {
            alert("input value");
        }
    }

    function listAct(){
        location.href="/emp/list.ok";
    }
</script>
</head>
<body >

<form:form commandName="emp" name="form" method="post" enctype="multipart/form-data">
<h2> 사원정보 등록 화면 </h2>
  <table width="500" border="0">
    <tr>
        <td align="right" width="100"> empno : </td>
        <td width="400">
            <input type="text" id="empno" name="empno" value="" maxlength="20" size="20"/>
            <br><form:errors path="empno" cssClass="error" />
        </td>
    </tr>            
    <tr>
        <td align="right"> ename : </td>
        <td>
            <input type="text" id="ename" name="ename" value="" maxlength="20" size="20"/>
            <br><form:errors path="ename" cssClass="error" />
        </td>
    </tr>
    <tr>
        <td align="right"> job : </td>
        <td><input type="text" id="job" name="job" value="" maxlength="20" size="20"/></td>
    </tr>
    <tr>
        <td align="right"> sal : </td>
        <td>
            <input type="text" id="sal" name="sal" value="" maxlength="20" size="20"/>
            <br><form:errors path="sal" cssClass="error" />
        </td>
    </tr>
    <tr>
        <td align="right"> deptno : </td>
        <td>
            <select name="deptno">
                <option value="10">10</option>
                <option value="20">20</option>
                <option value="30">30</option>
            </select>
        </td>
    </tr> 
    <tr>
        <td align="right"> photo </td>
        <td>
            <input type="file" id="file" name="file" value="" size="30"/><br>            
            <form:errors path="file" cssClass="error" />
        </td>
    </tr> 
    <tr height="10"><td></td></tr>
    <tr>
        <td align="center" colspan="2">
            <input type="submit" value="저장" /> 
            <input type="button" value="취소" onclick="listAct()"/>
        </td>
    </tr>    
  </table>
  
</form:form>
</body>
</html>

```

Emp.java 수정

- 사원정보 모델 객체인 Emp클래스에 MultipartFile 클래스의 getter/setter를 추가한다.
com.spring.mvc.emp.model.Emp.java
```
package com.spring.mvc.emp.model;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

import org.apache.commons.lang.builder.ToStringBuilder;
import org.apache.commons.lang.builder.ToStringStyle;
import org.springframework.web.multipart.MultipartFile;

public class Emp {

    private int empno;
    private int mgr;
    private int sal;
    private int deptno;
    private String ename;
    private String job;
    private Date hiredate;

    MultipartFile file;

    public MultipartFile getFile() {
        return file;
    }

    public void setFile(MultipartFile file) {
        this.file = file;
    }

    public Date getHiredate() {
        return hiredate;
    }

    public void setHiredate(Date hiredate) {
        this.hiredate = hiredate;
    }

    public void setHiredateString(String hiredateString) {
        try {
            this.hiredate = parseDate(hiredateString, "yyyy/MM/dd HH:mm:ss");
        } catch (ParseException e) {
            e.printStackTrace();
        }
    }

    public int getEmpno() {
        return empno;
    }

    public void setEmpno(int empno) {
        this.empno = empno;
    }

    public int getMgr() {
        return mgr;
    }

    public void setMgr(int mgr) {
        this.mgr = mgr;
    }

    public int getSal() {
        return sal;
    }

    public void setSal(int sal) {
        this.sal = sal;
    }

    public String getEname() {
        return ename;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    public int getDeptno() {
        return deptno;
    }

    public void setDeptno(int deptno) {
        this.deptno = deptno;
    }

    public Date parseDate(String day, String pattern) throws ParseException {
        DateFormat formtter = new SimpleDateFormat(pattern, Locale.KOREA);
        Date date = formtter.parse(day);
        return date;

    }

    public String toString() {
        return ToStringBuilder.reflectionToString(this, ToStringStyle.MULTI_LINE_STYLE);
    }
}

```

EmpSimpleFormController.java 수정

- 사원정보 등록할 때 파일첨부 하도록 수정하자
- Emp 모델객체를 통해서 파일정보를 얻어와(emp.getFile()), 서버에 저장하는 부분(writeFile(MultipartFile multipartFile))이 추가 되었다.
- 스프링에서 지원해주는 Resource 인터페이스에 의존성 주입으로 파일객체를 생성하여 업로드할 디렉토리를 설정한다.
- InitializingBean 인터페이스를 통해서 uploadPath의 의존성 주입이 안되었을 경우 오류가 발생하도록 한다.
com.spring.mvc.emp.controller.EmpSimpleFormController.java
```
package com.spring.mvc.emp.controller;

import java.io.BufferedInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.util.Date;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.apache.commons.io.IOUtils;
import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.core.io.Resource;
import org.springframework.util.Assert;
import org.springframework.validation.BindException;
import org.springframework.web.multipart.MultipartFile;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.SimpleFormController;

import com.spring.mvc.emp.model.Emp;

public class EmpSimpleFormController extends SimpleFormController implements InitializingBean {
    private static final Log LOG = LogFactory.getLog(EmpRegisterController.class);
    private Resource uploadPath;

    public EmpSimpleFormController() {
        setCommandClass(Emp.class);
        setCommandName("emp");
    }

    @Override
    protected ModelAndView onSubmit(HttpServletRequest request, HttpServletResponse response, Object command,
            BindException errors) throws Exception {

        Emp emp = (Emp) command;
        emp.setHiredate(new Date());
        LOG.debug(" ### emp : " + emp);

        MultipartFile multipartFile = emp.getFile();
        writeFile(multipartFile);

        ModelAndView mv = new ModelAndView();
        mv.setViewName("emp/view");
        mv.addObject("emp", emp);

        return mv;
    }

    private void writeFile(MultipartFile multipartFile) {
        OutputStream out = null;

        try {

            out = new FileOutputStream(uploadPath.getFile().getAbsolutePath() + "/"
                    + multipartFile.getOriginalFilename());
            BufferedInputStream bis = new BufferedInputStream(multipartFile.getInputStream());
            byte[] buffer = new byte[8106];
            int read;

            while ((read = bis.read(buffer)) > 0) {
                out.write(buffer, 0, read);
            }

        } catch (IOException ioe) {
            LOG.error(ioe);
        } finally {
            IOUtils.closeQuietly(out);
        }
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        // tomcat start 할 때 uploadPath가 설정되었는지 체크한다.
        Assert.notNull(uploadPath, "FileUpload Path must be defined!");

        // 디렉토리가 존재하지 않는다면, 디렉토리를 만든다.
        if (!uploadPath.getFile().exists()) {
            uploadPath.getFile().mkdirs();
        }
    }

    public void setUploadPath(Resource uploadPath) {
        this.uploadPath = uploadPath;
    }
}

```

EmpSimpleFormValidator.java 수정

- 업로드 파일의 사이즈를 1메가로 제한하도록 Validator를 설정한다.
- validate 메소드에 파일 사이즈 체크하는 부분을 추가한다.
com.spring.mvc.emp.validator.EmpSimpleFormValidator.java
```
public void validate(Object target, Errors errors) {

        Emp emp = (Emp) target;

        if (emp.getEmpno() < 1) {
            errors.rejectValue("empno", "required");
        }

        if (StringUtils.isEmpty(emp.getEname())) {
            errors.rejectValue("ename", "required");
        }

        if (emp.getSal() < 1) {
            errors.rejectValue("sal", "required");
        }

        if (emp.getFile().getSize() > 1024000) {
            errors.rejectValue("file", "over.maxUploadSize");
        }
    }

```

messages_ko.properties 수정

- over.maxUploadSize.emp.file 오류 메세지를 추가한다.
- form.jsp에 file 태그 아래에서 오류메세지를 출력하도록 설정하였다.
messages_ko.properties
```
required.emp.empno = 사원번호를 입력해 주세요. 
required.emp.ename = 사원명을 입력해 주세요
required.emp.sal =  사원급여를 입력해 주세요
over.maxUploadSize.emp.file = 파일 제한사이즈를 초과하였습니다.

```

mvc-dispatcher-servlet.xml 파일 설정 변경

- org.springframework.web.multipart.commons.CommonsMultipartResolver를 추가한다.
/WEB-INF/mvc-dispatcher-servlet.xml
```
    <bean id="multipartResolver"  class="org.springframework.web.multipart.commons.CommonsMultipartResolver" >
      <property name="maxUploadSize" value="1000000"/>
    </bean> 
 

```

mvc-dispatcher-servlet-emp.xml 파일 설정 변경

- empFormController 빈에 uploadPath에 대한 의존성을 추가한다.
- uploadPath가 변수로 선언되어있는 것을 확인 할 수 있다.
/src/main/resources/springmvc/mvc-dispatcher-servlet-emp.xml
```
...
    <bean id="empFormController" class="com.spring.mvc.emp.controller.EmpSimpleFormController">
        <property name="formView" value="emp/form" />
        <property name="successView" value="emp/view" />     
        <property name="uploadPath"  value="file:${uploadPath}" />
        <property name="validator">
            <bean class="com.spring.mvc.emp.validator.EmpSimpleFormValidator" />
        </property>   
    </bean>
...

```

FileUpload 파일 경로 설정

- build-local.filter, build-release.filter 파일에 uploadPath 경로를 프로젝트에맞게 수정한다.
- Project를 clean하여 재 컴파일 한다.
build-local.filter
```
uploadPath = C:/workspace/spring-project/webapps/upload

```

테스트

- 톰캣을 Startup 한 후 아래 URL을 실행시킨다.
- http://test.spring.com/emp/form.ok
- 사원정보와 첨부파일을 선택하여 업로드를 테스트 한다.
- 
