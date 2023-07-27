입사 후 늘 프론트를 JSP로만 개발을 진행하다가 처음으로 Thymleaf로 개발을 해볼 수 있는 기회가 생겨서 Thymleaf에 대해서 공부를 해보려고 한다.


  ### Thymleaf란
  - '서버 템플릿 엔진'. html 태그에 속성을 추가해 페이지에 동적으로 값을 추가하거나 처리할 수 있다. 스프링에 권장하나 문법이 어려움.
  EX)
  <input type="text" value="test" th:value="${item}"/>
  ht:value를 통해 item 변수에 값이 존재하면 해당 값 세팅.
  item이 존재하지 않으면 value="test" 값이 세팅된다.
  th:xxx 가 붙은 부분은 서버 사이드 렌더링 

  ※ 서버 템플릿 엔진 : 서버에서 DB 또는 API 등을 통해 가져온 데이터를 미리 정의된 템플릿에 넣어 HTML을 그려내 클라이언트에 전달해준다.
                     즉, HTML 코드에서 고정적으로 사용되는 부분은 템플릿으로 만들어두고 동적으로 생성되는 부분만 템플릿 특정 장소에 끼워넣는 방식.
  ```   
      네임스페이스 :<html lang="ko" xmlns:th="http://www.thymeleaf.org">
  ```   
  
  ### Thymleaf 문법
  - 표현식: <div th:[속성]=”서버에서 받는 값 및 조건식”/>  
  - 변수 : ${...} - ${student.id}
  - 선택자 : *{...} - *{id}
  - 메시지 : #{...} - #{id}
  - 링크URL : @{...} - @{https://www.naver.com}
  - 부분적 표현 : ~{...} -
  - 조건 연산자 : and, or, not, !   
       ${student.age} > 20 and ${student.age} < 10 처럼 각각 분리하여서 사용하거나   
       ${student.age > 20 or student.age < 10} 처럼 한 번에 묶어서 사용하는 것도 가능   
  -  텍스트 결합 : ${student.id}+${student.name}
  -  문장 결합 : |학생 아이디 : ${student.id}, 학생 이름 : ${student.name} | - | 로 전체 문장을 묶어줌   
       if-then : if ? then - ${student.age < 20} ? '청소년'   
       if-then-else : if ? then : else - ${student.age < 20} ? '청소년' : '성인'   
       default : value ?: defaultValue    

   ### - 기본기능
   1. th:text="${}" : jsp의 el 표현식인 ${}와 마찬가지로 ${} 표현식을 통해서 컨트롤러에서 전달받은 데이터 접근 가능.   
                     ```     
                       ex) <div th:text="${item}"></div>      
                     ```      
                   ※ th:utext 속성도 있는데. html태크를 escape 처리하지 않기 때문에 보안에 취약해서 주의해서 사용.
   3. th:href="@{}" : a 태그의 href속성과 동일하다.   
                    ex) <a th:href="@{/testPage?currPage={page}}">   
                    model에 {"param1", "data1"} {"param2", "data2"} 넣은 경우
      
                    -쿼리 파라미터    
                    : @{/hello(param1=${param1}, param2={param2})}   
                    -> /hello?param1=data1&param2=data2   
                    
                    - 경로 변수   
                    : @{/hello/{param1}/{param2}(param1=${param1}, param2=${param2})}    
                    -> /hello/data1/data2   
                    
                    - 경로 변수 + 쿼리 파라미터   
                    : @{/hello/{param1}(param1=${param1}, param2=${param2})}   
                    -> /hello/data1?param2=data2    
   5. th:with="${}" : 새로운 변수값을 생성할 수 있다. JSTL에서 c:set과 유사하지만 선언한 요소의 하위태그에서만 사용할 수 있다.     
                  ```      
      ex)      
      <div th:with="userid=${number}"> <p th:text="${userid}"></p> <div>   
                  ```   
   7. th:value="${}" : input의 value에 값을 넣을 때 사용한다.
                       여러개의 값을 넣을 땐 + 기호를 사용한다.
      ```   
      ex) <input type="text" th:value="${userid}">
      ```   
   9. th:block : block은 타임리프 표현을 어느 곳에서든 사용할 수 있도록 하는 구문이다. 동적인 처리가 필요할 때 사용. layout기능이나 switch에 많이 사용.
                   ex) <th:block th:with="userid=${number}"></th:block>
   10. th:if, th:unless : 조건문 if, else
                   ex) <p th:if="${student.grade > 80}">합격</p>
                       <p th:unless="${student.grade > 80}">불합격</p>
   11. th:each, 상태변수 : th:each를 사용할때 기본적으로 status 변수를 제공해주고 이를 이용하여 index나 count등의 값을 사용할 수 있다.
                         기본적으로 변수명Stat로 사용할 수 있다. 
                         index : 현재 인덱스(0부터 시작)
                         count : 현재 인덱스(1부터 시작)
                         size : 전체 개수
                         current : 현재 요소
                         even : 현재 반복이 짝수인지(boolean)
                         odd : 현재 반복이 홀수인지(boolean)
                         first : 현재 반복이 첫번째인지(boolean)
                         last : 현재 반복이 마지막인지(boolean)
                   ex) <tr th:each="student : ${studentList}">
                           <td th:text="|${student.id} : ${student.name}"></td>
                           <td th:text=${'index : ' + studentStat.index}></td>
                       </tr>
    9.  <!-- /* 이렇게 하면 타임리프 파싱될 때 일반 html 주석이 아니라 타임리프 주석으로 처리되어 클라이언트에서 볼 수 없습니다. 소스보기에서 숨겨야 하는 주석일 경우 타임리프 주석으로 처리하면 됩니다. :) */ --
                       - 쿼리 파라미터





