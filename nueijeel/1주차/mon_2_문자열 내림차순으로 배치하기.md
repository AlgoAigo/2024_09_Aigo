# 문자열 내림차순으로 배치하기

## 문제 설명
- 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12917
- 난이도(백준 티어, 프로그래머스 레벨) : 프로그래머스 Lv1

## 문제 풀이

### 문제 내용 정리
영문 대소문자로만 구성된 문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새 문자열로 반환
-> 대문자가 소문자보다 작은 것으로 간주

### 문제 유형
문자열

### 풀이 방법
문자열 s를 문자 배열로 바꾸고 내림차순으로 정렬한 뒤 문자열 형태로 출력하도록 했다.

### 소스 코드
```kotlin
class Solution {
    fun solution(s: String): String {
        return s.toCharArray().sortedDescending().joinToString("")
    }
}
```