### 1. JSX - ClassName   
- index.js가 App.js에 있는 HTML을 index.html에 넣어주기 때문에 App.js의 코드가 보여진다.   
- React에서는 HTML처럼 생겼지만 똑같지 않은 JSX 문법을 사용한다.   
- 클래스명을 지정할때는 className="클래스명" 으로 사용한다.   

### 2.  데이터 바인딩
- 중괄호 {}에 변수,함수,이미지 등을 넣어서 데이터를 쉽게 넣을 수 있다.
  ```
  import logo from './logo.svg';
  ...
  ...
  let posts = 'hello react'
  function test(){
    return 'bye react';
  }
  
  return(    
    <div className="App">   
      <p>{posts}</p>
      <p>{test()}</p>
      <img src={logo}/>
    </div>   
  );
  ```
### 3. style 속성
- 오브젝트 형식으로 넣어줘야 하고, 중괄호를 활용한다.   
  ```   
  <div style={{color:"red", fontSize:"25px"}}>Hello React</div>
  ```

### 4. state
- 데이터는 변수에 넣거나 state에 넣어서 사용 가능하다.   
- state를 사용하기 위해서 import {useState} from 'react'; 임포트 추가.   
- let [a,b] = useState('씨부렁씨부렁') 의 형태로 사용한다. a는 데이터, b는 데이터를 변경하는 함수가 된다.
- 문자, 숫자, array, object와 같은 형식들 모두 저장 가능하다.   
 ```
 let [title, setTitle] = useState(["제목1", "제목2"]);   
 return(    
    <div>
      <p>{title[0]}</p>   
    </div>   
 );
 ```
- state는 웹/앱 사이트에서 데이터가 바뀌면 새로고침 없이도 HTML이 자동으로 재렌더링된다. => 변경이 잦은 데이터는 state를 사용.


참조  : https://velog.io/@kiyoog02/React-%EA%B8%B0%EC%B4%88-2-JSX%EC%99%80-state-%EC%82%AC%EC%9A%A9  
  
