# 약수의 개수와 덧셈

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/77884
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1

## 문제 풀이

### 문제 내용 정리
정수 left, right가 주어질 때 left부터 right까지의 모든 수들 중에서 약수 개수가 짝수인 수는 더하고, 약수 개수가 홀수인 수는 뺀 수를 반환

### 문제 유형
특별히 알고리즘을 구현하거나 자료구조를 사용하는 유형이 아닌 간단한 구현 문제

### 풀이 방법
약수 개수가 홀수인 경우는 가장 큰 약수가 그 수의 제곱근일 때 이므로 제곱근을 이용해 판별하는 로직을 구현했다.

### 소스 코드
```kotlin
class Solution {
    fun solution(left: Int, right: Int): Int {
        var result = 0

        for (num in left..right) {
            val sqrt = Math.sqrt(num.toDouble())
            if (sqrt == sqrt.toInt().toDouble()) {
                result -= num
            } else {
                result += num
            }
        }

        return result
    }
}
```