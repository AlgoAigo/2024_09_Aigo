# 피보나치수

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12945
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv2

## 문제 풀이

### 문제 내용 정리
2이상의 n에 대해 피보나치 수 구하여 1234567로 나눈 나머지 반환.

### 문제 유형
재귀 또는 DP

### 실패 상황
재귀 함수를 호출하도록 피보나치를 구현했더니 일부 테스트 케이스에서 시간 초과 발생
-> 피보나치를 재귀적으로 구현할 경우 O(2^n)의 시간복잡도를 가지는데 n의 범위가 2 ~ 100,000 이기 때문에 최악의 경우 2의 10만 제곱에 해당하는 연산을 수행한다.

```kotlin
class Solution {
    fun solution(n: Int): Int {
        return fibonacci(n) % 1234567
    }
    
    fun fibonacci(num: Int): Int {
        if (num == 0) return 0
        else if (num == 1) return 1
        else return fibonacci(num-2) + fibonacci(num-1)
    }
}
```

### 풀이 방법
메모리제이션을 통해 f(n)을 구할 때 이미 앞선 연산을 통해 값이 구해진 f(n-1), f(n-2) 결과를 가져와 사용함으로 써 중복되는 연산을 줄인다. 정수형 배열을 선언해 연산 결과를 저장하고 필요할 때 불러와 사용하는 방식으로 구현했다.

### 소스 코드
```kotlin
class Solution {
    fun solution(n: Int): Int {
        val arr = Array(n+1) {0}
        return fibonacci(n, arr)
    }
    
    fun fibonacci(num: Int, arr: Array<Int>): Int {
        if (num <= 1) return num
        if (arr[num] > 0) return arr[num]
        arr[num] = (fibonacci(num - 1, arr) + fibonacci(num - 2, arr))%1234567
        return arr[num] % 1234567
    }
}
```