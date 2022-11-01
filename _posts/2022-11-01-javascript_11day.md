---
title: Javascript 11일차
updated: 2022-11-01 23:54
---

### 49번 문제 함수 한개로 만들기 도전 중

##### 실패 흔적들
```javascript
function deepCopyObject(obj) {
  const ret1 = [];
  const ret2 = {};
  for (k in obj) {
    const v = obj[k]
    // console.log(k)
    console.log("1층 -",v, typeof(v))
    if (Array.isArray(v)) {
      console.log("2층 어레이",v, "-개별 인덱스 :",v[0],v[1],v[2],v[3],v[4])
      for (let s = 0; s<v.length; s+=1) {
        console.log(v[s], typeof(v[s]))
      }
    }
    else if (typeof(v) === 'object') {
      console.log("2층 타입오브", v)
      for (i in v) {
        console.log("3층: ", i)
      }
    }
    else {
      ret2[k] = obj[k]
    }
    // if (Array.isArray(v)) {
    //   deepCopyObject(v)
    // }
    // else if (typeof v === 'object') {
    //   deepCopyObject(v)
    // }
    // else {
    //   ret.push(v)
    // }
  }
  return ret2
}
// ----------------------------------------------------------------------

// function abc(obj) {
//   const newobj = {};
//   for (k in obj) {
//     newobj[k] = obj[k]
//   }
//   return newobj
// }

const kim = {
	nid: 3,
	addr: 'Pusan',
	arr: [1, 2, 3, { aid: 1 }, [10, 20]],
	oo: { id: 1, name: 'Hong', addr: { city: 'Seoul' } },
};



const newkim = deepCopyObject(kim);
newkim.addr = 'Daegu';
// newkim.oo.name = 'kim';
// newkim.arr[0] = 100;
// newkim.arr[3] = 200;
// newkim.arr[4][1] = 300;
// newkim.oo.addr.city = 'Daejeon';
console.log('kim = ', kim)
console.log('new kim = ', newkim);

for (i in newkim) {
  console.log("현재 newkim의 키의 값 : ",i,)
}

// const newKim = deepCopyObject(kim);
// newKim.addr = 'Daegu';
// newKim.oo.name = 'Kim';
// newKim.arr[0] = 100;
// newKim.arr[3].aid = 200;
// newKim.arr[4][1] = 300;
// newKim.oo.addr.city = 'Daejeon';
// console.log('kim= ',kim, 'newkim =', newKim);
// console.log(kim, newKim); // oo와 arr이 다르면 통과!
```

##### 새로 도전중

```javascript
// function deepCopyObject(obj) {
//   const ret1 = [];
//   const ret2 = {};
//   for (k in obj) {
//     const v = obj[k]
//     console.log(k)
//     console.log("1층 -",v, typeof(v))
//     if (Array.isArray(v)) {
//       console.log("2층 어레이",v, "-개별 인덱스 :",v[0],v[1],v[2],v[3],v[4])
//       for (let s = 0; s<v.length; s+=1) {
//         console.log(v[s], typeof(v[s]))
//       }
//     }
//     else if (typeof(v) === 'object') {
//       console.log("2층 타입오브", v)
//       for (i in v) {
//         console.log("3층: ", i)
//       }
//     }
//     else {
//       ret2[k] = obj[k]
//     }
//   }
//   return ret2
// }

const { arrayBuffer } = require("stream/consumers")


// function deepCopyObject(obj) {
//   const ret1 = {}
//   for (i in obj) {
//     // console.log(i, typeof(obj[i]))
//     if (typeof(obj[i]) === 'object' && Array.isArray(obj[i])) {
//       console.log(obj[i], typeof(obj[i]))
//       deepCopyObject(obj[i])
//       ret1[i] = obj[i]
//     } 
//     else {
//       ret1[i] = obj[i]
//     }
//   }
//   return ret1
// }

function deepCopyObject(obj) {
  const ret1 = {}
  for (i in obj) {
    console.log("i의 값 : ",i, typeof(i))
    console.log("obj[i]의 값 : ", obj[i], typeof(obj[i]))
    if (Array.isArray(obj[i])) {
      console.log("if - obj[i]의 값 : ", obj[i], typeof(obj[i]))
      ret1[i] = []
      // for (let k = 0; k < obj[i]; k+=1) {
      //   console.log("k의값 : ",k)
 
      // }
      deepCopyObject(obj[i])
      
    }
    else if (typeof(obj[i]) === 'object' ) {
      console.log("else if- obj[i]의 값 : ", obj[i])
      ret1[i] = {}
      for (let k = 0; k < obj[i].length; k+=1) {
        console.log("k의값 : ",k)
        ret1[i][k] = obj[i][k]
      }
       
      deepCopyObject(obj[i])

    }
    else {
      ret1[i] = obj[i]
    }
  }
  return ret1
}

const kim = {
	nid: 3,
	addr: 'Pusan',
	arr: [1, 2, 3, { aid: 1 }, [10, 20]],
	oo: { id: 1, name: 'Hong', addr: { city: 'Seoul' } },
};

const newkim = deepCopyObject(kim);
newkim.addr = 'Daegu';
// newkim.oo.name = 'kim';
// newkim.arr[0] = 100;
// newkim.arr[3] = 200;
// newkim.arr[4][1] = 300;
// newkim.oo.addr.city = 'Daejeon';
console.log('kim = ', kim)
console.log('new kim = ', newkim);

for (i in newkim) {
  console.log("현재 newkim의 키의 값 : ",i,)
}


```

### 애매한 버전

* 어느정도 되긴하는데, 재귀함수가 작동하지 않음

