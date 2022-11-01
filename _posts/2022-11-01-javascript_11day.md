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