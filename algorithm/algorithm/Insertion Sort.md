# Insertion Sort

## 삽입정렬이란?

카드게임을 하고 있다고 가정을 해보자. 나는 이미 4개의 정렬된 패를 가지고 있다. 그런데 딜러가 새로운 카드를 줬고 이 카드가 제자리에 들어가게 하는 상황 일 때처럼 정렬하는 것을 삽입 정렬이라고 한다.

### 삽입 함수

n+1개의 배열을 가지고 있고 마지막 인덱스의 값이 새로 추가하는 값이라고 가정할 때 로직은 아래와 같다.

1.  새로운 변수인 key를 선언하고 새로 추가하는 값인 array[n+1]을 할당한다.
2.  key와 array[n]의 값을 비교한다.
3.  key < array[n] 일 경우 array[n+1]에 array[n] 값을 넣는다.(slide)
4.  key와 array[n-1]을 비교하고 slide한다.
5.  key >= array[i] 일 때까지 반복한다.
6.  array[i+1]에 key값을 삽입한다.

마지막 프로세스의 경우 

현재 i의 값은 key보다 작거나 같을것이고,

i+1와 i+2의 값은 slide되어 같을 것이다. 따라서 i+1에 삽입한다.

```java
// n+1개의 배열을 가지고 있고 마지막 인덱스의 값이 새로 추가하는 값이라고 가정할 때 올바른 자리에 삽입하는 메서드다.
static void insert(int[] array, int rightIndex, int value) {
  int key = array[value]; // key라는 새로운 변수로 추가하는 값을 복사한다.
  int i = rightIndex; // rightIndex부터 i--해서 반복할 것이다.
  while (i >= 0 && array[i] > key) { // key가 제자리를 찾을 때까지 비교한다.
    array[i + 1] = array[i];       // slide를 구현했다. 오른쪽 인덱스에 자신의 값을 복사한다.
    i--;
  }
  array[i+1] = key;                   // 복사한 key를 제자리에 넣어준다.
}
```

### 삽입정렬 구현

삽입하는 함수를 위에서 구현했다. 삽입정렬은 우리가 딜러에게 카드를 받기 전에 카드를 1개만 들고 있는 경우라고 가정하면 된다. 가지고 있는 카드가 1장이면 이 카드는 한 장이니까 정렬되어 있다고 말할 수 있다. 카드를 한장받고 삽입함수를 실행하고 또 한장을 받고 실행, 카드를 받고 실행, 받고 실행, 받고 실행하듯 index = 0부터 index = array.length 까지 반복하면 될 것이다. 

쉽게 정리하자면 정렬하려는 array  함수가 있다고 가정하자.

1. 우리는 1개의 배열을 가지고 있고 새로운 값을 추가한다.
   * 1개의 배열은 1개니까 정렬되어 있고 삽입 함수를 실행했으니 2개의 배열은 정렬되었다.
2. 우리는 2개의 배열을 가지고 있고 새로운 값을 추가한다.
3. ...
4. 우리는 n-1개의 배열을 가지고 있고 새로운 값을 추가하였다. 따라서 n개의 배열은 정렬되었다.

코드로 보면 조금 더 편하다.

```java
// insert를 반복하여 전체 n개의 배열을 정렬하는 메서드다.
static void insertSort(int[] array){
  // 자기자신을 비교할 필욘 없으니 1부터 n-1번 반복한다.
  for (int i = 1; i<array.length; i++) {
    insert(array, i - 1, i);
  }
}
```

### 분석

크게 프로세스는 두가지로 나눌 수 있다.

1. insert method
2. insertSort method

2번이 1번을 호출하는 구조이니 2번부터 보자.

#### insertSort

이 함수의 경우 모든경우 for문을 n-1번 반복한다. 따라서 Θ(n-1)이 된다.

#### insert

이 함수의 경우 while 반복문을 사용했다. 반복문이 몇번 될지는 모른다. key의 값이 제자리를 찾을때까지 반복하기 때문에 1번만 실행해서 제자리를 찾을 수도(이미 정렬되어있다면), rightIndex+1번 반복할 수 도 있다. 

따라서 전체 프로세스는 간단하게 O(n^2)이라고 표현할 수 있을 것이다. 좀 더 정리를 해보자면

- 최악의 경우: O(n^2)
- 최상의 경우: Ω(n)
- 임의의 배열에 대한 평균적 경우: Θ(n^2)