```javascript
// function deepCopyObject(obj) {
//   const ret1 = [];
//   const ret2 = {};
//   for (k in obj) {
//     const v = obj[k]
//     console.log(k)
//     console.log("1층 -",v, typeof(v))
//     if (Array.isArray(v)) {
//       console.log("2층 어레이",v, "-개별 인덱스 :",v[0],v[1],v[2],v[3],v[4])
//       for (let s = 0; s<v.length; s+=1) {
//         console.log(v[s], typeof(v[s]))
//       }
//     }
//     else if (typeof(v) === 'object') {
//       console.log("2층 타입오브", v)
//       for (i in v) {
//         console.log("3층: ", i)
//       }
//     }
//     else {
//       ret2[k] = obj[k]
//     }
//   }
//   return ret2
// }

const { arrayBuffer } = require("stream/consumers")


// function deepCopyObject(obj) {
//   const ret1 = {}
//   for (i in obj) {
//     // console.log(i, typeof(obj[i]))
//     if (typeof(obj[i]) === 'object' && Array.isArray(obj[i])) {
//       console.log(obj[i], typeof(obj[i]))
//       deepCopyObject(obj[i])
//       ret1[i] = obj[i]
//     } 
//     else {
//       ret1[i] = obj[i]
//     }
//   }
//   return ret1
// }

function deepCopyObject(obj) {
  const ret1 = {}
  for (i in obj) {
    console.log("i의 값 : ",i, typeof(i))
    console.log("obj[i]의 값 : ", obj[i], typeof(obj[i]))
    if (Array.isArray(obj[i])) {
      console.log("if - obj[i]의 값 : ", obj[i], typeof(obj[i]))
      ret1[i] = []
      for (k in obj[i]) {
        console.log("[]k의값 : ",k)

        ret1[i][k] = obj[i][k]
 
      }
      deepCopyObject(obj[i])
      
    }
    else if (typeof(obj[i]) === 'object' ) {
      console.log("else if- obj[i]의 값 : ", obj[i])
      ret1[i] = {}
      
      for (k in obj[i]) {
        console.log("k의값 : ",k)
        
        ret1[i][k] = obj[i][k]
        
      }
      deepCopyObject(obj[i])
    }
    else {
      ret1[i] = obj[i]
    }
  }
  return ret1
}

const kim = {
	nid: 3,
	addr: 'Pusan',
	arr: [1, 2, 3, { aid: 1 }, [10, 20]],
	oo: { id: 1, name: 'Hong', addr: { city: 'Seoul' } },
};

const newkim = deepCopyObject(kim);
newkim.addr = 'Daegu';
newkim.oo.name = 'kim';
newkim.arr[0] = 100;
newkim.arr[3] = 200;
// newkim.arr[4][1] = 300;
newkim.oo.addr.city = 'Daejeon';
console.log('kim = ', kim)
console.log('new kim = ', newkim);

for (i in newkim) {
  console.log("현재 newkim의 키의 값 : ",i,)
}

```

출력값

```javascript
[nodemon] clean exit - waiting for changes before restart
[nodemon] restarting due to changes...
[nodemon] starting `node 22.11.01_homework.js`
Debugger attached.
i의 값 :  nid string
obj[i]의 값 :  3 number
i의 값 :  addr string
obj[i]의 값 :  Pusan string
i의 값 :  arr string
obj[i]의 값 :  [ 1, 2, 3, { aid: 1 }, [ 10, 20 ] ] object
if - obj[i]의 값 :  [ 1, 2, 3, { aid: 1 }, [ 10, 20 ] ] object
[]k의값 :  0
[]k의값 :  1
[]k의값 :  2
[]k의값 :  3
[]k의값 :  4
i의 값 :  0 string
obj[i]의 값 :  1 number
i의 값 :  1 string
obj[i]의 값 :  2 number
i의 값 :  2 string
obj[i]의 값 :  3 number
i의 값 :  3 string
obj[i]의 값 :  { aid: 1 } object
else if- obj[i]의 값 :  { aid: 1 }
k의값 :  aid
i의 값 :  aid string
obj[i]의 값 :  1 number
i의 값 :  4 string
obj[i]의 값 :  [ 10, 20 ] object
if - obj[i]의 값 :  [ 10, 20 ] object
[]k의값 :  0
[]k의값 :  1
i의 값 :  0 string
obj[i]의 값 :  10 number
i의 값 :  1 string
obj[i]의 값 :  20 number
i의 값 :  oo string
obj[i]의 값 :  { id: 1, name: 'Hong', addr: { city: 'Seoul' } } object
else if- obj[i]의 값 :  { id: 1, name: 'Hong', addr: { city: 'Seoul' } }
k의값 :  id
k의값 :  name
k의값 :  addr
i의 값 :  id string
obj[i]의 값 :  1 number
i의 값 :  name string
obj[i]의 값 :  Hong string
i의 값 :  addr string
obj[i]의 값 :  { city: 'Seoul' } object
else if- obj[i]의 값 :  { city: 'Seoul' }
k의값 :  city
i의 값 :  city string
obj[i]의 값 :  Seoul string
kim =  {
  nid: 3,
  addr: 'Pusan',
  arr: [ 1, 2, 3, { aid: 1 }, [ 10, 20 ] ],
  oo: { id: 1, name: 'Hong', addr: { city: 'Daejeon' } }
}
new kim =  {
  nid: 3,
  addr: 'Daegu',
  arr: [ 100, 2, 3, 200, [ 10, 20 ] ],
  oo: { id: 1, name: 'kim', addr: { city: 'Daejeon' } }
}
현재 newkim의 키의 값 :  nid
현재 newkim의 키의 값 :  addr
현재 newkim의 키의 값 :  arr
현재 newkim의 키의 값 :  oo
Waiting for the debugger to disconnect...
[nodemon] clean exit - waiting for changes before restart
```