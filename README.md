# JS100_2
JS 알고리즘 100문제 모음집 2권
<br>
<br>

## 51. merge sort를 만들어보자
💡 문제 : 병합정렬(merge sort)은 대표적인 정렬 알고리즘 중 하나로 다음과 같이 동작합니다.

> 1. 리스트의 길이가 0 또는 1이면 이미 정렬된 것으로 본다. 그렇지 않은 경우에는
> 2. 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다.
> 3. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다.
> 4. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다.
(출처 : 위키피디아)

다음 코드의 빈칸을 채워 병합정렬을 완성해 봅시다.
```js
function mergeSort(arr){
  if (arr.length <= 1){
    return arr;
  }

  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0,mid);
  const right = arr.slice(mid);

  return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right){
  let result = [];

  while (/*빈칸을 채워주세요*/ && /*빈칸을 채워주세요*/){
    if (/*빈칸을 채워주세요*/){
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  while (left.length) {
    /*빈칸을 채워주세요*/
  }
  while (right.length) {
    /*빈칸을 채워주세요*/
  }

  return result;
}

const array = prompt('배열을 입력하세요').split(' ').map(n => parseInt(n, 10));

console.log(mergeSort(array));
```
<strong>- 내가 푼 답</strong>
```js
function mergeSort(arr){                               // 3. array를 파라미터로 받음
  if (arr.length <= 1){                                //    if문으로 배열의 길이가 1보다 작거나 같으면 반환하는 조건
    return arr;                                        
  }

  const mid = Math.floor(arr.length / 2);              // 4. merge sort는 배열을 균등하게 나누기 때문에 기준이 되는 mid 설정
  const left = arr.slice(0,mid);                       //    왼쪽배열, 0부터 mid - 1까지
  const right = arr.slice(mid);                        //    오른쪽배열, mid부터 끝까지

  return merge(mergeSort(left), mergeSort(right));     //    if문에 들어가지 않았다면 아직 길이가 2이상이기 때문에 재귀로 다시 돌림
}
function merge(left, right){                           // 5. mergeSort에서 왼쪽배열, 오른쪽배열로 나눠준 것을 매개변수로 받음
  let result = [];                                     //    merge sort는 새로운 리스트를 필요로한다 의 그 새로운 리스트

  while (left.length && right.length){                 // 6. 아직까지 크기 비교하는 부분이 없네? 그럼 merge가 비교하는 함수구나, 파라미터로 들어온 건 써야지
    if (left[0] < right[0]){                           //    정렬이 완료된 리스트를 합병하는 로직 : 2개의 리스트의 값들을 처음부터 하나씩 비교하여  
      result.push(left.shift());                       //    두 개의 리스트의 값 중에서 더 작은 값을 새로운 리스트(sorted)로 옮긴다.
    } else {
      result.push(right.shift());
    }
  }
  while (left.length) {
    result.push(left.shift());
  }
  while (right.length) {
    result.push(right.shift());
  }

  return result;
}

const array = prompt('배열을 입력하세요').split('').map(n => parseInt(n, 10)); // 1. 문자열로 받은 것을 공배으로 나눠주고 map으로 돌면서 정수화 (split 수정)
console.log(mergeSort(array));                                             // 2. mergeSort함수에 array를 아규먼트로 전달

```
<br>

## 52. quick sort
💡 문제 : 다음 빈 칸을 채워 퀵 정렬을 완성해주세요.
```js
function quickSort(arr){
  if (arr.length <= 1){
    return arr;
  }

  const pivot = arr[0];
  const left = [];
  const right = [];

  for (let i=1; i<arr.length; i++){
    if(/*빈칸을 채워주세요*/){
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }
  return /*빈칸을 채워주세요*/
}

const array = prompt('배열을 입력하세요').split(' ').map(n => parseInt(n, 10));

console.log(quickSort(array));
```
 <strong>- 내가 푼 답</strong>
```js
function quickSort(arr){  //만약 배열의 길이가 1이하이면 정렬완료로 보고 리턴
  if (arr.length <= 1){
    return arr;
  }

  const pivot = arr[0]; //퀵 솔트는 머지솔트와 다르게 리스트를 비균등하게 나누기 때문에 기준점을 임의로 설정한다.
  const left = []; //왼쪽배열 담을 공간
  const right = []; //오른쪽 배열 담을 공간

  for (let i=1; i<arr.length; i++){ // 피벗을 인덱스 0으로 잡았기 때문에 1부터 시작함
    if(arr[i] < pivot){  // 작으면 왼쪽에
      left.push(arr[i]);
    } else {
      right.push(arr[i]); // 크면 오른쪽배열에 푸쉬
    }
  }
  return quickSort(left).concat(pivot, quickSort(right)); //concat : 두개의 문자열을 하나로 합쳐주는 메서드, 지금처럼 쓰면 세개를 이어줌
}

const array = prompt('배열을 입력하세요').split('').map(n => parseInt(n, 10)); // 왜 이거 자꾸 스플릿 공백으로 받는걸까?

console.log(quickSort(array)); //quickSort함수에 array를 배열로 넘겨줌

}

const array = prompt('배열을 입력하세요').split('').map(n => parseInt(n, 10));

console.log(quickSort(array));
 ```

