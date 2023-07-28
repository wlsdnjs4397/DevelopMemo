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
  
  
  
