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