<br>

## 53.  괄호 문자열
💡 문제 : 괄호 문자열이란 괄호 기호인 '{', '}', '[', ']', '(', ')' 와 같은 것을 말한다. 그중 괄호의 모양이 바르게 구성된 문자열을 바른 문자열, 그렇지 않은 문자열을 바르지 않은 문자열이라 부르도록 하자. 
(())와 같은 문자열은 바른 문자열이지만 ()()) 와 같은 문자열은 바르지 않은 문자열이다.
(해당 문제에서는 소괄호만 판별하지만,  중괄호와 대괄호까지 판별해 보세요.)
입력으로 주어진 괄호 문자열이 바른 문자열인지 바르지 않은 문자열인지 "YES"와 "NO"로 구분된 문자열을 출력해보자.

 <strong>- 내가 푼 답</strong>
```js
const input = prompt('체크하고싶은 괄호를 입력하세요').split('')

let countLeft = 0;
let countRight = 0;
for (let i = 0; i < input.length; i++){
  if ((input2[i] === '(' || input[i] === '{' || input[i] === '[') && (i % 2 === 0){
    countLeft++;
    console.log(i, countLeft)
  } 
  if ((input[i] === ')' || input[i] === '}' || input[i] === ']') && (i % 2 === 1)){
    countRight++;
    console.log(i, countRight)
  }
}  
  if (countLeft === countRight){
    console.log('YES')
  } else {
    console.log('NO')
  }
  
  // 열린괄호가 먼저 와야된다는 조건 충족안됨
  // 괄호별로 경우 다 나눠서 카운트를 다른 변수에서 셀까?
  // 진짜 멋없다 
  // (해당 문제에서는 소괄호만 판별하지만, 중괄호와 대괄호까지 판별해 보세요.) -> ? 문제를 잘 읽읍시다.
 ```
 ```js
const input = prompt('확인하고싶은 괄호를 입력하세요').split('');

let count= 0;

for (let i = 0; i < input.length; i++){
  if (input[i] === '('){
    count++;
    console.log(i, count)
  } 
  if (input[i] === ')'){
    count--;
    console.log(i, count)
  }
  if (count < 0){
    break;
  }
} 

if (count === 0){
  console.log('YES');
} else {
  console.log('NO');
}
 ```
<br>

## stack
```js
스택 :  차곡차곡 쌓아 올린 형태의 자료구조
정해진 방향 (top)을 통해서만 접근 가능
top을 통해 삽입하는 연산을 'push' , top을 통한 삭제하는 연산을 'pop'
가장 마지막에 삽입된 자료가 가장 먼저 삭제
후입선출(LIFO, Last-In-First-Out) 구조

웹 브라우저 방문기록 (뒤로 가기) : 가장 나중에 열린 페이지부터 다시 보여준다. // 오오 대박 이렇게 쓰는거구나
역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력한다.
실행 취소 (undo) : 가장 나중에 실행된 것부터 실행을 취소한다.
후위 표기법 계산 : 컴퓨터가 연산하기 쉽게(?) 연산자를 나중에 써주는 것 // 연산자는 스택에 담고 숫자는 그대로 표기 1+2*3이면 스택에서는 후입선출이기 때문에 123*+
수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사) //53번 문제를 예시로 `가장 나중에 쌓은 열린 괄호`를 `닫힌 괄호가 들어 왔을 때 가장 먼저 pop`했음

```
<br>

## 54. 연속되는 수
💡 문제 : 은주는 놀이공원 아르바이트를 하고 있다. 은주가 일하는 놀이공원에서는 현재 놀이공원 곳곳에 숨겨진 숫자 스탬프를 모아 오면 선물을 주는 이벤트를 하고 있다. 숫자 스탬프는 매일 그 수와 스탬프에 적힌 숫자가 바뀌지만 그 숫자는 항상 연속된다. 
그런데 요즘 다른 날에 찍은 스탬프를 가지고 와 선물을 달라고 하는 손님이 늘었다.

스탬프에 적힌 숫자가 공백으로 구분되어 주어지면 이 숫자가 연속수인지 아닌지 "YES"와 "NO"로 판별하는 프로그램을 작성하시오
```js
입력1
1 2 3 4 5

출력1
YES


입력2
1 4 2 6 3

출력2
NO
```
<strong>- 내가 푼 답</strong>
```js
const input = prompt('정수를 공백으로 구분하여 입력').split(' ')

const sortInput = input.sort((a, b) => a - b);
let count = 0;
for(let i = 0; i < sortInput.length-1; i++){
  if (parseInt(sortInput[i]) + 1 !== parseInt(sortInput[i+1])) {
    count++;
  }
}
if (count !== 0){
  console.log('NO');
} else {
  console.log('YES');
}
```
<br>

