## 프로젝트 구조
* src : web application 에 필요한 java file 위치 
* Libraries
    * Apache Tomcat v8.5 : tomcat library(servlet-api.jar위치)
    * JRE System libary : jre library 
* WebContent : view directory (html,css,js,jsp,image ... )
    * META-INF 
    * WEB-INF 
        * lib : web application에 필요한 확장 library
        * web.xml : web application의 설정 파일 
                    web module 3.0이상부터는 annotation으로 대체가능 
## Servlet 
* 자바 서블릿은 자바를 사용하여 웹페이지를 동적으로 생성하는 서버측 프로그램 혹은 그 사양을 말하며, 흔히 **서블릿**이라 불린다.
* 자바 서블릿은 웹 서버의 성능을 향상하기 위해 사용되는 **자바 클래스**의 일종이다.
* JSP가 HTML 문서 안에 Java코드를 포함하고 있는 반면, 서블릿은 자바 코드 안에 html을 포함하고 있다는 차이점이 있다. 

## Servlet LifeCycle 
* Servlet class는 javaSE에서의 class와는 다르게 main method가 없다. 
* 즉 객체의 생성부터 사용(method call)의 주체가 사용자가 아닌 Servlet Container에게 있다. 
* Client가 요청을 하게 되면 Servlet Container는 Servlet객체를 생성하고, 초기화하며 요청에 대한 처리(요청시마다 반복)를 하게 된다. 
* 또한 Servlet객체가 필요 없게 되면 제거하는 일까지 Container가 담당하게 된다. 

## Servlet LifeCycle의 주요 method
* init() 서블릿이 메모리에 로드될때 한번 호출 , 최초 한번만
* doGet() Get방식으로 data전송 시 호출, 요청시마다 반복
* doPost() Post방식으로 data전송 시 호출 , 요청시마다 반복
* service() 모든 요청은 service()를 통해서 doXXX()메소드로 이동 , 요청시마다 반복
* destroy() 서블릿이 메모리에서 해제되면 호출  , 최초 한번만

## Parameter 전송방식
 * GET : 전송되는 데이터가 URL뒤에 QueryString으로 전달. 
        * 장점 : 간단한 데이터를 빠르게 전송 
                form tag뿐만 아니라 직접 URL에 입력하여 전송가능.
        * 단점 : 데이터 양에 제한이 있다. 
                location bar(URL + Parameter)를 통해 전송할 수 있는 데이터의 사이즈는 2kb로 제한 
 * POST : URL과 별도로 전송, HTTP header 뒤 body에 입력 스트림 데이터로 전달 
        * 장점 : 데이터의 제한이 없다. 최소한의 보안 유지 효과를 볼 수 있다. 
        * 단점 : 전달 데이터의 양이 같을 경우 GET방식보다 느리다. 


## JSP (Java Server Page)

* JSP는 HTML내에 자바 코드를 삽입하여 웹 서버에서 동적으로 웹 페이지를 생성하여 웹 브라우저에 돌려주는 언어이다. Java EE 스펙 중 일부로 웹 애플리케이션 서버에서 동작한다. 
* 자바 서버 페이지는 실행시에는 자바서블릿으로 변환된 후 실행되므로 서블릿과 거의 유사하다고 볼 수 있다. 
*   하지만, 서블릿과 달리 HTML 표준에 따라 작성되므로 웹 디자인하기에 편리하다. 
* 최소JSP 요청 시 jsp file 변경 시 jsp가 servlet으로 변경 됨

* JSP 스크립팅 요소 - 선언 
  : 멤버변수 선언이나 메소드를 선언하는 영역 
  * 형식  <%! 멤버변수와 method작성 %>
* JSP 스크립팅 요소 - 스크리브릿 
  : Client 요청 시 매번 호출 영역으로, Servlet으로 변환 시 service() method에 해당되는 영역.
   request, response에 관련된 코드 구현 
   * 형식  <% java code %>
* JSP 스크립팅 요소 - 표현식 
  : 데이터를 브라우저에 출력할 때 사용 
   * 형식  <%= 문자열 %>
* JSP 스크립팅 요소 - 주석
  : 코드 상에서 부가 설명을 작성 .
   * 형식  <%--주석 할 code --%>
   * 참고 : html 주석(<!-- -->)과 jsp 주석의 차이점 
            html 주석의 경우 브라우저 소스보기하면 사용자에게 보여짐. 
            jsp 주석의 경우 브라우저에서 보여지지않음.

## JSP 지시자(Directive)
   1. page Directive 
       * 컨테이너에게 현재 JSP페이지를 어떻게 처리할 것인가에 대한 정보를 제공한다. 
       형식( <%@ page attr1="val1" %>)
    2. include Directive 
       * 특정 jsp file을 페이지에 포함 
       * 여러 jsp페이지에서 반복적으로 사용되는 부분을 jsp file로 만든 후 반복 영역에 include 시켜 반복되는 코드를 줄일 수 있다. 
       형식 ( <%@ include file = "/template/header.jsp" @>)
    
    3. taglib Directive 
       * 사용자에 의해서 만든 커스텀 태그를 이용할 때 사용되며 jsp 페이지 내에 불필요한 자바 코드를 줄일 수 있다 . 
       형식 ( <@ taglib prefix ="c" url ="http://java.sun.com/jsp/jstl/core" %>)

   ## JSP 지시자(Directive) - page
   * language : java  : 스크립트에서 사용 할 언어 지정 
   * info : 현재 jsp 페이지에 대한 설명 
   * contentType : text/html; charset=ISO-8859-1 : 브라우저로 내보내는 내용의 MIME형식 지정 및 문자 집합 지정 
   * pageEncoding : ISO-8859-1 : 현재 JSP 페이지 문자집합 지정 
   * import : 현재 JSP 페이지에서 사용할 java 패키지나 클래스를 지정 
   * session : true : 세션의 사용 유무 설정 

   ## JSP 기본객체의 영역(scope) - 공통 method 
   * servlet과 jsp 페이지 간에 특정 정보를 주고 받거나 공유 하기 위한 메소드를 지원 
   * void setAttribute (String name, Object value) :
   문자열 name 이름으로 Object형 데이터를 저장한다. 
   Object형이므로 어떠한 자바객체도 저장이 가능하다
   * Obejct getAttribute(String name) : 문자열 name에 해당되는 속성 값이 있다면 Object 형태로 가져오고 없으면 null을 리턴한다. 따라서 리턴 값에 대하 적절한 형 변환이 필요하다.
   * Enueration getAttributeNames() : 현재 객체에 저장된 속성들의 이름을 Enumeration형태로 가져온다. 
   
