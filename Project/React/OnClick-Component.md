### 클릭 & state 활용   
ex ) ♥를 눌렀을 때 숫자 증가   
```
let [heart, setHeart] = useState(0);
return(
  <div>
    <p>{title[0]} <span onClick={()=>{setHeart(heart+1)}}>♥</span>{heart}</p>
  <div>
);
```

### state 복사 활용
```   
let [list, setList] = useState('list1', 'list2', 'list3');   
function changeList(){   
  let newList = [...list];   
  newList[0] = 'list99999';   
  setList(newList);   
}   
```
- 복사할 때는 deep copy를 해야한다. let newList = list이라고 하면 값을 공유하는 것. let newList = [...list]의 형식으로 복사를 해야한다.   

### Component   
```
function App() {   
  return(   
    <div className='App'>   
      <Modal></Modal>   
    <div>   
  );   
}   

function Modal(){    
  return(    
    <div className='modal'>   
      <p>제목</p>   
      <p>날짜</p>    
      <p>상세내용</p>   
    </div>   
  );   
}   
```   
- 함수를 만들어주고 그 안에 HTML을 넣는다.
- 해당 HTML을 넣어줄 위치에 <함수명></함수명> 넣는다.
- Component의 이름은 대문자로 시작하도록 만들고, return() 안에 태그 하나로 묶어서 사용한다. ```<></>```를 사용해서 html을 묶어줄 수 있다.
- Component는 function App()과 같은 선상에서 만들어 주면 된다.
- 반복사용, 자주 바뀌는 HTML UI(재렌더링 자주), 다른 페이지 만들 때 => Component 사용한다.
- 상위 컴포넌트에서 만든 state를 마음대로 사용할수 없어 props 문법을 사용해야 하기 때문에 컴포넌트를 너무 많이 만들면 복잡해진다.