## 55. 하노이의 탑
💡 문제 : 하노이의 탑은 프랑스 수학자 에두아르드가 처음으로 발표한 게임입니다. 하노이의 탑은 A, B, C 3개의 기둥과 기둥에 꽂을 수 있는 N 개의 원판으로 이루어져 있습니다. 이 게임에서는 다음의 규칙을 만족해야 합니다.

> 1. 처음에 모든 원판은 A 기둥에 꽂혀 있다.
> 2. 모든 원판의 지름은 다르다.
> 3. 이 원반은 세 개의 기둥 중 하나에 반드시 꽂혀야 한다.
> 4. 작은 원반 위에 큰 원반을 놓을 수 없다.
> 5. 한 번에 하나의 원판(가장 위에 있는 원판)만을 옮길 수 있다.

이 규칙을 만족하며 A 기둥에 있는 원반 N 개를 모두 C 원반으로 옮기고 싶습니다.
모든 원반을 옮기기 위해 실행되어야 할 최소 원반 이동 횟수를 계산하는 프로그램을 완성해 주세요.
```js
const route = [];

function hanoi(num, start, end, temp){
  //원판이 한 개일 때에는 바로 옮기면 됩니다.
  if (num === 1) {                       
    route.push([start, end]);            
    return NaN;                          
  }                                     

  //원반이 n-1개를 경유기둥으로 옮기고
  hanoi(/*내용을 채워주세요.*/);
  //가장 큰 원반은 목표기둥으로
  route.push(/*내용을 채워주세요.*/);
  //경유기둥과 시작기둥을 바꿉니다.
  hanoi(/*내용을 채워주세요.*/);
}

hanoi(3, 'A', 'B', 'C');                 
console.log(route);
console.log(route.length);
```

<strong>- 내가 푼 답</strong>
```js
const route = [];

function hanoi(num, start, end, temp){
  //원판이 한 개일 때에는 바로 옮기면 됩니다.
  if (num === 1) {                     //원반이 하나라면
    route.push([start, end]);          //루트에 [A, C] -> [[A, C]]
    return NaN;                        //return NaN의 의미 : 유효한 연산이 아니어서 NaN 값을 통해 잘못된 결과임을 인식하고,
  }                                    //필요에 따라 이를 처리할 수 있도록 하는 것

  //원반이 n-1개를 경유기둥으로 옮기고
  hanoi(num-1, start, temp, end);      //더 작은 값으로 자기 자신을 호출해서 n-1개의 원반을 경유 기둥으로 옮김 : 대체 여기서 어떻게 n-1개가 큰거부터 쌓이는데....????
  //가장 큰 원반은 목표기둥으로
  route.push([start, end]);            //여기는 이해
  //경유기둥과 시작기둥을 바꿉니다.
  hanoi(num-1, temp, end, start);      //실행순서가 hanoi(num-1, start, temp, end); 이걸 다 돌리고 여기로 넘어온다는데....
}

hanoi(3, 'A', 'B', 'C');               //3 : 원반개수, A : 시작기둥, B : 경유기둥, C : 목표기둥
console.log(route);
console.log(route.length);
```
<br>


## 56. 객체의 함수 응용
💡 문제 : 다음의 객체가 주어졌을 때 한국의 면적과 가장 비슷한 국가와 그 차이를 출력하세요.

```js
데이터
nationWidth = {
     'korea': 220877,
     'Rusia': 17098242,
     'China': 9596961,
     'France': 543965,
     'Japan': 377915,
     'England' : 242900,
}

출력
England 22023
```
<strong>- 내가 푼 답</strong>
```js
const nationWidth = {
  'korea': 220877,
  'Rusia': 17098242,
  'China': 9596961,
  'France': 543965,
  'Japan': 377915,
  'England': 242900,
};
const nationWidthToArray = Object.values(nationWidth);

const changedArray = []
for (let i = 1; i < nationWidthToArray.length; i++){
  let changed = nationWidthToArray[i] - nationWidthToArray[0];
  if(changed < 0) {
    changedArray.push(-1 * changed)
  } else {
    changedArray.push(changed);
  }
} 
const result = changedArray.sort((a, b) => a - b)
console.log(result[0])

```
<br>

## 57. 1의 개수
💡 문제 : 0부터 1000까지 1의 개수를 세는 프로그램을 만들려고 합니다. 예를 들어 0부터 20까지 1의 개수를 세어본다면 1, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19에 각각 1이 들어가므로 12개의 1이 있게 됩니다. 11은 1이 2번 들어간 셈이죠.
그렇다면 0부터 1000까지의 수에서 1은 몇 번이나 들어갔을까요? 출력해 주세요.
<br>

<strong>- 내가 푼 답</strong>
```js
let str = '';
let count = 0;
for (let i = 0; i <= 1000; i++) {
  str += i;
}
const strToArr = str.split('');
strToArr.forEach(e => {
  if (e === '1') {
    count++;
  }
});
console.log(count);
```
<br>

## ㅇㅇ. 템플릿
💡 문제 : 
```js
ㅇㅇ
```
<strong>- 내가 푼 답</strong>
```js
ㅇㅇ
```
<br>
