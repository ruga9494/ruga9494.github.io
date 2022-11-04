---
title: react 1일차
updated: 2022-11-04 23:12
---

```javascript
import { useEffect, useRef, useState } from 'react';
import { useSession } from '../hooks/session-context';
import { Login } from './Login';
import { Profile } from './Profile';

// export const My = ({ session, login, logout, removeCartItem }) => {
export const My = () => {
  // console.log('@@@ My');
  const { session, removeCartItem } = useSession();
  const [sec, setSec] = useState(0);
  const ulRef = useRef();

  // run * 2 ===> (render -> [useLayoutEffect] -> mount -> [useEffect]) -> unMount -> mount
  /*
  [1, 2, 3].reduce((pre, a) => pre + a, 0);

  pre      currentValue(a)         action
   0             1                 0 + 1
   1             2                 1 + 2
   3             3                 3 + 3
   return 6;
*/
  const astyle = {
    color: 'black',
    backgroundColor: '',
    fontFamily: 'Arial',
    height: 1500,
    width: 800,
    border: '1px solid black',
  };
  const bstyle = {
    color: 'black',
    backgroundColor: '',
    fontFamily: 'Arial',
    height: 50,
    width: 100,
    border: '1px solid black',
    margin: 10,
  };

  useEffect(() => {
    // console.log('ul-height>>', ulRef.current.clientHeight);
    const intl = setInterval(() => {
      setSec((sec) => sec + 1);
    }, 1000);

    return () => clearInterval(intl);
  }, []);

  return (
    <>
      <div>sec: {sec}</div>
      {session.loginUser ? (
        // <Profile session={session} logout={logout} />
        <Profile />
      ) : (
        // <Login login={login} />
        <Login />
      )}

      <div style={astyle}>
        <button style={bstyle}>글쓰기</button>
        <ul ref={ulRef}>
          {session.cart.map((item) => (
            <li key={item.id}>
              {item.name} <small>(₩{item.price.toLocaleString()})</small>
              <button onClick={() => removeCartItem(item.id)}>X</button>
            </li>
          ))}
        </ul>
      </div>
    </>
  );
};
```

* import는 다른 폴더에서 불러오는거임
* export는 밖에서 꺼내쓸 수 있게 하는거임
* 그 밑에는 변수 잡아주는거임 = 밖에서 불러온 무언가
<br>

* astyle, bstlye은 css 요소 넣음
* useEffect는 시간설정해주는거 
* return 아래는 html, js 섞어 놨음
<br>

* html 처럼 틀 잡아주고 그 안에 js 작동하게끔 만들어놈
* 제일 밖에 div가 큰틀 
* button은 글쓰기 버튼
* ul쪽은 다른 폴더에서 불러온 'cart'라는 요소를 map시켜버리기 (요소 하나하나씩 꺼내줌)
* li쪽은 아이템의 아이디를 key로 잡는다
* 아이템 이름을 적고 그다음 아이템 가격을 적는다 이말이다 이말이야
* 그리고 버튼 이벤트를 만들어서 removeCartItem 함수를 실행하게 한다. 누르면 아이템아이디가 없어짐 / 리엑트세계에서도 지워짐